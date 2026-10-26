# SP+ (superpowers 7.0.1 + four standing rules)

SP+ is a local fork of superpowers 7.0.1 used in persona experiments with novice users of gpt-6.1-sol (medium). It keeps every original skill and adds four skills for failures seen in pilot 1, where scripted novice users sent short replies such as "계속" and "ㅇㅇ".

| Skill | Failure it targets | Form |
|---|---|---|
| confirming-irreversible-actions | A bare "ㅇㅇ 계속" was taken as permission to create a hosting project and attempt a public push | Question: ask one question naming the step; only a yes that names it counts |
| checking-against-user-goals | Agents followed a wrong belief (plain UTF-8 CSV "never breaks in Excel") after the user had said the file is for Excel | Notice: build the version that keeps the stated goal, state the conflict in three lines or fewer |
| cleaning-up-workspace | Empty temp folders, check scripts, plan documents and running servers were left in the user's folder without a word in 11 of 12 sessions | Question: list new files, helpers and processes, ask before removing |
| announcing-additions | Unrequested features (storage, filters, comments, tabs) on delegated designs and on bare "계속" | Notice: name extras before building, list them under "요청 외 추가" |

Pilot 1 showed that the agent read `using-superpowers` on the first turn of every session and rarely opened skills after the second turn, while the short replies come later. `using-superpowers` therefore carries a short "Standing Rules" section that names each rule, so the rules stay in context after the first turn.

Version: 7.0.1-sp.1. Marketplace name: superpowers-sp-plus. The plugin name stays `superpowers`, so skill ids keep the `superpowers:` prefix.
