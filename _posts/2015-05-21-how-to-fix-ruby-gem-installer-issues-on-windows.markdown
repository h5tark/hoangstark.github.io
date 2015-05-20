---
layout: post
title:  "How to fix Ruby Gem installer issues on Windows"
date:   2015-05-21 04:35:00
categories: windows
author: Hoang Stark
---
How to fix Ruby Gem installer issues on Windows

### Encoding

After use [Ruby Installer](http://rubyinstaller.org/) to use gem on Windows. I got this error when try the command "gem install":
{% highlight php %}
C:\Users\Hoang>gem install sass
ERROR:  While executing gem ... (Encoding::ConverterNotFoundError)
    code converter not found (UTF-16LE to Windows-1258)
{% endhighlight %}

=> Just run "chcp 850" before run "gem install".

### Build tools required

For example, I run *"gem install jekyll"* to install jekyll, but I got this error.

{% highlight php %}
ERROR:  Error installing jekyll:
        The 'posix-spawn' native gem requires installed build tools.

Please update your PATH to include build tools or download the DevKit
from 'http://rubyinstaller.org/downloads' and follow the instructions
at 'http://github.com/oneclick/rubyinstaller/wiki/Development-Kit'
{% endhighlight %}

=> Download development kit at [http://rubyinstaller.org/downloads/](http://rubyinstaller.org/downloads/). 
- I use Ruby 2.1.x and Windows 8.1 x64 so I choose the exe file in this section: "For use with Ruby 2.0 and above (x64 - 64bits only)".
- Make a new folder named "Ruby DevKit", copy the downloaded exe file to this folder, then run it for extracting (7z). 
- When the file is extracted, In the Ruby DevKit folder, hold Shift then click the right mouse button, select Open command window here.
- On the command windows, run *"chcp 850"*, then run *"ruby dk.rb init"*, then *"ruby dk.rb install"* to bind it to ruby installations in your path.
- Try the install command *"gem install jekyll"* again