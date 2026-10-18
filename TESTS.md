# Verification record

Production source was checked with TypeScript strict compilation, 32 Node tests and 19 browser scenarios for the redesigned one-page pixel sheet. Browser results and timestamps are in `qa/browser-results.json`. Chrome ran in a separate temporary profile; deterministic dice inputs were injected only into that test browser.

| Requested case | Evidence and result |
| --- | --- |
| 1 · canonical level 9 | Unit: HP 75, AC 20, initiative +7, PB +4, d8, DC17, speed30/40, reactions2. Passed. |
| 2 · six saves | Unit: +4/+7/+8/+14/+9/+4; separate mental d8. UI INT roll 10+14+6=30. Passed. |
| 3 · skills and tools | Unit: all18 definitions; Stealth10, Investigation9+d8, Arcana9+d8, Sleight7, lock11. UI Investigation advantage/Lucky+d8. Passed. |
| 4 · rapier Focus / other | UI Focus +11, 1d8+7 and Studied Strike; critical 4d8+7=29. Other +8, 1d8+4, no Studied checkbox. Unit crossbow/dagger totals too. Passed. |
| 5 · ink rider | UI inspecting and rolling leaves4; confirmed hit/use changes4→3; DC17; failed save records Blinded. Unit rejects unconfirmed hit/use. Passed. |
| 6 · Robes | UI5→4, reactions2→1. Short rest leaves item charges; long rest restores5. Same event cannot take another reaction. Passed. |
| 7 · Potent Observation | UI only permits save, proficient skill/tool check, or damage vs Focus; no attack/non-Focus damage option. Passed. |
| 8 · Flourish | UI roll5 gives AC25 only; no counterattack/movement controls. Level9 feature test excludes later upgrades. Passed. |
| 9 · long rest | UI preview/cancel changes nothing; confirm HP75, HD0→4, Robes5; ink2 and tattoo consumed remain. Passed. |
| 10 · dawn | UI d4=3 with ink2 previews4, commits only on confirmation. Unit cap checked. Passed. |
| 11 · end combat | UI HP23, Robes1, ink2, tattoo consumed, Focus and notes all preserved. Unit exact equality except combat boolean. Passed. |
| 12 · Lucky initiative | UI raw1→replacement12, total19 with+7; both values visible. Unit replacement1 stays final. Passed. |
| 13 · non-Focus Words | UI Confound on another hearing target: reaction + failed save +2d8=8. Dread action success offers no damage. Passed. |
| 14 · persistent session | Browser reload retains notes, Focus, HP, charges, consumed tattoo, initiative, round and combat portrait. Unit serialization does not depend on elapsed wall time. Offline reload passed. |
| 15 · backup | Real downloaded JSON, validated preview, confirmed import in a fresh browser context restores all fields except the new write timestamp. Malformed/future saves rejected. Passed. |
| 16 · narrow / landscape | All continuous-sheet sections, inline editing and quick controls at320×568,390×844,844×390; no horizontal document overflow, enabled controls at least44px. Dialog and card screenshots inspected. Desktop1440×1100. Passed in Chrome. |

Additional checks: standard temporary HP expire on long rest but persist on End Combat; CON edits recompute HP while a manual max-HP override survives; rope target-action DEX escape failure retains Restrained and success removes it; Help records advantage; Focus blocks tattoo casting; tattoo consumption and explicit minute advancement persist; a deployment-style subpath also works offline.

## Limits

No physical iPhone or Safari/WebKit install test was performed. Responsive Chrome is not proof of Safari behaviour. The original build validation did not include live deployment, a hardware endurance test, multi-week real-device retention or a remote GitHub Actions run. Managed Sites publication is handled separately. Enemy save outcomes, action economy, condition/effect durations and ammunition are intentionally DM/player-managed.

## Pixel-sheet redesign

The old page navigation was removed. Automated browser checks confirm one continuous sheet contains six abilities, six saves, all18 skills and all six supplied poses. Existing schema-v1 saves, Focus, notes, resources, combat mode and round survive. Pixel fonts and the new reference image load offline. The redesigned browser report contains19 scenarios; the unchanged rule/storage utilities retain32 passing unit tests.

## Compact window, dice and collapsed sections

- Desktop Focus tested at1440×1100: width400px, lower-right placement, no modal backdrop; underlying roll-mode control remains usable and preserves the draft. Escape cancels without changing saved Focus.
- Focus remains modal at390×844 and844×390 landscape. Optional discovery fields expand and save successfully in the initiative flow.
- Class features, equipment and character bonds start collapsed and toggle using both mouse click and keyboard Enter. Session notes remain accessible.
- INT save displays distinct d20 and d8 polyhedral silhouettes. The five-second popup timer restarts for another roll, hides automatically and keeps all saved history.
- Responsive controls, item/rest confirmations, export/import, reload persistence and offline caching all passed again. Animation respects reduced-motion CSS; no physical iPhone test was performed.

## All desktop popups

The shared popup treatment was extended to HP, all three rests, all three weapons, Words of Power, reactions, rope, tattoo, Help, conditions, history, Deduction and confirmations. Browser checks verified400px width, a620px maximum height, lower-right placement, access to the sheet behind the popup and no internal horizontal overflow. HP damage and healing both saved correctly. Switching from a rolled Dawn preview to Short Rest starts a fresh preview, and mobile HP remains a responsive modal. All19 browser scenarios passed on this revision; the rule/storage utility code was unchanged.
