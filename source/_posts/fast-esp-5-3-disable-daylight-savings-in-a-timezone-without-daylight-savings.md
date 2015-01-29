title: FAST ESP 5.3 - Disable daylight savings in a timezone without daylight savings
tags:
  - Bug
  - FAST
  - Microsoft
id: 59
categories:
  - FAST ESP
date: 2010-04-27 14:24:25
---

I'm installing a FAST ESP 5.3 sp3 setup in India. No I'm not there physically, via a remote desktop. As you might know, FAST doesn't like Daylight Savings Time Adjustment. The Indian Timezone used by the server does not obey Daylight Savings, but the FAST ESP 5.3 sp3 installer still blocked on it's check of Daylight Savings. To disable this correctly I opened up the timezone-adjustment dialog, switched to Amsterdam Timezone, unchecked Daylight Savings Support, switched back to the Indian timezone and pressed ok. FAST ESP 5.3 sp3 Installer is happy again :$