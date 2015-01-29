title: "BizTalk Web Service Publishing Wizard Error: Method not found: System.Xml.Serialization.XmlMapping.get_ElementName()"
id: 18
categories:
  - BizTalk 2004
date: 2007-08-17 11:38:29
tags:
---

I was stunned, I had defined a Request schema and a Response schema to be used by a Web Service I wanted to implement in BizTalk 2004\. The Request schema was straightforward, just some fields which made up a Service Request. The response would be a collection of 0 to N "Records".

I had the Response Schema defined somewhere around the lines of this:
<pre class="brush: xml">
&lt;?xml version="1.0" encoding="utf-16"?&gt;
&lt;xs:schema xmlns="http://BizTalk_Webservice_Publishing_issue.Schema2"
  xmlns:b="http://schemas.microsoft.com/BizTalk/2003"
  targetNamespace="http://BizTalk_Webservice_Publishing_issue.Schema2"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="Root"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
        &lt;xs:element minOccurs="0" maxOccurs="unbounded" name="Record"&gt;
          &lt;xs:complexType&gt;
            &lt;xs:sequence&gt;
              &lt;xs:element name="Field1" type="xs:string" /&gt;
              &lt;xs:element name="Field2" type="xs:string" /&gt;
              &lt;xs:element name="Field3" type="xs:string" /&gt;
            &lt;/xs:sequence&gt;
          &lt;/xs:complexType&gt;
        &lt;/xs:element&gt;
      &lt;/xs:sequence&gt;
    &lt;/xs:complexType&gt;
  &lt;/xs:element&gt;
&lt;/xs:schema&gt;
</pre>

Looks sensible right? It compiles okay, I can make an Orchestration with a Request-Response port, everything looks fine, until the Web Service Publishing Wizard gives me:

<pre class="brush: csharp">
Failed to create project http://localhost/BizTalk_Webservice_Publishing_issue_Proxy.
[Microsoft.BizTalk.WebServices.PublishingException] Failed to construct code for schema "http://BizTalk_Webservice_Publishing_issue.Schema2".
Method not found: System.String System.Xml.Serialization.XmlMapping.get_ElementName().
</pre>
I didn't get it, what was wrong? After searching the internet (in which I obviously found one of [Patrick's blogpost](http://bloggingabout.net/blogs/wellink/archive/2007/05/22/solving-the-microsoft-biztalk-webservices-publishingexception-with-imported-schema-s.aspx) which didn't help in this case as I had no imported schema's) I began some experiments. I determined that the cause lies in the multiplicity on the **Record** element. It didn't matter what values I used, as soon as the schema allowed more than one **Record** element to be a part of the message, the Wizard failed on me.

I don't remember how I got the idea, but the solution is rather simple. It appears that the Wizard doesn't like the multiplicity _on the **element**_. So, let's put the multiplicity one level higher, **_around_** the element, like this:
<pre class="brush: xml">
&lt;?xml version="1.0" encoding="utf-16"?&gt;
&lt;xs:schema xmlns="http://BizTalk_Webservice_Publishing_issue.Schema2"
  xmlns:b="http://schemas.microsoft.com/BizTalk/2003"
  targetNamespace="http://BizTalk_Webservice_Publishing_issue.Schema2"
  xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="Root"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
        &lt;xs:sequence minOccurs="0" maxOccurs="unbounded"&gt;
          &lt;xs:element name="Record"&gt;
            &lt;xs:complexType&gt;
              &lt;xs:sequence&gt;
                &lt;xs:element name="Field1" type="xs:string" /&gt;
                &lt;xs:element name="Field2" type="xs:string" /&gt;
                &lt;xs:element name="Field3" type="xs:string" /&gt;
              &lt;/xs:sequence&gt;
            &lt;/xs:complexType&gt;
          &lt;/xs:element&gt;
        &lt;/xs:sequence&gt;
      &lt;/xs:sequence&gt;
    &lt;/xs:complexType&gt;
  &lt;/xs:element&gt;
&lt;/xs:schema&gt;
</pre>

So after encapsulating the **Record** element in a _Sequence_ on which I added the multiplicity, all was well. I don't think I fully understand why the Wizard (or XSD.exe which is running the show in the background) fails on the first version, but now I do know how to solve this.

**Update:** fixed the formatting of the XML Schema's for readability.