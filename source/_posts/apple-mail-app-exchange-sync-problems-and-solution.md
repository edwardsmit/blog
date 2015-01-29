title: Apple Mail.app Exchange sync problems and solution
id: 101
categories:
  - OSX
date: 2010-11-24 15:35:51
tags:
---

At our [company](http://www.matchminds.nl) we have decided to relocate our mailserver to an hosted Exchange 2010\. We've been using Zimbra for the past three years, but we feel that development of Zimbra isn't moving into the direction of better OSX support (we are all using MacBook Pro's) but is more focussed on enhancing their webclient and own desktop-mail-client. In the meantime OSX has received good Exchange support. So after a test-period with a limited number of users we decided to all switch to Exchange 2010.

My sync problems started when I was trying to move complete folders with hundreds of e-mails to my Exchange account. I use a big folder-structure within my Exchange account to separate all kinds of e-mails by customer and by action. Mail and Exchange than got angry with each other. Mail was slowing down to an unusable state, refused to sync some mailfolders and started throwing errors:
> <div id="_mcePaste">23-11-10 19:07:28	Mail[34524]	*** Assertion failure in -[EWSConnection sendMessage:forRequest:], /SourceCache/Message/Message-1082/MessageStores.subproj/EWSConnection.m:374</div>> 
> <div id="_mcePaste">Received an unexpected error: Error Domain=EWSExchangeWebServicesErrorDomain Code=165 UserInfo=0x119f3b210 "The operation couldn’t be completed. (EWSExchangeWebServicesErrorDomain error 165.)", response: (null)</div>> 
> <div id="_mcePaste">(</div>> 
> <div id="_mcePaste">0   Message                             0x00007fff83bbc6e4 -[MFAssertionHandler _handleFailureWithPreamble:description:arguments:] + 137</div>> 
> <div id="_mcePaste">1   Message                             0x00007fff83bbc649 -[MFAssertionHandler handleFailureInMethod:object:file:lineNumber:description:] + 220</div>> 
> <div id="_mcePaste">2   Message                             0x00007fff83afe01b -[EWSConnection sendMessage:forRequest:] + 1117</div>> 
> <div id="_mcePaste">3   Message                             0x00007fff83b095b9 -[EWSGateway sendMessage:forRequest:] + 79</div>> 
> <div id="_mcePaste">4   Message                             0x00007fff83b1ca63 -[EWSRequestOperation executeOperation] + 104</div>> 
> <div id="_mcePaste">5   Message                             0x00007fff83bcaab9 -[MonitoredOperation main] + 229</div>> 
> <div id="_mcePaste">6   Foundation                          0x00007fff832e7de4 -[__NSOperationInternal start] + 681</div>> 
> <div id="_mcePaste">7   Foundation                          0x00007fff833c6beb __doStart2 + 97</div>> 
> <div id="_mcePaste">8   libSystem.B.dylib                   0x00007fff86bea2c4 _dispatch_call_block_and_release + 15</div>> 
> <div id="_mcePaste">9   libSystem.B.dylib                   0x00007fff86bc8831 _dispatch_worker_thread2 + 239</div>> 
> <div id="_mcePaste">10  libSystem.B.dylib                   0x00007fff86bc8168 _pthread_wqthread + 353</div>> 
> <div id="_mcePaste">11  libSystem.B.dylib                   0x00007fff86bc8005 start_wqthread + 13</div>> 
> <div id="_mcePaste">)</div>
<div>These errors wouldn't stop, the syncing wasn't complete, OMG</div>
<div>Apparently I wasn't the first to encounter these problems, but the solutions either sounded too far off for me, or were to rigorous for my taste.</div>
<div>I have found a much easier and faster method to get Exchange and Mail back to communicating with each other.</div>
<div>1 ) Remove Exchange account from Mail</div>
<div>2 ) Remove Exchange account from iCal</div>
<div>3 ) Remove Exchange account from Address Book</div>
<div>4 ) Close all three programs</div>
<div>5 ) Verify that the local mailbox was removed. In ~/Library/Mail there shouldn't be a directory named EWS-[USERNAME]@[EXCHANGE-SERVER] if it is there throw it away, and empty thrash.</div>
<div>6 ) Start Mail</div>
<div>7 ) Add Exchange-account using the Wizzard</div>
<div>8 ) Only move tiny batches of e-mail between accounts</div>
<div>Although tedious, it does work :)</div>