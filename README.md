# game-and-watch-retro-go-save-state-backup

This repository only contains a description of the "game-and-watch-retro-go save state" process, as already explained by kbeckmann.

Aim: describe the roms "Save state" process from a Nintendo® Game & Watch™ (G&W) flashed with "game-and-watch-retro-go" (ie, the rom "save" option within the G&W, that can be backuped locally on your computer & restored at any time, on the G&W, even after a re-flash with other roms).
Why?: I'm always afraid of loosing my "data"; this "save state" process allows me to backup the rom "save" state at any time (from the G&W <-> locally onto my computer), to be restored later, whatever I do with my G&W (or even, transfert the rom "save state" to another G&W).

## Sources
* game-and-watch-retro-go source: https://github.com/kbeckmann/game-and-watch-retro-go
* Discord source: https://discord.com/channels/781528730304249886/784362150793707530/795914729142091784 (Date: 2021/01/05 08:20AM, Author: kbeckmann)

## yEd "game-and-watch-retro-go" & "save state" diagram

Here a *yEd diagram* describing all the *fash roms* to *backup & restore "save states"* for the G&W.

=> available there: https://www.yworks.com/yed-live/?file=https://gist.githubusercontent.com/myStphane/602be41298a69f175c462e239bf84b97/raw/6d6a944f7a144a693ef67e5fae7eb6315214080d/Game%20%26%20Watch%20retro-go(2)

Find in the next paragraphs full description...

## yEd scheme & step-by-step process description

Please refers to the above source repository for details on game-and-watch-retro-go usage.
Please refers to the above yEd diagram.

### 1. Flash 3 roms ("A, B, C") to G&W / game-and-watch-retro-go
* Aim: flash roms on the G&W
* Context: have 3 roms -lets named it: "A", "B", "C"- ready to flash
* Action: using common game-and-watch-retro-go command `./make [...]` to flash roms on the Game & Watch
* Status: once done, you may have those 3 roms (A, B, C) running & playable on the Game & Watch

WARNING: keep the `build/gw_retro_go.elf` file for further usage (-> step 3.)

NOTE: At this time, no "save state" (ie, the rom game backup) is available on the Game & Watch


### 2. Play roms on game-and-watch-retro-go & perform "save states"
* Aim: play roms & perform "save state" on the G&W
* Context: having 3 roms, named A, B, C on the G&W
* Action: plays with all roms and perform, on the G&W, a "Save state" for each of A, B, C roms, using the in-game "PAUSE/SET" "Save & Continue" or "Save & Quite" options
* Status: once done, you may have, for each rom, a "save state", on the Game & Watch


### 3. Backup (extract) the "save states" from G&W locally on your computer
* Aim: backup locally on your computer each "save state" from the G&W
* Context: having 3 roms, named A, B, C on the G&W, each having a "save state"

WARNING: you MUST have the previously used `build/gw_retro_go.elf` (from step 1.)

* Action: execute `./dump_saves.sh build/gw_retro_go.elf` to save locally on your computer, each rom "save state"
* Status: once done, you may have, locally for each rom, a "save state" backup in directory "./save_states/", sub-folders: `./save_states/<emu>/<rom name>.save` (located, for our example, in 3 folders: `./save_states/<emu>/A.save & ./save_states/<emu>/B.save & ./save_states/<emu>/C.save`)

### 4. Flash 3 (new) roms ("B, C, D") to G&W / game-and-watch-retro-go
* Aim: flash new roms on the G&W
* Context: have 3 (new) roms -lets named it: "B", "C" & "D"- and one removed rom -the "A" one- ready to flash
* Action: using common game-and-watch-retro-go command `./make [...]` to flash roms on the Game & Watch
* Status: once done, you may have those 3 (new) roms (B, C, D, but no more A) running & playable on the Game & Watch

WARNING: keep the *new* `build/gw_retro_go.elf` file for further usage (-> step 5.)

NOTE: At this time, no "save state" (ie, the rom game backup) is available on the Game & Watch (or, maybe if you're luck a possible "trace" for B & C, but could be crappy)

### 5. Restore the "save states" to the G&W
* Aim: restore the save state for matching roms on the G&W
* Context: having your "save states" for some roms (A, B, C) on your computer, restore it to roms B & C (and not for A & D, as A is no more on the G&W and D has no save state bacuped on the computer)

WARNING: you MUST have the previously used `build/gw_retro_go.elf` (from step 5.)

* Action: execute `./program_saves.sh build/gw_retro_go.elf` command, on the new .elf (-> from step 4.) to write the local backuped "save state" to the matching roms, on the G&W
* Status: once done, you may have, on the G&W, the restored save states for B and C roms.


----

## Complete dump of Discord from kbeckmann
```
I have now added scripts to backup and restore save states.
the idea is that it should work to backup save states from the currently running device, given that you have the corresponding elf file. 
Later on, you can restore the save states to a newer build.

Not sure if this is easy to understand, PRs welcome if you can explain it better:

# Backing up and restoring save state files

Save states can be backed up using ./dump_saves.sh build/gw_retro_go.elf. Make sure to use the elf file that matches what is running on your device! It is a good idea to keep this elf file in case you want to back up at a later time.

This downloads all save states to the local directory ./save_states. Each save state will be located in ./save_states/<emu>/<rom name>.save.

After this, it's safe to change roms, pull new code and build & flash the device.

Save states can then be programmed to the device using a newer elf file with new code and roms. To do this, run ./program_saves.sh build/gw_retro_go.elf - this time with the new elf file that matches what's running on the device. Save this elf file for backup later on.

The program_saves.sh will upload all save state files that you have backed up that are also included in the elf file. E.g Let's say you back up saves for rom A, B and C. Later on, you add a new rom D but remove A, then build and flash. When running the script, the save states for B and C will be programmed and nothing else.
```

