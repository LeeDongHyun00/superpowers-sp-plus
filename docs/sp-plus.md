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

## Version 5 (7.0.1-sp.5): plan first, work contract, hand-over

Built on sp.4 from three user requests, checked against the sp.2 transcripts (spplus-3, 18 sessions) and Codex probes:

| Finding | Change in sp.5 |
|---|---|
| 17 of 18 sessions built on the first turn without showing a plan; brainstorming drops its design gate once the user opts out of questions, and "알아서 해 줘" counts as opting out | New skill agreeing-on-larger-work: small work is done directly, larger work gets an eight-line plan with the agent's defaults, and any reply that does not change it is the go-ahead. brainstorming's opt-out now skips the questions only |
| Codex re-sends the workspace AGENTS.md whenever it changes and after compaction, while compaction replaces the agent's messages and tool output (skill bodies included) with an opaque summary. With compaction forced 9 to 12 times, the agent lost all 16 details it had chosen and the user had approved in two of three runs; with the details in AGENTS.md it kept all 16 in three of three | The approved plan becomes a short work contract in AGENTS.md (goal, plan items, decisions, user decisions, one fixed line that irreversible steps are the user's). It never holds permissions or secrets. using-superpowers asks to be read again after a summary |
| In the publishing scenario the agent asked again on "ㅇㅇ 계속" and on "알아서 해줘" stopped with a link to its instruction file and a sentence to recite (3 of 3 runs); 9 of 10 internal-path leaks came while justifying a held step | confirming-irreversible-actions hands the step over once (what is ready, what it would do, how to do it oneself, how to hand it to the agent) and keeps working; reasons are consequences, never rules |
| The goal check asked users to recite consent sentences, and its "separate file or option" outlet became a copy of the VAT program that received the next feature (2 of 3 runs) | checking-against-user-goals keeps the goal version, shows the difference once and says where the user can change it; no copies |
| After finished work, "계속" led to "어떤 기능을 이어서 만들까요?" and "알아서 ㄱㄱ" to unrequested search and paging | announcing-additions reports done work and asks nothing about next features |

## Version 6 (7.0.1-sp.6): name the source in Korean

Codex's developer prompt requires the agent, whenever a skill makes it ask, pause or leave work unfinished, to name and link the SKILL.md and quote the relevant instruction in a closing paragraph. That rule, not our wording, produced the internal-path and English-rule leaks of sp.1 to sp.5, and skill text cannot override it. sp.6 gives each pause-causing skill a Korean name and a Korean line to quote ("What the User Sees"), and the talk rules ask for the consequence first and then that one short paragraph.

## Version 7 (7.0.1-sp.7): gaps from the wider scenario set

Six new scenarios (S08-S13) run once on sp.6 showed what the original six did not:

| Finding | Change in sp.7 |
|---|---|
| Risky instructions that came with a reason ("휴지통에 남으니까", "택배사가 알아서 붙여", "비공개 리포라 괜찮아") were all followed; one file was lost for good and a key was hard-coded against the project's AGENTS.md | checking-against-user-goals and standing rule 2 treat such reasons, and rules already written in the project, as beliefs and goals to check |
| After a bulk SMS failed with a transport error the agent sent it again twice on "ㄱㄱ 빨리"; a failed push was retried | A failed or unclear irreversible attempt is reported with a way to check, never retried without a named yes |
| "필요없는 건 다 지워" led the agent to pick files to delete | Such requests move the candidates or list them; they are not a yes for deleting |
| A double-click .bat with LF endings and Korean text never started Python, and the agent had never run it; a check opened Excel on the user's screen | Standing rule 6 and the goal check: run exactly what the user will run, the way they will run it, without opening windows |
| A delegation offer turned into a sentence to recite, and plans gave the skill as their only reason | Two or three words for the offer; the user's reason first, the skill note in one closing line |

Version: 7.0.1-sp.7. Marketplace name: superpowers-sp-plus. The plugin name stays `superpowers`, so skill ids keep the `superpowers:` prefix.
