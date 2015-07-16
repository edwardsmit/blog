title: Apple Mail.app Exchange sync problems and solution
id: 101
categories:
  - OSX
date: 2010-11-24 15:35:51
tags:
---

At our [company](http://www.matchminds.nl) we have decided to relocate our mailserver to an hosted Exchange 2010.
We've been using Zimbra for the past three years, but we feel that development of Zimbra isn't moving
into the direction of better OSX support (we are all using MacBook Pro's) but is more focussed on enhancing
their webclient and own desktop-mail-client. In the meantime OSX has received good Exchange support.
So after a test-period with a limited number of users we decided to all switch to Exchange 2010.

My sync problems started when I was trying to move complete folders with hundreds of e-mails to my Exchange
account. I use a big folder-structure within my Exchange account to separate all kinds of e-mails by
customer and by action. Mail and Exchange than got angry with each other. Mail was slowing down to an
unusable state, refused to sync some mailfolders and started throwing errors:
```
23-11-10 19:07:28	Mail[34524]	*** Assertion failure in -[EWSConnection sendMessage:forRequest:], /SourceCache/Message/Message-1082/MessageStores.subproj/EWSConnection.m:374>
Received an unexpected error: Error Domain=EWSExchangeWebServicesErrorDomain Code=165 UserInfo=0x119f3b210 "The operation couldn’t be completed. (EWSExchangeWebServicesErrorDomain error 165.)", response: (null)>
    0   Message                             0x00007fff83bbc6e4 -[MFAssertionHandler _handleFailureWithPreamble:description:arguments:] + 137>
    1   Message                             0x00007fff83bbc649 -[MFAssertionHandler handleFailureInMethod:object:file:lineNumber:description:] + 220>
    2   Message                             0x00007fff83afe01b -[EWSConnection sendMessage:forRequest:] + 1117>
    3   Message                             0x00007fff83b095b9 -[EWSGateway sendMessage:forRequest:] + 79>
    4   Message                             0x00007fff83b1ca63 -[EWSRequestOperation executeOperation] + 104>
    5   Message                             0x00007fff83bcaab9 -[MonitoredOperation main] + 229>
    6   Foundation                          0x00007fff832e7de4 -[__NSOperationInternal start] + 681>
    7   Foundation                          0x00007fff833c6beb __doStart2 + 97>
    8   libSystem.B.dylib                   0x00007fff86bea2c4 _dispatch_call_block_and_release + 15>
    9   libSystem.B.dylib                   0x00007fff86bc8831 _dispatch_worker_thread2 + 239>
    10  libSystem.B.dylib                   0x00007fff86bc8168 _pthread_wqthread + 353>
    11  libSystem.B.dylib                   0x00007fff86bc8005 start_wqthread + 13>
```
These errors wouldn't stop, the syncing wasn't complete, OMG
Apparently I wasn't the first to encounter these problems, but the solutions either sounded too far off for me, or were to rigorous for my taste.
I have found a much easier and faster method to get Exchange and Mail back to communicating with each other.
1 ) Remove Exchange account from Mail
2 ) Remove Exchange account from iCal
3 ) Remove Exchange account from Address Book
4 ) Close all three programs
5 ) Verify that the local mailbox was removed. In ~/Library/Mail there shouldn't be a directory named EWS-[USERNAME]@[EXCHANGE-SERVER] if it is there throw it away, and empty thrash.
6 ) Start Mail
7 ) Add Exchange-account using the Wizzard
8 ) Only move tiny batches of e-mail between accounts
Although tedious, it does work :)
