# Oct 12 Update 24: the Lantern bearer is solid (hotfix)

Drag `DMP_Oct12_Update24.rbxmx` into Studio, then press Play again. It's cumulative: it includes Updates 8–23, so it's fine if you skipped one. Your TarotClient isn't in it.

## Why it was 0.001
Two things, both mine:
1. **The 0.001 was a bug in my fade-in code.** It only updated the transparency when the fade had moved more than 0.01, so the very last step to "fully solid" never happened. He stayed at about 0.001 for the whole event.
2. **His robe was see-through on purpose.** I'd made him "ghostly": the cloth was 18% see-through, the tatters 20%, the cuffs and hands 10–15%, and his legs were invisible.

## What changed
- **The bearer is solid all the time.** No part of him is see-through. The only exceptions are the lantern's Glass pane and the invisible HumanoidRootPart, which every character has.
- **He no longer fades in and out.** He climbs up out of the plate at the start and sinks back into it at the end. If you ever want the fade back, set `SEE_THROUGH = true` at the top of `EventClients > procession`.
- **This update replaces your Bearer model** with the solid one. If you changed the old one, your copy is in `ServerStorage > DMP_Backups`.
- **The same 0.001 bug was in Bone Baker, Ghost Guardian and Gargoyle Ward.** I fixed it there too: they now end exactly solid, or exactly at the look their model was built with. Death Pulse (the banshee) has the same code, but you said it's great, so I left it alone. Say if you want it fixed there too.

## Tested (NOT Studio)
I ran it in my test bench on your Oct 8 export:
- **The fix itself:** he is never see-through, not even 0.001, at any moment of the event, and he climbs out of the plate at the start.
- **Everything else:** 840 scenario checks pass on the installed game, it installs cleanly on top of 87 different mixes of earlier updates, every event of the game runs with nothing new against Update 23, and a type-check of the whole game shows nothing new.

How he looks is still yours to judge in Studio.
