+++ 
date = "2016-12-25"
title = "New Macbook Pro!"
slug = "new-macbook-pro"
tags = ["macOS", "Macbook Pro", "Homebrew", "Sublime Text", "Hyper terminal", "Zsh"]
categories = []
+++

It has been almost five years since I last posted anything here. I intend to change that going forwards, starting right now with this post. I recently got myself a new Macbook Pro (the [13" 2016 Touch Bar model](http://www.apple.com/macbook-pro/)). Five years ago I wrote a post about how I set it up and now I figured a good way of starting off again would be to write a new version about how I set up my new Macbook.

This time I won't focus on Ruby and Ruby on Rails as I don't do much Ruby programming anymore, I will just generally outline the tools I have decided on using.

## Package manager
The package manager [Homebrew](http://brew.sh) is still going strong and has only become better. You no longer need to manually install XCode for it to work, instead Apple now provides the basic buildtools separately. When installing Homebrew it will fetch and install all requirements on its own. Excellent!

## Text editor
I still use Sublime Text as my texteditor, it is still actively maintained. [Sublime Text 3](https://www.sublimetext.com/3) is available as a very solid beta. I've been using it for years on both Windows and macOS. While Sublime Text is great on its own the plugin support makes it even better. To install plugins I use the awesome [Package Control](https://packagecontrol.io), a package manager for Sublime. Right now I have Sublime Text setup primarily for Python development using the following plugins:

* [Jedi - Python Autocompletion](https://github.com/srusskih/SublimeJEDI)
* [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter3) (and the add-in [SublimeLinter-pep8](https://github.com/SublimeLinter/SublimeLinter-pep8))
* [GitGutter](https://github.com/jisaacks/GitGutter)
* [Materialize](https://github.com/saadq/Materialize), specifically I use Material Spacegray as showcased on the Github page

## Terminal
I no longer use the trusty old [iTerm2](https://www.iterm2.com), while it easily is the most solid terminal application for macOS I have decided to give the up and coming [Hyper](https://hyper.is) terminal a go. Shortly after I decided on Hyper iTerm2 added support for the Touch Bar though so I might end up falling back to iTerm2 in the future but for now I am quite happy with Hyper. Unlike iTerm2 it is highly plugable, I use a list of plugins to get it to behave as I want it to. Here is a list of the plugins I use:

* [hyperterm-material](https://www.npmjs.com/package/hyperterm-material) - a theme, looks similar to the Sublime Text theme I use
* [hyper-blink](https://www.npmjs.com/package/hyper-blink) - makes the cursor blink
* [hyperterm-tab-icons](https://www.npmjs.com/package/hyperterm-tab-icons) - shows a small icon depending on what is running in the tab
* [hyperterm-clicky](https://www.npmjs.com/package/hyperterm-clicky) - makes links in the terminal clickable
* [hyperterm-summon](https://www.npmjs.com/package/hyperterm-summon) - summon the terminal and hide it with a global hotkey
* [hyperterm-close-on-left](https://www.npmjs.com/package/hyperterm-close-on-left) - moves the close tab button to the left of the tab, macOS style
* [hyperterm-tab-numbers](https://www.npmjs.com/package/hyperterm-tab-numbers) - shows the number of the tab to make quickswitch to tab with cmd+<tab num> easier

### Shell
For my shell I use [Zsh](http://zsh.sourceforge.net) and the gorgeous prompt [Pure](https://github.com/sindresorhus/pure) along with the handy little tool [thefuck](https://github.com/nvbn/thefuck) and [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting).

## Miscellaneous
* For image/photo editing I use [Affinity Photo](https://affinity.serif.com/en-gb/photo/)
* [Spark](https://sparkmailapp.com) is my email client of choice, both on iOS and macOS
* I use [Divvy](http://mizage.com/divvy/) for getting my windows where I want them
* I'm going with Safari as my primary browser, for ad-blocking I'm trying [Wipr](http://giorgiocalderolla.com/wipr.html)
