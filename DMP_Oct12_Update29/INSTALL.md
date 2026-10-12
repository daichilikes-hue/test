# Oct 12 Update 29: your two to-do items (the tarot draw, safe plates in 1 / 2 plate rounds)

Drag `DMP_Oct12_Update29.rbxmx` into Studio, then press Play again. It's cumulative (Updates 8–28 are in it).

**⚠ This one DOES carry your TarotClient** (the draw changes live in it). It's your copy, with the sound fade you pasted in, plus the changes below. The installer will see that you edited TarotClient and **won't overwrite it at first**: click **Install update** again to let it through (the installer keeps a backup of yours).

## The tarot draw
- **A new setting: Settings > Gameplay > "Silent Tarot Draw"** (starts OFF). When it's on, your card is drawn for you in every countdown (like Auto Draw) with **no animation at all**: nothing comes up on your screen, no toast, and the little card stays face down. Clicking the little card draws silently too. (*My call:* if you click the little card afterwards, the small panel shows your card, so you can still check it if you want to. Nothing pops up by itself.)
- **A much longer window to draw**: you can draw at any time **except while you're alive in a round** (and the second it starts):
  - in the lobby **before the countdown**;
  - in the countdown, as before;
  - **after you're knocked out**: that card is for your **next** round, and it stays through this round's end;
  - while the round ends.
- Knocked out: the first click on the little card draws your next card; after that it opens your ghost flip, as before.
- Wheel of Fortune drawn outside the countdown waits for the next vote to open.

## One Plate / Two Plates
In a round with one of those plate modifiers, **no event can destroy the plates** (they're guarded inside your PlateSpawner, so every plate-breaking event is covered: Falling Bell, meteors, the Spade ...). **Sudden Death still can**, so those rounds can still end. `LAYOUT_SAFE = false` at the top of `SpawnPlates` in PlateSpawner turns it off. Events that only warn first (a red glow, a crack) still show the warning, then the plate just holds.

**Changes to YOUR scripts** (the installer keeps a backup):
- `StarterPlayerScripts > TarotClient` (your edit + the above), `ServerScriptService > TarotServer`, `Shared > SettingsConfig` (the new switch).
- `Systems > PlateSpawner` (the "Layout" guard), `Systems > SuddenDeath` (one line: it says it's Sudden Death when it destroys a plate).

**Tested (NOT Studio):** I ran it in my test bench on your Oct 8 export.
- It went in cleanly on top of the export and on 102 mixes of Updates 8–28.
- **Your edited TarotClient**: with a change of "yours" in it, the first install kept your copy and said so; Install update again put this one in and listed yours in the backups.
- The changes passed 30 new checks:
  - drawing before the countdown;
  - refused while you're alive in a round;
  - allowed once you're knocked out, after which the ghost flip still works;
  - that card stays through the round's end, works in your next round, and is gone after it;
  - Silent Draw draws in the countdown and on a click, with no stage, no toast, and the card face down;
  - One and Two Plates: Falling Bell can't break the plates, and neither can a direct DestroyPlate (the way every plate-breaking event does it). Sudden Death can, and a normal round is as before.
- Your 100 tarot checks still pass, and so does every earlier scenario test (1189 checks in all). Every event of the game ran with and without it: nothing new went wrong. A type-check of the whole game shows nothing new.

How it looks and feels is yours to judge.
