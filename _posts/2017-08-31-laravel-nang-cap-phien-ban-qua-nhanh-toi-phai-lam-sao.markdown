---
layout: post
title:  "Laravel nâng cấp phiên bản quá nhanh, tôi phải làm sao?"
date:   2017-08-31 11:16:00
categories: laravel
author: Hoang Stark
---
Chào mọi người, có thể thấy là rất nhiều ace cảm thấy việc ra phiên bản mới của Laravel hàng loạt khiến cho "không kịp trở tay", chưa học hết bản này đã qua bản khác. Vây nên nhân dịp `Laravel 5.5 LTS` ra mắt, mình có đôi điều muốn chia sẻ với các bạn.

## Laravel ra phiên bản mới liên tục, tại sao?
Công nghệ thay đổi chóng mặt, lượng developer sử dụng Laravel cũng tăng lên. Cho nên nhiều đòi hỏi sẽ càng tăng lên, việc Laravel chăm nâng cấp phiên bản là một điều rất tốt.

## Tôi vẫn còn đang sử dụng Laravel 5.2, có lạc hậu quá không?
Câu trả lời của mình là còn tùy, các bạn để ý các phiên bản được gắn thêm `LTS` ở phía sau phiên bản.

LTS - Long Term Support: Các phiên bản `LTS` sẽ được fix lỗi trong vòng 2 năm và được cập nhật các bản vá bảo mật trong vòng 3 năm. Trong khi các bản không phải LTS thì con số này chỉ là 6 tháng và 1 năm. Như vậy điều chúng ta quan tâm nhất ở `LTS` chính là các bản vá lỗi & bảo mật được kéo dài hơn.

Một lời khuyên của mình, đối với các dự án của riêng bạn, hay của riêng công ty phát triển, có một đội đi theo chăm sóc, thì hãy cứ sử dụng phiên bản mới nhất. Còn đối với các dự án dành cho khách hàng, bạn không đi theo nhiều mà chỉ bảo trì và đảm bảo bảo mật, các bạn nên ưu tiên chọn `LTS`.

Sau thời gian 3 năm nữa, tức là ví dụ bây giờ bạn bắt đầu một dự án với `5.5 LTS`, thì bạn có thể giữ cho dự án vẫn chạy ở `5.5` trong vòng 3 năm, sau đó thì đầu tư thời gian nâng cấp toàn bộ dự án của bạn lên phiên bản mới.
