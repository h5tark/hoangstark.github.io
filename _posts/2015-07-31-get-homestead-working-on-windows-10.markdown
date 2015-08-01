---
layout: post
title:  "Get homestead working with Windows 10"
date:   2015-07-31 09:39:11
categories: windows
author: Hoang Stark
---
After update my PC from Windows 8.1 to Windows 10, when I tried to "homestead up", I got this error

{% highlight php %}
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["hostonlyif", "create"]

Stderr: 0%...
Progress state: E_FAIL
VBoxManage.exe: error: Failed to create the host-only adapter
VBoxManage.exe: error: Code E_FAIL (0x80004005) - Unspecified error (extended info not available)
VBoxManage.exe: error: Context: "int __cdecl handleCreate(struct HandlerArg *,int,int *)" at line 66 of file VBoxManageHostonly.cpp
{% endhighlight %}

To solve this issue, please follow below instructions:

### Preparation:
- [VirtualBox 5.0](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant 1.7.4](https://www.vagrantup.com/downloads.html)

### Install:
1. Install Virtualbox 5 and Vagrant 1.7.4
2. Comment line 17: config.vm.network :private_network, ip: settings["ip"] ||= "192.168.10.10" in homestead.rb
3. Comment line 64: b.use ClearNetworkInterfaces in action.rb (path ~\HashiCorp\Vagrant\embedded\gems\gems\vagrant-1.7.4\plugins\providers\virtualbox\action.rb)
4. Homestead init and/or up
5. Homestead halt
6. In Virtualbox preferences -> network -> host-only networks edit existing Host-Only adapter and add 192.168.10.10 as IP address
7. Select homestead box in Virtualbox and go to settings -> network -> adapter 2 and select Host-only network (the one edited in step above)
8. Homestead up, provision

### Cài đặt
1. Install Virtualbox 5 and Vagrant 1.7.4
2. Go to *C:\Users\<YourWindowsUserName>\AppData\Roaming\Composer\vendor\laravel\homestead\scripts* then open *homestead.rb*
3. Add # before line 17: *config.vm.network :private_network, ip: settings["ip"] ||= "192.168.10.10"* in *homestead.rb*
4. Vào *C:\HashiCorp\Vagrant\embedded\gems\gems\vagrant-1.7.4\plugins\providers\virtualbox* mở *action.rb*
5. Add # before line 64: *b.use ClearNetworkInterfaces*
6. Run *homestead init* if this is the first time you install homestead, if fix the issue when update from Windows 8.1, run *homestead up*
7. Run *homestead halt* and waith Virtualbox turn off the virtual machine
8. Open Virtualbox with Admin permission. Go to *File -> Preferences -> Network -> Host-only Networks*, right click on Host-Only Adapter... and select Edit change the first IP to 192.168.10.10
9. Right click homestead box in Virtualbox then go to *Settings -> Network -> Adapter 2* then select Host-only network that you just edit above
10. Open *homestead.rb*, find the line 52 then change *80 => 8000* to *80 => 80*
11. Run Homestead up, provision

Yeah! Machine booted and ready!

[Homestead on Windows 10]({{ site.url }}/images/Screenshot 2015-07-31 03.09.16.png)

### You may search for
- How to install vagrant homestead on Windows 10
- Issue with vagrant homestead on Windows 10
