# Oct 12 Update 27: the last four backlog events (18–21)

Drag `DMP_Oct12_Update27.rbxmx` into Studio, then press Play again. It's cumulative (Updates 8–26 are in it). Your TarotClient isn't in it. **That finishes the backlog: all 21 events are in.**

| `/setevent` | What happens |
|---|---|
| `patch` **Pumpkin Patch** (20 s) | 6–10 small pumpkins sprout on the plates. Hold E to smash one (**2 each**): **+20 HP**, **20% faster for 10 s**, **an item**, or **Hop Stone** (your next 2 jumps go higher). What came out floats over the pumpkin on your screen. |
| `ghostpop` **Ghost Pop** (30 s) | Old bones lie on the plates and a ghost dog waits on one. Pick up a bone (**one each**): it's in your hand. **Click** = crush it: an item, **−5 soul**. **TOSS** (a button on your screen, or T, or drop it) = an item. **Give it to the dog** (hold E at the dog) = an item, **+5 soul**. |
| `smores` **Smores** (25 s) | A campfire on a plate, a marshmallow on a stick for each player (+1). Hold E to roast one (**once each**): **+10 HP** and one buff: **Shared Warmth** (30 s: everyone within 6 studs of you, you too, heals 1 HP a second), **Thick Skin** (30 s: the first hit of each kind, fire / poison / bleed / everything else, does half damage) or **Second Wind**. |
| `confession` **Midnight Confession** (20 s) | An old confession booth grinds up out of a plate, a bell on its roof. Step in and hold E (**once each**): the bell tolls and **one curse is lifted**: a stat shift that makes you weaker (Weighing of the Heart and the like) or, if you have none, a burn / poison / bleed (and that kind of damage can't hurt you for 6 s). *My call:* nothing to lift = +5 HP, so the walk is never wasted. |

**Your buff list, what I did with it here:**
- **Hop Stone** is "Jump ×1.3" for your next 2 jumps, the same as Firefly Swarm's jump. Your game uses JumpPower, so that's 30% more jump *power* (the jumps go about 1.7× as high). Change `EventUtil.HopStoneBoost` to taste.
- **Quick Hands** and **Keen Nose** (Pumpkin Patch) are left out. Quick Hands would need prompts to be faster for one player only, which Roblox can't do reliably. Keen Nose would make pumpkins / bones / dig spots glow for one player, but those are already easy to see. Tell me if you want a different one.
- **Midnight Confession never touches** item effects, feed / haunt effects or contract prices: only the stat-shift events' debuffs and burns / poison / bleeding.

**Changes to YOUR scripts** (on top of your Oct 8 copies; the installer keeps a backup):
- `Systems > StatShift`: new `StatShift.Debuffs(player)` and `StatShift.Cure(player)` (ends the newest shift that makes you weaker, quietly). Your stat-shift events work exactly as before.
- `Systems > EventUtil`: the buffs Hop Stone, Shared Warmth, Thick Skin, and `EventUtil.Cure`.

**Journal lines** (paste into both JournalConfig copies):
```lua
{ Id = "patch", Kind = "Oddity", Danger = 1, Text = "Pumpkins sprout on the plates. Smash them open: there's always something inside.", Tip = "Two each, so pick your pumpkins." },
{ Id = "ghostpop", Kind = "Visitor", Danger = 1, Text = "Old bones and a hungry ghost dog. Crush a bone, toss it, or give it to the dog.", Tip = "Be kind to the dog: your soul will thank you." },
{ Id = "smores", Kind = "Oddity", Danger = 1, Text = "A campfire with marshmallows round it. Roast one for a warm little blessing.", Tip = "Stay close to friends with Shared Warmth." },
{ Id = "confession", Kind = "Visitor", Danger = 1, Text = "An old confession booth rises. Step inside and its bell lifts a curse from you.", Tip = "Cursed by a stat shift? Run to the booth." },
```

**Tested (NOT Studio):** I ran it in my test bench on your Oct 8 export.
- It went in cleanly on top of the export and on 96 mixes of Updates 8–26.
- The 4 new events passed 71 checks:
  - all four pumpkin outcomes really give what they say;
  - crush / toss / dog / drop each give the item and the right soul change;
  - Thick Skin halves only the first hit of each kind, and Shared Warmth heals only the people near you;
  - the bell lifts a curse but not a good boon.
- Every earlier scenario test passed again (1083 checks in all). Every event of the game ran with and without it: nothing new went wrong. A type-check of the whole game shows nothing new.

How it looks, sounds and feels is yours to judge.
