# Security

hi.ai is not a sandbox. It starts your agents and keeps their work organised. It does not hold them back.

## What hi.ai protects against

- **Other computers and web pages reaching hi.ai.** The server listens on 127.0.0.1 and refuses any Host header that is not a local name (`HI_AI_HOSTS` adds names). A route that starts a program or changes a file also checks the Origin header, so a page on another site cannot use it.
- **A rule you switched on being skipped by accident.** A rule is written only after you have seen the exact change and said yes, and "off" puts the old bytes back.
- **Keys lying around.** A model server's key is kept in the system keyring (Secret Service, Keychain or Credential Manager). A key goes into a file only when you say so. The call log and the request record hold no keys, and the request record is cut and passed through a secret guard.
- **Mistakes in your own commits.** The leak guard (`tools/leak-guard`) blocks a commit that holds key shapes or words from your private list.

## What hi.ai does not protect against

- **An agent in a hi.ai terminal has your rights.** It runs as your user, in a terminal like your own. It can read and write every file you can, use your network, your SSH keys, your git credentials and your logged in tools, and start any program.
- **Hooks and rules are hygiene, not containment.** They act on the agent's own tools (for example, Claude Code's file and shell tools) and on commits. They do not watch a program the agent starts. The rule "Block reading `.env` files" judges a shell command by the folder it runs in: a command that reads another project's `.env` by its full path is not caught. An agent that does not honour its hooks, or that is told to ignore them, is not stopped.
- **Worktrees isolate the working copy only.** A task gets its own git worktree and branch, so its edits do not land in your main folder. The agent's shell, network, credentials and other repos are the same as everywhere else, and it can walk out of the worktree folder.
- **A malicious agent, model, prompt or repo.** Treat what an agent runs like a script you downloaded. Run agents you do not trust inside a virtual machine or a container of your own, with only the files and keys they need.
- **Other people on your computer.** Anyone who can run programs as your user can reach hi.ai. Its state files are private to your user (mode 0600 where hi.ai creates them), but your own account is the boundary.

The phone link is off until you switch it on. It then also listens on this computer's address in a private mesh network (100.64.0.0/10), and only a device paired with the one time code can use the board and the terminals. Switch it off when you do not need it.

## What hi.ai reads and writes

Files (default places; `XDG_CONFIG_HOME`, `XDG_STATE_HOME` and `XDG_DATA_HOME` move them):

- `~/.config/hi.ai/`: your agents and models (`agents.json`) and the leak guard's word list.
- `~/.local/state/hi.ai/`: the call log, the request record, the board, the brain read log, pictures and pastes, proposals, reports, research, the server log.
- `~/.local/share/hi.ai/`: your notes (the vault), the app window's browser profile, tray icons.
- `~/.local/share/applications` and `~/.local/share/icons`: the menu entry and icons, only after `hi-ai desktop install`.
- In a project you use on the board: `.hi-ai/worktrees/<card>` with the branch `hi-ai/<card>`, and a line in `.git/info/exclude`.
- In a project, after your yes to a rule or a skill link: the agent's own settings, hooks and skills files (for Claude Code `.claude/settings.local.json`; other agents' places are in `docs/agent-places-proof.md`), and, after a yes at the end of a session, one lesson line in `AGENTS.md`.
- It reads, and never writes, your agent's own folder (for the start load pages) and the repos under `~/src` (or `HI_AI_REPOS`) for the idea box. It reads the agents' session records for the tokens of each turn.

Keyring: a model server's key and a deep research key are stored in, and read from, the system keyring. hi.ai never writes it anywhere else unless you choose a file.

Network, and when:

- **Once a day while hi.ai runs:** the public model list from `raw.githubusercontent.com`. It is kept only when its signature verifies. Set `HI_AI_CATALOG_URL` to an empty value to turn it off.
- **Only after your yes in Setup:** the install commands it showed you (they run in a terminal as you), and downloads of a local model server, a model, the speech model and its graphics libraries, and OpenViking's installer, from GitHub, Hugging Face and NVIDIA.
- **When you use them:** a model call to the server you set up (a local one or a hosted one, the prompt goes there), the report check (it fetches the public pages a report cites; local and private addresses are refused), a clone of a repository you picked, and a deep research you start on `/research`: your question and your key go to the provider you picked (OpenAI, Perplexity or Google), and hi.ai asks it every 15 seconds how the job goes until the report is back.
- **Local only:** the agents' hooks call `hi-ai hook`, which posts to this computer's own server.
- Your agents then send what they always send, with their normal network access. Apart from the calls above, hi.ai sends nothing anywhere: it has no usage tracking.

## Report a security problem

Use GitHub's private vulnerability reporting: on the [hi.ai-releases](https://github.com/thejocorp/hi.ai-releases) page open **Security**, then **Report a vulnerability**. Please do not open a public issue for it. Say what you did, what you expected and what happened, and the version (`hi-ai --version`). Only the newest release gets fixes.
