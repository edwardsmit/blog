title: Switching to Git
id: 13
categories:
  - Digital Life
date: 2009-08-11 23:08:18
tags:
---

I've been using subversion for a very long time. During that period I've got several people and one company hooked on this version control system after I got frustrated with SourceSafe. SourceSafe was the only version control software developers on the Microsoft platform knew, if they did any. For those people subversion was a giant leap, but once they saw it in action on they're large .net projects they were sold.
Once I moved to the Mac OS X platform subversion happily travelled along for my local version control.
I've always had two main frustrations with subversion:

1.  In a local situation you are stuck with a directory on your system which doesn't contain anything sensible: your local repository
2.  It is not easy to convert a local directory to a working copy under version control (add/commit/checkout)
Now I've switched to [Git](http://git-scm.com/ "Git") and I will undoubtly find issues using it, but so far my two main frustrations are solved with three lines of code
<pre class="brush: bash">git init
git add .
git commit -m "First commit"</pre>