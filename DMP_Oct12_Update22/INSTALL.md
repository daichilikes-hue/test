# Oct 12 Update 22: LANTERN PROCESSION (your backlog, healing event 2)

**Always install the WHOLE file** (drag `DMP_Oct12_Update22.rbxmx` into Studio; the DMP Installer does the rest).
Scripts pasted in one by one are not enough. Then press Play again. To see it at once: `/setevent procession`.

It is cumulative like the others: it holds everything since your Oct 8 export (Updates 8 to 21 too), so skipping one is fine.
**Gentle Rain (Update 21) shipped right after Cloud in a Bottle** in the last chat. If you never installed it, this file brings it in too (`/setevent gentlerain`); its Journal line is at the bottom.
Your **TarotClient is NOT in it** (you changed its sounds yourself): your copy stays exactly as it is.

## What it is
"Lantern Procession (20 s): 2-3 ghost bearers walk a lap across the plates carrying pale lanterns. Anyone within about 8 studs of a lantern regenerates."

- **2 or 3 ghost bearers** rise out of the plates and walk **one slow lap** (about 10 studs a second) over the ring of plates round the middle, spread out evenly, then fade away at the end.
- **Anyone alive within 8 studs of a bearer heals 1 HP every half second** (2 HP a second, on top of your normal 1 HP a second regen). Two lanterns at once do **not** stack.
- **No circle, no ring:** the lantern's own pale light on the plates is about as big as its reach (Range = 8 + 2 studs). A faint sparkle on whoever it heals, the lantern flares a little, and a soft chime on your own screen (at most every 3 s).
- They **float**, so they cross the gaps between the plates, and they rise over a plate that is higher than the rest (Risen Crypt, Rising Tomb ...).
- One toast: "Lantern Procession".

## The bearer is an R6 character (your standing order)
The model **Bearer** under `ServerScriptService > Events > LanternProcession`: HumanoidRootPart, Torso, Head, arms and legs on the six standard Motor6Ds, a Humanoid with an Animator. Hooded moss-grey robe (a little see-through: he's a ghost), a dark face with two faint eyes, bony hands, rope belt, tattered hem; the **rusted iron lantern** (Bail, Cap, Post1..4, Glass, Flame with the PointLight `Light` and the emitter `Motes`, Base) is **welded to his right hand**. Restyle him freely in Studio; keep the R6 parts, `Flame > Light`, `Flame > Motes`.

**His walk: `BearerWalk`** (1.8 s loop: a slow solemn glide, head bowed, the lantern held out in front), a KeyframeSequence in `ReplicatedStorage > EventClients > procession > Animations`.
- In Studio it plays straight from there.
- For the real game: **right-click it > Save to Roblox**, then paste the id into `ANIMATIONS` at the top of `EventClients > procession` (`BearerWalk = <id>`). Later updates keep your id.
- Not uploaded yet: he glides with his lantern arm held out (no walk). Output says so once per client (same line the banshee had).

## Event Journal (please paste this)
Your `Shared > JournalConfig` has no page for a new event (it would show the Unknown text and never be earned). Paste this line into **both** of your JournalConfig copies, with the other entries:

```lua
{ Id = "procession", Kind = "Visitor", Danger = 1, Text = "Ghosts in hooded robes walk a slow lap over the plates, each holding out a pale lantern.", Tip = "Walk in their lantern light. It heals you while you stay close." },
```
(Visitor = the page fills in the first time a lantern heals you.)

Gentle Rain's line, if you have not pasted it yet:
```lua
{ Id = "gentlerain", Kind = "Oddity", Danger = 1, Text = "A soft grey rain falls over the whole arena. It heals everyone a little every second and puts out any fire.", Tip = "Hurt? Stand in it. While it rains, fire can't touch you." },
```

## Knobs
`ServerScriptService > Events > LanternProcession` (top):
| Knob | Now | What |
|---|---|---|
| DURATION | 20 | seconds |
| MIN_BEARERS / MAX_BEARERS | 2 / 3 | how many ghosts (at random) |
| RADIUS | 8 | studs from a bearer that his lantern heals (seen from above) |
| REACH_UP / REACH_DOWN | 9 / 3 | how far above / below the ground he floats over your feet may be |
| HEAL / TICK | 1 / 0.5 | HP every TICK seconds (= 2 HP a second) |
| LAP | 0.42 | how far out the lap goes (0 = middle, 1 = the outer edge of the plates) |
| CORNER | 10 | how round its corners are |
| LAPS | 1 | laps in DURATION (the speed follows from it) |

`ReplicatedStorage > EventClients > procession` (top): BEARER_SCALE 1.1, HOVER 1.2 (studs over the plate), RISE 2.5, FADE 1.5, CLIMB 4, LIGHT_EXTRA 2 (light Range = RADIUS + this), LIGHT_FLICKER 0.12, CHIME_EVERY 3.
Sounds (`SOUNDS`, kept by later updates): **LanternChime** (a stand-in ping: put your own soft bell in) and **BearerRise** (silent until you give it an id).

## New in your game
- `ServerScriptService > Events > LanternProcession` (ModuleScript) + the model `Bearer` under it.
- `ReplicatedStorage > EventClients > procession` (ModuleScript) + the Folder `Animations` with `BearerWalk` under it.
Both are new because a new event is one Events module + one EventClients module. Nothing of yours changed; no shared script changed.

## Tested (NOT Studio)
Run in my test bench on your Oct 8 export (your real scripts, no Roblox): the package installed by its own installer (55 installer checks), on top of mixes of Updates 8 to 21; the procession played (27 checks: 2-3 R6 bearers for everyone, one lap at an even pace, ending where they started, floating 1.2 studs over the plates and rising over a raised plate, fading in and out, the walk playing in Studio and the lantern held out without it; following a bearer healed 39 HP in 20 s, waiting on the lap healed 6, the middle plate 0, no stacking, a sparkle for every heal and only then, one toast); every earlier scenario test again (755 checks in all, 0 failed); every event of the game once with and once without the update (smoke test); a Roblox type-check of the whole game: nothing new.
**How it looks, sounds and feels is yours to judge**: the bench draws no lights, glow or particles. `Procession_preview.png` = his walk (contact sheet) and two bench stills.
