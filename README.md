# Superpowers SP+ for Codex

SP+ is [Superpowers](https://github.com/obra/superpowers) 7.0.1 by Jesse Vincent and Prime Radiant, adjusted for people who are not developers and who talk to Codex in short Korean replies such as "ㅇㅇ", "계속" or "알아서 해". It keeps every original skill, adds five skills and six standing rules, and was tuned with the Codex CLI on Windows and gpt-6.1-sol at medium reasoning.

For the original Superpowers documentation, see the [upstream README at v7.0.1](https://github.com/obra/superpowers/blob/v7.0.1/README.md).

## What Changes When You Use It

| When you | Codex with SP+ |
|---|---|
| ask for something larger than a small change (several features or screens, login, stored data, installs) | shows a plan of at most eight lines first, with the defaults you will notice (hours, time units, file names), and starts after any reply that does not change it ("ㅇㅇ", "계속", "알아서 해") |
| come back after a long conversation, or start a new one | continues from the plan it keeps in your project's `AGENTS.md`: "계속" means the next unchecked item, and when every item is done it says so and starts nothing new |
| reach a step that is hard to undo: publishing or deploying, pushing, deleting files you already had, sending messages, acting on your accounts, registering startup items or scheduled tasks | stops at that step, says once what is ready, what the step would do and how you can do it yourself, and carries on with the rest. It takes the step only after a yes that names it ("배포해 줘"), only on the service you named, and it does not retry a failed attempt on its own. A program it builds to send messages is checked against a stand-in, so nothing goes out before you run it. For something that should start by itself, it prepares a file you double-click once, and one that turns it off again |
| ask how friends or customers can open what it built | says who could open it with each option (only this PC, phones on the same Wi-Fi, anyone with the link on the internet) and offers the same Wi-Fi before publishing anything |
| ask for something because of what you heard ("CSV는 UTF-8이면 엑셀에서 안 깨진대요"), or with a reason that makes a risk sound safe ("휴지통에 남으니까 지워도 돼요") | keeps the version that serves what you said the result is for, in every later file built from the same data too, shows the difference once with your data and tells you where you can change it yourself. Files that must stay as they are stay, and converted copies go next to them |
| repeat that request with only who wants it ("팀장님이 그렇게 하래요"), your years of experience, or what someone in charge is said to require against a rule written in your project | changes no file for it that turn, says where you can change it yourself, and gives you one sentence to pass on to that person |
| ask it to tidy a folder or to delete files you already had | shows which files would move where before touching them. If you repeat a reason it has just corrected ("휴지통에서 살리면 돼요, 그냥 지워"), it keeps the files and tells you how to delete them yourself |
| say a file is missing | lists what it moved, renamed or deleted, the Recycle Bin included, and offers to put it back |
| hand the decisions over ("예쁘게", "필요한 거 다") | lists everything it added that you did not ask for under "요청 외 추가". An extra never changes what you asked for: a file you named keeps its name on every run, and data you asked to see is shown in full |
| ask for a developer's way of working by name ("테스트 먼저 쓰고", "코드 리뷰 받아 보고 싶어요") | uses the Superpowers developer workflows for it. For a non-developer's small program it skips them, which keeps sessions shorter and cheaper |
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
superpowers@superpowers-sp-plus  installed, enabled  7.0.1-sp.9  ...
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
| `agreeing-on-larger-work` (new) | 작업 범위 확인 | Plan larger work first, with the defaults users will notice, and keep the agreed plan in `AGENTS.md`; open questions become plan defaults; tidying the user's files is larger work too |
| `confirming-irreversible-actions` (new) | 되돌리기 어려운 작업 | Publish, delete, send, account, startup-item and scheduled-task steps only after a yes that names them; hand the step over instead of blocking; no retry after a failed attempt; say who could open it with each option; a yes that repeats a corrected belief keeps the files; a missing file gets a list of what was moved or deleted |
| `checking-against-user-goals` (new) | 목표 확인 | Keep the user's stated goal when an instruction rests on a belief or a reassuring reason, or would break a rule already written in the project; a repeat with only who wants it, experience or a relayed rule changes no file; converted copies go next to files that must stay; the kept version carries into later files built from the same data |
| `cleaning-up-workspace` (new) | 작업 폴더 정리 | Report new files, helpers and running servers; ask once about removing helpers |
| `announcing-additions` (new) | | List unrequested additions under "요청 외 추가"; extras never change how a requested item works; after finished work, report instead of starting something new |
| `using-superpowers` (changed) | | Six standing rules that hold on every turn, including a bare "계속"; talk rules for Korean users; keep tool output small; developer workflows for people who ask for that way of working; after a summary, read only the skill for the current step |
| `brainstorming` (changed) | | Opting out of questions skips the questions, not the plan for larger work |

The descriptions of eight developer workflow skills (writing and executing plans, test-driven development, worktrees, code review, parallel and sub-agent work, finishing a branch) now say they are for developers or for people who ask for that way of working. Their instructions, and all other skills, are unchanged from Superpowers 7.0.1. The plugin keeps the name `superpowers`, so skill ids keep the `superpowers:` prefix. The findings behind each version are in [docs/sp-plus.md](docs/sp-plus.md).

## How It Was Tested

Each version was compared with the one before it in scripted sessions where simulated Korean users asked Codex for small programs and replied the way beginners do: non-developers (a salon owner, a club treasurer, an impatient online seller and others) and, to check that the changes were not fitted to them, beginner developers (a bootcamp student, a computer science student, a startup intern and others). Hidden acceptance checks and blind reviewers graded the results. The test harness is not part of this repository.

In the latest comparisons, version 7.0.1-sp.9 used 38% fewer credits than 7.0.1-sp.8 on the same five scenarios, started no sub-agents and read about half as much skill text. It passed all 54 requirement checks (sp.8: 75 of 81) and followed a planted wrong belief in 1 of 8 cases (sp.8: 3 of 12); a repeated request that cites a manager ("팀장님이 그렇게 하래요") or the user's years of experience was kept in every later run. On six new scenarios with beginner developers it matched 7.0.1-sp.4 on requirements (53 of 60, sp.4 55 of 62), with fewer problems flagged by reviewers (12, sp.4 18) and fewer larger changes built before a plan (8 of 14, sp.4 14 of 16). The rules that did not carry over to those scenarios were fixed and checked again. On a further six scenarios written afterwards and used for nothing else, sp.9 passed 45 of 50 requirement checks (sp.4: 44), followed 2 of 12 planted beliefs (sp.4: 4) and used 30% fewer credits. Known weak spots: later requests in a long conversation are often built without a plan, a pull request is handed over without the git commands, and a pause sometimes gives only the project's rule as the reason. The details are in [docs/sp-plus.md](docs/sp-plus.md).

SP+ is experimental. It has been tested only with the Codex CLI on Windows and with gpt-6.1-sol at medium reasoning.

The `diagnosing-superpowers` skill can offer to report problems to the upstream Superpowers issue tracker. Problems caused by SP+ changes do not belong there.

## Credits and License

Superpowers is by [Jesse Vincent](https://blog.fsck.com) and [Prime Radiant](https://primeradiant.com), released under the MIT License. SP+ changes are released under the same license; see [LICENSE](LICENSE). SP+ is not affiliated with or endorsed by the Superpowers authors.
