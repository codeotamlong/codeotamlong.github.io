---
title: "[Firefox Awesome] Tối ưu Firefox (P4): Các thứ linh tinh khác"
date: 2023-10-03 21:45:00 +0700
categories: [awesome, firefox, optimize]
tags: [awesome, firefox, optimize]     ## TAG names should always be lowercase
---
> Có **02*- cách chính để thay đổi các tham số của Firefox:
> 1. Vào `about:config`, tìm và sửa tham số theo nhu cầu
> 2. Sửa file `user.js` (**khuyến khích** để có thể theo dõi thay đổi và backup):
>       + Mở `about:support` => Open Profile Folder
>       + Đóng Firefox (tắt hẳn - _chú ý với MacOS: Close khác với Quit_)
>       + Tạo mới nếu chưa có
>       + Thêm dòng mới `user_pref("<tham số>", <giá trị mới>);`
>       + Save và mở Firefox
{: .prompt-info }

> `user.js` là file javascript nên có thể sử dụng `//` và `/**/` để viết ghi chú
{: .prompt-tip }

## Mở Early Hints để tăng tốc độ tải trang[^fn-nth-1]

```javascript
// Enable Early hints
user_pref("network.early-hints.enabled", true);
user_pref("network.early-hints.preconnect.enabled", true);
user_pref("network.early-hints.preconnect.max_connections", 20);
```
{: file="user.js"}

Thông tin thêm <https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/103>
: `HTTP 103 Early Hints` là phản hồi của server ngay từ lúc đang xử lý yêu cầu, bao gồm các gợi ý về các tài nguyên _được cho là_ sẽ sử dụng. Điều này cho phép trình duyệt bắt đầu `tải trước tài nguyên` trước khi server xử lý xong và trả về kết quả.

## Bật `punycode` để miễn nhiễm với tên miền giả mạo

Bảo mật và riêng tư luôn đi liền với bất tiện, nhìn chung nên xác định điều này và Firefox mặc định nó đủ bảo mật và riêng tư rồi, chỉ cái:


| network.IDN_show_punycode | true |

Là ai cũng nên bật vì nó sẽ phá mấy trang web dùng unicode thành dạng `xn--abcxyz` giúp mấy trang lừa đảo giả tên miền kiểu `google.com` không còn linh nữa.

Ví dụ `フラワーナイトガール.攻略wiki.com` khi bật punycode sẽ bị buộc thành `xn--eckq7fg8cygsa1a1je.xn--wiki-4i9hs14f.com`

Hoặc ngoạn mục là `GOOGᒪE.com` được sửa thành `xn--googe-bkz.com`, `𝐠𝐨𝐨𝐠ʟ𝐞.𝐜𝐨𝐦` thành `xn--googe-hxc.com`

Đó là sự đáng sợ của tên miền giả mạo, và tụi hacker tụi nó không nhân từ như mình mà nó y hệt `google.com` luôn.

##  Tối ưu giảm RAM cho Firefox (đánh đổi bằng bảo mật) (Chi tiết về cách thức hoạt động và các cấp độ của Fission)

> Dưới đây là tối ưu giảm RAM, đặc biệt hiệu quả khi dùng [Progressive Web Application](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24276732) do đặc thù chỉ dùng 1 trang web của nó.
{: .prompt-info }

Làm theo những cái bôi đen trong mục Tối ưu Firefox: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22174347>

| dom.ipc.processCount | 1 |
| fission.autostart | false |

```javascript
// Reduce RAM usage (lower security)
user_pref("dom.ipc.processCount", 1 );
user_pref("fission.autostart", false );
```
{: file="user.js"}

### Các cấp độ Fission

1. Không giới hạn số tiến trình: *Chính là cài đặt mặc định*
: Nội dung (bao gồm: page, iframe, ...) đến từ mỗi root domain được xử lý bởi tiến trình riêng (dù là trong cùng 1 tab). VD: mở cái link sau đây sẽ thấy Firefox dùng 9 "Isolated web content process" và 1 "Isolated service worker process" cho riêng tab đó: <https://voz.vn/u/haidangtueba.1457647/>. Check tại `about:processes` hoặc `about:support#remote-processes`.
: Nội dung trong nhiều tab nhưng đến từ cùng 1 root domain được dùng không quá 4 tiến trình (giá trị mặc định của *dom.ipc.processCount.webIsolated*).

2. Giới hạn bởi số root domain: `dom.ipc.processcount.webisolated = 1`
: Nội dung trong nhiều tab nhưng đến từ cùng 1 root domain được dùng 1 tiến trình. VD: mở 7 tab [www.google.com](http://www.google.com), mail.google.com, docs.google.com, drive.google.com[COLOR=rgb(44, 130, 201)], cloud.google.com[COLOR=rgb(44, 130, 201)], translate.google.com[COLOR=rgb(44, 130, 201)], bard.google.com[/COLOR] [/COLOR][/COLOR] chỉ tốn 1 "Isolated web content process".

3. Giới hạn bởi content value: `fission.webContentIsolationStrategy = 2`
: Chỉ những *high value content* mới chạy trong tiến trình riêng (không rõ Mozilla coi những trang nào là high value, chắc là các trang payment, email...), các Nội dung còn lại sẽ được xử lý bởi các "Shared web content process", số process này chính là giá trị của *dom.ipc.processCount*.

4. Không tách biệt Nội dung: `fission.webContentIsolationStrategy = 0`
: Gần giống với tắt Fission vì hầu hết Nội dung đều được xử lý bởi "Shared web content processes" nhưng vẫn có các tiến trình riêng để xử lý service workers.

5. Tắt Fission: `fission.autostart = false`
: Mọi nội dung đều được xử lý bởi "Shared web content processes".

Có thể thấy từ **cấp độ 3** trở xuống thì `dom.ipc.processCount` mới có ý nghĩa.

Thói quen, sở thích duyệt web kết hợp với cấu hình máy của thím sẽ giúp thím tìm được setup phù hợp. :sexy_girl:

## Tối ưu tốc độ bật Firefox

Do cấu hình của Floorp tắt SkeletonUI đi mặc Firefox/tete/Mercury đều bật mặc định, vào config chỉnh. Cái SkeletonUI này giúp bật phát hiện luôn Firefox, nên không có lý do gì để mà tắt cả và nó hữu ích cho người già, vì họ thường nhấp liên tục vào biểu tượng trình duyệt nếu chưa thấy cửa sổ hiện lên, nhiều khi bật hàng trăm hàng nghìn Firefox lên gây tràn luôn cả RAM:

| browser.startup.preXulSkeletonUI | false |

```javascript
// Disable SkeletonUI
user_pref("browser.startup.preXulSkeletonUI", false );
```
{: file="user.js"}

Xem thêm
: <https://firefox-source-docs.mozilla.org/dom/ipc/process_model.html>
: <https://searchfox.org/mozilla-central/source/dom/ipc/ProcessIsolation.cpp>

## Bật chế độ bỏ qua hỏi han quấy rầy Cookie Banner[^fn-nth-3]

À, trước để 1 nghĩa là `Bỏ qua tất`, còn 2 thì là `Bỏ qua tuy nhiên nếu cần thiết Chấp nhận` :D, tùy theo mức độ riêng tư mà chọn 1 hay 2 thôi, sửa lại là thế này đúng là 2 nó ẩn đi nhiều hơn 1, ngoài ra bật luôn trong Private Browsing:

### Bỏ qua tuy nhiên nếu cần thiết Chấp nhận:

| cookiebanners.service.mode | 2 |
| cookiebanners.service.mode.privateBrowsing | 2 |

### Bỏ qua hết (nếu không cho bỏ qua thì không ẩn được):

| cookiebanners.service.mode | 1 |
| cookiebanners.service.mode.privateBrowsing | 1 |

```javascript
// Bypass Cookie Banners: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPTS - to remove banner);
user_pref("cookiebanners.service.mode", 2 );
user_pref("cookiebanners.service.mode.privateBrowsing, 2 );
```
{: file="user.js"}

Test trên Firefox 113, hoạt động cực tốt. Đỉnh nhất trong các sự lựa chọn ẩn cookie vì nó dùng 2 thuật toán chính, click như người thật (tốt hơn add-on là click máy) và nhúng cookie:

| cookiebanners.bannerClicking.enabled | true |
| cookiebanners.cookieInjector.enabled | true |

```javascript
// Bypass Cookie Banners - emulator CLICK, cookie INJECTOR: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPTS - to remove banner);
user_pref("cookiebanners.bannerClicking.enabled", true );
user_pref("cookiebanners.cookieInjector.enabled", true );
```
{: file="user.js"}

Các trang test:
: <https://stackoverflow.com/questions/37365561/flexbox-row-inside-flexbox-column>

Chốt lại là sau này Firefox sẽ bật cái này mặc định thì dùng của Firefox sẽ tốt hơn dùng của uBlock (tốt hơn rất nhiều vì nó giúp tránh rất nhiều lỗi khó chịu mà trang web tạo ra nếu chỉ ẩn bằng CSS).

## Cách bật nhanh chế độ Compact (gọn gàng) có sẵn của Firefox[^fn-nth-4]

Thêm một bài rất đơn giản cơ mà hữu ích cho đa phần những ai thích giao diện nhỏ gọn cho Firefox, đó là bật giao diện "Compact" của Firefox mà không cần dùng userChrome.

| browser.compactmode.show | true |

```javascript
// Compact mode (slim toolbar)
user_pref("browser.compactmode.show", true );
```
{: file="user.js"}

Sử dụng
: Chuột phải vào thanh toolbar
: Chọn `Customize` ![](https://voz.vn/attachments/1685073662176-png.1857635/)
: Chọn `Compact`

Kết quả nó sẽ gọn như này
: ![](https://voz.vn/attachments/1685073724165-png.1857641/)



## Nguồn:
[^fn-nth-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-188#post-25845776>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-194#post-25938099>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-106#post-24935068>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-157#post-25530119>