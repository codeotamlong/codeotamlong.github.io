---
title: "[Firefox Awesome] Các addon hay ho (P2): Auto Tab Discard và ProxySwitchy Omega"
date: 2023-09-29 21:30:00:00 +0700
categories: [awesome, firefox, addon]
tags: [awesome, firefox, addon, auto tab discard , proxy switchy omega]     ## TAG names should always be lowercase
---
## [Auto Tab Discard](https://addons.mozilla.org/en-US/firefox/addon/auto-tab-discard/): Tự động unload tab không dùng tới giảm RAM và CPU[^footnote] 

Firefox hay Chrome đi chăng nữa thì từ khi lên multi-process (đa tiến trình) khi dùng sẽ mở lên rất nhiều process kiểu `firefox.exe` hay `chrome.exe`, điều này không tốt cả về mặt hiệu năng lẫn bảo mật, mà tính năng unload tab có sẵn trong Firefox rất tệ như mình đã giải thích ở đây. Nên việc cài một addon dạng unload tab như `Auto Tab Discard` để tắt những tab không dùng đi bạn sẽ tiết kiệm được rất nhiều RAM và CPU do các trang web chạy ngầm gây ra, ngoài ra khi nội dung web bị loại bỏ khỏi bộ nhớ thì kể cả lỗ hổng bảo mật mang tên Spectre and Meltdown cũng bó tay chịu trói.

Ngoài ra khi cài xong thì ấn vào biểu tượng của Auto Tab Discard, chỉnh phần `When the number of inactive tabs exceeds:` là **1** cho nó tắt tab đi thường xuyên hơn, chứ mặc định là `6 là dành cho những ai luôn mở >6 tab`, rất nhiều người dùng trình duyệt mở 3-4 tab thôi nên cho thành 1 để nó unload nhiều hơn. Còn đây là ảnh Firefox của mình mở 5568 tab:

![](https://voz.vn/attachments/1685460921166-png.1866383/)

### Cách để Auto Tab Discard unload tab mạnh tay hơn không bỏ sót trang nào (xem phần hướng dẫn dưới cùng)[^fn-nth-2]

Cũng đúng đó, chả đâu ra mình dùng Firefox 6 tháng tắt một lần, mỗi lấn tắt tổng số tab lên tới 10,000, nhìn chung cứ cài Auto Tab Discard là 1 triệu tab còn mở được chứ chả gì, đây là một vài mẹo bảo trì (maintain) giúp Firefox mở cả 6 tháng mà không bị chậm:

- Vào `about:memory` rồi chọn `GC` để Firefox giải phóng bớt RAM thừa đi
- Vào `Task Manager` thi thoảng thấy có cái process `firefox.exe` nào chiếm RAM thì End Process đi, *chú ý **không** động vào cái firefox.exe cha, chỉ mấy thằng con thôi*.
- Vào `about:unloads` rồi nhấp liên hồi vào nút `Unload` nếu như muốn tự tay unload tab


Ngoài ra khi dùng Auto Tab Discard, vào `about:config` xóa sạch trong `extensions.webextensions.restrictedDomains` để nó unload tất không khoan nhượng bố con thằng nào cả, mặc định nó bỏ sót rất nhiều trang của Mozilla.

## [ProxySwitchy Omega](https://addons.mozilla.org/en-US/firefox/addon/switchyomega/) - Fake IP cực đỉnh[^footnote]
Add-on này hỗ trợ đổi qua lại các proxy chỉ với một cú nhập chuột, và quan trọng hơn là tính năng chỉ fake proxy trên tên miền, một tính năng mà mình luôn yêu cầu cho mọi addon dạng thay đổi nội dung web mà mình giới thiệu từ trước tới giờ, ví dụ như uBlock có, Noscript có, RequestPolicy có, Custom User-Agent String có.

Tại sao `ProxySwitchy` chứ không phải `FoxyProxy` ? *Đơn giản vì FoxyProxy không dễ sử dụng chút nào.*

Cách sử dụng thì cứ tạo profile proxy bình thường rồi nhấp biểu tượng ProxySwitchy rồi đổi thôi.

Còn tính năng chỉ dùng proxy trên tên miền/trang mà mình ưa thích thì tạo một cái `Profile Auto-Switch` nhé, rồi để `Default` là `Direct`, còn phần `Switch Rules` để `Condition type` là `wildcard` cho dễ dùng, phần `Condition Details` thì ví dụ mình muốn chỉ dùng proxy trên `artstation.com` chẳng hạn thì để là `artstation.com`, còn phần `Profile` thì dẫn tới profile của proxy được tạo bên trên thôi.

### 1. Cách fake mà không fake IP để vào các trang bị nhà mạng chặn[^fn-nth-3]

Hướng dẫn cách fake IP mà không fake IP để vượt DPI những trang cần vượt sử dụng ProxySwitchy Omega ở #1 tại một số bạn không dùng ECH được.

#### Ưu điểm:
- Hoạt động trên 100% trang web thậm chí không cần ECH, không quan tâm là Medium, Bonhup hay ẾchVid...
- Giải pháp mang tính toàn tổng hơn sử dụng cách thức băm nhỏ gói tin ClientHello ra để vượt cạn
- KHÔNG HỀ fake IP, nghĩa là tốc độ sẽ nguyên 100%, không tốn 1 xu, không dựa dẫm vào một ai cả
- Không gây lỗi web như GoodbyeDPI vì nó chỉ hoạt động trên những trang cần thiết chứ không toàn bộ hệ thống

#### Cách thức:
- Với Windows: Tải [Demergi](https://github.com/hectorm/demergi), giải nén, bật lên
- Với MacOS:

```bash
npm install -g demergi
demergi --help
```

> Mẹo
> - [Sử dụng NSSM để cài đặt Demergi/ChunkRust thành dịch vụ hệ thống tự chạy khi mở máy và không hiện cửa sổ](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27609873)
> - [ Hoặc dùng file .vbs ném vào thư mục Startup của @Fioren](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27615299)
{: .prompt-tip }

- Vào phần thiết lập của `ProxySwitchy Omega` tạo một `Proxy Profile` tên `ChunkRust`, điền vào là `127.0.0.1` port `8080` rồi Apply
- Tạo tiếp một `Switch Profile` tên `GoodbyeDPI` rồi `Add condition` rồi chọn Type là `Host regex`, Details là `^.*?(?:medium.com|pornhub.com|xvideos.com)` chọn Profile là `ChunkRust` rồi Apply

> Chú ý: Muốn thêm trang nào thì tự thêm vào phần Details
{: .prompt-info }

- Chọn proxy là `GoodbyeDPI` trên thanh toolbar của ProxySwitchy Omega, và thế là xong.

![](https://voz.vn/attachments/1683953751695-png.1831626/)
![](https://voz.vn/attachments/1683953737924-png.1831625/)
![](https://voz.vn/attachments/1683953719334-png.1831624/)

Vào Medium, Bonhup hay ẾchVid... test là thấy sẽ qua tuốt.

Đây là video mình test, ngon nuột nà với VNPT (chú ý video đã bị che gần như 100%): (https://streamable.com/efyjim)

![](https://voz.vn/attachments/1683953882046-png.1831628/)

### 2. Fake IP miễn phí vĩnh cửu chọn quốc gia tùy ý với Tor Control Panel[^fn-nth-4]

[Tải về cài đặt](https://github.com/abysshint/tor-control-panel/releases), chạy rồi Start, đợi một lúc, sau đó đặt proxy mà nó hiện ra ở phần mềm thường là `127.0.0.1:9050` hoặc `127.0.0.1:9051` vào socks của ProxySwitchy là xong thôi. Cụ thể port nó nằm ở:

![](https://voz.vn/attachments/1695470625450-png.2088817/)

Sau đó muốn chọn quốc gia thì vào `Settings` chọn `Filter`, bỏ đánh dấu tất cả mấy cái ngôi sao nhìn thấy đi cho đến khi `Entry, Middle, Exit` đều là `0, 0, 0` (cứ click chuột vào ngôi sao đen) sau đó chọn một quốc gia ưa thích, đánh 3 dấu sao vào như hình dưới, chọn `Apply` rồi `Change Circuit`.

Muốn nhanh chọn các nước có ping thấp và gần Việt Nam, thông số tốc độ có hết trong mục `Filter`, các bạn cứ mạnh dạn ấn vào để sắp xếp theo thứ tự như Ping, Alive (thời gian sống, sống càng lâu càng tốt), Country (quốc gia) rồi chọn một cái ưng ý.
![](https://voz.vn/attachments/1682008215021-png.1791084/)


### 3. Vào các trang đuôi `.onion` với Tor Control Panel mà không khiến trang web thường bị chậm đi[^fn-nth-5]


Đọc thấy bài viết này [Cần phải sử dụng trình duyệt tor một lần trong đời, kèm địa chỉ hidden wiki](https://voz.vn/t/can-phai-su-dung-trinh-duyet-tor-mot-lan-trong-doi-kem-dia-chi-hidden-wiki.847804/)

Thế Firefox hay Floorp thường có thể vào Tor được hay không thì câu trả lời là Có, mà là Có nhưng nhanh nữa vì hướng dẫn này sẽ chỉ hẳn cách dùng Tor + chọn quốc gia như mong muốn để vào các tên miền `.onion`.

#### Ưu điểm:

- Không bao giờ khiến trang web hàng ngày hay vào chậm đi
- Chọn được quốc gia nên không có chuyện dùng máy chủ Tor tận châu Phi gây chậm, mà dùng hẳn Singapore, Hong Kong

#### Yêu cầu:

- SwitchyOmega ở #1
- Tor Control Panel (TCP) ở mục SwitchyOmega #1

#### Thực hiện:

- Cài TCP ở bài trên, làm y xì cách đặt quốc gia là Singapore hay Hong Kong để max tốc độ khi dùng Tor
- Ấn vào biểu tượng Switchy rồi `Options` -> `New Profile`
- Đặt tên là `Tor`
- Ở phần Protocol chọn `SOCKS5`, Server `127.0.0.1`, Port `9050` hoặc `9051`, tùy theo cái port mà TCP phân cho rồi Save.
![](https://voz.vn/attachments/1695435030596-png.2087800/)

- Tạo tiếp một Switch Profile, đặt tên là `Onion` 

>Nếu các bạn đang dùng Switch Profile cho việc vượt DPI với ChunkRust hay Demergi thì tạo một cái Condition mới là ok, không cần tạo cái Switch Profile tên `Onion` này
{: .prompt-tip }

![](https://voz.vn/attachments/1695434991214-png.2087799/
)
- Chọn `Host regex` (bật `Advanced` settings nếu không thấy), điền vào là `^.*?\.onion`
- Phần profile chỉnh thành `Tor`, Save
![](https://voz.vn/attachments/1695435206585-png.2087805/)

- Chỉnh proxy từ SwitchyOmega thành `Onion`.

> Sau đó vào các trang `.onion` rồi hưởng thụ thành quả, mấy trang này chứa rất nhiều hàng hiếm (có thể tham khảo bài bên trên có chia sẻ vài trang căn bản), thậm chí là chống lại nhân loại, nói chung là tiết chế để tránh bản thân trở nên sa sút
{: .prompt-warning}

Rất là ez nhé:
![](https://voz.vn/attachments/1695435721069-png.2087820/)

## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24609843>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25233313>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24766263>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27899373>

