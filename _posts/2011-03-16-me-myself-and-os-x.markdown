---
layout: post
title: Me, myself and OS X
published: true
categories: 
- OS X
- Sublime Text 2
- Ruby 1.9.2
- Ruby on Rails 3
- RVM
---

**First off, YAY MY MACBOOK PRO ARRIVED!**

I've been spending the last few days configuring and installing a bunch of stuff on it. I might do a more generic post on the things I've done later on. This post will only focus on the developer enviroment for [Rails 3](http://rubyonrails.org).

# Sublime Text 2
First off, the text-editor I use is called [Sublime Text 2](http://www.sublimetext.com/2). It's a good alternative to TextMate and it works on OS X, Windows and Linux. The theme I use is from [Railscasts](http://railscasts.com/about), it's actually made for TextMate but Sublime loads that just fine. I know everyone has their own thoughts on which text-editor to use so I'll just leave that section open.

# Homebrew - Package manager for OS X
Most of you probably have some experience with unix-enviroments. A (most of the times) great thing in unix-distributions is the package manager. Luckily there are some unofficial package managers out there for OS X! The one which seems to be the most used one as of 2011 is [Homebrew](https://github.com/mxcl/homebrew). So this was the first thing I installed because it makes installing Git easy as pie. And I like pie. More on Git later!

# XCode 4 - WTF $4.99 !!!
[XCode 4](http://itunes.apple.com/us/app/xcode/id422352214?mt=12&v0=WWW-NAUS-ITUHOME-NEWAPPLICATIONS&ign-mpt=uo%3D2) was recently [released](abbr:March 9, 2011) on the Mac App Store. While might complain about the newly added pricetag of $4.99, I don't really see the problem, but that's a completely different discussion. 

But why do we need XCode? We're not making any iOS applications you might be thinking! XCode includes the buildtools that Homebrew relies on to build applications. 

## Free alternative?
If you're prefer not paying for XCode 4 you can find XCode 3 for free, which still works fine with Homebrew. I went with XCode 4 though because I plan on getting into iOS programming eventually.

# Git
With Homebrew up and running we're now able to install [Git](http://git-scm.com) with the command `brew install git`. Git is awesome for so [many reasons](http://whygitisbetterthanx.com). If you're just starting out with programming or if you already are a programmer using another system such as SVN or maybe even no version-control at all. If you want to get started with Git and Github you should check out the guide over at [Github](http://help.github.com/set-up-git-redirect).

# RVM - Ruby Version Manager
RVM is the easiest way to handle different versions of Ruby. OS X includes a older version of Ruby. You might think it would be easier to just update that, however by using RVM you're protecting yourself for problems down the road. Some day you might be working on a Ruby project that requires a different version of Ruby than the one you happen to have installed. Then RVM will really shine. Installing RVM requires a few commands so fire up your terminal and head over to [the installation guide for RVM](http://rvm.beginrescueend.com/rvm/install).

When RVM is installed you can start using it by running the following commands
    rvm install 1.9.2-head
    rvm use 1.9.2-head --default
Running `ruby -v` it should tell you something along the lines of `ruby 1.9.2p180`. The 180 number might be higher if there's been any new updates to Ruby since I wrote this post. With `rvm use 1.9.2-head --default` we instructed RVM to always use 1.9.2-head as the default Ruby version.

# Finally, Ruby on Rails!
When we've come this far installing Rails will be a small effort. Something we might want to do before that though is to turn off ri and rdoc generation for RubyGem installations, this will make installing gems a lot faster. It will however disable the local documentation for gems but everyone uses Google these days anyway right? Alright so how do we do this? It's simple, all you have to do is add `gem: --no-ri --no-rdoc` to `~/.gemrc`. If you have been following along this guide that file shouldn't exist so this can be done by running `echo "gem: --no-ri --no-rdoc" > ~/.gemrc` in a terminal window.

Rails time! The command `gem install rails` will install the Rails gem and all required dependencies (there's quite a lot) for you. After that you can generate your first Rails project by running `rails new my_awesome_rails_application`.

## Learning Ruby on Rails
My tip on getting started with Ruby on Rails is to get the book [Rails 3 in Action](http://www.manning.com/katz/) by [Ryan Biggs](http://www.twitter.com/ryanbigg) and [Yehuda Katz](http://www.twitter.com/wycats). It's current in the process of being finished but by buying it now you'll get early access to it. Feel free to join #RubyOnRails at irc.freenode.net as well.