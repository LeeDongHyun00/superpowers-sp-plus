# Superpowers SP+ for Codex

SP+ is [Superpowers](https://github.com/obra/superpowers) 7.0.1 by Jesse Vincent and Prime Radiant, adjusted for people who are not developers and who talk to Codex in short Korean replies such as "ㅇㅇ", "계속" or "알아서 해". It keeps every original skill, adds five skills and six standing rules, and was tuned with the Codex CLI on Windows and gpt-6.1-sol at medium reasoning.

For the original Superpowers documentation, see the [upstream README at v7.0.1](https://github.com/obra/superpowers/blob/v7.0.1/README.md).

## What Changes When You Use It

| When you | Codex with SP+ |
|---|---|
| ask for something larger than a small change (several features or screens, login, stored data, installs) | shows a plan of at most eight lines first, with the defaults you will notice (hours, time units, file names), and starts after any reply that does not change it ("ㅇㅇ", "계속", "알아서 해") |
| come back after a long conversation, or start a new one | continues from the plan it keeps in your project's `AGENTS.md`: "계속" means the next unchecked item, and when every item is done it says so and starts nothing new |
| reach a step that is hard to undo: publishing or deploying, pushing, deleting files you already had, sending messages, acting on your accounts | stops at that step, says once what is ready, what the step would do and how you can do it yourself, and carries on with the rest. It takes the step only after a yes that names it ("배포해 줘"), and it does not retry a failed attempt on its own |
| ask for something because of what you heard ("CSV는 UTF-8이면 엑셀에서 안 깨진대요"), or with a reason that makes a risk sound safe ("휴지통에 남으니까 지워도 돼요") | keeps the version that serves what you said the result is for, in every later file built from the same data too, shows the difference once with your data and tells you where you can change it yourself |
| ask it to tidy a folder or to delete files you already had | shows which files would move where before touching them. If you repeat a reason it has just corrected ("휴지통에서 살리면 돼요, 그냥 지워"), it keeps the files and tells you how to delete them yourself |
| say a file is missing | lists what it moved, renamed or deleted, the Recycle Bin included, and offers to put it back |
| hand the decisions over ("예쁘게", "필요한 거 다") | lists everything it added that you did not ask for under "요청 외 추가". An extra never changes what you asked for: a file you named keeps its name on every run |
| get finished work | lists new files, helper files and running servers, and asks once whether to remove its helpers |
| are given something to run, such as a `.bat` file to double-click | has run exactly that, the way you will run it, without opening windows on your screen |

## Requirements

- The Codex CLI with plugin support. SP+ was tested with Codex CLI 0.164.0-alpha.11.1 and 0.165.0-alpha.1.2 on Windows 11.
- Git. Codex uses it to download the plugin from GitHub.

## Install

If you already use the official Superpowers plugin (`codex plugin list` shows `superpowers@openai-curated-remote` as installed), uninstall it first from `/plugins` in the Codex CLI or from Plugins in the Codex app. Both plugins use the same skill names.

Then run:

```bash
codex plugin marketplace add LeeDongHyun00/superpowers-sp-plus
```

```bash
codex plugin add superpowers@superpowers-sp-plus
```

Check the result:

```bash
codex plugin list
```

```text
PLUGIN                           STATUS              VERSION     SOURCE
superpowers@superpowers-sp-plus  installed, enabled  7.0.1-sp.8  ...
```

SP+ applies to Codex sessions started after the install.

## Recommended Settings

**Keep tool output small.** Everything a command prints stays in the conversation and is sent again with every later step. SP+ was measured with this cap. Open `~/.codex/config.toml` (on Windows `%USERPROFILE%\.codex\config.toml`) and add this line near the top, above every line that starts with `[`:

```toml
tool_output_token_limit = 6000
```

A line added below a `[section]` header belongs to that section, and Codex ignores it there.

**Turn off the visual companion's telemetry.** Brainstorming's optional visual companion loads the Superpowers logo from the upstream authors' website, which tells them the Superpowers version in use and nothing about your project. To turn it off, set `SUPERPOWERS_DISABLE_TELEMETRY` before starting Codex:

- Windows: run `setx SUPERPOWERS_DISABLE_TELEMETRY 1`, then open a new terminal.
- macOS or Linux: add `export SUPERPOWERS_DISABLE_TELEMETRY=1` to your shell profile.

## Using It

Talk to Codex as usual. A few things work differently:

- **Plans.** For larger work you get a short plan first. Reply "ㅇㅇ" or "진행해" to start, or say what to change.
- **The work contract.** After you agree to a plan, SP+ writes a short "작업 약속" section in your project's `AGENTS.md`: the goal in your words, the plan as a checklist, what was decided, and one fixed line saying that publishing, deleting files you had, sending messages and account actions stay yours. Codex reads this file at the start of every session and again after a long conversation is summarized, so in a new conversation "계속" or "이어서 해 줘" picks up where you left off. You can edit or delete the section. It never holds permissions, passwords or personal data.
- **Steps that are hard to undo.** Name the step to hand it over: "배포해 줘", "푸시해 줘", "문자 보내 줘". "계속", "ㅇㅇ" or "알아서 해" alone never count for these steps.
- **Requests based on what you heard.** When SP+ keeps a different version than the one you asked for, it shows the difference once and says where you can change it yourself. If you still want your version after hearing the consequence, say so in your own words ("엑셀에서 깨져도 괜찮아요, 그래도 바꿔 주세요") and it makes the change.
- **Cleanup.** At the end it lists the files it made and asks once whether to delete its helper files. The `AGENTS.md` section is not a helper and stays.

## Update

```bash
codex plugin marketplace upgrade superpowers-sp-plus
```

This downloads the latest SP+ and replaces the installed version. Start a new Codex session afterwards.

## Uninstall

```bash
codex plugin remove superpowers@superpowers-sp-plus
```

```bash
codex plugin marketplace remove superpowers-sp-plus
```

## Troubleshooting

- **`codex` is not recognized (Windows).** The Codex CLI is not on your PATH. If you use the Codex app, it keeps its own copy of the CLI under `%LOCALAPPDATA%\OpenAI\Codex\bin`. In PowerShell, find it once and run the install commands through it:

  ```powershell
  $codex = (Get-ChildItem "$env:LOCALAPPDATA\OpenAI\Codex\bin" -Recurse -Filter codex.exe | Sort-Object LastWriteTime | Select-Object -Last 1).FullName
  & $codex plugin marketplace add LeeDongHyun00/superpowers-sp-plus
  & $codex plugin add superpowers@superpowers-sp-plus
  ```

  The other commands in this README work the same way: replace `codex` with `& $codex`.
- **`Filename too long` during `marketplace add` on Windows.** Git could not write into the Codex home folder because its path is too long. This happens only when `CODEX_HOME` points to a deeply nested folder; the default `%USERPROFILE%\.codex` works.
- **The skills do not show up.** Start a new Codex session: a running session keeps the skills it started with. Then check that `codex plugin list` shows the plugin as `installed, enabled`.

## What Is in SP+

| Skill | Named to users as | Purpose |
|---|---|---|
| `agreeing-on-larger-work` (new) | 작업 범위 확인 | Plan larger work first, with the defaults users will notice, and keep the agreed plan in `AGENTS.md`; tidying the user's files is larger work too |
| `confirming-irreversible-actions` (new) | 되돌리기 어려운 작업 | Publish, delete, send and account steps only after a yes that names them; hand the step over instead of blocking; no retry after a failed attempt; a yes that repeats a corrected belief keeps the files; a missing file gets a list of what was moved or deleted |
| `checking-against-user-goals` (new) | 목표 확인 | Keep the user's stated goal when an instruction rests on a belief or a reassuring reason, or would break a rule already written in the project; the kept version carries into later files built from the same data |
| `cleaning-up-workspace` (new) | 작업 폴더 정리 | Report new files, helpers and running servers; ask once about removing helpers |
| `announcing-additions` (new) | | List unrequested additions under "요청 외 추가"; extras never change how a requested item works; after finished work, report instead of starting something new |
| `using-superpowers` (changed) | | Six standing rules that hold on every turn, including a bare "계속"; talk rules for Korean users; keep tool output small |
| `brainstorming` (changed) | | Opting out of questions skips the questions, not the plan for larger work |

All other skills are unchanged from Superpowers 7.0.1. The plugin keeps the name `superpowers`, so skill ids keep the `superpowers:` prefix. The findings behind each version are in [docs/sp-plus.md](docs/sp-plus.md).

## How It Was Tested

Each version was compared with the one before it in scripted sessions where simulated Korean non-developers (a salon owner, a club treasurer, an impatient online seller and others) asked Codex for small programs and replied the way beginners do. Hidden acceptance checks and blind reviewers graded the results. The test harness is not part of this repository.

In the latest comparison, version 7.0.1-sp.8 against 7.0.1-sp.4 (13 scenarios, three runs each, 78 sessions, blind reviewers), SP+ followed a planted wrong belief in 5 of 30 cases instead of 11 of 29, made no literally false completion claims (17 before), started larger work without a plan 8 times in 52 instead of 37 in 56, and kept an accurate work contract in 23 sessions, at the same cost. Requirements passed in 189 of 195 checks (183 of 194 before). Known weak spots: a repeated request that cites a manager ("팀장님이 그렇게 하래요") is still often followed after a warning, and an unrequested privacy measure (masked phone numbers) sometimes hid what the user asked to see.

SP+ is experimental. It has been tested only with the Codex CLI on Windows and with gpt-6.1-sol at medium reasoning.

The `diagnosing-superpowers` skill can offer to report problems to the upstream Superpowers issue tracker. Problems caused by SP+ changes do not belong there.

## Credits and License

Superpowers is by [Jesse Vincent](https://blog.fsck.com) and [Prime Radiant](https://primeradiant.com), released under the MIT License. SP+ changes are released under the same license; see [LICENSE](LICENSE). SP+ is not affiliated with or endorsed by the Superpowers authors.
