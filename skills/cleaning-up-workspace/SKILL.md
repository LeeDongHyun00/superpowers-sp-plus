---
name: cleaning-up-workspace
description: Use when about to report work as done or end a turn after creating test files, scripts, plan documents, logs, temp folders, zips, browser profiles or other helper files in the user's folder, or while a server or background process you started is still running
---

# Cleaning Up the Workspace

## Overview

Novice users see every file in their folder and cannot tell which ones they need. Test folders, check scripts, plan documents and empty temp folders left without a word confuse them, and servers keep running after the session ends.

**Core principle:** the user hears about every file and process you leave behind, and decides what stays.

## While Working

- Put scratch work in one folder at the workspace root, `.agent-tmp/`. Point temp directories there: TMP and TEMP, `tempfile` directories, browser profiles, logs, throwaway scripts.
- Keep a running list of the files you create and the processes you start (command, PID or port).
- Tests and checks work on copies of the user's data inside `.agent-tmp/`, never on the originals.
- The work contract in AGENTS.md (superpowers:agreeing-on-larger-work) is not a helper. List it under 새로 만든 파일 the first time and never offer it for removal.

## Before the Final Message

Look for new files and folders in the workspace, including empty temp folders left by failed test runs, and for processes you started that are still running.

## Final Message Slots

When anything is new since your last report, end the final message with these sections in the user's language. Leave out an empty section.

```
새로 만든 파일
- index.html, style.css, app.js: 점심 메뉴 추천 화면

작업하면서 만든 보조 파일
- tests/: 동작 확인용 테스트 (앱 실행에는 필요 없어요)
- .agent-tmp/: 임시 폴더

켜져 있는 서버
- http://127.0.0.1:5000 (python app.py)

보조 파일은 지우고 서버는 끌까요? 추천: 지우고 끄기. 테스트는 나중에 고칠 때 쓰려면 남겨도 돼요.
```

The question is required: whenever a helper file or process of yours remains that the user has not decided about, the last line of the final message is this question, with your recommendation. Listing the items without the question is not enough. Offer only helper files and processes you created. Deliverables and the user's own files are never offered for deletion here; for those, use superpowers:confirming-irreversible-actions.

If superpowers:confirming-irreversible-actions needs a question in the same message, ask that one instead, list the helpers without a question, and ask about them in a later turn.

## Handling the Reply

| Reply | Do |
|---|---|
| Yes ("지워줘", "네", "꺼 주세요") | Remove only the listed helpers, stop only the listed processes, report what was removed |
| Delegation ("알아서 해", "편하신 대로") | Follow your recommendation, report what was removed |
| No ("남겨 두세요") | Keep them; do not ask about these items again |
| Anything else (a new request, "계속") | Keep them; include them again the next time new items appear |
| The environment blocks the deletion | List the exact paths and tell the user they can delete them; do not retry |

## Rationalizations

| Excuse | Reality |
|---|---|
| "Empty temp folders are harmless" | They show up in the user's folder with random names. List them. |
| "Tests are useful; they'll want them" | Maybe. Say what they are and let the user decide. |
| "The server is needed to view the app" | Then say it is running, where, and recommend keeping it. |
| "The plan document is for me" | It sits in their folder. Keep it in `.agent-tmp/` or list it. |
| "It's in .gitignore" | The user does not read .gitignore. |
| "I'll mention it at the end" | The end of this turn is the end the user sees. |
| "I listed them; that is enough" | A list informs; the question lets the user decide. End with the question. |
| "Deletion will be blocked anyway" | Ask anyway. If it is blocked, give the paths so the user can delete them. |
