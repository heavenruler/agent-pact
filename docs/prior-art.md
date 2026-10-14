# Prior art and differences (2026-10-14; each project page was opened and checked)

| Project | What it is | How agentpact differs | Verdict |
|---|---|---|---|
| [multi-agent-governance](https://github.com/simaba/multi-agent-governance) | A multi-file documentation framework for multi-agent governance (roles, decision authority, escalation logic, accountability, control design); MIT | It is documentation for people to read; agentpact is one prompt an agent executes directly | Borrow ideas |
| [agent-playbook-template](https://github.com/screenleon/agent-playbook-template) | A portable governance template for AI coding agents (AGENTS.md, skills, adapters, GitHub Actions, evals); MIT. **The page marks it archived; development moved to pm-dispatch** | Many files, needs wholesale adoption; and archived | Borrow ideas |
| [agent-memory-system](https://github.com/Romadethat/agent-memory-system) | A file-based agent memory system template (init scripts, skills, knowledge base, multi-agent coordination); MIT | Its focus is persistent memory, not boundaries before entering an environment | Not applicable |

Conclusion: we found no ready-made approach of "one prompt that makes each agent generate its boundary settings from its own memory", so we built it.
