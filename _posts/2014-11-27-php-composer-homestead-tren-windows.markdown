---
layout: post
title:  "PHP 5.6, Composer và Homestead 2.0 trên Windows"
date:   2014-11-27 04:54:45
categories: laravel
author: Hoang Stark
image: /images/Screenshot 2014-11-27 03.40.12.jpg
---
![PHP 5.6, Composer và Homestead 2.0 trên Windows]({{ site.url }}/images/Screenshot 2014-11-27 03.40.12.jpg)

Cài đặt Homestead trên Linux hay OSX thì khá dễ dàng, tuy nhiên mình thấy nhiều bạn gặp khó khăn trong quá trình cài đặt lên Windows. Bài viết này mình dành cho đối tượng là các bạn newbie không quen làm việc với command, cho nên mặc dù chưa phải là cách cài hay nhất nhưng mình cố gắng đơn giản hóa các bước để phù hợp với các bạn.

### Bước 1: Cài PHP

- Tải Visual [C++ Redistributable for Visual Studio 2012 x86 or x64](http://www.microsoft.com/en-us/download/details.aspx?id=30679) và cài đặt.
- Tải PHP 5.6.3 tại đây:
	- Windows 32 bit: [php-5.6.3-Win32-VC11-x86.zip](http://windows.php.net/downloads/releases/php-5.6.3-Win32-VC11-x86.zip)
	- Windows 64 bit: [php-5.6.3-Win32-VC11-x64.zip](http://windows.php.net/downloads/releases/php-5.6.3-Win32-VC11-x64.zip)
- Giải nén file zip trên và đổi tên thư mục ***php-5.6.3-nts-Win32-VC11-xXX*** thành PHP.
- Bên trong thư mục PHP này các bạn đổi tên file php.ini-production thành php.ini. Mở file này bằng trình soạn thảo như Sublime Text hoặc trình tương tự cho dễ sửa.
- Tìm đoạn sau (dòng 737) 
{% highlight php %}
extension_dir = "ext"
{% endhighlight %}

- Thêm vào bên dưới dòng đó đoạn sau:
{% highlight php %}
extension_dir = "C:\PHP\ext"
{% endhighlight %}

- Tìm đoạn sau và bỏ dấu chấm phẩy phía trước đi (;)
{% highlight php %}
;extension=php_openssl.dll
{% endhighlight %}

- Sau đó chép thư PHP mục này vào ổ C:\

### Bước 2: Cài Virtual Box và Vagrant

- Tải Virtual Box mới nhất tại: [https://www.virtualbox.org](https://www.virtualbox.org)
- Tải Vagrant mới nhất tại: [https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
- Cài đặt cả hai ứng dụng trên.

### Bước 3: Cài Composer

- Tải file cài đặt Composer: [Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe)
- Chạy file này, đánh dấu vào Install Shell Menus và click Next. Ấn Browse để chọn đến file C:\PHP\php.exe rồi click Next và cài đặt như bình thường.
image

![Cài đặt Composer]({{ site.url }}/images/Screenshot 2014-11-27 03.56.11.jpg)

### Bước 4: Cài homestead

- Mở Command Promt và chạy 
{% highlight php %}
vagrant box add laravel/homestead
{% endhighlight %}

- Đợi một lát (khá lâu để tải homestead image) sau đó chạy 
{% highlight php %}
composer global require "laravel/homestead=~2.0"
{% endhighlight %}

- Vào Control Panel -> System and Security -> System -> cột bên trái chọn Advanced system settings. Sang tab Advanced chọn Environment Variables

- Ở phần System variables bên dưới tìm mục Path và click đúp để sửa.

- Thêm vào cuối ô Variable value đoạn sau (có dấu ; ở trước): 
{% highlight php %}
;C:\Users\Hoang Stark\AppData\Roaming\Composer\vendor\bin
{% endhighlight %}

![Thêm vào cuối ô Variable value]({{ site.url }}/images/Screenshot 2014-11-27 04.39.35.jpg)

- Trong đó Hoang Stark tương ứng với user trong máy của bạn.
- OK 3 lần để lưu lại.
- Quay lại Command Prompt và chạy 
{% highlight php %}
homestead init
{% endhighlight %}

Như vậy là trong thư mục ***C:\Users\Hoang Stark*** sẽ xuất hiện thêm thư mục .***homestead*** có chứa file ***Homestead.yaml*** ở bên trong để các bạn có thể cấu hình.
Chi tiết về ***Homestead.yaml*** có thể xem bài viết của @luuhoangnam tại [blog](http://blog.luuhoangnam.com/virtual-machine/homestead-youre-my-friend.html) hoặc [tài liệu của Laravel](http://laravel.com/docs/4.2/homestead)

### Bước 5: Tạo Public và Private SSH Key

Bước này chúng ta sẽ sử dụng Putty Key Generator để tạo SSH Key

- Mở Conmmand Prompt (CMD), mặc định CMD sẽ ở thư mục C:\Users\<username> và chạy lệnh: 
{% highlight php %}
mkdir .ssh
{% endhighlight %}
- Tải [puttygen.exe](http://the.earth.li/~sgtatham/putty/latest/x86/puttygen.exe) và chạy file này sau đó ấn nút Generate.
- Để quá trình tạo key diễn ra nhanh thì các bạn rê chuột qua lại ở phần màu xám bên dưới thanh tiến trình màu xanh
![Giao diện puttygen lúc tạo key]({{ site.url }}/images/Screenshot 2014-11-27 06.33.40.jpg)
- Sau khi tạo key xong, các bạn ấn nút Save Public Key và chuyển tới thư mục ***C:\Users\<username>\.ssh***
- Ghi tên file là ***id_rsa.pub***
![Lưu Public Key](/images/Screenshot 2014-11-27 06.35.02.jpg)
- Tiếp tục Save Private Key, sẽ có một cảnh báo nhưng các bạn có thể bỏ qua bằng cách ấn Yes
![Cảnh báo khi lưu Private Key]({{ site.url }}/images/Screenshot 2014-11-27 06.38.07.jpg)
 và chuyển tới thư mục ***C:\Users\<username>\.ssh***
- Ghi tên file là ***id_rsa***
![Lưu Private Key]({{ site.url }}/images/Screenshot 2014-11-27 06.38.07.jpg)
- Lúc này bạn đã có thể chạy lệnh ***homestead up***
- Lần chạy đầu tiên Firewall sẽ hỏi bạn và bạn chọn như hình sau rồi ấn Allow access
![Lựa chọn Firewall cho Homestead]({{ site.url }}/images/Screenshot 2014-11-27 06.40.59.jpg)