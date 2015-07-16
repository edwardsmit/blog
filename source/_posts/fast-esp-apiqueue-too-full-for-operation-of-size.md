title: FAST ESP Apiqueue too full for operation of size
id: 110
categories:
  - FAST ESP
date: 2011-02-03 13:03:15
tags:
---

In FAST ESP 5.3 when trying to index large files, you might run in to the problem that the indexer API-queue
can't handle the document because of its size.
By default the indexer API Queue is set at 52428800 bytes (50Mb). Mind that you only re-size this
API Queue when a **single** document is larger than the 50Mb, otherwise you can try to limit the size
of the submitted batch by whichever connector you are using.

If you are sure you need to enlarge the indexer API Queue do the following:

1.  On the admin-server edit the file $FASTSEARCH\etc\config_data\RTSearch\webcluster\rtsearchrc.xml
2.  Add the attribute maxQueueSize="**78643200**" to set the indexer API Queue Size to 75Mb, adjust to
    an appropriate value for your environment.
3.  Do a **nctrl reloadcfg** on the admin-server
4.  Do a restart of all indexer processes (either via **nctrl** or the System Management tab in the Admin-UI)
