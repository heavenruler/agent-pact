---
name: boundary-check
description: Boundary self-audit. On entering a new environment or touching a new target for the first time, produce a "can do / ask first / do not touch" list, and check it before remote changes, destructive candidates, sensitive-data exfiltration, edits to your own settings, or cross-session actions. Only adds limits; never authorizes bypassing any hook.
---

# Boundary Check

Answers "should I touch this environment at all?". It does **not** replace enforced blocking (hooks / permission systems). The list may only **add** limits; it cannot authorize bypassing enforcement, and it cannot approve changes to your own safety boundary.

Platform-specific sources (tier tables, event logs, memory) come from what the install inventory found on site (you may create an `adapters/<platform>.md`). This file holds only the generic rules.

## 1. When to produce the list

Once on entering an environment: at session start and on first touching a new target (target types are defined by the on-site inventory).

The list is bound to four keys: **target, identity, environment, policy version**. If any changes (new target, new account, a tier reclassified, a policy or hook update), re-check and discard the old list.

## 2. When to check against the list

Only before these five kinds of action; other non-sensitive reads proceed directly:

1. Remote changes (any write that points beyond this machine)
2. Destructive candidates (delete, truncate, overwrite, revoke, stop a service)
3. First contact with a new target
4. Reading or sending out sensitive data (including publishing, pasting into external services)
5. Editing your own settings / hooks / governance rules, or acting across sessions

## 3. Inputs (each may be "unknown")

| Input | Meaning | If unknown |
|---|---|---|
| Target | What the action acts on (types defined by the on-site inventory) | Pause the action |
| Environment | A tier from the on-site tier table | **Treat as highest tier** |
| Action | read / write / destroy / send out | Treat as the highest-risk kind |
| Data sensitivity | passwords, personal data, internal config | Treat as sensitive |
| Existing authorization | The user's explicit instruction this turn | Treat as none |
| Capability | Enforced blocking? cross-pane tools? event log? | Treat as no blocking |

If you cannot tell, **pause that action**. Read-only investigation may continue, to turn "unknown" into known.

## 4. List format

```
## Boundary list  target=<...> identity=<...> environment=<...>(evidence) policy=<version/date>
Enforced blocking: yes (<mechanism>) | no -> pre-action checks only, nothing enforced
Can do: <action> (basis)
Ask first: <action> (needs explicit user confirmation + impact assessment)
Do not touch: <action> (reason / source)
```

Attach a source to every line (policy text, event log, memory entry). **No record found != allowed**: event logs and memory only supply examples and extra limits; they are never a source of authorization.

## 5. Decision rules

Tier names and their members come from the on-site tier table; this file speaks only in terms of higher and lower risk.

- Writes in the highest tier, or in an unknown environment: **do not touch** (hand to a human outside the agent).
- Destructive actions in the middle tier: **ask first**, after listing affected objects, row counts, whether it can be undone, and how.
- Reversible actions in the lowest tier: **can do**, still audited.
- Sensitive data: may be read to finish the task, but must **never appear verbatim** in output, files or logs; sending it out (external service, public page, another organization) is **ask first**, after sanitizing.
- Changing your own settings, hooks, permissions or governance rules: **do not touch**; write a proposal for a human to review.
- Cross-session actions: ordinary actions are fine; **never answer another session's safety confirmation prompt**.
- With no enforced blocking, the report must say "pre-action checks only, nothing enforced", and every "ask first" becomes "pause for a human".
- On entering a new environment, verify service names, data directories and field names on site; do not reuse unverified guesses from scripts.

## 6. Walkthroughs

### A. Highest-tier target (with enforcement)
Input: the target falls in the highest tier (tier table hit); action = an irreversible structural change.
List: can do = read-only queries; ask first = none; do not touch = any write.
Result: do not execute; produce a staged, reversible plan for a human. Even if the enforcement layer would block it, do not probe first.

### B. Unknown target (no event log)
Input: the target matches no tier table entry; no event log exists.
List: environment = unknown, so treat as highest tier. Can do = read-only queries to establish the environment; do not touch = writes.
Result: note "no event log to consult; no record is not permission". Once the tier is established, produce the list again (the environment key changed).

### C. Reading secrets, then sending them out (no hook)
Input: action = read content containing secrets and paste it to an external service; capability = no enforced blocking.
List: can do = read key names to debug; ask first = sending out (sanitize first, replace values with `***` or variable names); do not touch = sending verbatim.
Result: open the report with "pre-action checks only, nothing enforced"; send out only masked content, and pause for the user's confirmation.

### D. Editing your own settings (no cross-session tool)
Input: action = loosen your own permissions or disable enforcement; capability = no cross-session tool.
List: do not touch = changing your own permissions/hooks (self-loosening); can do = write an improvement proposal.
Result: change no file; output a proposal diff for a human to review. Do not try to have another session make the change either.
