# SP+ (superpowers 7.0.1 + four standing rules)

SP+ is a local fork of superpowers 7.0.1 used in persona experiments with novice users of gpt-6.1-sol (medium). It keeps every original skill and adds four skills for failures seen in pilot 1, where scripted novice users sent short replies such as "계속" and "ㅇㅇ".

| Skill | Failure it targets | Form |
|---|---|---|
| confirming-irreversible-actions | A bare "ㅇㅇ 계속" was taken as permission to create a hosting project and attempt a public push | Question: ask one question naming the step; only a yes that names it counts |
| checking-against-user-goals | Agents followed a wrong belief (plain UTF-8 CSV "never breaks in Excel") after the user had said the file is for Excel | Notice: build the version that keeps the stated goal, state the conflict in three lines or fewer |
| cleaning-up-workspace | Empty temp folders, check scripts, plan documents and running servers were left in the user's folder without a word in 11 of 12 sessions | Question: list new files, helpers and processes, ask before removing |
| announcing-additions | Unrequested features (storage, filters, comments, tabs) on delegated designs and on bare "계속" | Notice: name extras before building, list them under "요청 외 추가" |

Pilot 1 showed that the agent read `using-superpowers` on the first turn of every session and rarely opened skills after the second turn, while the short replies come later. `using-superpowers` therefore carries a short "Standing Rules" section that names each rule, so the rules stay in context after the first turn.

## Version 2 (7.0.1-sp.2)

The first comparison (6 scenarios, superpowers against sp.1, one run each) showed that sp.1 stopped the unauthorized publish and kept the workspace clean, while three things did not hold:

| Finding in sp.1 | Change in sp.2 |
|---|---|
| Both arms gave in when the user repeated a wrong request; Base64 passwords and string-built SQL stayed in the final code | checking-against-user-goals: a repeat without new facts keeps the goal-preserving version and gets a safe outlet (a separate file, column or option); the main behavior changes only when the user accepts the consequence in their own words |
| Novice users were shown skill names, instruction file paths and English rule text, and the same publish question was asked three times | using-superpowers announces skills in progress updates only; the standing rules forbid showing instruction names, paths or English text; a question about the same step is asked once |
| Helpers were reported but the cleanup question was never asked | cleaning-up-workspace: the closing question is required while any helper remains undecided; tests use copies of the user's data; a blocked deletion is answered with the exact paths |
| Unrequested extras (pagination, security headers, input rules, branding) went unannounced even after the skill was read | announcing-additions: compare the build with the user's words item by item and list every extra, security measures and design included, under "요청 외 추가" |

## Version 4 (7.0.1-sp.4): sp.2 plus tool-output discipline

The lean experiment (sp.3, six scenarios times three runs per arm) cut credits by only 5%: quiet test runs and output caps cut re-sent tool output by 68%, while reading one skill per step doubled skill reads and outweighed the slimmer skills. sp.4 keeps sp.2 and adds only the output rules ("Keep Tool Output Small" in using-superpowers) and, in the novice profile, `tool_output_token_limit = 6000`. The lean work stays on branch sp-plus-lean.

Version: 7.0.1-sp.4. Marketplace name: superpowers-sp-plus. The plugin name stays `superpowers`, so skill ids keep the `superpowers:` prefix.
