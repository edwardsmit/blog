title: Getting the UK SDC BizTalk 2004 Documenter to run
id: 22
categories:
  - BizTalk 2004
date: 2006-09-21 10:03:05
tags:
---

Finally I've managed to get the BizTalk 2004 Documenter to run. If you've got problems creating documentation using this tool yourself maybe this will do the trick for you as well. The problem I had was that after the generation a Error box would show up, and nothing was created. After fixing both problems below the tool worked like a charm.

<font size=3>The TMP environment-variable
</font>On&nbsp;the machine I'm currently using the TMP environment-variable was mapped to %userprofile%\local settings\temp and the UserProfile is redirected to a network-share. I changed the TMP environment-variable to a directory on the local drive. You can change this in a dialog which you can&nbsp;edit after pressing the Environment Variables button on the&nbsp;the Advanced tab of the System Properties which you get when selecting Properties from the context menu of My Computer.

<font size=3>The path to Microsoft.BizTalk.XLangView.dll
</font>The documenter relies on forementioned dll. The path to this dll is configured in the Microsoft.Sdc.BiztalkDocumenter.exe.config file. When you've got a default install, the path to this dll is set correctly, but in my case BizTalk 2004 is installed on a non-default location, so I had to change this path.&nbsp;It was there right under my nose the whole time...

&nbsp;