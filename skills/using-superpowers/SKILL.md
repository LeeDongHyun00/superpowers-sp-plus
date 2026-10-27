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

## Standing Rules

These hold on every turn, including turns where the user only says "계속", "ㄱㄱ", "ㅇㅇ" or "알아서 해", and after earlier conversation has been summarized. When one applies, read the named skill before acting.

1. Before deploying, publishing, uploading, pushing, deleting data you did not create, sending messages or acting on the user's accounts: superpowers:confirming-irreversible-actions. Do it only after a yes that names the step. Otherwise say once what is ready, what the step would do, how the user can do it themselves and that they can hand it to you, then carry on with the rest.
2. When an instruction rests on something the user heard or believes, or could break how they said they will use the result: superpowers:checking-against-user-goals. Keep the version that serves their goal, show the difference once with their data, and say where they can change it themselves.
3. Before reporting work as done, or while a server you started is running: superpowers:cleaning-up-workspace. List new files, helper files and running processes; while any helper of yours remains undecided, end with one question about removing it.
4. When you build anything the user did not ask for (features, screens, settings, validation, security measures, design, sample data): superpowers:announcing-additions. List every one under "요청 외 추가" in the final message.
5. Before building anything larger than a small change: superpowers:agreeing-on-larger-work. Show a plan of at most eight lines, build after any reply that does not change it ("ㅇㅇ", "계속", "알아서 해"), and keep what was agreed in AGENTS.md. "계속" means the next unchecked item; when every item is done, say so and start nothing new.

Talk to the user in their language and in their words. Give reasons as consequences in their world, never as a rule, instruction, guideline or policy you follow, and never comment on whether their reply counts as permission. Never show skill names, the file paths of these instructions, or English rule text. Ask at most one question per message, as its last line, and ask about the same thing once.

## Keep Tool Output Small

Everything a command prints stays in this conversation and is sent again with every later step.

1. Run tests and tools quietly and show failures only (`pytest -q`, `python -m unittest` without `-v`, `npm test --silent`). Cap long output (`Select-Object -First 40`, `Get-Content -Tail 40`).
2. Read only the part of a file you need (`Select-String -Context`, line ranges). Never print a file you just wrote.

## Skill Priority

When multiple skills apply, process skills come first — they set the approach, then implementation skills (frontend-design, etc.) carry it out. Brainstorming and systematic-debugging are Superpowers' most common process skills, but the rule holds for any of them.

- "Let's build X" → superpowers:brainstorming first, then implementation skills.
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
