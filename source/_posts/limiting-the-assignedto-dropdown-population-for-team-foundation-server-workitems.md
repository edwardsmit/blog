title: Limiting the AssignedTo dropdown-population for Team Foundation Server workitems
id: 23
categories:
  - .Net
  - Team Development
  - Team Foundation Server
date: 2006-08-02 10:46:04
tags:
---

### The Situation

You are running multiple Team Foundation Server projects with different developers working on different projects. All of the projects use the MSF Agile process. When a workitem is created (Task, Bug, etc.) you are able to assign a workitem to a designated user. The UI contains with a dropdown which is filled with all TFS users, not just the projectmembers. Furthermore you find it undesirable that new workitems are assigned to the creator by default.

### Desired situation

When selecting a person to assign a workitem to, the dropdown is filled with persons assigned to the project's Contributors or Project Administrator group. New workitems are assigned to no one in paticular. Both new and current projects should work this way.

### Steps to get there

Download the process template for MSF Agile using the Process Template Manager.
Modify the files `Bug.xml`, `QoS.xml`, `Risk.xml`, `Scenario.xml` and `Task.xml` (located in the `"MSF for Agile Software Development - v4.0\WorkItem Tracking\TypeDefinitions"` directory) such that
<pre class="brush: xml">&lt;FIELD name="Assigned To" refname="System.AssignedTo" type="String"&gt;
   &lt;VALIDUSER/&gt;
&lt;/FIELD&gt;</pre>
is changed into
<pre class="brush: xml">&lt;FIELD name="Assigned To" refname="System.AssignedTo" type="String"&gt;
   &lt;ALLOWEDVALUES expanditems="true" filteritems="excludegroups"&gt;
      &lt;LISTITEM value="[Project]\Project Administrators" /&gt;
      &lt;LISTITEM value="[Project]\Contributors" /&gt;
      &lt;LISTITEM value="Unassigned" /&gt;
   &lt;/ALLOWEDVALUES&gt;
   &lt;DEFAULT from="value" value="Unassigned" /&gt;
 &lt;/FIELD&gt;</pre>
The syntax of [ALLOWEDVALUES](http://msdn2.microsoft.com/en-us/library/aa337646.aspx), [LISTITEM](http://msdn2.microsoft.com/en-us/library/ms194974.aspx) and [DEFAULT](http://msdn2.microsoft.com/en-us/library/aa337630.aspx) as well as [some info on expansion](http://msdn2.microsoft.com/en-us/library/ms194969.aspx) can be read in the [MSDN Library](http://msdn2.microsoft.com/en-us/library/default.aspx). After you've added users or groups to the project groups don't forget to do a refresh of the project before opening a workitem, otherwise the list isn't populated correctly, I think that expanding of the lists is done on the server, not on the client.

To correct any pre-existing projects you'll have to use the [witimport](http://msdn2.microsoft.com/en-US/library/ms253163.aspx) tool to update the template files in each project. So for all your projects you have to run the following commands in a command window (ofcourse substituting the placeholders for your own TFS ServerName and ProjectName):
<pre class="brush: shell">witimport /t &lt;TFS ServerName&gt; /p &lt;ProjectName&gt; /f &lt;fullPathToModifiedFile&gt;\Bug.xml
witimport /t &lt;TFS ServerName&gt; /p &lt;ProjectName&gt; /f &lt;fullPathToModifiedFile&gt;\QoS.xml
witimport /t &lt;TFS ServerName&gt; /p &lt;ProjectName&gt; /f &lt;fullPathToModifiedFile&gt;\Risk.xml
witimport /t &lt;TFS ServerName&gt; /p &lt;ProjectName&gt; /f &lt;fullPathToModifiedFile&gt;\Scenario.xml
witimport /t &lt;TFS ServerName&gt; /p &lt;ProjectName&gt; /f &lt;fullPathToModifiedFile&gt;\Task.xml</pre>
Again, remember to refresh any running Team Explorer instances to receive the changes on the client machines.