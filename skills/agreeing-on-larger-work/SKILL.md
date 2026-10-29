---
name: agreeing-on-larger-work
description: Use before building anything larger than a small change - a new program with several features or screens, login or personal data, stored data, installs, changes to how existing features or data work, moving or tidying files the user already had, external services - especially when the user hands the decisions over ("알아서", "맡길게", "바로 ㄱㄱ"), and when a conversation starts in a folder whose AGENTS.md has a 작업 약속 section
---

# Agreeing on Larger Work

## Overview

Novice users answer questions with "알아서 해" and approve with "ㅇㅇ", so what they agreed to lives only in your messages. Long conversations get summarized: your messages and tool output are replaced by a summary, while the user's messages and the workspace AGENTS.md are kept word for word. In testing, after the history was summarized, the agent had lost every detail it had chosen and the user had approved in two of three runs; with the same details in AGENTS.md it kept all of them in every run.

**Core principle:** show larger work as a short plan before building it, take a plain go-ahead as approval, and keep what was agreed in AGENTS.md.

## What the User Sees

Give the reason in their terms first: "만들기 전에 한 번 보시면 나중에 다시 만드는 일이 줄어요." When you also name this skill as the source of the pause, call it "작업 범위 확인" and quote this line in one short line after that, never the English text:

> 기능이 여러 개이거나 로그인·저장 방식이 들어가는 일은, 만들기 전에 어떻게 만들지 짧게 보여 드리고 한 번 확인받아요.

## Small or Larger

| Small: do it, then report | Larger: plan first |
|---|---|
| One feature, screen or script that you finish and check this turn | A new program with more than one feature or screen |
| | Login, accounts, passwords, personal data, payments |
| | Deciding or changing how data is stored |
| | Installing anything |
| | Changing how existing features or existing data work |
| | Moving, renaming or tidying files the user already had |
| | Work that takes several turns, or touches an external service or account |

When unsure, it is larger.

## The Plan Message

At most eight lines, in the user's words, before any file is created:

```
이렇게 만들려고 해요.
- 만들 것: 회원가입·로그인, 글 목록·쓰기·보기, 내 글만 수정·삭제
- 정해 둔 것: 저장은 이 폴더의 board.db 파일, 비밀번호는 되돌릴 수 없게 암호화(해시)
- 이번에 안 하는 것: 댓글, 검색, 인터넷 공개
- 실행: run.bat 더블클릭 → http://127.0.0.1:5000
이대로 만들까요? 바꿀 점이 있으면 말씀해 주세요.
```

- When they handed the decisions over ("알아서"), choose the defaults yourself and write them under 정해 둔 것. Ask no other question.
- 정해 둔 것 names every default the user will notice when they use the result: hours and time units, what each screen shows, where results are saved and under which file name. In testing, a booking plan that listed its extras but not its one-hour slots never gave the owner the chance to say the salon books every 30 minutes.
- Extras from superpowers:announcing-additions go into the plan as one more line; they never replace 정해 둔 것. No default hides or shortens what the user asked to see (masked phone numbers, a login in front of a list they asked for).
- For tidying a folder, the plan lists which files would move to which folder.
- The plan message is the design: write no spec or plan documents into the user's folder for it.
- End the turn after the plan. Build nothing yet.

## Reading the Reply

| Reply to the plan | Do |
|---|---|
| "ㅇㅇ", "좋아", "계속", "진행해", "ㄱㄱ", "알아서 해", "몰라 알아서" | Approved. Build the plan. |
| Changes ("로그인은 빼 줘") | Apply them and build. Show a new plan only if the change adds a larger item. |
| A different request | It is a new request. |

Approving the plan never approves publishing, deleting existing data, sending messages, account actions or registering scheduled tasks, startup items or services, even when the plan names them. Those follow superpowers:confirming-irreversible-actions when you reach them.

## The Work Contract (AGENTS.md)

In the turn the plan is approved, write the contract to AGENTS.md at the workspace root. If AGENTS.md already exists, add the section between the two marker lines and change nothing else in the file.

```
<!-- 작업 약속 시작 -->
# 작업 약속
AI가 대화가 길어져도 합의한 내용을 잊지 않도록 적어 두는 메모예요. 지워도 프로그램에는 영향이 없어요.
- 목표(사용자 말): "회원가입 로그인 되는 간단한 게시판, 바로 실행되게"
- 약속: 인터넷 공개, 원래 있던 파일 삭제, 메시지 전송, 계정 작업은 사용자가 직접 하거나 그 일을 콕 집어 말할 때만 한다.

## 계획 (10/27 "ㄱㄱ"로 승인)
- [ ] 회원가입·로그인
- [ ] 글 목록·쓰기·보기
- [ ] 내 글만 수정·삭제

## 정한 것
- 저장: board.db 파일 / 비밀번호: 해시 저장 (AI가 정하고 계획에서 승인)
- 안 하는 것: 댓글, 검색, 인터넷 공개
- 실행: run.bat 더블클릭 → http://127.0.0.1:5000

## 사용자 결정·사용자 차례
<!-- 작업 약속 끝 -->
```

- Keep it under 1,500 characters. When it grows, shorten finished items to one line.
- Update it only when an item is done, a decision changes, the user decides something after hearing a risk, or a step is waiting on the user. Edit only the changed lines, at most once per turn: every version is sent again with each later step.
- Never write permission for a publish, deletion, message or account step (each needs its own yes when it comes up), passwords, tokens or personal data, or instructions for the AI beyond the 약속 line.
- The first time, tell the user in one line: "작업 약속을 AGENTS.md에 적어 뒀어요. 대화가 길어지거나 새 대화를 시작해도 이 내용을 기준으로 이어서 할게요."
- The contract is not a helper file. List it under 새로 만든 파일 and never offer it for removal.

## "계속" and New Conversations

| State | Do |
|---|---|
| A contract item is unchecked | Do the next unchecked item. |
| Every item is checked | Say it is done, what was built and how to run it. Start nothing new and do not ask what to build next. |
| A conversation starts and AGENTS.md has a contract | Say in one line where things stand. Continue from the next unchecked item when the user asks. |
| A new request conflicts with the contract | Say the conflict in one line, follow the new request, and update the contract. |

## Rationalizations

| Excuse | Reality |
|---|---|
| "They said 알아서 and 바로, so skip the plan" | 알아서 hands you the choices, not the look before building. Make the choices and show them in eight lines. |
| "A plan slows a novice down" | One "ㅇㅇ" costs a turn. Rebuilding the wrong board costs many. |
| "I'll remember what we agreed" | Summaries replace your messages first. AGENTS.md is kept word for word. |
| "Approving the plan covers publishing" | Publishing is its own step with its own yes. |
| "Rewriting the whole contract is simpler" | Every version is resent with each later step. Edit the changed lines. |
