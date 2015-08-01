---
layout: post
title:  "Khắc phục lỗi Laravel Homestead trên Windows 10"
date:   2015-07-31 10:39:11
categories: windows
author: Hoang Stark
---
Sau khi update máy tính từ Windows 8.1 lên Windows 10, tôi đã gặp phải lỗi này khi chạy "homestead up":

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

Để xử lý vấn đề trên, hãy thực hiện cách sau

### Chuẩn bị
- [VirtualBox 5](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant 1.7.4](https://www.vagrantup.com/downloads.html)

### Cài đặt
1. Cài đặt Virtualbox 5 và Vagrant 1.7.4
2. Vào *C:\Users\<YourWindowsUserName>\AppData\Roaming\Composer\vendor\laravel\homestead\scripts* mở file *homestead.rb*
3. Thêm dấu # trước dòng 17: *config.vm.network :private_network, ip: settings["ip"] ||= "192.168.10.10"* trong file *homestead.rb*
4. Vào *C:\HashiCorp\Vagrant\embedded\gems\gems\vagrant-1.7.4\plugins\providers\virtualbox* mở *action.rb*
5. Thêm dấu # trước dòng 64: *b.use ClearNetworkInterfaces*
6. Chạy *homestead init* nếu bạn cài lần đầu, nếu fix lỗi khi update từ Windows 8.1 thì chạy *homestead up*
7. Chạy *homestead halt* và đợi Virtualbox tắt xong máy ảo
8. Mở Virtualbox với quyền Admin. Vào *File -> Preferences -> Network -> Host-only Networks* click phải vào Host-Only Adapter... và chọn Edit rồi thay IP trên cùng thành 192.168.10.10
9. Click phải homestead box trong Virtualbox và vào *Settings -> Network -> Adapter 2* và chọn Host-only network vừa sửa ở trên ở trên'
10. Mở *homestead.rb* ở trên tìm dòng 52 sửa *80 => 8000* thành *80 => 80*
11. Chạy Homestead up, provision

Và Yeah! Machine booted and ready!

![Homestead on Windows 10]({{ site.url }}/images/Screenshot 2015-07-31 03.09.16.png)

### Có thể bạn tìm
- Hướng dẫn cài đặt vagrant homestead trên Windows 10
- Gặp lỗi với vagrant homestead trên Windows 10