---
title: "[MPV Awesome] Script hay ho cho MPV (P1): Thay đổi giao diện với UOSC và những người bạn!"
date: 2023-10-01 21:45:00 +0700
categories: [awesome, mpv, uosc, thumbfast, quality-menu]
tags: [awesome, mpv, uosc, thumbfast, quality-menu]     ## TAG names should always be lowercase
---
## [UOSC - Feature-rich minimalist proximity-based UI for MPV player](https://github.com/tomasklaen/uosc)[^fn-nth-1]
Bạn đã cài uosc cho MPV chưa ? Nếu chưa thì nên cài vì nó tiện cực kỳ cho người mới, còn người đã dùng MPV tỉ năm như mình thì không cần tới vì quen phím tắt + plugin vào rồi nên bạn cài thử.

Thôi mình dùng post này làm thành một bài cài uosc hoàn chỉnh cho tiện, sau này có bạn khác hỏi cứ đưa link là chuẩn 100% không bao giờ nhầm lẫn:

* Tạo folder `portable_config` trong cùng một thư mục với `mpv.exe` nếu chưa tạo (**Xem:** **[Cấu trúc folder chuẩn để dễ dàng làm theo hướng dẫn trong thread]('https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23849603'))**
* Tạo folder tên `scripts` và tên `script-opts` trong thư mục `portable_config`
* Tải **uosc.zip** tại đây vào đúng folder `portable_config`: <https://github.com/tomasklaen/uosc/releases>
* Giải nén `Extract Here` (sao cho folder `scripts` trong file nén chèn vào folder `scripts` trong thư mục `portable_config` và thư mục `fonts` nằm chung với thư mục `scripts`). Chi tiết xem ảnh sau:
![]("https://voz.vn/attachments/1695213956640-png.2083027/")
* (Không cần thiết lắm) Tải file config của uosc tại đây vào folder `script-opts`: <https://raw.githubusercontent.com/tomasklaen/uosc/main/script-opts/uosc.conf>
* (CỰC KỲ QUAN TRỌNG) Tạo một file tên `mpv.conf` (nếu chưa từng tạo) trong thư mục `portable_config` rồi copy toàn bộ đoạn dưới này vào rồi Save:

```
#uosc
# required so that the 2 UIs don't fight each other
osc=no
# uosc provides its own seeking/volume indicators, so you also don't need this
osd-bar=no
# uosc will draw its own window controls if you disable window border
border=no
```
{: file='./portable_config/mpv.conf'}
    
## Hướng dẫn cài thumbfast cho uosc và MPV zin + MPV.net[^fn-nth-2][^fn-nth-3]

**Chú ý: Đọc cấu trúc folder MPV ở SPOILER thứ 3 ở #1 nếu không rành.**

- Tài thumbfast tại đây và làm theo hướng dẫn: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23171592>
**(Nếu dùng uosc thì dừng lại tại đây, nếu là MPV zin hay MPV.net thì tiếp tục)**

* **(Nếu là MPV zin hay MPV.net)** Tài file này thẳng vào vào thư mục `scripts`: <https://raw.githubusercontent.com/po5/thumbfast/vanilla-osc/player/lua/osc.lua>
* Rổi thêm `osc=no` vào `mpv.conf`

Kết quả (MPV zin): <https://gfycat.com/SimpleConcreteHind>

Nó rất đơn giản thôi nhưng mình viết rất cẩn thận để đảm bảo ai cũng làm được. :D
Ngoài ra cái thumbfast này siêu nhẹ vì nó hoạt động dựa trên cái tính năng decoder của MPV, không gây ngốn CPU như nhiều kiểu làm thumbnail của các trình xem phim khác hoặc plugin khác. :D

Mẹo cho uosc:

* [**Giảm kích thước timeline (thanh trạng thái xem)**]('https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24989650')
* [**Giao diện mod song ngữ, tím huế Twitch tinh giảm**]('https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25899316')


Sau đó mỗi khi muốn hạ độ phân giải bạn ấn vào nút Quality rồi hạ thôi, dùng như dùng Youtube + nhiều tính năng hơn, sâu cày tính năng đổi chất lượng: <https://gfycat.com/JitterySatisfiedBlackfly>
Kết quả và hướng dẫn:

* <https://user-images.githubusercontent.com/47283320/195073006-bfa72bcc-89d2-4dc7-b8dc-f3c13273910c.webm>


![https://user-images.githubusercontent.com/47283320/195072935-44d591d9-00bb-4a55-8795-9cf81f65d397.png](https://user-images.githubusercontent.com/47283320/195072935-44d591d9-00bb-4a55-8795-9cf81f65d397.png)


Mình vừa test thấy được thumbfast, để cho nhanh thì [**tải file này**]('https://voz.vn/attachments/portable_config-zip.1863600/') giải nén phát xong luôn, có gì tự chỉnh trong thumbfast.conf nhé của mình để thumbnail bự vậy cho dễ nhìn thôi.

Mở folder `portable_config` rồi `Extract Here` cho nó chèn đè vào nhé, kớt quở:

![]("https://voz.vn/attachments/1685352409501-png.1863593/")


Test thử: `mpvnet.exe https://www.youtube.com/watch?v=M-8HZCFTbtk`

## Cài quality-menu cho MPV hoặc uosc [^fn-nth-4]

Đúng rồi cần cả quality-menu + cái này.

Chắc để mình làm thêm bài cài quality-menu vì thằng này là một trong những plugin không thể thiếu khi dùng MPV mà nó tương thích uosc.
Cách cài `quality-menu`:

* Tải tại: <https://github.com/christoph-heinrich/mpv-quality-menu>
* Copy file `quality-menu.lua` vào thư mục `scripts`


Xong, nếu dùng chung với `uosc`, mọi thứ đều tự động tích hợp vào menu.


## Nguồn:
[^fn-nth-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-31#post-23246313>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-51#post-23869287>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-162#post-25597851>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-354#post-28040183>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-156#post-25522101>