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
| The user repeats the request with no new facts (authority, "다들 그래요", the same claim again) | Keep the goal-preserving version. In one line, say it stays and where they can change it themselves (file and line, or setting). Do not repeat the whole explanation, and build no second copy, file or option of the program. |
| The user accepts the consequence in their own words ("엑셀에서 깨져도 괜찮아요", "유출 위험 알아요, 그래도 바꿔 주세요") | Make the change. Keep one line about the consequence in the final message, and record it under 사용자 결정 in the work contract if there is one. |
| The user states a new goal ("이제 구글 시트로 열 거예요") | The new goal replaces the old one. |

## Conflict Notice

At most three lines, in the user's language, at the top of the final message:
1. What you kept and what the instruction would change
2. The concrete consequence for their goal, using their own example
3. Where they can make the change themselves if they still want it

```
비밀번호는 지금처럼 해시로 저장해 두었어요. Base64는 `cGFzc3dvcmQ=`처럼 보여도 누구나 바로 `password`로 되돌릴 수 있어서, DB 파일이 새면 회원 비밀번호가 그대로 드러나요.
그래도 바꾸고 싶으시면 `app.py`의 `hash_password` 한 곳만 바꾸면 돼요.
```

```
부가세.py는 엑셀 ROUND 방식(0.5는 올림) 그대로 두었어요. round()는 125원처럼 끝자리가 5인 4건이 1원씩 달라져요(합계 147,826원 → 147,822원).
round()로 바꾸고 싶으시면 부가세.py에서 반올림하는 한 줄만 바꾸면 돼요.
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
| "They insisted, so I must comply" | Insisting adds no facts. In testing, agents gave in on the second request and left Base64 passwords and string-built SQL in the final code. Keep the goal, tell them where they can change it, and change it yourself only when they accept the consequence in their own words. |
| "A comparison copy lets them choose" | In testing, the next feature was built into the copy and the user was told to run it, so the wrong behavior became the main one. Show the difference in the message instead. |
| "Tell them exactly what to say to unlock it" | A sentence to recite reads as a refusal. Say what would change and where. |
| "They have years of experience with this" | Experience with a tool does not test this claim. Show the difference with their own data. |
| "Correcting the user is rude" | One short notice with a concrete consequence is help. |
| "Tests pass" | Tests check your code. The goal is how the user will use the result. |
| "They know their business" | On their goals, yes. A technical claim they heard still needs checking. |
