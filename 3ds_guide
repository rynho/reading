Everything You Wanted to Know About the 3DS but Were Afraid to Ask
Ask questions, comment, critique, correct! All your feedback are belong to me.

This is an overview of some concepts that aren’t widely covered in other guides. For instance, did you want to use the MicroSD Manager from the New console on an Old console? Would you like to know what those files in the essential.exefs are for? How about restoring your saves, even if they’re encrypted? Removing system apps from the home menu? Or maybe you just want to learn more about what makes a 3DS tick. Read on to find out more.

Last updated 20 December 2018.

Contents

 1. Overview

     a. SD

     b. NAND

     c. NNID, Friend Codes, and More

 2. Tips & Tricks

     a. MicroSD Manager

     b. Essential.exefs, Seedminer, and Restoring Encrypted Saves

     c. Console Profiles and Erased Icons

          i. Restricting Apps for Children

          ii. eShop Access

          iii. Scripts

     d. StreetPass

          i. Mii Plaza Saves

     e. Resetting the Clock

     f. NAND Transfers

          i. System

          ii. CTRNAND

          iii. Manual

 3. Disclaimer

OVERVIEW

Below is some terminology and concepts that are used for more advanced ideas later.

IMPORTANT NOTE: Always make a NAND backup before doing anything you're not certain about.

ANOTHER NOTE: Never uninstall CFW to try to fix a problem. You could be making things more difficult, or even impossible, for yourself.

SD

The SD:\Nintendo 3DS folder has a 32-character ID0 folder whose name is derived using your movable.sed file, which controls encryption on your console. In fact, if you copied your movable.sed to someone else’s console, they could have the same encryption as you (and same ID0 folder) and you could share an SD card (though it’s best if you make a copy of the SD card instead).

Inside the ID0 is the ID1 folder, whose name is irrelevant. Then you have the following folders: backups (save backups made by the OS when you direct it to), dbs (database for your titles), extdata (extra data created by games, and some games store saves here), title (app data and saves), and Nintendo DSiWare (exported DSi games, as done in system settings).

NAND

The NAND has a few partitions: CTR (the main filesystem for operation of the 3DS), TWL (for DSiWare), FIRM (firmware, 2 for redundancy, contains B9S when installed), and a few others that aren’t that important. When you use decrypt9, GM9, etc. to output a NAND.bin (or NANDmin.bin if you opt for a minimally sized file), you get all these partitions at once, and all encrypted. When you use decrypt9/godmode9 to output a CTRTransfer image, you get the CTR partition only, decrypted.

Regarding the FIRM partition: it contains firmware for a variety of processes, which are listed here. The NATIVE_FIRM is loaded by the bootrom and is used to set up the ARM9 and ARM11 kernels (for running the console). The SAFE_MODE_FIRM is just for running the System Updater. The TWL_FIRM is for running DSi apps. And the AGB_FIRM is used to run GBA VC and to write saves to the agbsave.bin area of the NAND, which can be accessed in the GM9 SYSNAND VIRTUAL drive.

You can’t use NAND backups on other consoles (console-specific keys are used for encryption, not just the movable.sed, plus this file would contain firmware that you don’t want to mess with), but you can use CTRTransfer images on multiple consoles because it just contains the data that the OS needs (no firmware). You can duplicate consoles this way. That data can be broken down as follows.

Inside the CTRNAND, you first have the data folder. If you delete this, the console will act like it was formatted and create a new one based on your movable.sed. It has the same ID0 as the SD. Inside is extra data for system apps (contains notification storage, game coin count, Miis, and more) and system data for system saves (like activity log, pedometer, savegames for built-in apps, and more). If the movable.sed changes, this folder will self-delete.

Next is the dbs folder. The important files are the title.db (title information for system apps) and ticket.db (tickets for all installed apps, whether system or SD). If you don’t know what tickets are for or how titles you’ve installed actually show up in your home menu, this is what the title.db, ticket.db, and app content data are for. In your SD:\...\title folder, you’ll find content folders under each titleID that contains app files, the files that contain the game itself. The title.db has a list of titles installed on its medium (the one on the CTRNAND is for system apps, the one on the SD is for installed games). System Settings reads the title.db file on the SD when you go to Data Management > 3DS > Software/Extra Data/DLC. Lastly, you need the ticket, which is a small file that gives you permission to open, or even see, a title.

The private folder has your movable.sed. The rw\sys folder has your LocalFriendCodeSeed_B, used for unbanning. The rw\sys folder also contains your SecureInfo_A, which has your console serial.

A short note for the TWL partition: its title folder is where you’d find the app data for DSiWare titles installed to your console, even though tickets for them are stored in the CTRNAND.

NNID, Friend Codes, and More

I've fielded a number of questions regarding resetting a NNID, a Friend Code, pedometer/Activity Log, and more. It used to be I would suggest formatting, dumping the clean file, then injecting it into a restored system. After extensive tests, I can confirm that deletion of any of the following from ctrnand/data/ID0/sysdata will cause the console to reset that file only:

NNID @ 00010038 (all regions)

Friend Code/List @ 00010032 (all regions)

Pedometer, etc. @ 00010022 (all regions) (delete with Activity Log to completely reset that app)

Activity Log @ 00020212 for U, 00020202 for J, 00020222 for E.

A note on the NNID. Every console, regardless of whether it has a NNID associated with it, will have a nnidsave.bin file, which you can dump/inject using decrypt9, or use GM9 to find the file at the location mentioned above. NNIDs will only login successfully if you have it on your console AND Nintendo’s servers associate it with your console. A NNID is associated with your serial number on Nintendo's servers. As such, if you change your serial, i.e. by hex editing the plaintext portion of the serial in ctrnand/rw/sys/SecureInfo_A, you can effectively dissociate the NNID on the servers. I would not recommend doing a system transfer at this point because you could accidentally choose a serial that exists in the real world that may have a NNID associated with it, which would no longer be associated if you transfer. If you want to create a temporary NNID and retain your own on your source console during a dsiware transfer, I would use the serial of a console you have control over.

TIPS & TRICKS

MicroSD Manager

Now to get into the good stuff. So you know that the New consoles have a microSD Manager that allows manipulation of the microSD card because they’re covered by a screwed on backplate? Kind of annoying it was designed that way, but at least the News got a way around it. The Olds never got that app, but some of us don’t like moving our SD to our computer often. Olds can use homebrew like FTPDB or 3DShell to FTP and mess with SD files, but it’s slow. MicroSD Manager uses SMB protocols to transfer files, which is, according to my tests, about 60% faster than my tests using the apps I just mentioned. I even used it to copy files directly from one Old console to another.

Want to put this app on your Old console? Well, first you need to get the app (not sure what the legality is of me uploading the app since it’s owned by Nintendo, so I won’t). And even though the app is only about a megabyte in size, you’ll need to either download a full CTRtransfer image from 3Down or The Guide or use 3DNUS to get it (I find 3DNUS to be hit-or-miss at times, but if you can use it, go for it). Once you get a CTR image, use OSFMount to mount the image and copy to your SD somewhere the title\00040010\2002x100 folder, where x is 3/4/5 for regions JPN/USA/EUR, respectively.

Open godmode9 (GM9) on your Old console and go to that folder you just copied over. Go into its content folder to see the app file. Select it, go into the NCCH options, and inject it to H&S. The injection process will make a backup of your existing H&S and then rename the app file to match the old H&S name. When you launch H&S now you’ll get the MicroSD Manager. And it works just fine, even creating a system save file. However, it does not close properly. At least on my O2DS and O3DS consoles, Luma will crash and force shutdown (maybe someone can fix this in the code?). You can get around this by just using Rosalina to reboot (it doesn’t matter if you have an active connection, just make sure you aren’t in the middle of a file transfer). Sit back and enjoy the faster speeds and more reliable connection (imho) that the app provides.

Despite what naysayers may say about H&S injection, it's perfectly fine to inject this into H&S because this is a system app. Don't inject apps that aren't homebrew or system apps because they may want to create a save file in the title folder, which system apps aren't allowed to do.

Since the original posting of this guide, it has been brought to my attention that a flag in the app can be edited to make it visible during a standalone installation. The forums I've read say you still get a crash issue on shutdown (or failure to launch apps until reboot). I also test injected a New System Settings over my Old one and it booted up fine, but it doesn't have the microSD Manager option (even though that's installed, too), implying that the app knows it's on an Old and refuses to show the manager.

In addition, a Windows 10 update disabled SMB v1.0 protocols, so you'll have to re-enable those to use microSD Manager on Win10 nowadays. Simply go to "control panel > programs and features > turn windows features on or off > enable SMB 1.0/CIFS File Sharing Support." However, as u/bungiefan_AK pointed out, it's not secure. Consider that if you use it. You could also probably get away with just enabling the SMB protocol temporarily.

Security Note: the decrypted save for this app contains the password for your network connection as cleartext.

Essential.exefs, Seedminer, and Restoring Encrypted Saves

I had a console motherboard get fried once (changed every other part before figuring this out, unfortunately). It was shutting off intermittently and I was barely able to get a CTRtransfer image off of it, along with some other important files, to ensure my existing titles and saves will be readable. Since then I keep a copy of important files for a specific console on my computer, copied immediately after the initial hax.

So GM9 creates an essential.exefs file in your gm9\out folder if you let it. You can also find it in your SYSNAND VIRTUAL drive in GM9. If you mount it in GM9, you’ll see a few files: frndseed (your friend code and friend list), movable (movable.sed), nand_cid, nand_hdr, otp, and secinfo (SecureInfo_A) files. You should also dump the boot9.bin from the MEMORY VIRTUAL drive in GM9.

Anyway, if your console suddenly dies, you can use the essential.exefs and the boot9.bin in fuse-3ds to decrypt your NAND backups on your computer, in order to extract a transferrable ctrnand image, copy system files, or satisfy your curiosity. Alternatively, you can use XORpads, readily available in GM9, and the 3DSFAT16tool to dump whatever partitions you need, though those take a lot more space.(deprecated) Mount decrypted partitions using OSFMount if you want to copy particular system files. You can also use fuse to decrypt your SD contents directly and acquire decrypted saves that way. Copy decrypted save files over the existing ones through GM9's SYSNAND SD menu.

You can use the frndseed to restore your friend code/list (write the file over the one mentioned in the "NNID, Friend Codes, and More" section). You can use the movable.sed to restore or transfer to another console your encryption. When consoles have the same encryption of titles/saves, they'll also have the same ID0 folder name and any encrypted files copied into there will be readable (including saves), so long as you have the title.db and ticket.db updated accordingly. You can update those databases by injecting versions of them from before a malfunction, which can be found in your last nand.bin (titles installed after a backup will not show up and will have to be reinstalled, though encrypted saves can be manually copied into the title folders after reinstallation).

Seedminer can give you the ability to brute-force compute the movable.sed that you need to decrypt your files (useful for those who used the DSiWare transfer to hack their systems and want to restore saves from before the hax). Say you have a situation like u/cant_relate had in this conversation where they formatted their console before attempting hax and lost their saves. Before seedminer, those saves would be gone, even with a backup of the SD card from before the format. However, seedminer was used successfully to generate most of the seed file. I say most because, at the time of my writing this, the seed file was only meant to be used at a particular website online (in the seedminer readme) in order to inject hax into a dsiware you own, and thus the file was missing a header and instructions for fixing the CMAC. Information about the movable.sed can be found here; as can be seen, the header is 4 bytes that translate as the magic word "SEED." So to make your brute-forced seed usable on your console, change those first 4 bytes, pop it into your ctrnand/private folder, then use godmode9 to fix the CMAC and you're good to go.

One final note regarding seedminer is an issue that came up during the solving of u/cant_relate's problem: if you want to compute the seed for an ID0 that is not currently active on your console, make sure to follow the step (in the readme) that says:

Take the seedminer_launcher(3).py script and run it inside the sdmc:/Nintendo 3DS/ folder (with argument ID0) and it should add the ID0 to your movable_part1.sed. You may optionally add an ID0 with command line: python seedminer_launcher.py id0 <32 digit hex number>

After you've restored your saves, you should use Checkpoint or JKSM to decrypt them on a regular basis, to make recovery easier in the future.

Console Profiles and Erased Icons

Your CTRNAND can basically be boiled down to the contents of the data and dbs folders and your movable.sed. Together, they contain everything except for some hardware calibration files, LFCS_B, SecureInfo_A, and your system title folder (which should only change when injecting H&S or when updating the firmware). So copying those three items in a particular way will allow you to create new profiles. Before I continue, please note that deleting the data folder is fine and will make the console think it’s been formatted, but deleting the dbs folder will cause it to brick (which can be undone).

You can have two or more console profiles, depending on the size of your NAND. Each profile could have its own databases, home menu, NNID, movable.sed, etc. So you could set one profile to be for your kids, one for eShop access, etc. I'll go over these examples to give you a better idea of what this technique can do.

RESTRICTING APPS FOR CHILDREN

So I bought my kids an O2DS recently, but I wanted to make sure I had maximum control and they had as little as possible (they’re almost 3, and they can’t read, so I wouldn’t put it past them to format the console if they could). My plan was to hack it like normal (install b9s, backup the essential.exefs, backup the NAND) and then remove access to critical system apps and all homebrew.

Some setup first (for those interested in setting up a console for their kids): I used ctrtransfer in decrypt9 and got their console to have the same encryption as mine. They got all my Miis, too, so I had to change the personal Mii to one of my kids’ Miis using 3dsMiiEditor (if the link isn't working, it's in my Mega). I set up the Parental Controls as normal. I set up a PIN on Luma and ensured that Luma resided only on the SD card. I backed-up the 2DS LFCS_B file and put on the console the one from my primary console, so I got a virgin one if I ever need it (consoles with the same LFCS_B can't become "friends" with each other via Local, and Wireless friending is just glitchy, so keep that in mind).

Then I figured out which titles I wanted to keep on their system and which I wanted to hide. For instance, I planned to hide H&S, Sound, Nintendo Zone, AR Games, eShop, Activity Log, System Settings, and all homebrew apps.

Copy the dbs folder (name it dbs_all_apps). If you copy it to the CTRNAND, a simple rename is all that's required for profile swapping.

Boot up and open FBI.

You can get the title IDs through the Titles menu and then delete the tickets for the apps you want to remove through the tickets menu. A reboot is required to show any changes for system apps.

Once verified it looks good, rename the dbs to dbs_kids_apps and rename the dbs_all_apps to dbs to "activate" the "all apps" profile (and vice versa for the "kids apps" profile). Use a script to speed up profile swaps (so the whole process takes just about one second).

(The longest step is the deletion of the tickets, so I suggest having a text file or something that lists what you want gone. You can't automate that in GM9.)

This method doesn't just remove the icons but permission to open them, too. So one of the nice things about this is that if you remove the System Settings icon, it can't be accessed, even using that shortcut in the Home Menu Settings drop-down.

If you want to install a new app to both profiles, just use a CIA and only delete it after installing to both. If you want to unhide an app in the "kids apps" profile, install the ticket for the app (which you can get from using GM9 to mount the ticket.db of the "all apps" profile).

My kids recently found a workaround and accessed the System Settings by using an Action Badge, a badge that runs an app. Having no ticket doesn't stop the action badges from working, unfortunately, so I had to write into my script a rename for the System Settings title folder (this is not reflected in the scripts stored online).

Note: A system update won’t reinstall the tickets for those now-missing system apps unless the update includes updates to the apps themselves (like when Sound was updated to patch the soundhax vulnerability). Just delete the ticket(s) again on the kids profile.

ESHOP ACCESS

When you load the eShop on a console that has custom themes installed (i.e. by using Howling Theme Tools) or DLC that wasn’t acquired through the eShop, the eShop will check your tickets and remove the “bad” ones accordingly. That’s annoying, so I decided to set up a “clean” profile (clean title.db, clean ticket.db) so I can access the eShop without worry. This profile is very similar to the "Kids" one above, but I include renaming lines to my scripts to take care of the data folder and movable.sed file in addition to the dbs folder.

Get clean title and ticket databases from the 11.5.0 image that can be found here.

Make sure your movable.sed is backed-up on your SD. Dump your nnidsave.bin and friendsave.bin, too, if you desire to have those on the other profile.

Copy the movable.sed in place with the name movable.sed.orig.

Careful on this step: use the homebrew app TinyFormat and immediately enter GM9 when it reboots. The app merely gives you a new movable.sed and nothing else. The console, however, will compare the ID0 that results from that to your data folder and delete that folder if they differ, which leads to the first-boot process. It won’t have deleted the folder yet if you interrupt the boot by loading GM9 (it will seem to take longer than usual to get to your payload).

Copy your dbs folder into your CTRNAND with a different name (dbs_orig) and rename the data folder to data_orig.

Inject the title and ticket databases from the ctrimage using decrypt9.

Boot the console and do the first-boot process. This both creates and initializes the data folder.

Set up any NNID you desire, even if it’s one that’s tied to your primary profile. Or not. You can access the eShop without one.

Create or download renaming scripts in GM9 to activate the files you desire. In my scripts I used "_eshop" and "_orig" for the folder names and ".eshop" and ".orig" for the movable.sed.

This uses a bit of space on your CTRNAND (about 186MB on my O3DS). You can set your scripts to copy files to your SD instead of just renaming them, but that process will take a lot longer. You can also opt to use the same movable.sed file in both profiles, but then you’d have to deal with renaming your SD card’s ID0 folder, too.

SCRIPTS

You can find my personal scripts here, which use the names I've used in these examples. Feel free to make some yourself. d0k3 released an excellent example of GM9 script usage in his HelloScript.gm9, included in the latest release of GM9.

StreetPass

With the demise of HomePass and official StreetPass relays, we are looking forward to a time when we can simulate the experience or replicate it in some way. While we're not there yet, I've posted some info on the subject at GBATemp as well.

To summarize, StreetPass transmissions are saved in the CECD (system save folder 00010026). FBI can't currently extract those contents, but the hex reveals it's a standard DISA filesystem format (similar to standard game save files) that can be extracted using 3ds-save-tool.

The parent CEC folder contains a folder for each game that you've set up StreetPass for, plus 2 metadata files; the "MBoxList____" is a simple plaintext list of StreetPass IDs (SPIDs don't necessarily coincide with the actual game ID of the region-specific title you've installed, but sometimes they do). The individual game folders always contain InBox and OutBox folders, plus 4 MBox files; game name in file 010, SPID in 050, unknown information in 001, and a 4th file is metadata. The InBox for each game always contains X+1 files, where X is the number of transmissions you've received and the 1 is metadata (X can be 0, btw). The OutBox always contains 3 files; 1 for your outbound transmission and 2 for metadata.

The OutBox transmission file is the key to setting up or faking a relay, as that contains the information that is sent to other consoles when they initiate a handshake. There will be one OutBox transmission for each game you've set up StreetPass for, up to a maximum of 12. In the GBATemp thread, I've uploaded a copy of my OutBox transmission for Super Mario 3D Land, if anyone wants to take a look.

If you back up your CECD when you have some transmissions, then you exhaust all those by running the associated games, you can restore your backup to reset the transmissions.

Ultimately I envision a homebrew that injects the OutBox files into your CECD to mimic a relay exchange. Configuring the metadata files is likely important, though.

Until that day, please go here for the Google Sheet I've set up to compile CECD info from various sources and their links.

Mii Plaza Saves

I got a special section for this because it can be a mess to deal with.

So Mii Plaza is a very unique title. The title is stored on the CTRNAND, but it stores some save data on the SD and stores some on the CTRNAND. The breakdown is like this:

The title has a system save on the CTRNAND that contains some Streetpass data. It’s called meet.dat and it’s in the 00020218 folder. When I delete that, everything for Mii Plaza resets, including saves for the individual DLC games. It has extra data on the SD (in the 218 folder) that contains the save info for all Mii Plaza games, including DLC games. It also has BOSS data on the SD that contains title-created notifications as well as data for all Miis you've ever come across through Streetpass.

The confusing part is if you go into the extra data on the SD card and try to match all the encrypted, numerically-named files to their decrypted counterparts (output of JKSM), you'll find some discrepancies: there are more files on the SD than the JKSM shows for game saves (even taking into account redundancies). Turns out that those extra files contain some BOSS data, like the “Streetpass Miis” file.

I did a lot of experimentation with these saves and found that when a game's save file is created/edited/accessed, it's maybe encoded with information that prohibits you from just copying in the encrypted files if you backed them up previously: it could be a complicated encoding that I know nothing about or it could just be a timestamp issue. Regardless, you can restore the saves if you inject decrypted JKSM saves into already-created save files. If you restored your encrypted backed-up SD saves after trying to load up any games, it would appear as though the saves vanished.

A possible fix for restoring encrypted saves might be to backup your current saves, put the original encrypted saves back on, use JKSM to decrypt them (remember, decrypt the BOSS and syssave data, too), put your recent backups back on, then JKSM to inject them. This is untested atm.

Below is a table of the JKSM-named files, their decrypted sizes, encrypted names (leading zeroes were removed, so a name of 6 corresponds to an actual filename of 00000006 in the extra data folder), then encrypted sizes. Ignore the encrypted name portion as I recently confirmed that these names change from one console/profile to another. Use the sizes to verify your saves; for games like Mii Trek and Market Crashers, that have the same encrypted size, there is no easy solution other than to backup your saves and delete a file to see which save resets.

NAME	DEC SIZE (KB)	ENC NAME	ENC SIZE (KB)
meet_ext0 = Find Mii I&II	130	6, 9	146
meet_u000 = Puzzle Swap	3420	A, 18	3492
Btl = Warrior's Way	4	D, 11	20
Car = Slot Car Rivals	49	C, 1C	65
Chf = Feed Mii	4	1F, 20	20
Exp = Mii Trek	9	23, 24	25
Flo = Flower Town	475	15, 16	491
Fsh = Ultimate Angler	192	13, 14	208
Nja = Ninja Launcher	1	21, 22	17
Pzd = Monster Manor	94	3, 7	110
Sht = Mii Force	49	F, 10	65
Trd = Market Crashers	9	1D, 1E	25
Zmb = Battleground Z	49	5, 12	65
On my console at least, some of the “additional” files that didn’t match a gamesave include stuff like Streetpass messages (encrypted names of 4, 8, B, and 17) and one massive file (relative to the rest) for the “Streetpass Miis” (encrypted name of 1B and is many MB in size). Also, the size of Puzzle Swap may change when new puzzles are released.

TL;DR – Whether you are backing up or restoring the Mii Plaza saves, do it all at once: backup/restore the system save, the extdata, and the BOSS data.

Resetting the Clock

Suppose you had to take out the battery from your console for whatever reason. Or maybe Daylight Savings just happened. One thing a lot of people dread is having to reset their clock and dealing with games that care about that ("Oh, your clock changed. You can't do anything for a whole day, now. Sorry!"). Well, now you don't have to worry about that.

The RTC is the real clock of the 3DS. The system settings clock that you set is just an offset that is saved in a configuration file. Set that offset to zero using the ctr-no-timeoffset app.

Now, with Daylight Savings or timezone changes or whatever, just change the RTC in godmode9 and you're done. But if your battery was removed or died, boot into godmode9 (once you get a good battery in it, of course). If it doesn't ask you to reset the RTC, then you don't need to do anything and your system clock should reflect the current time. If it does ask you to reset the RTC, do so.

Then you have to back up your system configuration save through godmode9 (copy CTRNAND/data/ID0/sysdata/00010017 to your SD somewhere). Alternatively, you can use decrypt9 to dump the system save file for the configuration (called configsave.bin). I find the latter method easier, but either works. Anyway, once that's dumped, Boot up the console. The configuration doesn't receive a reset signal for the system clock offset until after the boot sequence starts, which means your system clock will be at zero-time during this boot. Reset the console and boot godmode9/decrypt9. Use that payload to inject your saved configuration file. Then when you boot up again, the offset will be reset to what it was before the battery died or was removed. Any games that sense a change in the offset will not see it as any different than before. Simply run the time offset app again and your games should be none the wiser.

NAND Transfers

SYSTEM TRANSFER

So there are three methods you can use to transfer your system. One is, obviously, the built-in system transfer. The drawbacks to doing that are that it can only be done once every seven days and that it doesn't transfer illegitimate tickets, like homebrew, custom themes, etc. The only thing this transfer does that the others don't is to move your NNID on Nintendo's servers so it's then associated with the target console. There's really not much more to it than that. This section is more devoted to the other methods.

CTRNAND TRANSFER

Most people know that you can dump a CTRNAND, rather than your entire NAND, to a file using godmode9 or decrypt9. The advantage with this method is that it transfers all your tickets (because it copies the ticket.db), not just legitimate ones. This is a great method to clone one console onto another. To get a partial clone, you basically just need the movable.sed and the ticket.db; this will let you read the SD card of another console and use the titles that were installed onto it. A full clone would include copying the data folder, too, to get all those system saves, NNID, notes, etc. copied over. A CTR transfer does it all in one fell swoop.

Sometimes you'll need to fix the CMACs after a transfer. The CMAC is like a signature that exists on certain system files (not CTR transfer files). If the signature doesn't match what it expects, it assumes that file is corrupt and recreates it (or crashes in some cases). The option to repair them shows when you press R+A in GM9 on the CTRNAND drive (drive 1). Sometimes fixing them doesn't repair all issues I've heard of people getting, so I often suggest to use decrypt9 instead of GM9 to write a CTR transfer image. That app automatically fixes CMACs and transfers some files that GM9 doesn't. I haven't done tests to determine which files, exactly, but for some people it works better.

One other thing is that sometimes DSiWare doesn't work after a CTR transfer, even if you manually copied your TWLN titles to where they need to be and the tickets for them through FBI. This is a fairly normal behavior. There's a section in the guide dealing with troubleshooting and repairing just such an issue.

MANUAL TRANSFER

You can do like I do and make a NAND backup and then subsequently only backup the data and dbs folders periodically, instead of making a full backup often. This saves a lot of time, and the files are readily accessible, too. Keeping that in mind, it's not difficult to clone a console. You should copy these two folders and the movable.sed (or the essential.exefs). That's really it. But I thought I'd dive into the specifics of something not a lot of people know how to do: transfer between Old and New consoles.

Before I get started, it's important to note that the vast majority of differences between an Old and a New console's CTRNAND filesystem are in the title folder. This folder contains all the titles used by the OS to actually run your console. In fact, the "firmware" is sort of contained here. It's not the firmware I've mentioned before (the FIRM partitions). No, what I mean is that the files in the title folder are what are actually updated during firmware updates; the version number that appears in system settings is tied to a file or files inside this folder. This is why CTRNAND transfer images have a firmware version number associated with them.

I mention the title folder because there are differences between an Old one and a New one. Which means there are ticket differences. This is why you see the transfer images having the model associated with them, too (so they have proper ticket.db files). If you put an Old image on a New console, or vice versa, it won't work. You'll just get a black screen. So if you want to transfer between Old and New models, you're gonna need to figure out that ticket issue.

I got a New model recently and wanted to clone my Old onto it. Even if your case is reversed, this method will still work. For the purposes of this guide, I'll just use Source and Target as the terms to represent these. In my case, the Source was a dead console, so the term more accurately references the last NAND/CTRNAND dump of said console. If all you have is a NAND backup and your essentials from your Source, use fuse-3ds to extract the CTRNAND.

On your Target, you'll want to mount the Source CTRNAND, extract the ticket.db, then mount that. Copy onto your SD somewhere the non-system tickets (use godmode9 v1.5.1 for this). Also, make a current backup of your Target NAND and essentials, just in case. Next, replace the data folder on the Target with the one from the mounted Source CTRNAND. Then copy the movable.sed from the Source essentials file to the Target. Fix all drive CMACs now.

You should be able to boot up the console just fine at this point (with the Source Nintendo 3DS folder on the SD card being read, too). But you won't see your titles until you use FBI to install all the tickets you copied previously. Once that's done, you can copy the TWLN partition from the Source CTRNAND if you had DSiWare titles, but you'll probably have to run through the troubleshooting guide as mentioned before. Saves for those are in that partition as well.

One minor issue I've seen creep up on both CTRNAND and Manual Transfers is that the TWL User Profile doesn't clone at all. So if you go to System Settings and then go to your Nintendo DS Profile, it won't show your user name/birthdate associated with the 3DS itself. To fix this, either enter the data manually or go to your user name/birthdate, make and undo a change to those values, then save. The data get copied to the TWL when it thinks there's been a change to them.

Disclaimer

Everything I've written is about stuff I've actually done on my consoles. If you find any problems or inconsistencies with this information or the given instructions, please let me know.
