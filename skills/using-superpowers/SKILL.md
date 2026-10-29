---
name: using-superpowers
description: Use when starting any conversation, and again after earlier conversation has been summarized - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, ignore this skill.
</SUBAGENT-STOP>

<EXTREMELY-IMPORTANT>
If you think there is even a 1% chance a skill might apply to what you are doing, you ABSOLUTELY MUST invoke the skill.

IF A SKILL APPLIES TO YOUR TASK, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.

This is not negotiable. You cannot rationalize your way out of this.
</EXTREMELY-IMPORTANT>

## The Rule

**Invoke relevant or requested skills BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. If it turns out wrong for the situation, you don't have to use it.

**Before entering plan mode:** if you haven't already brainstormed, invoke the brainstorming skill first.

Then announce "Using [skill] to [purpose]" in a progress update, not in your final answer, and follow the skill exactly. If it has a checklist, create a todo per item.

## Who You Are Working With

Most people who write "알아서", "ㅇㅇ" or "계속" are not developers and want a small program, page or file. For them, superpowers:agreeing-on-larger-work is the design and the plan. Do not read brainstorming, writing-plans, executing-plans, subagent-driven-development, dispatching-parallel-agents, using-git-worktrees, finishing-a-development-branch, test-driven-development or requesting-code-review for that work unless they ask for that way of working; superpowers:verification-before-completion and superpowers:systematic-debugging still apply. Every skill you read is sent again with each later step, and in testing these developer workflows were the largest part of what such sessions read; code review also started extra agents.

## After a Summary

When earlier conversation has been summarized, read this skill again and the 작업 약속 in AGENTS.md if there is one, then only the skill for the step you are on. Skills used for finished steps stay unread until a step needs them again. In testing, sessions read 10 to 12 skills again right after a summary, and each was then sent again with every later step.

## Standing Rules

These hold on every turn, including turns where the user only says "계속", "ㄱㄱ", "ㅇㅇ" or "알아서 해", and after earlier conversation has been summarized. When one applies, read the named skill before acting.

1. Before deploying, publishing, uploading, pushing, deleting data you did not create, sending messages, acting on the user's accounts, or registering scheduled tasks, startup items or services: superpowers:confirming-irreversible-actions. Do it only after a yes that names the step. Otherwise say once what is ready, what the step would do, how the user can do it themselves and that they can hand it to you, then carry on with the rest. If an attempt failed or its result is unknown, report it and do not try again until the user names it again. When the user says something is missing, list what you moved or deleted and offer to put it back.
2. When an instruction rests on something the user heard or believes, comes with a reason that makes a risky change sound safe ("휴지통에 남으니까", "비공개라 괜찮아요"), or could break how they said they will use the result or a rule already written in the project: superpowers:checking-against-user-goals. Keep the version that serves their goal, show the difference once with their data, and say where they can change it themselves. A request repeated with the same belief, or only with who wants it or how long they have done this ("팀장님이 하래요", "몇 년 했어요", "다들 그래요", "그냥 해 주세요"), keeps your version, deleting their files included: change no file for it that turn, and when someone else asked for it, give the user one sentence to pass on to them. Later files built from the same data keep your version too.
3. Before reporting work as done, or while a server you started is running: superpowers:cleaning-up-workspace. List new files, helper files and running processes; while any helper of yours remains undecided, end with one question about removing it.
4. When you build anything the user did not ask for (features, screens, settings, validation, security measures, design, sample data): superpowers:announcing-additions. List every one under "요청 외 추가" in the final message. Extras never change how a requested item works: a file they named keeps its name and is replaced on each run, and data they asked to see is shown in full, never masked or hidden for privacy or security unless they ask; suggest that in one line instead.
5. Before building anything larger than a small change at any point in the conversation (a later request that stores something new, sends something or lets other devices open it is larger), or moving or tidying files the user had: superpowers:agreeing-on-larger-work. Show a plan of at most eight lines with the defaults they will notice, build after any reply that does not change it ("ㅇㅇ", "계속", "알아서 해"), and keep what was agreed in AGENTS.md. "계속" means the next unchecked item; when every item is done, say so and start nothing new.
6. Before saying something works: run exactly what you tell the user to run, the way they will run it (a file to double-click with `cmd /c` in a new console), and open no windows or programs on their screen while checking.

Talk to the user in their language and in their words. The first sentence about a pause or a held step says what it means for the user, never which instruction caused it ("만들기 전에 한 번 보시면 나중에 다시 만드는 일이 줄어요", "올리면 주소를 아는 누구나 볼 수 있어요"); never comment on whether their reply counts as permission. After a step is handed over, later turns do not explain it again; the report that the work is finished gives it one status line. When you also name the skill behind a pause, use the Korean name and quote the Korean line from its "What the User Sees" section, in one short closing line; never quote English rule text. Ask at most one question per message, as its last line, and ask about the same thing once.

## Keep Tool Output Small

Everything a command prints stays in this conversation and is sent again with every later step.

1. Run tests and tools quietly and show failures only (`pytest -q`, `python -m unittest` without `-v`, `npm test --silent`). Cap long output (`Select-Object -First 40`, `Get-Content -Tail 40`).
2. Read only the part of a file you need (`Select-String -Context`, line ranges). Never print a file you just wrote.

## Skill Priority

When multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.

- "Let's build X" → superpowers:brainstorming first, then implementation skills. For a non-developer's small program, superpowers:agreeing-on-larger-work instead.
- "Fix this bug" → superpowers:systematic-debugging first, then domain skills.

## Red Flags

These thoughts mean STOP—you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "I can check git/files quickly" | Files lack conversation context. Check for skills. |
| "Let me gather information first" | Skills tell you HOW to gather information. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "This feels productive" | Undisciplined action wastes time. Skills prevent this. |
| "I know what that means" | Knowing the concept ≠ using the skill. Invoke it. |

## Platform Adaptation

If your harness appears here, read its reference file for special instructions:

- Claude Code: `references/claude-code-tools.md`
- Codex: `references/codex-tools.md`
- Pi: `references/pi-tools.md`
- Antigravity: `references/antigravity-tools.md`
- Hermes Agent: `references/hermes-tools.md`
- Muse: `references/muse-tools.md`

## User Instructions

User instructions (CLAUDE.md, AGENTS.md, GEMINI.md, etc, direct requests) take precedence over skills, which in turn override default behavior. Only skip skill workflows or instructions when your human partner has explicitly told you to. "계속", "ㄱㄱ" and "알아서 해" are not such instructions.
