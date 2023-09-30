---
title: "[Firefox Awesome] Part 1: Cách nhảy nhót các bản mod của Firefox mà không mất dữ liệu (.aka backup dữ liệu Firefox)"
date: 2023-09-29 09:20:00 +0700
categories: [awesome, firefox]
tags: [awesome, firefox]     # TAG names should always be lowercase
---
# 1. Lợi ích gì khi sử dụng các bản mod của Firefox ? [^footnote]
Tốc độ
: Firefox zin mặc định không được biên dịch (compile) bằng các tập lệnh tối ưu, mà thực tế ra được biên dịch bằng các tập lệnh tối ưu khiến Firefox mượt lên rất nhiều mà tier list là SSE > SSE2 > SSE3 > AVX2, nhược điểm là càng lên cao độ tương thích phần cứng càng giảm, yêu cầu các hệ máy mới hơn.

Tính năng mới
: Tùy theo từng bản mod mà được tích hợp các tính năng hữu ích như Portable, ẩn địa chỉ IP, chống theo dõi...

# 2. Các bản mod hay ho, uy tín của Firefox
>- Privacy = Riêng tư
>- Portable = Không cần cài đặt, không để lại rác, cho vào USB/mang sang máy khác giữ 100% dữ liệu
>- Adblock = Chặn quảng cáo dạng native
>- SSE2/AVX/LTO (các từ khóa đầu tiên) = Tập lệnh tăng tốc biên dịch

## Firefox Tete009 - SSE2/AVX2+Portable
Nếu như nói tới bản mod uy tín và lâu đời nhất (từ Firefox 2 nghĩa là 2006 tới nay), không thể không nói tới tete009, bản mod này được biên dịch tối ưu bằng tập lệnh SSE2 nên tương thích với đa phần hệ máy thời nay, giúp tăng tốc độ xử lý so với Firefox thường, ngoài ra tác giả áp dụng rất nhiều lệnh tối ưu PGO trong suốt mấy chục  năm trời nên nhìn chung về độ uy tín và an toàn là không có gì bản. Bản này không khác gì Firefox thường, tuy nhiên có thể biến thành Portable 100% không cần Launcher như Portableapps.

Hiện tại (14/9/23) Tete đã chính thức lên kệ AVX2.

Ngoài ra một điểm mạnh nữa của tete là bản này là bản stable nhưng lại là Nightly, nên nó có thể cài được Fastforward, Multi-Threaded Download Manager và iMacros.
- Download: <www1.plala.or.jp/tete009/en-US/software.html#FFDL>
- Folder chứa các bản cũ (có cả 32bit): <https://drive.google.com/drive/folders/0BwJVYWis62cRalRwX2tsZklqUkk>
- Cách đặt Tete thành Firefox Portable xịn Pin được, đặt Default Browser được:<https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23354773>
- Cách đặt Tete Portable thành Default Browser:<https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24612099>

## Firefox Mercury- AVX2+Privacy
Tuy không lâu đời nhưng bản này được biên dịch dựa trên tập lệnh AVX2, mà AVX2 còn nhanh hơn cả SSE2 nên khá phù hợp cho những bạn chỉ quan tâm tới tốc độ. Ngoài ra tác giả cũng bê nhiều cái tối ưu của Librewolf, FireDragon... là những bản mod khác về để thêm mắm thêm muối.
- Download: <https://github.com/Alex313031/Mercury/releases>

## LibreWolf & Tor & Mullvad - Privacy
Đây là bản Firefox tập trung vào bảo vệ sự riêng tư của người dùng, tắt sạch telemetry và bật các tính năng kháng tạo fingerprint (dấu vân tay) để khiến các trang như Google, Facebook... không theo dõi được.
Mullvad thì mặc định chặn quảng cáo với uBlock.
Lưu ý là khi dùng các trình duyệt thuộc họ Privacy, hạn chế cài các addon chặn quảng cáo hay Userscript vì nó khiến trang web phát hiện ra mình dùng addon gì, từ đó khiến fingerprint không còn thuộc về đám đông nữa.
- Download:
    + LibreWolf: <https://librewolf.net/>
    + Tor: <https://www.torproject.org/download/>
    + Mullvad: <https://github.com/mullvad/mullvad-browser/releases>

## Slimbrowser - Adblock+DownloadManager+Portable
SlimBrowser là một trong những bản mod đàng hoàng nhất của Firefox, đàng hoàng ở đây nghĩa là nó tự viết lấy tất cả tính năng chứ không cài addon vào rồi gọi là bản mod như nhiều bản mod khác (mà mình không bao giờ cho vào post này).
Cái AdBlock mặc định cùi bắp, nên thay bằng uBlock, còn lại đều ngon.
Có Portable Pin được như Tete009.
- Tính năng:
    + AdBlock built-in như Brave, tuy nhiên cùi bắp nên bỏ cài uBlock
    + Download Manager có thể kéo link Youtube dễ dàng, tất nhiên chia luồng được như IDM (đáng tiền)
    + Portable kiểu Pin được như Tete009, có thể đặt mặc định để ép Discord, Zalo, Telegram... mở vào nó (đáng tiền)
    + Dịch thuật như Google Chrome (đáng tiền)
    + Thời tiết (cùi bắp), nên tắt
    + Upload ảnh không cần vào web (đáng tiền)
    + Facebook (tàm tạm)
Với từng đấy tính năng trình duyệt này khá đáng thử cho những người lười, cài phát đủ tính năng xong không quan tâm tới addon nữa.
- Download: <https://www.slimbrowser.net/>

## Pulse Browser - Sidebar
Firefox + 2 Sidebar như Edge.
- Download: <https://github.com/pulse-browser/browser/releases>

## Floorp - LTO+Portable+Sidebar+VerticalTab+Workspace+UnloadTab+...]
Bản Firefox mod của tác giả người Nhật mới nổi thời gian gần đây trên các trang Reddit như /r/browsers, /r/firefox bởi nó cũng khá là đặc sắc khi so với Firefox gốc, mà cái đặc sắc nằm ở:
- Sidebar bên tay phải để mở nhanh các tính năng như bookmark, history, addons... (native)
- Hỗ trợ giao diện đẹp như Lepton, Chrome, Edge (cứ vào Settings là thấy)
- Ngủ đông tab giống Auto Tab Discard cơ mà tốt hơn vì nó unload nhiều hơn, và là native
- Hỗ trợ tab dọc (native)
- Hỗ trợ đổi phím tắt tùy ý (native)
- Workspace giống Vivaldi để quản lý tab theo từng vùng một cho gọn, ví dụ chia ra cho: Công việc, Cá nhân, Ăn chơi... (native)
- Tối ưu bằng tập lệnh PGO+LTO nên nhanh hơn cả tete (SSE2+PGO) và thậm chí Mercury (AVX) mà vẫn giữ nguyên tính tương thích với hệ máy cũ chứ không như AVX kén hệ máy mới
- Và nhiều tùy chỉnh nhỏ khác nữa rất khó liệt kê hết vì nói chung nó nằm trong Settings ấy...

~~**Chú ý:** Các bạn nên chỉnh lại `about:config` của Floorp để không bị loophole WebRTC, sẽ khiến tải một số trang chậm như Chat.Zalo.me~~ Đã được sửa ở bản mới
- Download: <https://github.com/Floorp-Projects/Floorp/releases>

Cơ bản là vậy, ngày xưa thời hoàng kim của Firefox còn có nhiều bản mod hơn như xunxun của Tàu Khựa và vô số kể, nhìn chung mình đề cao thằng Tete009 nhất vì nó trải qua bài thử của thời gian rồi với lại được ông tác giả cặm cụi chỉnh từng dòng tối ưu trong gần 20 năm trời, chắc chắn phải ra ngô ra khoai rồi, trong quá trình sử dụng mình cũng thấy bản này mượt hơn Firefox thường (phiên bản mình đang dùng là 104 32-bit SSE2), bản AVX2 chắc sẽ rất nhanh nếu bạn nào tò mò muốn thử xem Firefox chạy hết 100% công suất sẽ nhanh ra sao.

> Mình không liệt kê `Waterfox` hay `Palemoon` vì hai thằng này cấu trúc profile khác Firefox thường, nên không nhảy distro được.
{: .prompt-info }

# 3. Cách nhảy các bản mod Firefox không lo mất dữ liệu [^fn-nth-2]
1. Đầu tiên ở Firefox đang dùng, gõ `about:support` rồi xem phần `Application Binary`, mở thư mục chứa `firefox.exe` lên
2. Tải bản mod dạng nén như 7z, zip, rar... về rồi giải nén thẳng vào thư mục chứa `firefox.exe`
3. Nếu mở lên báo lỗi không tương thích thì vào folder `profile` xóa file `compatibility.ini` đi là xong

# 4. Làm sao tạo mới profile mà vẫn giữ được 90% dữ liệu ?

Đây là một bài viết mà sau khi đọc xong bạn có một cái nhìn toàn tổng về profile của Firefox, giúp bạn xoay sở trong những tình huống khó nhất.

## Mục tiêu:
- Giữ được bookmark, history
- Giữ được mật khẩu
- Giữ được đăng nhập
- Giữ được about:config
- Giữ được addon đã cài (tuy nhiên mất hết tùy chỉnh của addon)

## Cách thức:
1. `about:support` => `Open Profile Folder`
2. Copy những file sau:

|----------------------------------|------------------|
| File/Folder                      | Tác dụng          |
|:---------------------------------|:------------------|
| places.sqlite                    | Bookmark; History |
| cookies.sqlite                   | Cookies           |
| - cert9.db<br> - key4.db<br> - logins.json | Mật khẩu|
| - extension-preferences.json<br> - extensions.json<br> - extension-settings.json<br> - thư mục `extensions` | Add-ons |
| prefs.js                         | about:config      |
| thư mục `storage`                | Tùy chỉnh add-on <br>*không dám chắc 100%*|
| thư mục `chrome`                 | Giao diện         |

3. Tạo profile mới bằng cách vào `about:profiles` -> Create a new profile -> Chọn thư mục -> Launch profile -> `about:support` -> Open Profile Folder -> Tắt Firefox -> Paste vào.

> Đừng quên `Set as Default Profile` cho cái profile mới tạo để từ nay nó là profile chính.
{: .prompt-info }

Vậy thôi, nó đơn giản nhưng mà không biết lại sợ không dám thử, nhưng biết rồi thấy ez vê lù thôi, khi nào `profile` có hiện tượng lạ hẵng làm còn không thì không quan tâm tới bài này, nhưng nó vẫn hữu ích trong trường hợp kiểu copy mật khẩu máy này qua máy khác, `profile` này qua khác, nghĩa là khi biết file nào làm nhiệm vụ nào thì khi đó dễ xoay sở như trên đề cập.

## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-302#post-27777028>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-302#post-27777028>