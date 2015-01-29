title: Snow Leopard with Ruby 1.9 and Rails 2.3.5
tags:
  - Ruby
  - Snow Leopard
id: 40
categories:
  - Dev
  - OSX
  - Ruby
date: 2009-12-24 10:39:44
---

I'm working my way through "Agile Web Development with Rails - Third Edition" and the latest version of the PickAxe "Programming Ruby - Third Edition" books of the Pragmatic Programmers.
As Snow Leopard is my OS I need to update the default shipped Ruby and Rails versions to get to Ruby 1.9 and Rails on top of that.

I've been installing and uninstalling multiple things before finally settling on my ultimate recipe for installing the correct Ruby version and Gems:
(Within Terminal and already running the latest version of [macports](http://www.macports.org/install.php) )
<pre class="brush: bash">sudo port install ruby19 +nosuffix
sudo port install sqlite3
sudo gem update --system
sudo gem install sqlite3-ruby
sudo gem install rails
</pre>