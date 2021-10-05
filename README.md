# Preservation-HiltonUltimateTeamPlay
Research, documentation and preservation efforts related to this unusual PSP title.

------
## About
Hilton Ultimate Team Play is a first-person interactive employee training program produced for the Hilton Garden Inn chain in the US between 2008 and 2009.  It was built by VirtualHeroes on the ViciousEngine for the Sony PSP.  A PC demo version was released in 2008, followed by the full version on PSP in 2009. 

The original press release has been archived here:
https://web.archive.org/web/20080501094530/http://www.virtualheroes.com/newsDetails.asp?nid=31

Hilton Hotels presented at a game developer conference and talked about the background of the game, design goals, and development process. A recording is available here:
https://www.gdcvault.com/play/1312/(305)-Hilton-ULTIMATE-TEAM-PLAY

The developer also references the game on their website:
https://www.virtualheroes.com/portfolio/Commercial/Hilton-Ultimate-Team-Play

## Game Components
Hilton Ultimate Team Play consists of:
  - The Game UMD Disc
  - A memory stick containing:
    - The data_psp folder/contents
    - The SALT Scores folder/contents
    - The game data installer EBOOT.PBP

After the game has been run for the first time, and the Game Data Installer process completes, the installer EBOOT.PBP is replaced with:
  - A game data install completed EBOOT.PBP
  - An encrypted GAME.PRX that can only be opened on the PSP that ran the installer.

## Preservation Status
|Component|Status|Location/Notes|
|---------|------|--------|
|UMD Disc       |Archived|https://archive.org/details/HiltonGardenInnUltimateTeamPlayUSA|
|data_psp folder|Archived|Included in the memorystick image on archive.org|
|SALT Scores folder|Archived|Included in the memorystick image on archive.org|
|Game Data Installer EBOOT.PBP|MISSING|-|
|Game Data Install Done EBOOT.PBP|Archived|Included in the memorystick image on archive.org|
|Encypted GAME.PRX|Archived (1 sample)|Included in the memorystick image on archive.org|
|MemoryStick Image|Archived (1 sample)|https://archive.org/details/HiltonGardenInnUltimateTeamPlayUSA|
|DATA.PAK|Reconstructed| TBD |
|Decrypted GAME.PRX|MISSING|No decryption tool exists|


The game disc and memory stick data have been preserved, but the game data installer EBOOT.PBP has not.  An example of the already installed EBOOT and encrypted GAME.PRX have been archived, but there is currently no known way to decrypt the file.

Because memory sticks use a simple FAT file system it is possible the installer eboot is hiding in the unallocated blocks of someone's original hilton memory stick.  Anyone who has one of these memory sticks should archive a raw disc image (such as a dd image) so we can look for any remnants of the original eboot.

There are known instances of someone owning a complete working set that includes the original disc, memorystick and matching PSP.  These need to be preserved until tools exist to decrypt the GAME.PRX file.

## Running the game without the missing components:
A pre-release version of the game is present on the disc, which is invoked if the user picks no at the game data installer, but this build of the game expects to find a valid data.pak archive on the memorystick.  Because the data.pak in the memorystick image is a dummy file, the game exits.  So to get the game running, we need to:
  - Rename GAME.PRX to _GAME.PRX, to invoke the on-disc build of the game
  - Replace the DATA.PAK dummy file with a valid archive.

This allows the umodified game iso or the original UMD disc to run on a normal PSP, but does not get it working on emulators like PPSSPP because the game data installer related functions are not implemented.  To get around this, we need to patch the loader portion to bypass these checks, and just run the fallback version of the game.  Since the ISO is being modified, we can include the game data files on the ISO an remove the dependency on have a pre-configured memory stick.
