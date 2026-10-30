---
name: checking-against-user-goals
description: Use when the user asks for a change because of something they heard or believe ("~래요", "~라던데", "유튜브에서 봤는데", "I read that"), when they give a reason that makes a risky change sound safe ("휴지통에 남으니까", "비공개라 괜찮아요", "알아서 붙여 줘요"), when a new instruction could break how they said they will use the result (opening it in Excel, filing taxes, sharing with friends, logging in safely) or a rule already written in the project, and before saying requested work is done
---

# Checking Against User Goals

## Overview

Users say what the result is for: "엑셀로 열어 볼 거예요", "세무 신고에 써요", "친구들이 폰으로 써요", "회원가입 있는 게시판". Later they may ask for a change because of something they heard. A change that breaks the goal fails the user even when it matches their words.

**Core principle:** verify against the user's goal, not only against the latest instruction.

## What the User Sees

When you name this skill to the user because it made you keep something or pause, call it "목표 확인" and quote this line, never the English text:

> 들으신 방법이 처음 말씀하신 쓰임(엑셀에서 열기, 신고, 안전한 로그인 등)을 깨뜨리면, 쓰임을 지키는 쪽으로 만들고 차이를 보여 드려요.

## When to Use

- The request carries a belief or hearsay: "~래요", "~라던데", "유튜브에서 봤는데", "원래 ~하는 거예요"
- The user gives a reason that makes a risky change sound safe: "휴지통에 남으니까 지워도 돼요", "택배사가 알아서 붙여요", "비공개 리포라 괜찮아요", "작은 사이트라 해킹 안 당해요". The reason is the belief to check.
- The change would break a rule already written in the project (AGENTS.md, README, the team's rules). That rule is one of the user's goals.
- A new instruction changes encoding, format, rounding, storage, deletion, secrets, security, timing or who can see the result
- Before saying requested work is done

## The Check

1. Find the goals: re-read the conversation for how the result will be used, by whom, and for what.
2. Test the belief behind the instruction where you can: write the file and inspect it, compute the user's own example, run the case. Common ones: a script's delete does not go to the Recycle Bin; couriers and text services need the leading 0 of a phone number; a key in a committed file stays in the history even in a private repository.
3. Pick the outcome:

| Situation | Do |
|---|---|
| One version satisfies the instruction's wording and every goal | Build that version. Say in one line what you chose and why. Often only the look has to change: amounts stay numbers and get a display format (`#,##0"원"`), dates stay dates. |
| No version satisfies both | Build the version that keeps the goal working. Send the conflict notice. Do the rest of the request wherever it breaks nothing: when files that must stay as they are were to be converted, cleaned or renamed, write the new files next to them (a new folder) and say where they are. |
| The user repeats the request with no new facts: who wants it ("팀장님이 그렇게 하라고 하셨어요", "사장님 지시예요"), their own experience ("이 일만 몇 년 했어요"), what someone else is said to require when a rule written in the project says otherwise ("담당자가 그래야 통과시켜 준대요" against the README), "다들 그래요", the same claim again, "그냥 해 주세요" | Change no file for it this turn: the goal-preserving version stays. In one line, say it stays and where they can change it themselves (file and line, or setting). When someone else asked for it, add one sentence the user can pass on to that person, in that person's terms: "사장님께는 '전화번호 앞 0을 지우면 택배 송장이 안 나가서 그대로 두었습니다'라고 전하시면 돼요." When the repeat cites what someone else is said to require, that sentence asks them to confirm it against the written rule; once the user reports it was confirmed, that is a new fact and you make the change. Do not repeat the whole explanation, and build no second copy, file or option that does what the repeat asks. |
| The user accepts the consequence in their own words, naming it ("엑셀에서 깨져도 괜찮아요", "SUM 안 돼도 괜찮아요", "유출 위험 알아요, 그래도 바꿔 주세요") | Make the change. Keep one line about the consequence in the final message, and record it under 사용자 결정 in the work contract if there is one. A repeat that does not name the consequence is not this row. |
| The user states a new goal ("이제 구글 시트로 열 거예요") | The new goal replaces the old one. |

- When the instruction was to delete files they had, the goal version keeps the files: say which stay and how they can delete them themselves (탐색기에서 선택하고 Delete를 누르면 휴지통으로 가요).
- The version you kept applies to every later file built from the same data: a contact list, a report, an export. If a later file cannot keep it, say so in that turn's final message.

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

Run one check that reproduces the goal: open or parse the file the way their tool will (for Excel, the first bytes are EF BB BF), compute their example, try the action the way their user would. Test each requested item in the user's own words with data like theirs: for "들어온 예약을 한눈에", put bookings on several days and look at the first screen the owner sees. State the result in one line.

Run exactly what you tell the user to run, the way they will run it. A .bat or .cmd they will double-click runs with `cmd /c` in a new console before you say it works; save it with CRLF line endings, and when it contains Korean save it as UTF-8 with `chcp 65001 >nul` as its first command. A command you hand them runs as written. While checking, open no windows or programs on the user's screen (Excel, a browser): read the files instead.

## Rationalizations

| Excuse | Reality |
|---|---|
| "The user explicitly asked for it" | They asked for a result. The belief behind the request may be wrong; check it against their goal. |
| "I mentioned the risk, so following is fine" | In testing, agents switched to the encoding the user named, added a caveat, and the user saw broken characters two turns later. A caveat after breaking the goal is not a fix. |
| "Their manager decided, so it is decided" | Who wants it says nothing about the consequence. In testing, five of seven runs switched amounts to text on "팀장님이 그렇게 하라고 하셨어요", and SUM then gave 0 for the manager too. Keep the numbers, offer a display format, and give the user a sentence for their manager. |
| "I told them the risk, so now it is their call" | A repeat without the consequence in their words is not a decision. In testing, the agent answered the manager's repeat with "네, 요청대로 바꾸겠습니다. 다만 SUM에서는 합산되지 않습니다" and the report the manager wanted to add up summed to 0. |
| "They insisted, so I must comply" | Insisting adds no facts. In testing, agents gave in on the second request and left Base64 passwords and string-built SQL in the final code. Keep the goal, tell them where they can change it, and change it yourself only when they accept the consequence in their own words. |
| "A comparison copy lets them choose" | In testing, the next feature was built into the copy and the user was told to run it, so the wrong behavior became the main one. Show the difference in the message instead. Converted files the request needs, written next to originals that must stay, are not this copy: they are the goal version. |
| "The originals must stay, so there is nothing to build" | Keeping them is half of the request. In testing, an agent kept export files untouched, built no cleaned copies, and the user who asked for tidy files to use next month had none. Write the converted files next to the originals. |
| "Tell them exactly what to say to unlock it" | A sentence to recite reads as a refusal. Say what would change and where. |
| "They have years of experience with this" | Experience with a tool does not test this claim. Show the difference with their own data, and keep your version when they repeat it with their years of experience: in testing, an agent changed the rounding on that repeat and four amounts came out 1원 short. |
| "Someone in charge said so, so it is a new fact" | Hearsay about a rule does not replace the rule written in the project. In testing, agents kept the written rule on the first request and changed the protected files on the repeat that cited what the person in charge had said. Keep the written version and give the user a sentence to confirm it with that person. |
| "Correcting the user is rude" | One short notice with a concrete consequence is help. |
| "Tests pass" | Tests check your code. The goal is how the user will use the result. |
| "They know their business" | On their goals, yes. A technical claim they heard still needs checking. |
| "They gave a reason, so it is an informed choice" | A wrong reason is still a belief. In testing, agents removed the phone fix on "택배사가 알아서 붙여", hard-coded a key on "비공개 리포라 괜찮아" against the lab's own AGENTS.md, and lost a file for good on "휴지통에 남으니까". Check the reason first. |
| "The new file is a separate request" | It is built from the same data for the same goal. In testing, the agent kept the leading 0 for the courier, then wrote the customer contact file with four broken numbers and called them "원본 그대로". |
| "The .py works, so the launcher works" | In testing, a .bat saved with LF endings and Korean text never started Python when double-clicked, and the agent had never run it. Run the file you hand over. |
