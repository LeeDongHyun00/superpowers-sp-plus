---
name: confirming-irreversible-actions
description: Use when about to deploy, publish, host, upload, share publicly, git push, delete or overwrite files or data the user already had, send messages, or act on the user's accounts or external services - especially when the user's latest reply is only "계속", "ㅇㅇ", "ㄱㄱ", "ok" or "알아서 해", or when a tool offers to publish or create a project
---

# Confirming Irreversible Actions

## Overview

Some steps cannot be taken back once they leave the workspace: a public site, a pushed commit, a deleted file, a sent message. A short reply such as "계속" means "keep working", not "take the irreversible step".

**Core principle:** an irreversible step runs only after a yes that names it. Without that yes, hand the step over; do not block the user.

## Which Steps Count

- Making anything reachable by others: deploy, publish, host, upload, share a link, create a site, app or project on a hosting service (built-in hosting and publishing tools included)
- `git push` to any remote, force push, creating remote repositories, releases or pull requests
- Deleting, overwriting or resetting files or data that existed before this session (`git reset --hard`, `git clean`, dropping tables, clearing records)
- Sending email, chat messages, notifications or webhooks; creating accounts, API keys or payments
- Changing settings outside the workspace (global config, installed services, scheduled tasks)

Helper files and processes you created in this session belong to superpowers:cleaning-up-workspace.

## What Counts as Yes

| User's latest message | Yes for this step? |
|---|---|
| Names the step and target: "netlify에 올려줘", "push 해줘", "backup 폴더 지워줘" | Yes, for that step and target only |
| Short yes (네, 응, ㅇㅇ, 좋아요, 해 주세요) right after your question or offer that named this exact step | Yes |
| "계속", "계속해", "ㄱㄱ", "ㅇㅋ 계속", "진행해" when you had not asked about this step | No |
| "알아서 해", "편하신 대로", "몰라", even right after your question | No |
| A yes to a different question, or an earlier yes for another target or version | No |

## When There Is No Yes: Hand It Over

The user wants the result. Without a yes that names the step, give them everything they need to take it, once:

1. Do every safe part: build, package, test locally.
2. Run nothing that creates state outside the workspace: no remote project, no push, no deletion.
3. In one message, in the user's words: what is ready; what the step would do (who can see it, what cannot be taken back, any cost or account); how to do it themselves, in at most four steps they can copy, with passwords and tokens typed only on their own screen; and that they can hand it to you.

```
공개용 파일은 `공개용` 폴더에 준비해 뒀어요. 아직 인터넷에는 올리지 않았어요.
올리면 주소를 아는 사람은 누구나 볼 수 있고, 퍼진 주소는 되돌리기 어려워요.
직접 올리려면: ① app.netlify.com/drop 접속·로그인 ② `공개용` 폴더를 화면에 끌어다 놓기 ③ 나온 주소를 친구들에게 보내기
제가 올려 드릴 수도 있어요. 원하시면 "올려 줘"라고 해 주세요.
```

After that the step is theirs. A reply that does not name it ("계속", "ㅇㅇ 계속", "알아서 해") is no reason to ask or explain again: carry on with the rest of the work, or report that it is done. In the final report the step gets one status line ("인터넷 공개: 아직 안 함 — 위 방법으로 직접 하시거나 '올려 줘'"). Do not raise it in later turns unless the user does.

## How to Talk About It

Give the reason as the consequence in the user's world: who will see it, what cannot be taken back, what it costs. A rule, instruction, guideline or policy is never the reason; never link or quote these instructions, and never tell the user their reply does not count ("‘계속’만으로는 안 돼요"). They asked for something; tell them what it would do and how to get it.

## If Something Already Happened

If you or a tool already created anything outside the workspace (a hosting project, a remote branch, a sent message), the final message names what was created, where, and how to remove it. Never call it "blocked" or "not done" when something was created.

## Red Flags - STOP

- About to run `git push`, a deploy CLI, or a publish or hosting tool
- About to put a token or credential into a command
- About to delete a path you did not create in this session
- Thinking "they want friends to use it, so publishing is implied"
- Thinking "it will fail in the sandbox anyway"
- About to quote a skill name, an instruction file or an English rule to the user
- About to explain that a rule requires confirmation, or to tell the user what words to say after they already heard the hand-over
- About to ask about a step you already handed over

## Rationalizations

| Excuse | Reality |
|---|---|
| "They asked how to share it, so they want it published" | A how-to question asks for an explanation. Prepare, then hand it over. |
| "'ㅇㅇ 계속' means go ahead with everything" | It answers no question about this step. |
| "The tool is available, so I'm allowed" | Availability is not permission. |
| "It's unlisted or a draft; I can delete it later" | It already exists on their account. Ask first. |
| "The push will fail anyway" | A failed attempt still leaves state: in testing, a hosting project was created before the push failed. |
| "Asking slows them down" | One reply costs seconds. A public post cannot be taken back. |
| "They said 알아서, so I must stop and wait" | Hand the step over and keep working on everything else. In testing, agents spent two turns repeating the question and the rule while the user still had no way to publish. |
| "Naming the rule is transparent" | To a novice it reads as a refusal on a technicality. Say what the step would do and how to take it. |
