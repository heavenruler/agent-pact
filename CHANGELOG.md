# Changelog

## 0.1.2-dev
- Verified all open items (docs/sample-run.md, run 2): English stage 1, shared layer, chat-only, stage-1 write, stage-2 append and refusal to loosen.
- Stage 2 now re-renders blocks from the exact rules.md in the same step; rules.md ends with "## Appended rules".
- Version string fixed.

## 0.1.0-dev
- Added the shared layer (`PACT.md` section 3): one rules source rendered into every agent's entry file, shared skills, shared one-fact-per-file memory, precedence and conflict rules. Not yet dry-run.
- First release: `PACT.md` (inventory, three modes, two-stage install), `defaults/safety.md`, `modules/boundary-check`.
- Added the "targets and risk tiers" inventory and a three-level risk ladder; unified the term "highest tier".
- Stage 1 was dry-run once each on Claude and Codex (`docs/sample-run.md`); chat-only agents, stage 2 and the post-install report are not yet verified.
- Internationalized: English is the default (`README.md`, `PACT.md`, `defaults/`, `modules/`, `docs/`); Traditional Chinese kept as `*.zh-TW.md`.
- Note: the dry runs used the earlier Traditional Chinese `PACT.md` (commit `116f79c`). The English `PACT.md` has not been re-run.
