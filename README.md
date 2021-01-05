# game-and-watch-retro-go-save-state-backup
Save state backup from game-and-watch-retro-go

This repository only contains a description of the "game-and-watch-retro-go save state" process, as already explained by kbeckmann.

## Sources
* Retro-go source : https://github.com/kbeckmann/game-and-watch-retro-go
* Discord source : https://discord.com/channels/781528730304249886/784362150793707530/795914729142091784
** Date: 2021/01/05 08:20AM
** Author: kbeckmann

## Dump of Discord

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

