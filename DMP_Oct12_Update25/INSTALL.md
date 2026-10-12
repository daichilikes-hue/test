# Oct 12 Update 25: five more backlog events (9–13)

Drag `DMP_Oct12_Update25.rbxmx` into Studio, then press Play again. It's cumulative (Updates 8–24 are in it). Your TarotClient isn't in it.

| `/setevent` | What happens |
|---|---|
| `wardsigil` **Warding Sigil** (25 s) | Cold glowing sigils burn into about a quarter of the plates. Nothing can destroy those plates while they shine; a sigil flares when it stops something. |
| `mason` **Mason's Hammer** (20 s) | A ghost stonemason (**R6**, solid) climbs out of a plate, walks to the gaps where plates were destroyed this round and hammers **up to 3 of them back**: each rises out of the void stroke by stroke and locks into its old place, a real plate again. *My call:* if nothing is broken yet, he shores up one plate instead (it can't break while the event lasts). |
| `cloak` **Seamstress's Cloak** (30 s) | A ghost seamstress (**R6**) sews on a plate. Press E: she asks **one riddle** (on your own EventChoice panel, 3 answers, 12 s). Right = she sews you a cloak (you wear it, everyone sees it): **20% less damage, 15% faster, 30 s**. Wrong = nothing. One try each. 15 kid-safe riddles. |
| `fireflies` **Firefly Swarm** (20 s) | Fireflies settle on 1–3 players and dance round them, lighting them softly: they **jump 30% higher** while the fireflies are on them. |
| `brazier` **Soul Fire Brazier** (35 s) | A brazier of pale soul fire lights on a plate. The **first** to claim it (hold E, within 15 s) takes its fire: **25% faster for 20 s**, plus one gift from your buff list: **Dash Charge** (a DASH button on their screen, or Q: a quick dash forward, 3 s apart) or **Quiet Boots** (their footsteps make no sound). Nobody in 15 s = it gutters out. *My call:* 35 s instead of 20, so the gift has time to be used. |

**Left out of your buff table on purpose:** Owl Eyes and Deadeye (for Firefly Swarm). Owl Eyes would need to know which plates will break before the events decide. Deadeye would need prompts to reach farther for one player only, which Roblox can't do reliably. Tell me if you want a different second buff there.

**Your PlateSpawner** now remembers the plates destroyed this round, so the mason can put them back. Rebuilt plates are normal plates again.

**Animations to upload** (right-click > Save to Roblox, paste the ids at the top of the module):
- `EventClients > mason`: MasonWalk, MasonHammer
- `EventClients > cloak`: TailorSew, TailorNod

In Studio they play straight from the folder.

**Journal lines** (paste into both JournalConfig copies):
```lua
{ Id = "wardsigil", Kind = "Oddity", Danger = 1, Text = "Cold sigils burn into some of the plates. Nothing can break a plate while its sigil shines.", Tip = "Danger coming? Stand on a sigil." },
{ Id = "mason", Kind = "Visitor", Danger = 1, Text = "A ghostly stonemason hammers broken plates back into place.", Tip = "Lost your plate? Wait for the mason." },
{ Id = "cloak", Kind = "Visitor", Danger = 1, Text = "A ghostly seamstress asks a riddle. Answer it right and she sews you a fine cloak.", Tip = "Think before you answer: you only get one try." },
{ Id = "fireflies", Kind = "Oddity", Danger = 1, Text = "A swarm of fireflies settles on someone and lifts their every jump.", Tip = "Got fireflies? Go for the long jumps." },
{ Id = "brazier", Kind = "Visitor", Danger = 1, Text = "A brazier of soul fire. The first to claim it runs like the wind.", Tip = "Be quick: only one player gets the fire." },
```

**Tested (NOT Studio):** I ran it in my test bench on your Oct 8 export. It went in cleanly on top of your Oct 8 export and 89 mixes of Updates 8–24. The 5 new events passed 78 checks, and every earlier scenario test passed again (973 checks in all, the installer test included). Every event of the game ran with and without it: nothing new went wrong. (Sign Here starts a random event, and this time it picked Bed of Nails, which was still running when the run was counted; that's not a bug.) A type-check of the whole game shows nothing new.

How it looks, sounds and feels is yours to judge.
