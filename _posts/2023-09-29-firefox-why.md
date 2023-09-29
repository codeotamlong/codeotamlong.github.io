---
title: "[Firefox Awesome] Part 0: Tại sao lại là Firefox"
date: 2023-08-28 11:33:00 +0700
categories: [firefox, awesome]
tags: [firefox, awesome]
---
# 1. Chrome không tốt như thế! "Do be evil!" [^footnote]
Chrome nó có tính năng "ăn gian" mà Firefox không có, nghĩa là khi bạn gõ `google.com` trên Chrome thì nó dùng thuật toán học máy để đoán trước trang web, ví dụ bạn vừa gõ `goo` nõ đã biết là `google` rồi và tải sẵn luôn trang web vào bộ nhớ, tính năng này khiến người dùng nghĩ (đánh lừa người dùng) là Chrome nhanh hơn Firefox nhưng không phải thế, nếu load chay thì nhanh ngang nhau cả thôi nhưng ông đây load trước vào bộ nhớ để ăn gian thì bố ai thắng nổi ông, cũng như trên đường chạy mà một ông đứng ngay vạch đích còn các ông khác thì chạy từ đầu sân ấy. 

> Vấn đề ở đây cần phải làm rõ là Chrome không hề nhanh hơn Firefox, mà nó có nhiều chiêu trò đánh lừa người dùng khiến họ nghĩ Chrome nhanh hơn.
{: .prompt-info }

Với Chrome:
> or instance, Chrome, predicts what the user is typing and fires the request even before the user has done typing and hitting enter. By the time they hit enter, the page is ready to load front the cache. This is done with some fair amount of ML.

Với Firefox (ý nói là Firefox không tải trước trang như Chrome) [^fn-nth-2] [^fn-nth-3]

> - Firefox will prefetch certain links if any of the websites you are viewing uses the special prefetch-link tag.
> - In order to reduce latency, Firefox will proactively perform domain name resolution on links that the user may choose to follow as well as URLs for items referenced by elements in a web page. 
> - To improve the loading speed, Firefox will open predictive connections to sites when the user hovers their mouse over thumbnails on the New Tab page or the user starts to search in the Search Bar, or in the search field on the Home or the New Tab page. In case the user follows through with the action, the page can begin loading faster since some of the work was already started in advance.

*Tạm dịch:*

> - Firefox sẽ tìm tải trước trước một số liên kết nhất định nếu trang web đang truy cập sử dụng thẻ `prefetch-link`, ví dụ: `<link rel="prefetch" href="https://example.com/landing-page" />`
> - Để giảm độ trễ, Firefox sẽ chủ động thực hiện phân giải tên miền trên các liên kết mà người dùng có thể chọn theo dõi cũng như URL của các mục được tham chiếu bởi các thành phần trong trang web, ví dụ `<link rel="dns-prefetch" href="https://example.com/" />`. Xem thêm: <https://bitsup.blogspot.com/2008/11/dns-prefetching-for-firefox.html>
> - Để cải thiện tốc độ tải, Firefox sẽ **mở các kết nối được dự đoán** tới các trang web khi người dùng di chuột qua hình thu nhỏ trên trang `New Tab` hoặc người dùng bắt đầu tìm kiếm trong `Thanh tìm kiếm` hoặc trong trường tìm kiếm trên `Homepage` hoặc trang `New Tab`. Trong trường hợp người dùng thực hiện theo dự đoán, trang có thể bắt đầu tải nhanh hơn vì một số công việc đã được bắt đầu trước.

Ngoài ra rất nhiều người dùng không muốn tính năng này vì nó **không tôn trong bảo mật thông tin cá nhân của người dùng**, vì chưa vào trang đã tải luôn rồi thì trang web mục tiêu nó đã ghi địa chỉ IP lại rồi, Firefox **không thêm tính năng này vì hộ tôn trọng sự bảo mật thông tin người dùng**. Không có cách nào thêm vào Firefox cả vì tính năng này hoạt động khi đang gõ trên thanh địa chỉ, thứ duy nhất có thể khiến Firefox gần giống Chrome là addon Load Faster này <https://addons.mozilla.org/en-US/firefox/addon/faster-pageload/>, nó khiến Firefox tải trang vào bộ nhớ khi đặt chuột lên link, Chrome cũng có tính năng này, bạn cứ dùng Chrome, đặt chuột lên một link bất kỳ, đợi 3s rồi ấn phát vào link là trang hiện ra tức thì không cần tải. Cơ mà như trên, tính năng này không tôn trọng quyền riêng tư của người dùng.

Tóm lại học được gì qua những gì mình nói:

> - Chrome nó tải nguyên trang web (DNS, HTML) vào RAM ngay khi bạn chưa gõ xong tên trang web, khi đặt chuột lên link.
> - Firefox mặc định chỉ tải trước DNS, không hề có HTML nên đó là lý do tại sao Firefox cảm giảc chậm hơn
{: .prompt-info }

# 2. uBlock Origin làm việc tốt nhất trên Firefox (uBO works best on Firefox) [^fn-nth-4] _Tạm dịch - Đọc bản gốc để hiểu rõ hơn_
## Truy nguyên CNAME

![Desktop View](https://user-images.githubusercontent.com/585534/103416937-b623c400-4b56-11eb-8e94-b4851a2248b7.png)
_Nguồn: "Characterizing CNAME Cloaking-Based Tracking on the Web"[^fn-nth-5], Asia Pacific Network Information Centre[^fn-nth-6], August 2020._

Các thanh màu xanh lục/đỏ đậm là uBO trước/sau khi nó có khả năng giải mã CNAME trên Firefox.

## Lọc HTML (HTML filtering)

HTML filtering là khả năng lọc nội dung phản hồi của tài liệu HTML trước khi trình duyệt phân tích cú pháp, cho phép xóa các thẻ cụ thể trong tài liệu HTML trước khi chúng được trình duyệt phân tích cú pháp và thực thi,. Tính năng này yêu cầu API `webRequest.filterResponseData()`, hiện chỉ có trên `Firefox`.

## Khởi chạy trình duyệt

**Firefox sẽ đợi uBO sẵn sàng trước** khi gửi yêu cầu mạng từ (các) tab đã mở khi khởi chạy trình duyệt. Trong các trình duyệt gốc Chromium, có sẵn một cài đặt, bị tắt theo mặc định, để giảm thiểu sự cố này trong các trình duyệt dựa trên Chrome và không hoạt động hiệu quả 100% tất cả các trường hợp.

## Tìm nạp trước (Pre-fetching)
Tính năng Pre-fetching, ** mặc định bị tắt trong uBO**, được ngăn chặn một cách đáng tin cậy trong Firefox. Các trình duyệt dựa trên Chromium ưu tiên các trang web hơn cài đặt của người dùng khi quyết định xem tính năng tìm nạp trước có bị tắt hay không.

Tham khảo: <https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-prefetching>

## WebAssembly
**Phiên bản Firefox của uBO sử dụng mã WebAssembly** để lọc các đường dẫn mã lõi. Với các trình duyệt dựa trên Chrome, trường hợp này không xảy ra vì tính năng này sẽ yêu cầu quyền bổ sung trong tệp `manifest` và có thể gây ra xung đột khi đưa lên Cửa hàng Chrome trực tuyến.

Thông tin thêm: <https://github.com/WebAssembly/content-security-policy/issues/7#issuecomment-441259729>

## Nén lưu trữ

Phiên bản Firefox của uBO sử dụng `tính năng nén LZ4` theo mặc định để lưu trữ danh sách bộ lọc thô, dữ liệu danh sách đã biên dịch và ảnh chụp nhanh bộ nhớ vào bộ lưu trữ trên đĩa. `Tính năng nén LZ4` yêu cầu sử dụng `IndexedDB`, điều này **gây ra vấn đề với các trình duyệt dựa trên Chrome ở chế độ ẩn danh** trong đó các trường hợp `IndexedDB` được reset, khiến uBO khởi chạy không hiệu quả và có danh sách bộ lọc lỗi thời (xem [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399) ). `IndexedDB` là bắt buộc vì nó hỗ trợ lưu trữ Blob dữ liệu dựa trên Blob, một khả năng không có sẵn cho `browser.storage.localAPI` .

# Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22179155>
[^fn-nth-2]: <https://old.reddit.com/r/firefox/comments/gjuqwz/does_firefox_preload_websites_on_search/>
[^fn-nth-3]: <https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections#w_prefetching>
[^fn-nth-4]: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox>
[^fn-nth-5]: <https://blog.apnic.net/2020/08/04/characterizing-cname-cloaking-based-tracking/>
[^fn-nth-6]: <https://www.apnic.net/about-apnic/>