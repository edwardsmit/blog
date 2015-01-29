title: Restoring MacBook Pro using Time Capsule
tags:
  - Backup
  - Mac
  - Time Machine
id: 34
categories:
  - Digital Life
date: 2009-10-26 11:40:50
---

To my horror suddenly my MacBook Pro wouldn't display anything anymore, a blank screen was all I got. Hooked up an external monitor, no success. Searched the internet and concluded that I might have a broken Nvidia graphics "card" (it's soldered on the board so it's not really a card) as the batch my MBP is from contains a faulty Nvidia card http://support.apple.com/kb/TS2377
So I went to an Apple Service Center where they concluded that indeed my graphics card is broken and that repair is covered by the extended warranty. The ASC had a MBP for rent for the duration of the repair, but as I was late on the day they weren't able to swap the harddisks.
So I took the MBP home and ventured out to restore a Time Machine backup. I have a Time Capsule so there should be a recent backup available.
The MBP booted into the installation of Leopard, after the introduction video (couldn't bypass watching the whole video) I was give the option to do a restore from a backup. Selected the option, the MBP found my Time Capsule but after I selected a backup-set got the Spinning Beachball and nothing happening for more than an hour, I uttered a small curse.
What the heck, let's boot into Leopard and start the Migration Assistant. Hmm, the same experience, found my Time Capsule but after selecting the backup-set a Beachball. Damn.
Read something about restoring a backup by starting the restore tool off from the OSX installation CD. So started the utilities, selected the restore, hmm it can't find my Time Capsule. Looked up a knowledgebase article on the Apple site and found that I had to start the Wireless network by clicking the WIFI icon in the upper right corner of the utilities screen. Ok, so the backup-set can be selected, but you guessed it, a Beachball.
Than it dawned me that the backup was made with Time Machine running Snow Leopard not Leopard, so I put in the Snow Leopard DVD, started the Utilities, selected restore from Time Capsule, saw the backupset, and now was able to select exactly which backup I wanted to restore. Selected the most recent (which was from just before the screen problems started) and went to bed.
The next morning I was greeted with my trusted login-screen and everything was installed in such a way that I couldn't tell that I was working on another machine. Great, love automatic backups. Note to Apple, a meaningful message along the lines of "Backup was created with a newer version of Time Machine" would have saved me a couple of hours.