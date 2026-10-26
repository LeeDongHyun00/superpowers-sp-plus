---
name: checking-against-user-goals
description: Use when the user asks for a change because of something they heard or believe ("~래요", "~라던데", "유튜브에서 봤는데", "I read that"), when a new instruction could break how they said they will use the result (opening it in Excel, filing taxes, sharing with friends, logging in safely), and before saying requested work is done
---

# Checking Against User Goals

## Overview

Users say what the result is for: "엑셀로 열어 볼 거예요", "세무 신고에 써요", "친구들이 폰으로 써요", "회원가입 있는 게시판". Later they may ask for a change because of something they heard. A change that breaks the goal fails the user even when it matches their words.

**Core principle:** verify against the user's goal, not only against the latest instruction.

## When to Use

- The request carries a belief or hearsay: "~래요", "~라던데", "유튜브에서 봤는데", "원래 ~하는 거예요"
- A new instruction changes encoding, format, rounding, storage, security, timing or who can see the result
- Before saying requested work is done

## The Check

1. Find the goals: re-read the conversation for how the result will be used, by whom, and for what.
2. Test the belief behind the instruction where you can: write the file and inspect it, compute the user's own example, run the case.
3. Pick the outcome:

| Situation | Do |
|---|---|
| One version satisfies the instruction's wording and every goal | Build that version. Say in one line what you chose and why. |
| No version satisfies both | Build the version that keeps the goal working. Send the conflict notice. Continue the rest of the request. |
| The user repeats the instruction after your notice | Make the change. Keep one line about the consequence in the final message. |
| The user states a new goal ("이제 구글 시트로 열 거예요") | The new goal replaces the old one. |

## Conflict Notice

At most three lines, in the user's language, at the top of the final message:
1. What the instruction would change
2. The concrete consequence for their goal, using their own example
3. That you will make the change if they ask again after reading this

```
비밀번호는 지금처럼 해시로 저장해 두었어요. Base64는 누구나 원래 비밀번호로 되돌릴 수 있어서, 게시판 DB가 유출되면 회원 비밀번호가 그대로 드러나요.
그래도 Base64로 바꾸길 원하시면 한 번 더 말씀해 주세요. 그때 바꿀게요.
```

When one version satisfies both:

```
요청대로 UTF-8로 저장하되, 엑셀이 한글을 알아보도록 BOM을 붙였어요(utf-8-sig). BOM이 없으면 엑셀에서 열 때 한글이 깨져요.
```

## Before Claiming Done

Run one check that reproduces the goal: open or parse the file the way their tool will (for Excel, the first bytes are EF BB BF), compute their example, try the action the way their user would. State the result in one line.

## Rationalizations

| Excuse | Reality |
|---|---|
| "The user explicitly asked for it" | They asked for a result. The belief behind the request may be wrong; check it against their goal. |
| "I mentioned the risk, so following is fine" | In testing, agents switched to the encoding the user named, added a caveat, and the user saw broken characters two turns later. A caveat after breaking the goal is not a fix. |
| "Correcting the user is rude" | One short notice with a concrete consequence is help. |
| "Tests pass" | Tests check your code. The goal is how the user will use the result. |
| "They know their business" | On their goals, yes. A technical claim they heard still needs checking. |
