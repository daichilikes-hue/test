# Oct 12 Update 23: SIX BACKLOG EVENTS + small stat buffs for the healing events

**Always install the WHOLE file** (drag `DMP_Oct12_Update23.rbxmx` into Studio). Then press Play again.
Cumulative: Updates 8 to 22 are in it too. Your **TarotClient is NOT in it** (you edited it): your copy stays.

Try them: `/setevent moss`, `/setevent lilies`, `/setevent baker`, `/setevent guardian`, `/setevent batnet`, `/setevent ward`

## The six events (backlog 3 to 8)
| Event | What happens |
|---|---|
| **Moss Bloom** (20 s) | Moss creeps over about a third of the plates (8 of 25). Standing on moss heals 1 HP every 0.75 s. It withers at the end, or at once if its plate breaks. |
| **Grave Lilies** (18 s) | 4–8 pale lilies bloom on random plates. Hold E to pick one (**one each**, so everyone gets a chance; `PER_PLAYER`): +10 HP, a buff (**Second Wind** or **Sure Footing**, from your buff list), 12% chance of a **Grave Lily** item. |
| **Bone Baker** (26 s) | A skeleton baker (an **R6 character** in a chef's hat and apron) climbs out of a plate and hurries plate to plate, hopping the gaps, setting down 4–6 trays. Each tray has 3 treats; hold E to eat (**one per tray each**): +20 HP, 25% chance of a random item (Cloud in a Bottle is in the pool). |
| **Ghost Guardian** (25 s) | A little friendly sheet ghost floats at one random player's shoulder and **takes their next hit** (a shield handler at priority 10). Then it flares and fades. It doesn't stop the void or other instant knock-outs (`BLOCK_KILLS`). |
| **Bat Net** (20 s) | Bats swarm under 1–3 plates. Fall off near one and they **toss you back onto that plate**, once; then that swarm flies off. |
| **Gargoyle Ward** (25 s) | A stone gargoyle (an **R6 character**) glides onto a plinth at a plate's outer corner. That plate **can't be destroyed** by any event (he rears up when it holds), and anyone on it takes **half damage**. |

The buffs (they live in `Systems > EventUtil.Buff`, so later events can give them too):
- **Second Wind**: the next hit that drops you below 25% health (and leaves you alive) heals you 15 at once. Once.
- **Sure Footing** (30 s): a plate you stand on crumbles 1.5 s later than it should.

## Small stat buffs for the healing events (your message)
Lantern Procession, Moss Bloom and Bone Baker now also give each player ONE small random stat buff for the rest of the round. **Gentle Rain does NOT** (left exactly as it was). Grave Lilies already gives its own buffs.
They go through **your StatShift** (the same thing as the stat-shift events: a Stats modifier, ended by being knocked out / the round ending, never the same one twice). The pool (`EventUtil.Boons`, change the numbers there):
**Stout** +10 max HP · **Mending** +0.5 HP/s regen · **Swift** +8% speed · **Springy** +10% jump · **Sturdy** −8% damage taken.
The player gets one toast naming it. They have no character visual (StatShiftVisuals has none for them). `BOON = false` at the top of an event switches it off there.

## Changes to YOUR scripts (made on top of your Oct 8 copies; the installer keeps a backup)
- **Systems > PlateSpawner**: `DestroyPlate` skips a protected plate (Gargoyle Ward) and waits 1.5 s for a Sure Footing player. New: `Protect`, `IsProtected`, `Saved`.
- **Systems > StatShift**: new `StatShift.Give(player, config)` / `StatShift.Has`. Your stat-shift events work exactly as before.
- Shared: `Systems > EventUtil` (Protect, Pin, Buff, Boon, Boons), `Shared > EventFX` (OnPlate, HoldPose).

## Animations to upload (right-click > Save to Roblox, paste the ids at the top of the module)
- `EventClients > baker > Animations`: **BakerWalk**, **BakerSet**
- `EventClients > ward > Animations`: **WardPerch**, **WardRoar**

In Studio they play straight from the folder. Until you upload them, the real game holds the baker and gargoyle in a fixed pose (the baker holds his tray out; the gargoyle sits still like a statue), and Output prints one "can't play yet" line.

## Sounds
Each client module has a `SOUNDS` block with Roblox stand-ins or silence. Put your own ids in; later updates keep them.

## Event Journal (paste into BOTH JournalConfig copies)
```lua
{ Id = "moss", Kind = "Oddity", Danger = 1, Text = "Soft moss creeps over some of the plates. Standing on it slowly heals you.", Tip = "Find a mossy plate and stay on it." },
{ Id = "lilies", Kind = "Oddity", Danger = 1, Text = "Pale grave lilies bloom on the plates. Picking one heals you and gives you a little luck.", Tip = "Only one each, so grab one fast!" },
{ Id = "baker", Kind = "Visitor", Danger = 1, Text = "A skeleton baker hurries across the plates, setting out trays of treats.", Tip = "Eat one from every tray. Sometimes there's something crunchy inside." },
{ Id = "guardian", Kind = "Visitor", Danger = 1, Text = "A little ghost floats at someone's shoulder and takes the next hit for them.", Tip = "If it picked you, you can take one risk for free." },
{ Id = "batnet", Kind = "Oddity", Danger = 1, Text = "Bats gather under some plates. Fall near them and they throw you back up, once.", Tip = "Fell off? Hope it was near the bats." },
{ Id = "ward", Kind = "Visitor", Danger = 1, Text = "A stone gargoyle guards one plate. It can't break, and it takes the edge off every hit.", Tip = "When things get rough, stand by the gargoyle." },
```

## Tested (NOT Studio)
I ran it in my test bench on your Oct 8 export:
- **Installer**: 55 checks, and it went in cleanly on top of mixes of Updates 8–22.
- **The six events**: 81 new checks, covering all of the following:
  - Moss on 8 of 25 plates heals about 25 HP over 18 s; a bare plate heals nothing.
  - Lilies: one per player; Second Wind and Sure Footing both really work.
  - Each tray appears exactly where the baker is standing; one treat per tray each; an empty tray goes away.
  - The ghost takes exactly one hit.
  - Falling near the bats throws you back onto the plate; the next person to fall there drops.
  - The warded plate survives a destroy while others break; damage on it is halved.
  - The boons are given once each, and Gentle Rain gives none.
- **Everything else**: every earlier scenario test passes again, every event of the game ran with and without the update, and a type-check of the whole game shows nothing new. Your stat-shift events still work.

How it looks, sounds and feels is yours to judge: `Update23_preview.png` has the models and the two new R6 characters' animations.
