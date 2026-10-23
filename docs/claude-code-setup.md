# Claude Code setup (hackathon cheat sheet)

This repo carries its own Claude Code setup, so every session that opens it (cloud or your computer) gets the same tools:

| Tool | Where it's configured | State |
|---|---|---|
| Ponytail (less code, fewer tokens) | `.claude/settings.json` | on, level `full` |
| Superpowers (brainstorm → plan → TDD) | `.claude/settings.json` | installed, **off** |
| Playwright MCP (browser control) | `.mcp.json` | on (headless Chromium) |
| Karpathy guidelines | `CLAUDE.md` | always loaded |
| `[PONYTAIL]` badge | `.claude/settings.json` → `statusLine` | terminal only |
| Claude Squad (`cs`) | your own computer | install separately |

## First run
1. Start Claude Code in the repo. Approve the marketplaces/plugins and the `playwright` MCP server when asked.
2. Check: `/plugin` (ponytail on, superpowers off) · `/mcp` (playwright ✔ connected) · type `/` (see `/ponytail…` commands) · badge `[PONYTAIL]` at the bottom (it appears after the first session start).
3. Ponytail may offer to add its badge to your personal `~/.claude/settings.json`. Say no: this repo already has it.
4. Own computer only: install the browser once with `npx @playwright/mcp@latest install-browser chrome-for-testing`.
5. Cloud sessions only: in the environment settings (title bar → environment → Edit), add the variable `PLAYWRIGHT_MCP_EXECUTABLE_PATH=/opt/pw-browsers/chromium`.

## The 6 workflows worth remembering
| When | Do this |
|---|---|
| Normal coding | Just ask. Ponytail keeps the change small and ends with what it skipped or didn't check. Read that line. |
| Unsure about the approach | Plan mode (`Shift+Tab` until "plan mode"): Claude proposes, you approve, then it edits. |
| Before a commit or the demo | `/ponytail-review` (bugs, security, missing tests, what to cut). `/ponytail-audit` for the whole repo. |
| Check the app really works | Run `streamlit run app_.py`, then: "Open http://localhost:8501, upload a clip from assets/demo_clips, and tell me the verdict." |
| A bigger feature | Turn Superpowers on (`/plugin` → superpowers → Enable, restart), say "let's build X", follow brainstorm → plan → build. Turn it off afterwards. |
| Two tasks at once | `cs` → `n` new session per task → `Enter` to talk, `Ctrl-Q` to leave → `Tab` to see the diff → `c` to commit and pause, then test the branch. Avoid `cs -y`. |

## Ponytail levels
- `lite`: builds what you asked, names a smaller option.
- `full` (default, recommended): smallest complete change, small test for risky logic.
- `ultra`: also pushes back on parts of the request it thinks you don't need.

Switch with `/ponytail lite|full|ultra`, pause with `/ponytail off` (or say "stop ponytail"), and `/ponytail` turns it back on.

## Turn something off fast
| What | How |
|---|---|
| Any plugin | `/plugin` → Installed → pick it → Disable (or `claude plugin disable <name> --scope project`), then restart |
| Playwright MCP | `/mcp` → playwright → Disable |
| Karpathy rules | Delete or trim `CLAUDE.md` |
| Badge | Remove the `statusLine` block from `.claude/settings.json` |

## Token habits
- `/clear` between unrelated tasks (free, instant).
- `/compact` when a long session is getting heavy, at a natural break, not mid-change.
- `/context` shows what is using space. Browser page snapshots are large, so `/clear` after a browser-heavy task.
