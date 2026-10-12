# Oct 12 Update 26: four more backlog events (14–17)

Drag `DMP_Oct12_Update26.rbxmx` into Studio, then press Play again. It's cumulative (Updates 8–25 are in it). Your TarotClient isn't in it.

| `/setevent` | What happens |
|---|---|
| `owl` **Owl's Feather** (20 s) | A great grey-brown owl glides across the arena and drops 3–5 feathers that drift down onto plates. Hold E to take one (**one each**): for 12 s you fall slowly (your gravity ×0.4: higher jumps, gentle falls), with the feather tucked in your back for everyone to see. |
| `horseshoe` **Lucky Horseshoe** (20 s) | An old horseshoe is nailed to a plate, glinting. The **first** to pry it loose (hold E) gets **Lucky Landing**: the next time they fall off this round, they're put straight back on the nearest plate. Once. |
| `blackcat` **Black Cat's Favour** (25 s) | A black cat pads from plate to plate, stopping to sit. Catch up and pet it (hold E, **once each**) for a bit of luck: **Grave Luck** (an item you don't have yet), **Plate Magnet** (30 s: fall off near a plate and you're pulled gently back toward it) or, rarely, **Borrowed Time** (a hit that would knock you out leaves you at 1 HP instead, once; not the void). |
| `dig` **Digging Site** (25 s) | A dig spot with a shovel stuck in it. Hold E to dig: a timing bar comes up on **your** screen; press (Space, E, click or tap) while the marker is in the lit zone. 3 good strokes = a random item; a miss jams the shovel for 1 s. One digger at a time; walk away and someone else can carry on. Judged on the server. |

The new buffs (Lucky Landing, Plate Magnet, Borrowed Time, Grave Luck) live in `Systems > EventUtil.Buff`, so later events can give them too.

**Journal lines** (paste into both JournalConfig copies):
```lua
{ Id = "owl", Kind = "Visitor", Danger = 1, Text = "An owl glides over the arena, dropping feathers. Hold one and you float down gently.", Tip = "Grab a feather before a big jump." },
{ Id = "horseshoe", Kind = "Oddity", Danger = 1, Text = "A lucky horseshoe is nailed to a plate. Whoever pries it loose is caught the next time they fall.", Tip = "Be first to the horseshoe!" },
{ Id = "blackcat", Kind = "Visitor", Danger = 1, Text = "A black cat wanders the plates. Pet it for a bit of luck... if you can catch up with it.", Tip = "Cut it off at its next stop." },
{ Id = "dig", Kind = "Oddity", Danger = 1, Text = "Something is buried in one of the plates. Dig it up with good timing.", Tip = "Wait for the marker to reach the light, then press." },
```

**Tested (NOT Studio):** I ran it in my test bench on your Oct 8 export.
- It went in cleanly on top of the export, on top of Updates 8–25 in a row, and on 89 other mixes of earlier updates.
- The 4 new events passed 39 checks, and every earlier scenario test passed again (1012 checks in all).
- Every event of the game ran with and without it, and nothing new went wrong. (Sign Here started a random event that was still running when the run was counted; that's not a bug.)
- A type-check of the whole game shows nothing new.

How it looks, sounds and feels is yours to judge.
