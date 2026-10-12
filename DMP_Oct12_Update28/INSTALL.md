# Oct 12 Update 28: your four fixes (Death Ledger, Photoshoot, The Circles, the Werewolf gun)

Drag `DMP_Oct12_Update28.rbxmx` into Studio, then press Play again. It's cumulative (Updates 8–27 are in it). Your TarotClient isn't in it.

## Death Ledger, rebuilt from your idea (`/setevent ledger`)
1. **The tome** (a new model: an old ledger, open, a blood-red seal on its pages, chains, loose pages circling it) floats and wanders over the arena, a little too high to touch. **Jump into it to catch it.** Nobody catches it in 30 s = it picks someone at random and swoops down to them.
2. **The seal puzzle** (a new panel, only on the holder's screen): six runes round a seal. The tome lights some of them one after another; **press them in the same order** (click / tap, or keys 1–6). Wrong = it shows you the order again. 25 s to break the seal, or the ledger refuses you and bites (−15).
3. **Seal a name**: your EventChoice player panel (nobody chosen in 10 s = the ledger picks).
4. **The curse**:
   - **The reaper** (a new R6 character: hooded robe, skull face, scythe) floats behind them.
   - **A clock** over their head counts down **60 s** (everyone sees it).
   - The one who sealed it is marked **"THE CURSER"** for everyone, and outlined in red on the cursed player's screen.
   - Every 10 s the cursed player gets **a quick riddle**: a slim strip at the top of their screen that never covers the middle, 3 s, three answers (keys 1–3). The riddles are quick sums, the biggest number, counting dots, "what colour is the word", or the odd one out. **Wrong or too slow = −20 s.**
   - **The only way out: knock out the curser before the clock runs out.** The clock runs out = the reaper's scythe comes down.

**Animations to upload**: `EventClients > ledger > Animations`: **ReaperHover**, **ReaperReap** (right-click > Save to Roblox, paste the ids at the top of the module). In Studio they play from the folder.

## Vampiette's Photoshoot (`/setevent photo`)
One star per player alive (on random plates) instead of a star on every plate. `STARS_PER_PLAYER` at the top if you want more.

## The Circles (`/setevent circles`)
- **Only SOME plates get a rule now**: about 40% of them, at most 12. Each one has a **Highlight with OutlineTransparency 0** in its rule's colour (and a soft pulsing fill), and **a sign over it** naming the rule. Every other plate is plain and **safe**.
- **The rules are spelled out**: a panel on the left of every screen lists the 3 rules in play, one line each, in their colours, marks **"◄ YOU"** on the one you're under, and counts down to the next set.
- Clearer names: **SLOW**, **SLIPPERY**, **HEAVY**, **NO JUMPING**, **HOT FLOOR** (standing still burns you).
- A rule is on you **while you stand on its plate**; step onto a plain plate and it wears off. (It used to stick until you reached another ring.)

## Werewolf Moon: the gun
**Why it didn't work**: `ReplicatedStorage > EventClients > werewolf` was missing from your game. It came with the Oct 8 update and didn't get in. The server checks every shot, but it only hears a shot when that module sends the click. It's rebuilt here from your `Events > WerewolfMoon` (your server script is unchanged): the hunter gets a crosshair, a click / tap fires (0.4 s apart), and everyone sees the silver streak, "-8" on the werewolf, "OOPS!" when the hunter hits someone else.

**Journal line** (your JournalConfig has no Death Ledger line yet: add it to both copies):
```lua
{ Id = "ledger", Kind = "Hunter", Danger = 3, Text = "A cursed ledger drifts over the arena. Whoever catches it can seal a name, and the reaper comes for them.", Tip = "Cursed? Knock out the one who wrote your name before your clock runs out." },
```

**Tested (NOT Studio):** I ran it in my test bench on your Oct 8 export.
- It went in cleanly on top of the export and on 99 mixes of Updates 8–27.
- The four fixes passed 76 checks:
  - **Werewolf**: the hunter's click hits the werewolf for 8; friendly fire costs the hunter 10; a miss hurts nobody; the 0.4 s fire rate holds; the crosshair comes and goes. The "No client module for 'werewolf'" warning your game printed (8 times in my run of every event) is gone.
  - **Photoshoot**: 3 players get 3 stars and 6 players get 6, and standing on one still gets you in the picture.
  - **The Circles**: only some plates get a rule; each is outlined; the panel and "◄ YOU" work; a plain plate is safe.
  - **Death Ledger**, played both ways to the end:
    - standing under the tome doesn't catch it, jumping into it does;
    - the puzzle ignores early presses, shows the order again after a wrong rune, and breaks on the right order;
    - the name is chosen on your player panel, the reaper, clock and mark show for everyone, and the riddle strip only for the cursed player;
    - a right answer costs nothing and a wrong one takes 20 s;
    - knocking out the curser saves you, and letting the clock run out gets you reaped.
- Every earlier scenario test passed again (1159 checks in all). Every event of the game ran with and without it, and nothing new went wrong. A type-check of the whole game shows nothing new.

How it looks, sounds and feels is yours to judge.
