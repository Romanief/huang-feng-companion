# Current release: Spiderbite Daggers

-49 automated tests passed: main-hand/off-hand totals, negative ability modifier handling, poison2d4 and DC override, trigger guard, critical/Lucky separation, schema-v4 migration/backup/override mapping, and all prior rules/storage checks.
- Production build passed.
- Browser checks through the real UI passed on a separate localhost origin: unnamed-Focus off-hand+10 /1d4+0; Studied Strike adds its own d8 and marks used; no poison controls before confirming both dagger hits; failed CON18 save records Poisoned through end of target's next turn and rolls exactly two d4; success does not create another effect or damage roll; a main-hand critical uses two weapon d4; HP/ink/Robes/reactions unchanged.
- Mobile390×844 and landscape844×390 dialogs fit without internal horizontal overflow. No physical iPhone test.

# Current release: Intelligence22 Tome benefit

-44 automated model/rendered-HTML tests passed, including exact updated saves, AC21, initiative+8, DC18, INT skills/passive Investigation, Focus weapon totals and Robes+6 support.
- Legacy saves migrate once to schema-v3 with a raw pre-Tome local backup. Deterministic tests confirm resources, notes, old rolls, current initiative and explicit fixed overrides are retained; an existing INT22 is not raised again and a higher score is not lowered. Later manual edits and JSON backups round-trip.
- All item effect DCs continue to follow the character DC. Summed2d8 support and unnamed Focus choices remain available.
- Production build passed. Browser interaction checks were unavailable; earlier records below are historical.

# Current follow-up: summed damage and optional Focus names

- Potent Observation against Focus always sums both d8s; a deterministic3+7 test returns10 with both dice kept. Its obsolete DM setting is removed and old v2 saves ignore it safely. Generic overlapping Intellect check bonuses still keep the highest.
- Attack and Potent Observation Focus options remain enabled without a tracked name, including Flourish counterattacks. The Focus editor accepts a blank name and records Unnamed Focus on confirmation. Stored Focus is not automatically altered when choosing a roll target.
-40 automated model/rendered-HTML tests and production build pass. Browser interaction checks remain unavailable in this chat.

# Current release: level 10

- 40 unit/rendered-HTML tests passed: exact level-10 stats (HP maximum 83, 10d8, PB +4, AC 20, DC 17), fixed saves/skills, rest recovery 5, summed 2d8 Focus support, non-Focus damage support, dynamic item DC overrides, save migration/backup/idempotence, export/import and unchanged dice/resource rules.
- Strict TypeScript compilation and the GitHub Pages production build passed.
- Rendered React HTML confirms level-10 identity, Unrivaled Genius, matching card/dialog/equipment DCs, and absence of the prior level-9 restrictions. These are markup checks, not browser interaction checks.
- Browser access was unavailable; new Flourish button flows, responsive visual checks, offline browsing and physical iPhone validation were not performed on this release. Publishing uses authenticated local Git. Deployment verification is recorded separately from these local checks.
- Original reference PDFs were read only.

The following is the historical verification record for earlier level-9 versions. Its HP/rest/schema expectations are not current release criteria.

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

## Streamlined targeting and stable portraits · 19 October 2026

The latest build passed TypeScript compilation and all32 core tests. Eleven focused browser checks were performed through the rendered UI in an isolated localhost origin:

- All six selected poses keep identical portrait/art slots, HP, stat, resource and vital-section bounds at1440×1100,390×844,320×568 and844×390. Gallery cards/art slots also match, with no horizontal overflow.
- Initiative swaps to fighting art without changing those same bounds at all four sizes.
- All four Words, all three reaction dialogs and Rope have no prerequisite confirmation checkboxes. Blank target fields leave use buttons available. Merely inspecting the cards spends nothing.
- Blank Dread target rolls psychic damage and records an unnamed target effect. Blank Rope target records Restrained only after a marked failed save. Help accepts an unnamed ally.
- Robes and Flourish spend the correct charges/reactions, enforce one reaction per event and retain their spent values after reload.

The existing repeatable browser script was updated for the removed checkboxes and optional-field labels. Its complete historical19-scenario suite was not rerun for this revision. Current focused results are retained locally in `qa/streamlined-controls-results.json`. No physical iPhone/Safari test was performed.

## Scroll rendering mitigation · 19 October 2026

Replaced full-subtree CSS clipping and negative-layer backgrounds on the 41 card/stat/HP/ability frames with painted nine-slice SVG borders. Removed the sheet-wide isolated stacking context. Finished dice animations now release their transform/opacity effects. Pixel styling and box dimensions are retained. Phone Focus cards now stretch consistently to their column width.

TypeScript and production build passed. Rendered UI checks covered repeated up/down scrolling at desktop and390×844, dice rolling while scrolling, release of completed dice transforms, phone card widths342px, no horizontal overflow, and the HP dialog at844×390. No blank cards or persistent flashes were observed in these checks. The reported intermittent flicker was not reliably reproduced before the change, so these checks cannot prove resolution on every browser/GPU. No physical iPhone/Safari test was performed. Game logic and storage were not changed.

## Pixel cursors · 19 October 2026

Added original32×32 cream/gold pixel arrow and hand SVGs as native CSS cursors, with standard cursor fallbacks and no pointer-following JavaScript. Fine-pointer/hover devices use the arrow on static text, the hand on controls and their child text/icons, the text cursor in editable text/number fields and notes, and not-allowed on disabled controls. Text remains selectable; touch controls and save data are unchanged.

Production build passed. Rendered-browser computed-style checks passed for headings, initiative button text, disclosure summaries, journal textarea, HP number inputs and a disabled Deduction button. Browser-selected cursor assets are bundled into the stylesheet and available in the offline shell. No physical Safari pointer test was performed.
