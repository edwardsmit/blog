title: Citrix SA Client for Mac OSX
tags:
  - Mac
  - VPN
id: 55
categories:
  - OSX
date: 2010-03-30 13:14:25
---

Some time ago for a specific client I needed to connect to some protected infrastructure using some proprietary Citrix client. The firewall protecting the infrastructure only allowed access via VPN technology as implemented in the Citrix SA Client. At the time I couldn't find a Mac OSX client, and the Administrator of the firewall protected environment also told me that no such software was available. So I ended up using parallels with a windows OS and running the client on that platform. Today I had some serious connection problems from windows to the aforementioned firewall, the connection would drop and reestablish every 15 seconds, not workable. I suspect there is something wrong with the parallels network driver within windows in combination with the Airport wireless network I'm using since a couple of days.
This let me to search for the Citrix SA Client once more, and guess what; [I found it](http://www.citrix.com/site/SS/downloads/details.asp?downloadId=1857838&productId=15005)! Installed like a charm, and now Remote Desktop-ing to the servers from OSX. I hate it when I need specific software for setting up a VPN, but I love it when it works like a charm.