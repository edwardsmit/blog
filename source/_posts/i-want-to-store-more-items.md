title: I want to store more items
id: 20
categories:
  - Digital Life
date: 2007-01-24 15:31:21
tags:
---

I'm running Vista and Office 2007\. Previously I used [Newsgator](http://www.newsgator.com) for all my blogreading, but the new Windows RSS platform in combination with Outlook 2007 brings me the exact same functionality.

It appears that the feeds have a limit for the number of items they can contain, this limit is by default set at 200\. That's not enough for me. You can set the limit by modifying the feed properties, but that would mean I needed to right-click al the feeds (100+) so I needed another way to modify all the feeds. Of course the Windows RSS Platform has an API, so some programming will come to the rescue. I originally thought that this would be an excellent opportunity to delve into Powershell, but it appears that Powershell is not yet available for Vista at this moment :-(

So some JavaScript to the rescue. Run it using cscript, and all feeds will be modified.
<pre class="brush: javascript">  var feedsManager, rootFolder;
  feedsManager = new ActiveXObject("Microsoft.FeedsManager");
  rootFolder = feedsManager.RootFolder;
  iterateFolders(rootFolder);

  function iterateFolders(folder)
  {
    if (null == folder) return;
    var currentFolder;
    var e = new Enumerator(folder.Subfolders);
    for(;!e.atEnd();e.moveNext())
    {
      currentFolder = e.item();
      iterateFolders(currentFolder);
    }
    iterateFeeds(folder);
  }

  function iterateFeeds(feedFolder)
  {
    if (null == feedFolder) return;
    var feed;
    var e = new Enumerator(feedFolder.Feeds);
    for(;!e.atEnd();e.moveNext())
    {
      feed=e.item();
      //feed.MaxItemCount = feedsManager.ItemCountLimit;
      feed.MaxItemCount = 0;
      WScript.Echo(feed.Name + ": " + feed.MaxItemCount);
    }
  }</pre>
Update: I previously set the MaxItemcount to the ItemCountLimit (2500), set it to 0 to set it to unlimited