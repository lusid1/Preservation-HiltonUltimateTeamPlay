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
https://virtualheroes.com/portfolio_/commercial-2/hilton-ultimate-team-play/

## Game Components
Hilton Ultimate Team Play consists of:
  - A UMD Disc containing:
    - The launcher (eboot.bin)
    - The (backup) game engine (game.prx)
  - A memory stick containing:
    - The data_psp folder/contents (the game assets)
    - The SALT Scores folder/contents
    - The patch installer/installed EBOOT.PBP
    - The patched game engine (game.prx) if installed.

After the game has been run for the first time, and the Game Data Installer process completes, the patch installer EBOOT.PBP is replaced with:
  - The 'patch installed' EBOOT.PBP
  - The patched GAME.PRX file, which can only be read on the system that ran the patch installer.

## Boot process and known bugs
  1. The launcher checks the memory stick for the data_psp/data.pak file to make sure the game assets are present
  2. The launcher runs the patch installer EBOOT.PBP
     * BUG 1: If the patch installer or patch installed eboot is not present it will not proceed to launch the backup game from UMD
  3. The launcher runs the patched GAME.PRX if present
     * BUG 2: GAME.PRX is not validated.  If the patch was installed by a different PSP it will attempt to load it anyway and hang or crash.
  4. If the patched GAME.PRX is missing it launches the backup GAME.PRX from the UMD drive
  5. The GAME.PRX loads the game data and runs the game
     - The patched GAME.PRX only loads game data in extracted, un-packed format.  
     - The backup GAME.PRX only loads game data from a data.pak archive
       * BUG 3: The provided data.pak file is a dummy file, which causes the game engine to exit the game. 

## Workarounds
  1. The official day0 patch fixes or avoids these bugs, but the patch installer has not been preserved.
  2. Apply these workarounds to successfully invoke the backup game.prx
     * Ensure the patch install completed eboot.pbp file is present on the memory stick (avoids bug#1)
     * Remove the game.prx file from the memory stick (avoids bug#2)
     * replace the empty data.pak with a valid data.pak (avoids bug#3)

## Preservation Status
|Component|Status|Location/Notes|
|---------|------|--------|
|UMD Disc       |Archived|https://archive.org/details/HiltonGardenInnUltimateTeamPlayUSA|
|data_psp folder|Archived|Included in the memorystick image on archive.org|
|SALT Scores folder|Archived|Included in the memorystick image on archive.org|
|Patch Installer EBOOT.PBP|MISSING|-|
|Patch Installed EBOOT.PBP|Archived|Included in the memorystick image on archive.org|
|Encrypted GAME.PRX|Archived (1 sample)|Included in the memorystick image on archive.org|
|Decrypted GAME.PRX|Archived|The decrypted patch has been recovered and is preserved in a private archive. |
|MemoryStick Image|Archived (1 sample)|https://archive.org/details/HiltonGardenInnUltimateTeamPlayUSA|
|DATA.PAK|Reconstructed| https://www.dropbox.com/s/hy3gz4sxdjmtaeu/data.pak?dl=1 |

The game disc and memory stick data have been preserved, and the plaintext patch has been recovered, but the patch installer EBOOT.PBP is still lost.  

Alternative patch installation methods are being explored.  These include:
  - Reconstructing the patch installer eboot.  (Currently not possible due to missing KIRK keys)
  - Patching the system firmware to allow custom installer eboots.
  - Creating a standalone patch installer  

## Running the game without the patch:
A pre-release version of the game is present on the disc, which is invoked if the user picks no at the game data installer, but this build of the game expects to find a valid data.pak archive on the memorystick.  Because the data.pak in the memorystick image is a dummy file, the game exits.  So to get the game running, we need to:
  - Remove the GAME.PRX file from the memory stick, to invoke the on-disc build of the game
  - Replace the DATA.PAK dummy file with a valid archive.

This allows the umodified game iso or the original UMD disc to run on a normal PSP, but does not work on emulators like PPSSPP because the patch installer related functions are not implemented.  
