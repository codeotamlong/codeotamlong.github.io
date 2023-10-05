---
title: "[Firefox Awesome] Các add-on hay ho (P7): Quick Cookie Manager, Dark Reader, Bitwarden, FastForward, New Tab Override"
date: 2023-10-01 10:30:00 +0700
categories: [awesome, firefox, add-on, quick cookie manager, dark reader, bitwarden, fastforward,  new tab override]
tags: [awesome, firefox, add-on, quick cookie manager, dark reader, bitwarden, fastforward,  new tab override]     ## TAG names should always be lowercase
---
## Quick Cookie Manager - Thêm, sửa, xóa, ghim, backup, chia sẻ Cookies[^footnote]
)[**Quick Cookie Manager**](https://addons.mozilla.org/en-US/firefox/addon/cookie-quick-manager/: Tính năng chính là cho phép thêm, sửa, xóa cookie mà hiện tại nhiều người vẫn dùng nó để chơi trò share account premium đấy.
Firefox thì có rất nhiều add-on quản lý cookie, tuy nhiên add-on quản lý cookie này mình đánh giá rất cao tại vì:

- Hỗ trợ quản lý cookie trong cả Container
- Hỗ trợ export ra file cookies.txt có thể chia sẻ cho nhau tài khoản Premium hay dùng cho yt-dlp mà trước [Chrome từng có thằng Save cookies.txt mà cả một subreddit cài vào là malware đó](https://i.reddit.com/r/youtubedl/comments/11i5vyq/psa_the_get_cookiestxt_extension_is_now_actively/)
- Hỗ trợ ghim cookie để ép cho cookie không bị xóa và đây là một tính năng hay và đi đầu
- GIao diện dễ sử dụng, nhẹ cài vào chả dùng nổi vài MB RAM

## Dark Reader - Ép "Chế độ ban đêm" cho trang web (kèm hướng dẫn tối ưu)[^footnote][^fn-nth-2]

Thấy nhu cầu của nhiều người dùng cần Chế độ ban đêm (Dark Reader), mà ở thời điểm hiện tại Firefox không có giải pháp tốt nhất cho chế độ này nghĩa là [**native (dùng chính engine WebRender để tạo màu đen cho web, hiệu năng cao nhất)**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25194758) nên mình sẽ viết một bài chi tiết cách sử dụng add-on này sao cho hiệu năng cao nhất.

[**Dark Reader**](https://addons.mozilla.org/en-US/firefox/addon/darkreader/) thì là add-on quá nổi tiếng rồi, trong các add-on ép Chế độ ban đêm cho trang web thì thằng này là số một, đa năng nhất, lâu đời nhất, hiệu quả nhất, hiệu năng cũng nhất tuy nhiên vẫn chậm một chút, để nó hoạt động hiệu quả các bạn nên làm phần hướng dẫn bên dưới chỉnh giá trị [**nglayout.initialpaint.delay**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23570551)[^fn-nth-3] để tăng hiệu năng của nó lên hết cỡ.

**Cài đặt: <https://addons.mozilla.org/en-US/firefox/addon/darkreader/>**

![](https://voz.vn/attachments/1685504097681-png.1867022/)
_Trang web sẽ đen xì như cục than như thế này đây_

Để Dark Reader có hiệu năng tốt hơn, làm theo bài này:
: [**`nglayout.initialpaint.delay` khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23570551)[^fn-nth-3] ([**Nguyên nhân**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22949373)[^fn-nth-4])

Chỉ vậy thôi là Dark Reader sẽ hoạt động trơn tru hơn. Nếu trang web nào nhìn không hợp lý thì chuyển qua chế độ khác như <span style="COLOR:rgb(65, 168, 95)">**Static</span>** (mặc định là <span style="color:rgb(41, 105, 176)">**Dynamic**</span> nhìn đẹp trên đa phần trang web, **<span style="color:rgb(65, 168, 95)">Static</span>** hiệu năng tốt nhất, **<span style="color:rgb(226, 80, 65)">Filter</span>** và <span style="color:rgb(226, 80, 65)">**Filter+**</span> hiệu năng rất tệ, nên tránh nếu có thể), sau đó chọn `Only for ...` để nó áp vào đúng trang hiện tại:

![](https://voz.vn/attachments/1685503710124-png.1867003/)

### **`nglayout.initialpaint.delay` khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU**[^fn-nth-3]

Ngày xưa hồi mà các bài báo Việt Nam đăng ồ ạt về tối ưu Firefox ấy, thì cái `nglayout.initialpaint.delay` là một trong những tối ưu sai rất sai khi họ khuyên người dùng hạ xuống thấp hơn 250, thực ra để giá trị này cải thiện hiệu năng thì nên tăng lên vì Firefox giờ rất thông minh rồi, tăng lên 1000000000000 thì khi trang tải xong Firefox cũng render một chạm cả trang luôn, cơ mà mình toàn để 2000 (nghĩa là nhắc Firefox cứ làm sao thì làm, sau 2s phải hiển thị trang web dựa trên những gì đã tải được) vì nhỡ sao trang web nó bị chậm có vài file css, js tải mãi không xong thì đợi dài cổ :D

Tăng giá trị `nglayout.initialpaint.delay` sẽ cực kỳ hiệu quả khi dùng add-on như Dark Reader, [**chi tiết**] (https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22949373).

#### Cách thức:
- Mở `about:config`, tìm và sửa lại:

|:-:|-|
| nglayout.initialpaint.delay | 2000 |
| nglayout.initialpaint.delay_in_oopif | 2000 |

[**Ngoài ra tham khảo thêm bài này để có một cái nhìn khái quát hơn về cách Firefox render trang web cũng như tối ưu xa hơn giữa `nglayout.initialpaint.delay` và `content.notify.interval`.**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27064564)


### Một cái nhìn khái quát hơn về cách Firefox render trang web cũng như tối ưu xa hơn giữa `nglayout.initialpaint.delay` và `content.notify.interval`.

Hiện mình đang test thử với thông số này thấy khá ổn, phần `content.notify.interval` để vậy cho chắc chứ `content.notify.backoffcount=0` là đủ, còn `nglayout.initialpaint.delay` sẽ thử cho xuống `250` (chính là thông số của Firefox thời 3-4.0) xem có khác biệt không:

| nglayout.initialpaint.delay | 2000 |
| nglayout.initialpaint.delay_in_oopif | 2000 |
| content.notify.backoffcount | 0 |
| content.notify.interval | 2000000 |
| content.notify.ontimer | true |

Đây là thông số mới, sẽ cập nhập bài nglayout để hoàn thiện nó sau khi thấy cái nào hiệu quả nhất, mục đích của tối ưu này là khiến Firefox chơi tốt với Dark Reader (nếu cần) cũng như tải trang không bị hiện tượng nhấp nháy mà một số bạn bị.

Thông số trải nghiệm 1 (chỉ reflow 2 lần tối đa) cứ mỗi 2s:

| nglayout.initialpaint.delay | 250 |
| nglayout.initialpaint.delay_in_oopif | 250 |
| content.notify.backoffcount | 2 |
| content.notify.interval | 2000000 |
| content.notify.ontimer | true |

Thông số trải nghiệm 2 (không reflow):

| nglayout.initialpaint.delay | 250 |
| nglayout.initialpaint.delay_in_oopif | 250 |
| content.notify.backoffcount | 0 |
| content.notify.interval | 2000000 |
| content.notify.ontimer | true |

### Nguyên nhân[^fn-nth-4]

Mặc định là tức thì đó và giá trị tính là mili giây, 1 giây là 1000 mili giây.

Firefox hiện tại để giá trị này là 5ms, Chrome là 0ms, của mình 2000ms nghĩa là 2s render một lần, tuy nhiên nếu trang web tải xong trước 2s thì render luôn nên không ảnh hưởng đến tốc độ tải trang đâu, Firefox giờ nó khôn lắm không lãng phí thời gian render đâu.

![](https://i.imgur.com/ljX3Fwv.png)

Còn đây là cách Firefox mình render trang web (trang web luôn hiện ra ở trạng thái 100%): <https://gfycat.com/AggressiveDimpledAntarcticgiantpetrel>

Cũng bài viết trên này và áp dụng với người dùng của Dark Reader (<https://addons.mozilla.org/vi/firefox/addon/darkreader/>):
>  I rather like the popular Dark Reader extension — an extension which forces "dark" versions of webpages via looking at the colors used. This is useful to reduce power usage on OLED displays and for more comfortable viewing in dark environments — but it causes significant rendering slowdown on my Android phone and causes the phone to heat up.

> Instructing Firefox to delay incremental redraw appears to have done a great deal to resolve the pain of this for me.

> Ordinarily, if Firefox has not downloaded a full webpage in 250 milliseconds, it tries to start rendering what it has pulled down anyway. This is a great idea if the page can be rendered quickly and not such a great idea if it's expensive to render, since it means that it has to render a webpage multiple times. Presently, it doesn't look like Firefox has any sort of automatic tuning of this value.

> I increased the time to 2000 milliseconds.

> For anyone else in the same boat:
> - Go to "about:config" in the URL bar.
> - Add an integer key "nglayout.initialpaint.delay". At least on my browser's installation, it did not exist and had to be added.
> - Insert the number of milliseconds that you're willing to wait until the browser tries to render the page if it still doesn't have a full copy downloaded. I used 2000.



Addon Dark Reader rất tiện, tuy nhiên add-on này sử dụng rất nhiều CSS và JS để thay đổi màu sắc từng vùng trên trang web (thực sự là add-on này phức tạp hơn rất nhiều người nghĩ là cứ cài vào nó biến trang web thành màu đen, nó còn phân tích màu sắc của font, các thẻ HTML lân cận để đưa ra quyết định có thay đổi màu sang đen hay không) khiến trang web phải render liên tục, tăng giá trị `nglayout.initialpaint.delay` sẽ giảm bớt số lần render của Firefox đi, khiến hạ bớt CPU đi khi tải trang. Tham khảo bài viết trên Reddit ở bên trên để rõ hơn:

> I rather like the popular Dark Reader extension — an extension which forces "dark" versions of webpages via looking at the colors used. This is useful to reduce power usage on OLED displays and for more comfortable viewing in dark environments — but it causes significant rendering slowdown on my Android phone and causes the phone to heat up.
> Instructing Firefox to delay incremental redraw appears to have done a great deal to resolve the pain of this for me.

> Ordinarily, if Firefox has not downloaded a full webpage in 250 milliseconds, it tries to start rendering what it has pulled down anyway. This is a great idea if the page can be rendered quickly and not such a great idea if it's expensive to render, since it means that it has to render a webpage multiple times. Presently, it doesn't look like Firefox has any sort of automatic tuning of this value.

> I increased the time to 2000 milliseconds.

> For anyone else in the same boat:

> Go to "about:config" in the URL bar.

> Add an integer key "nglayout.initialpaint.delay". At least on my browser's installation, it did not exist and had to be added.

> Insert the number of milliseconds that you're willing to wait until the browser tries to render the page if it still doesn't have a full copy downloaded. I used 2000. 

## Bitwarden - Tiện ích lưu mật khẩu mã hóa đáng tin cậy![^footnote]
[**Bitwarden - Tiện ích lưu mật khẩu mã hóa đáng tin cậy!**](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/): Thật ra bình thường mình sẽ không giới thiệu một tiện ích lưu mật khẩu online và mình sẽ chỉ nói rằng đặt Master Password là thừa bảo mật, cơ mà Bitwarden khá đáng dùng nếu bạn cần một tiện ích giúp quản lý và đồng bộ mật khẩu trên máy bàn qua lại giữa Windows -> Linux -> Mac -> Android -> iOS và được mã hóa một chiều trên máy chủ (theo những gì người ta nói) nên dù hacker có hack được cục database thì nó cũng như một cục đất vô tri vô giác. Ngoài ra BItwarden còn hỗ trợ việc chạy máy chủ lưu mật khẩu offline luôn qua Bitwarden Vault hay Vaultwarden, và đây là lý do tại sao mình giới thiệu nó chứ không phải Lasspass.

## FastForward - Bỏ qua thời gian chờ trên một số dịch vụ web[^footnote]
[**FastForward**](https://addons.mozilla.org/en-US/firefox/addon/fastforwardteam/): Bỏ qua bộ đếm bắt chờ kiểu đợi 30-60s mới được tải và bỏ qua link rút gọn trên mấy trang phổ biến, khá tiện cho ai có sở thích tải ứng dụng được chia sẻ bởi mấy ông chơi kiếm tiền online mà không muốn bị hành xác tốn thời gian.

> ~~**Chú ý:**Addon đã bị xóa khỏi Mozilla do bị report DMCA chơi xấu, chi tiết và cách khắc phục <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24177537>~~
{: .prompt-info }

## New Tab Override - Chuyển hướng trang New Tab
[New Tab Override](https://addons.mozilla.org/en-US/firefox/addon/new-tab-override/) là một tiện ích mở rộng dành cho trình duyệt Firefox, thường được sử dụng để thay đổi trang tab mới (New Tab page) của trình duyệt. Điều này cho phép bạn thay đổi cách trang tab mới được hiển thị và hoạt động, tùy chỉnh nội dung hiển thị trên trang tab mới theo ý muốn của bạn.

## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/#post-22174347>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25633915>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-38#post-23570551>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-16#post-22949373>