---
title: "[Firefox Awesome] Part 2b: Các add-on hay ho - HeaderEditor"
date: 2023-09-29 21:30:00 +0700
categories: [awesome, firefox, add-on]
tags: [awesome, firefox, add-on, header editor]     # TAG names should always be lowercase
---
# [Header Editor](https://add-ons.mozilla.org/en-US/firefox/add-on/header-editor/) - Đổi User-Agent/Language, tùy ý thay đổi nội dung trang web[^footnote]
`Header Editor` là  add-on cực mạnh giúp phá và sửa trang web, tính năng:
- Thêm/xóa/sửa header kiểu User-Agent, Referer.. từ đó ép các trang web dùng bản Mobile hay hiển thị theo ý thích, vượt giới hạn trình duyệt kiểu các trang chỉ cho Chrome/Edge vào
- Thêm/xóa/sửa NỘI DUNG WEB (nâng cao) giúp chặn những loại quảng cáo, anti-adblock khó nhằn nhất
- Và rất nhiều trò khác mà cụ thể xem ở dưới:

## Cách ép Youtube Mobile, ép Bing Chat chạy trên Firefox[^fn-nth-2]

Mà thằng CUAS này kể ra dùng cứ lỗi lỗi kiểu gì ấy, có thằng này hay hơn :D

Giới thiệu một add-on mà nó mạnh hơn cái CUAS bên trên, nghĩa là nó hỗ trợ thay đổi giá trị của HTTP header, mà thay đổi User-Agent là một trong những tính năng căn bản: <https://add-ons.mozilla.org/en-US/firefox/add-on/header-editor/>

Ví dụ ngoài đổi User-Agent có thể đổi Accept-Language để ép trang web trả về ngôn ngữ mình muốn giống post này: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/page-37#post-23544524>

Còn để ép Youtube Mobile với Header Editor thì làm như sau:

![](https://voz.vn/attachments/1682059315018-png.1792113/)
UA: `Mozilla/5.0 (Android 12; Mobile; rv:109.0) Gecko/113.0 Firefox/113.0`
~~`Opera/12.02 (Android 4.1; Linux; Opera Mobi/ADR-1111101157; U; en-US) Presto/2.9.201 Version/12.02`~~

Còn nếu muốn ép Bing Chat chạy trên Firefox thì tương tự như trên tạo cái rule mới cho `bing.com` và `www.bing.com` với UA:


- **<span style="color:rgb(65, 168, 95)">Nếu là Firefox PC:</span>** `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36 Edg/112.0.1722.48`
- **<span style="color:rgb(41, 105, 176)">Nếu là Firefox Mobile:</span>** `Mozilla/5.0 (Linux; Android 8.1.0; Pixel Build/OPM4.171019.021.D1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.109 Mobile Safari/537.36 EdgA/42.0.0.2057`


Vào `about:config` chỉnh `layout.css.overflow-overlay.enabled` thành true.

Đây là add-on rất hay nếu có hiểu biết về lập trình web, bởi nó hỗ trợ không chỉ thay đổi Request header mà nó còn hỗ trợ thay đổi Response header và Response body (giống Proximitron/Proxidomo) giúp sửa xóa trang web tùy ý. Và vì nó rất nâng cao nên các bạn tự tìm hiểu nhé mình chỉ giới thiệu sơ qua.

Kết quả đây, không cần CUAS vẫn ép Youtube Mobile được:

![](https://voz.vn/attachments/1682059348762-png.1792114/)

## Cách sửa xóa Response header[^fn-nth-3]
Cập nhập thêm bài viết và add-on Header Editor nà, lần này là cách để xóa Response header, giúp ép liên kết bắt phải tải về phải mở trong trình duyệt web :D

Cái Header Editor này cực mạnh, nó giúp thay đổi gần như tất cả mọi thứ trên trang web, cái chính là biết cách sử dụng thôi, nếu nói về tính tùy biến nó cũng ngang cơ với uBlock hay External Application, có thể phát triển thêm nhiều hướng dẫn được, thậm chí nó chặn được những quảng cáo mà uBlock không thể (chỉ trên Firefox vì Firefox có API cho lọc nội dung gói tin HTTP), kết hợp qua lại với External Application thì sẽ làm được thêm nhiều trò đồi bại nữa :D <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-24051554>

Ví dụ: <https://www.st.com/resource/en/datasheet/stm32f303re.pdf>

### Biển hiện:
- Khi bấm vào thì Firefox không mở xem bằng trình xem pdf.js cùi bắp mặc định được

### Lý do:

- Response header Content-Disposition có tác dụng ép tất cả mọi thể loại link phải tải về, không cho xem trên trình duyệt, rất nhiều trang web truyện tranh cũng làm điều tương tự bằng cách sử dụng Google Image Proxy, mở file ảnh ra thì bị tải về `p.txt`. Chi tiết: <https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition>

### Cách thức:
- Chặt response header Content-Disposition

### Vận hành:

- Mở cửa sổ Header Editor -> Add
- Chọn Modify Response Header
- Chọn Domain (có thể dùng URL hay Regex thì sẽ cụ thể hơn, cơ mà ví dụ này mình dùng domain cho dễ hiểu)
- Match Rule điền vào `www.st.com`
- Header name điền `Content-Disposition`
- Header value điền `_header_editor_remove_`

Cứ muốn xóa header thì dùng `_header_editor_remove_` nhé, nó là cú pháp đặc biệt của thằng này: <https://he.firefoxcn.net/en/FAQ.html#can-i-delete-a-header-in-a-simple-way>

Xong, mở link trên và test, sẽ thấy Firefox mở ra xem được bằng trình xem `pdf.js` cùi bắp :D

## Cách sửa xóa Request header[^fn-nth-4]

Thêm một bài viết nữa về Header Editor (HE) để chỉnh sửa, ở đây mình lấy ví dụ là thêm header [`Sec-CH-Prefers-Reduced-Motion: "reduce"`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-Prefers-Reduced-Motion) để hỏi trang web rằng có thể trả lại nội dung web không có animation (nội dung chuyển động).

### Thao tác:
- Đầu tiên cái HE ở #1 nếu chưa làm, đây là một add-on rất hay và nhẹ, làm được rất nhiều trò bệnh hoạn.
- Sau đó click vào biểu tượng HE ở thanh công cụ, chọn Manage
- Click vào dấu `+`
- Thêm y như sau:

![](https://voz.vn/attachments/1685262571667-png.1861563/)

Để kiểm tra, vào trang này: <https://httpbin.org/headers>

Thành công nghĩa là sẽ giống thế này `"Sec-Ch-Prefers-Reduced-Motion": "\"reduce\"",`:

```javascript
{
  "headers": {
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8",
    "Accept-Encoding": "gzip, deflate",
    "Accept-Language": "en-US,en;q=0.5",
    "Host": "httpbin.org",
    "Sec-Ch-Prefers-Reduced-Motion": "\"reduce\"",
    "Upgrade-Insecure-Requests": "1",
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0",
    "X-Amzn-Trace-Id": "Root=1-64731088-792597b1153c6c3203c4c7e5"
  }
}
```

Rất ez, bài viết này mục đích để làm ví dụ khả năng dùng HE để thêm Request Header vào kết nối HTTP/HTTPS, có thể làm nhiều trò như thêm header `Authorization` để khiến trang web tự động xác thực cho mình và nhiều trò khác.

Còn header [`Sec-CH-Prefers-Reduced-Motion: "reduce"`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-Prefers-Reduced-Motion) vẫn đang trong giai đoạn thử nghiệm, cơ mà khi thành chính thức và các trang web áp dụng vào sẽ ít bị quấy rối bằng animation nặng nề khiến nóng máy.


## Cách cho phép CORS không cần cài thêm add-on CORS[^fn-nth-5]
Dùng thằng Header Editor thì mình support được nhé, vì chuẩn hóa add-on không dùng khác nhau với lại thằng nay uy tín và mạnh: (https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-24125806)

Muốn cho phép CORS cho trang nào thì:

- Mở cửa sổ Header Editor -> Add
- Chọn Modify Response Header
- Chọn Domain (có thể dùng URL hay Regex thì sẽ cụ thể hơn, cơ mà ví dụ này mình dùng domain cho dễ hiểu), nếu muốn tất cả thì chọn All (**rất không nên làm**[^fn-nth-6] , và bỏ qua mục kế)
- Match Rule điền vào tên miền, ví dụ `www.st.com`
- Header name điền `Access-Control-Allow-Origin`
- Header value điền `*`

> CORS thì chỉ nên cho phép khi cần thiết, ví dụ các Userscript cần tải dữ liệu qua XmlHttpRequest thì mình cứ tự thêm thủ công thôi dùng `All` kể ra nguy hiểm vì ở đây có hai nguy cơ:
> - Lỗi web
> - Mất đi lớp bảo vệ mà trang web tạo cho mình, ví dụ sẽ làm sao khi trang web ất ơ nào đó thử gọi XHR vào `accounts.google.com` để làm điều mờ ám, ví dụ dùng API để lấy email, đây chỉ là ví dụ thực tế tất nhiên sẽ không hoạt động
{: .prompt-warning }
> Bởi CORS là cách trang web và trình duyệt xác thực với nhau là cái liên kết này có được phép tải qua XHR hay không, nếu có trang web trả về `Access-Control-Allow-Orgin: *`, còn nếu trang web không trả về thì trình duyệt sẽ không tải.
> Thực tế thì khi dùng add-on hay native thì họ bao hết khoản CORS rồi, như các add-on dịch online (TWP/Linguist).
> <br>Ngoài ra [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) cũng có tác dụng bảo vệ mình, cơ mà cái này là trang web hoàn toàn định đoạt, trang web nói sao trình duyệt làm theo chứ không có khoản xác thực như CORS. Dễ hiểu nhất thì CSP chính là Firewall của trang web, nó sẽ cho phép tranh ảnh/video/script từ trang này trang kia và chặn hết phần còn lại.
{: .prompt-info }

Thông tin về CORS: <https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Origin>
Làm như này sẽ hiểu sâu được cách thức CORS hoạt động ra sao thay vì cài vào xong không rõ nó làm gì.

## Cách sửa mọi thứ trong trang web, phá tan nát trang web, chặn những quảng cáo gần như khó nhất với Header Editor[^fn-nth-6]

Hướng dẫn sử dụng Header Editor để triệt hạ thẳng tay mọi thể loại quảng cáo khó nhất vũ trụ, sử dụng trang của nợ ` idoitmyself.xyz` làm ví dụ để cho thấy **sự bá cháy của Header Editor, bố tụi nó cũng bó tay chịu trói.**

Thao tác:

- Cài Header Editor ở #1
- Click vào biểu tượng Header Editor ở Toolbar -> Manage -> Options
- Tích chọn:

![](https://voz.vn/attachments/1684423016563-png.1842843/)

- Chuyển qua Rule List
- Ấn vào dấu `+`
- Thêm vào một rule như sau:

Custom function
```javascript
if(detail.type === 'main_frame'){
    return val.replace(/devtoolsDetector.launch\(\);/g, '');
}
```

![](https://voz.vn/attachments/1684423074126-png.1842845/)

Kết đắng ngắt, bố nó cũng chết dưới tay Header Editor :D

![](https://voz.vn/attachments/1684421456055-png.1842811/)

Cơ mà mình đặc biệt khuyến nghị các bạn báo cho uBlock để họ sửa lỗi nhé, như vậy sẽ tốt hơn, mọi người cũng được hưởng lợi: <https://github.com/uBlockOrigin/uBlock-issues/issues>

## Chuyển hướng trang web với HE mà không cần add-on như Redirector/RequestControl[^fn-nth-7] và Nâng cao với Custom function[^fn-nth-8]
Hôm nay lại tiếp tục viết một hướng dẫn khác về HE, chủ đề: **Chuyển hướng trang web**

HE chính là lý do tại sao mình không giới thiệu Redirector luôn mặc dù nó là một add-on "đinh" của Firefox nhé, một thời nó luôn nằm trong bảng xếp hạng các add-on bảo mật tốt nhất của Firefox, thế nhưng HE làm được tất cả mọi thứ Redirector có thể + nhiều thứ không thể.

### Bài viết này lấy ví dụ là sử dụng Reddit chuyển hướng bản New thành bản Old, rất ez thôi.

Tạo một rule mới:

- Name: OldReddit
- Redirect request
- Regular expression
- Match: `^https://www.reddit.com/(.*?$)`
- Redirect: `https://old.reddit.com/$1`

### Tiếp tục một ví dụ nữa cho hiểu bài, link trực tiếp cho `v.redd.it` để xem Reddit mà không cần phải tải trang, lưu file dễ dàng:

- Name: Direct VReddit
- Redirect request
- Regular expression
- Match: `^(https://v.redd.it/[^\.]*?$)`
- Redirect: `$1/DASH_360.mp4`

Thế là có thể xem video mà nó tải thẳng video luôn, có thể lưu về dễ dàng.
Đây chỉ là cái nền, rất nhiều trang khác có thể làm tương tự ví dụ như ImgUr -> Cubari... Các bạn phát triển thêm theo ý mình.

Ngoài ra lưu ý là TẤT CẢ rule của Redirector đều có thể sử dụng cho HE mà không cần sửa một chữ.

### Dùng HE để bypass trang redirect "vô dụng" của vn-z

- Name: Bypass Redirect VN-Z
- Redirect request
- URL Prefix
- Match: `https://vn-z.vn/redirect`
- Redirect (Custom Function): `return atob(detail.url.split('to=')[1])`

## Chặn quảng cáo theo kiểu triệt hạ[^fn-nth-9] (_Ví dụ:_ Xóa triệt thanh sidebar ở trang chủ Voz khiến trang load nhanh như điện[^fn-nth-10])

Một bài hướng dẫn nữa về HE: **Cách *xóa triệt* nội dung web**</span>****

Các bạn chắc đã quá quen với tính năng Element Picker của Adblock (uBlock, Adguard, ABP...), đó là tính năng **<span style="color:rgb(226, 80, 65)">ẩn nội dung web đi</span>**, thế nhưng ẩn khác xa với chặn, ẩn thì những bức ảnh, rác rưởi vẫn sẽ tải ngầm và vẫn lãng phí băng thông, còn với HE thì bài này mình hướng dẫn hẳn **<span style="color:rgb(65, 168, 95)">xóa nội dung web đi</span>**, đã xóa là đứt con nòng nọc không để lại hậu quả về sau.

Ưu điểm:

- Xóa triệt giống nòi, không để lại hậu quả (kết nối ngầm)
- Hiệu năng cao nhất (do hoạt động ở tầng mã nguồn, nghĩa là xóa trước khi trang web hiển thị)
- Xóa được những quảng cáo khó nhất **đọc bài về cách mình dùng HE chặn Anti-Ablock mà cả uBlock cũng gần như chịu thua (chỉ uBlock của Firefox mới qua được nhưng khó vô cùng)**[^fn-nth-7]

**Bài viết yêu cầu người đọc có hiểu biết về Regex ở mức độ vừa phải để sau này tự phát triển ra khi cần.**

[Sử dụng trang web RegEx101 này để viết code, copy nội dung web vào trang này rồi viết code theo thời gian thực sẽ rất dễ dàng.](https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27875389)
> Regex dễ học thôi, cứ dùng trang <https://regex101.com/> viết và kiểm tra thời gian thực luôn, họ dạy cách dùng từng tính năng một và giải thích cả cách thức hoạt động:
> ![](https://voz.vn/attachments/1695307557133-png.2085373/)

### Đầu tiên là trang web ví dụ, mình dùng trang này: (https://blogtruyenmoi.com/c402446/bat-nat-chap-1)

#### Vấn đề: 
Khi tải trang nó tải cả phần comment với ảnh động, tốn bandwidth và tài nguyên CPU/GPU để render.
![](https://voz.vn/attachments/1695310955464-png.2085463/)

#### Giải pháp: Xóa tiệt nó đi

#### Cách thức:

- Bật `Modify response body (only supports Firefox)` nếu chưa từng bật
- Từ HE, tạo một rule mới
- Name thì đặt gì cũng được
- Modify response body
- Regular Expression
- Match: `^.*?blogtruyen.*?/c`
- Custom function: `return val.replace(/<section style="background: white;margin: 10px auto; width: 1200px;height: 1200px; z-index: 999; position: relative;">[\s\S]*?<section class="bg-white comments"[\s\S]*?<div class="clear-fix"><\/div>[\s\S]*?<\/section>/, '<!-- CLEANED -->');`
- Ở phần trên mình sẽ giải thích kỹ hơn, các bạn chuột phải vào trang ví dụ rồi `View Source`, các bạn sẽ xóa là xóa nội dung HTML trong các mã nguồn đó, thì phần comment nó ở đoạn này:
![](https://voz.vn/attachments/1695312779230-png.2085496/)
- Mục đích ở đây là các bạn viết code RegEx sao cho nó nhặt toàn bộ đoạn này và xóa đi. Khi bạn F5 ở phần View Source sẽ thấy nó bị xóa hoàn toàn:
![](https://voz.vn/attachments/1695312955378-png.2085499/)

- Nói chung là như hình sau:
![](https://voz.vn/attachments/1695312295853-png.2085486/)

- Save và F5, sẽ thấy cái khung comment bị triệt hết cả giống nòi, trang load siêu nhanh bởi không còn phí thời gian tải Facebook, rác rưởi, cặn bã...:
![](https://voz.vn/attachments/1695312232944-png.2085485/)

**Kết bài:**
HE là một vũ khí khủng khiếp giúp bạn thâm nhập sâu vào mã nguồn trang web, nếu thành thạo các bạn có thể tăng tốc lướt web lên bằng cách xóa những thứ rác không cần thiết, cách này vượt trội so với ẩn đi bằng CSS `display:none` của uBlock/Adguard/ABP, và trị những quảng cáo cứng đầu nhất.

> **<span style="color:rgb(226, 80, 65)">Tuy nhiên nhược điểm là nó yêu cầu khá cao từ phía người dùng.</span>**
{: .prompt-warning }

### Ví dụ đời thực là trang chủ Đen Vâu:

Ở đây là mình ẩn bằng uBlock, nghĩa là kể cả ẩn đi rồi Tiktok vẫn load ầm ầm, vẫn track người dùng, vẫn tốn bandwidth và tất nhiên áp dụng cho cả Youtube, nếu sử dụng HE xóa triệt sẽ lại là một câu chuyện khác:
![](https://voz.vn/attachments/1695314107674-png.2085528/)

#### Cách thức:

- Bật `Modify response body (only supports Firefox)` nếu chưa từng bật
- Từ HE, tạo một rule mới
- Name thì đặt gì cũng được
- Modify response body
- Regular Expression
- Match: `^.*?voz.vn/$`
- Custom function: `return val.replace(/<div class="block" data-widget-id="8" data-widget-key="forum_overview_new_profile_posts" data-widget-definition="new_profile_posts" data-xf-init="lightbox">[\s\S]*?<div class="block" data-widget-id="9" data-widget-key="forum_overview_forum_statistics" data-widget-definition="forum_statistics">/, '<!-- CLEANED --><div class="block" data-widget-id="9" data-widget-key="forum_overview_forum_statistics" data-widget-definition="forum_statistics">');`

Cụ thể:
![](https://voz.vn/attachments/1695314792685-png.2085539/)

F5 lại cái, và anh ấy đã trết, trang tải nhanh như tên lửa, đó là cả một thế giới mới đó. Benchmark hẳn luôn tốc độ tải trang, chưa tới 1s <https://streamable.com/uigw5h>. :D
![](https://voz.vn/attachments/1695314519849-png.2085533/)
![](https://voz.vn/attachments/1695314749241-png.2085538/)

> Đó là sức mạnh của Header Editor (HE), khi mà đẩy giới hạn của nó lên mức cao nhất.
{: .prompt-info }

# Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-24051554>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-24125806>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-25574511>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-24200957>
[^fn-nth-6]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27506429>
[^fn-nth-7]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-25364481>
[^fn-nth-8]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27401212>
[^fn-nth-9]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27401702>
[^fn-nth-10]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27876504>
[^fn-nth-11]: <https://voz.vn/t/tong-hop-nhung-add-on-chat-cho-firefox-pc-mobile.682181/post-27877026>

