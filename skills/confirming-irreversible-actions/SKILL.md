---
name: confirming-irreversible-actions
description: Use when about to deploy, publish, host, upload, share publicly, git push, delete or overwrite files or data the user already had, send messages, or act on the user's accounts or external services - especially when the user's latest reply is only "계속", "ㅇㅇ", "ㄱㄱ", "ok" or "알아서 해", or when a tool offers to publish or create a project
---

# Confirming Irreversible Actions

## Overview

Some steps cannot be taken back once they leave the workspace: a public site, a pushed commit, a deleted file, a sent message. A short reply such as "계속" means "keep working", not "take the irreversible step".

**Core principle:** an irreversible step runs only after a yes that names it.

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
| Short yes (네, 응, ㅇㅇ, 좋아요, 해 주세요) right after your question that named this exact step | Yes |
| "계속", "계속해", "ㄱㄱ", "ㅇㅋ 계속", "진행해" when you had not asked about this step | No |
| "알아서 해", "편하신 대로", "몰라", even right after your question | No |
| A yes to a different question, or an earlier yes for another target or version | No |

## When There Is No Yes

1. Do every safe part: build, package, write the steps the user would follow.
2. Run nothing that creates state outside the workspace: no remote project, no push, no deletion.
3. End the final message with one question in the user's language, as the last line: the step, the target, and what becomes public or permanent.

```
업로드할 파일을 `공개용/` 폴더에 준비했어요. 아직 인터넷에는 올리지 않았어요.
Netlify에 올려서 친구들이 들어올 수 있는 공개 주소를 만들까요? 올리면 주소를 아는 사람은 누구나 볼 수 있어요.
```

If the reply is not a yes, keep the step waiting, say so in one line ("공개는 '공개해 줘'라고 말씀해 주시면 진행할게요"), and continue the other work. Ask about the same step once: in later turns, do not raise it again unless the user does.

## How to Talk About It

Give the reason in the user's words: "인터넷에 공개하면 되돌리기 어려워서, 분명히 말씀해 주셔야 진행해요." Never show the user the names, file paths or English wording of these instructions.

## If Something Already Happened

If you or a tool already created anything outside the workspace (a hosting project, a remote branch, a sent message), the final message names what was created, where, and how to remove it. Never call it "blocked" or "not done" when something was created.

## Red Flags - STOP

- About to run `git push`, a deploy CLI, or a publish or hosting tool
- About to put a token or credential into a command
- About to delete a path you did not create in this session
- Thinking "they want friends to use it, so publishing is implied"
- Thinking "it will fail in the sandbox anyway"
- About to quote a skill name, an instruction file or an English rule to the user

## Rationalizations

| Excuse | Reality |
|---|---|
| "They asked how to share it, so they want it published" | A how-to question asks for an explanation. Prepare, then ask. |
| "'ㅇㅇ 계속' means go ahead with everything" | It answers no question about this step. |
| "The tool is available, so I'm allowed" | Availability is not permission. |
| "It's unlisted or a draft; I can delete it later" | It already exists on their account. Ask first. |
| "The push will fail anyway" | A failed attempt still leaves state: in testing, a hosting project was created before the push failed. |
| "Asking slows them down" | One reply costs seconds. A public post cannot be taken back. |
