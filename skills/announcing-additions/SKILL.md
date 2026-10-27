---
name: announcing-additions
description: Use when the user hands over design or scope ("알아서", "맡길게", "예쁘게", "필요한 거 다"), when the user only says "계속" or "ㄱㄱ" after the requested work is finished, or when about to add a feature, screen, setting, stored data or file the user did not ask for
---

# Announcing Additions

## Overview

When a user hands over design ("알아서 예쁘게"), agents add features nobody asked for: storage, filters, extra tabs, comments. Each extra is code the user has to understand, and unrequested storage later forces data migrations.

**Core principle:** the user hears about every extra before it is built and sees it listed when it is done.

## Before Building

In the first message of the turn, before editing files, write two short lists in the user's language:
- 요청하신 것: each item, in the user's words
- 덧붙일 것: each extra in one line, with the stated goal it serves

Build an extra only when it is small: it changes only files you are already editing for the request, and adds no new page or screen, no new stored data, no login or account, and no external service. List every other extra under "추가로 할 수 있는 것" in the final message as a proposal, without building it.

## Final Message Slot

Before writing the final message, compare what you built with the user's words, item by item. Everything not in their words is an extra: features, screens, settings, validation rules, security measures, design and branding, sample data. When any extra exists, the final message has this section, with every extra on its own line:

```
요청 외 추가
- 다시 뽑기 버튼: 같은 메뉴가 연달아 나오지 않게 (빼려면 말씀해 주세요)
- 글 목록 10개씩 나눠 보기
- 입력 규칙: 아이디 3~20자, 비밀번호 8자 이상
```

## When the User Only Says "계속"

| State | Do |
|---|---|
| Requested work is unfinished | Continue it. |
| Requested work is finished | Start no unrequested feature. Say it is finished, with the evidence, list up to three options under "다음에 할 수 있는 것", and ask which one to do. |
| The user then delegates ("알아서 ㄱㄱ") | Build the smallest option, listed under 덧붙일 것 and 요청 외 추가. |

## Rationalizations

| Excuse | Reality |
|---|---|
| "They said 알아서, so anything goes" | Delegation covers how, not how much. Say what you are adding. |
| "More features are more value" | In testing, an unrequested save feature forced a data migration two turns later. |
| "I wrote it in the plan document" | The user reads the chat, not the plan document. |
| "'계속' means build the next thing" | It means keep going on what was asked. When that is done, say so and offer options. |
| "Security headers and input checks are just good practice" | Good practice is welcome. List it anyway; the user should know their board limits passwords and pages. |
| "I listed the features" | A feature list that mixes requested and added items hides the additions. Put the extras under 요청 외 추가. |
