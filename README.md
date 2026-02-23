# Preservation-HiltonUltimateTeamPlay
Research, documentation and preservation efforts related to this unusual PSP title.

------
## About
Hilton Ultimate Team Play is a first-person interactive employee training program produced for the Hilton Garden Inn chain in the US between 2008 and 2009.  It was built by VirtualHeroes on the ViciousEngine for the Sony PSP.  A PC demo version was created in 2008, followed by the full version on PSP in 2009. 

The original press release has been archived here:
https://web.archive.org/web/20080501094530/http://www.virtualheroes.com/newsDetails.asp?nid=31

Hilton Hotels presented at a game developer conference and talked about the background of the game, design goals, and development process. A recording is available here:
https://www.gdcvault.com/play/1312/(305)-Hilton-ULTIMATE-TEAM-PLAY

The developer also references the game on their website:
https://virtualheroes.com/portfolio_/commercial-2/hilton-ultimate-team-play/

## Why the UMD disc was labeled "The Hilton Family"
The UMD Disc was labeled "The Hilton Family" because they planned to launch a version of the game for each Hilton property.  Each version would have used the same launcher UMD, and the game content and user runtime engine could be updated for each property without requiring a new UMD to be authored.  This would have saved the developers from having to submit each future variant for review and UMD pressing, and is the reason for the unique structure of the content for this title. Hilton Gardens Inn Ultimate Team Play was the first property in the Hilton Family to be produced.  The project was cancelled due to the 2009 ecenomic recession and training games for the other hilton hotel chains were never produced.

## Game Components
Hilton Ultimate Team Play consists of:
  - A UMD Disc containing:
    - The launcher (eboot.bin)
    - The developer build of the game engine runtime (game.prx)
  - A memory stick containing:
    - The data_psp folder/contents (the game assets)
    - The SALT Scores folder/contents
    - The patch installer/installed EBOOT.PBP
    - The user build of the game engine runtime (game.prx) if installed.

After the game has been run for the first time, and the Game Data Installer process completes, the patch installer EBOOT.PBP is replaced with:
  - The 'patch installed' EBOOT.PBP
  - The patched GAME.PRX user runtime, which can only be read on the system that ran the patch installer.

## Two different runtime game engines, two different memory stick images
There are two different builds of the game engine, each requiring a different file structure on the memory stick.
  - The developer runtime:
    - game data must be in a data.pak file
  - The user runtime:
    - game data must not be in a data.pak file

## Boot process
  1. The launcher checks the memory stick for the data_psp/data.pak file to make sure the game data is present
  2. The launcher invokes the game data installer for ms0:/PSP/GAME/UCUS94341/EBOOT.PBP
     * Note: If the eboot.pbp is not present it will not proceed to launch the backup game engine from the UMD disc.
  3. (One time only) The game data installer installs GAME.PRX and locks it to that console's unique FuseID. 
  4. The launcher runs the patched ms0:/PSP/GAME/UCUS94341/GAME.PRX if present
     * Note: GAME.PRX is not validated.  If the patch was installed by a different PSP it will attempt to load it anyway and hang or crash.
  5. If the user runtime GAME.PRX is missing it launches the developer runtime GAME.PRX from the UMD disc.
  6. The selected runtime GAME.PRX loads the game data and runs the game
     * Notes:
       - The user runtime GAME.PRX only loads game data in extracted, un-packed format.  
       - The developer runtime GAME.PRX only loads game data from a data.pak archive
       - The data.pak file in the user memory stick image is a dummy file, which causes the game to exit the game. 

## Options for running the game
  1. Install the user runtime game engine.  Note the official patch installer has not been recovered.
  2. Convert the available user memory stick image to a developer memory stick image:
     * Delete ms0:/PSP/GAME/UCUS94341/GAME.PRX
     * Replace the empty data.pak with a valid data.pak (see below)
  3. Use a cheat engine to patch the game (required for emulators like PPSSPP)

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
|User MemoryStick Image|Archived (1 sample)|https://archive.org/details/HiltonGardenInnUltimateTeamPlayUSA|
|DATA.PAK|Reconstructed| https://www.dropbox.com/s/hy3gz4sxdjmtaeu/data.pak?dl=1 |

## Current Status
The game disc and memory stick data have been preserved, and the plaintext patch has been recovered, but the patch installer EBOOT.PBP is still lost.  

Alternative patch installation methods are being explored.  These include:
  - Reconstructing the patch installer eboot.  (Currently not possible due to missing KIRK keys)
  - Patching the system firmware to allow custom installer eboots.
  - Creating a standalone patch installer  
 
