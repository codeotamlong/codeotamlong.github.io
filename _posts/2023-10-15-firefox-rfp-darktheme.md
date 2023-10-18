---
title: "[Firefox Daily] Dark Theme và Resist FingerPrinting"
date: 2023-10-15 21:33:00 +0700
categories: [firefox, daily, resist fingerprint, darktheme]
tags: [firefox, daily, rfp, resist fingerprint, darktheme]
---

Chuyện là Firefox có tham số `privacy.resistFingerprinting` để kích hoạt chế độ chống ghi dấu trình duyệt (`fingerprint`, _dịch ra bựa vãi_ - đại khái là nó sẽ đánh dấu trình duyệt để nhận dạng, định danh người sử dụng). Chuyên sâu hơn, thì `user.js` của `arkenfox` còn có riêng 1 section dành cho resist fingerprinting, mà nếu bật lên thì sẽ duyệt web "nhạt toẹt": **đóng hộp, trắng tinh, không màu sắc, không mùi vị**. Tác dụng (phụ?) của cái `privacy.resistFingerprinting` là **ép** website chỉ hiển thị light-theme, hay thậm chí là xóa sạch các loại hiệu ứng màu sắc của website. Vẫn biết càng bảo mật thì càng khó dùng, nhưng dark-theme đang là trend, thì liệu có giải pháp nào để tô đen cho website trong khi đang được bảo vệ?

![](/assets/img/firefox-rfp-darktheme/ff-over-rfp.webp)
_Hậu quả của tự bảo vệ quá đà_

## Resist FingerPrinting (RFP) là gì[^rfp-1] 

> Đoạn dưới này được trích và lược dịch từ wiki của `arkenfox.js` và nhiều trang khác
>
> Nguồn: <https://github.com/arkenfox/user.js/wiki/3.3-Overrides-[To-RFP-or-Not]>
{: .prompt-info}

> Điều tốt nhất mà bất kỳ trình duyệt nào cũng có thể tự tin làm được, _ngoại trừ Tor Browser và Mullvad Browser_, là đánh lừa các script "vô tri". Trong Firefox, công cụ tốt nhất cho việc đó là Resist FingerPrinting (RFP) - nó hoạt động hiệu quả, không rò rỉ các giá trị thực và có các biện pháp giảm thiểu thời gian chống lại các cuộc tấn công kênh bên (side-channel attacks). Lý tưởng nhất là có thể sống chung với các tác dụng phụ của RFP, nếu không, hãy cân nhắc sử dụng CanvasBlocker nếu phù hợp với mô hình mối đe dọa (threat model) của bạn
{: .prompt-tip }

> Nếu threat model của bạn yêu cầu ẩn danh và bảo vệ dấu vân tay nâng cao thì **SỬ DỤNG TORBROWSER**. 
>
> Link: <https://www.torproject.org/>
{: .prompt-warning }

Kể cả khi không làm gì trên máy tính thì bạn vẫn có khả năng bị định danh là `unique`(_tạm dịch:_ cá thể duy nhất) - chỉ riêng các số liệu về màn hình, cửa sổ và phông chữ có lẽ là đủ - thêm múi giờ, ngôn ngữ ưa thích và hàng chục số liệu khác và trò chơi kết thúc. Kết quả của một nghiên cứu được thực hiện vào năm 2016 cho thấy 99.24% tỷ lệ nhận diện chính xác[^rfp-tracking-rate-research] (và điều đó không bao gồm các địa chỉ IP - xem thêm hướng dẫn fake IP ở dưới[^rfp-vpn-guide]).

> Hướng dẫn thực chiến về fake IP: <https://educatedguesswork.org/posts/traffic-relaying/>
>
> Trích kết luận của hướng dẫn
> : Địa chỉ IP là một vectơ theo dõi quan trọng và hiệu quả cao và nếu muốn duyệt web ở chế độ riêng tư, bạn cần phải làm gì đó để che giấu IP của mình và điều này chủ yếu có nghĩa là qua kênh trung gian: Bất kỳ hệ thống trung gian nào cũng sẽ che giấu danh tính của bạn khỏi máy chủ, **miễn là nhà cung cấp của bạn không thông đồng với máy chủ**. Bất kỳ hệ thống một bước nào nhất thiết có nghĩa là bạn _tin tưởng nhà cung cấp_ sẽ không theo dõi hành vi của bạn và không thông đồng với máy chủ. Cuối cùng, điều quan trọng cần biết là ngay cả hệ thống tốt nhất cũng chỉ cung cấp khả năng bảo vệ hạn chế. Kẻ tấn công có cái nhìn toàn cảnh về mạng thường có thể thực hiện đủ phân tích lưu lượng để xác định ai ở mỗi đầu lưu lượng. May mắn thay, hầu hết chúng ta không cần phải lo lắng về kẻ tấn công mạnh mẽ này.
{: .prompt-info }

> Thay đổi một vài `prefs` từ mặc định sẽ không khiến bạn "độc đáo hơn" - không có chuyện đó đâu. 
> : Đừng bối rối với những nghịch lý thông tin đơn giản, ví dụ như là Blink (engine web của Google) thay vì Gecko (engine của Firefox). 
{: .prompt-danger }

Chỉ Tor Browser mới có thể tự tin giải quyết các script theo dõi phức tạp (_nguyên văn:_ advance) với đầy đủ điều kiện cần thiết về `dữ liệu` và `nguồn lực`. Điều tốt nhất mà bất kỳ trình duyệt nào khác có thể tự tin làm là đánh lừa các script đơn giản (_nguyên văn:_ naive) bằng các giá trị ngẫu nhiên - nếu cảm thấy chưa đủ, hãy bổ sung các điểm dữ liệu lỏng lẻo từ IP/VPN của bạn. 

> Thực ra đoạn này rất khó hiểu, "naive script" không biết là để chỉ các script "ngây thơ", dễ lừa với các tham số giả hay là thuật toán Naive Bayes trong Khoa học dữ liệu để tính "xác suất xảy ra biến cố B khi có biến cố A". Hiểu thế nào cũng đc, thì thuật toán NaiveBayes cũng sẽ bị lừa nếu cho vào đấy 1 đống các giá trị ngẫu nhiên
{: .prompt-info }

> Arkenfox **không và không bao giờ tuyên bố có thể đánh bại tính năng theo dõi phức tạp** và không quan tâm liệu hai hoặc ba tham số `prefs` có lợi ích thực tế có thay đổi bất kỳ số liệu ổn định nào hay không, bởi vì **bản thân mỗi cá thể đã là duy nhất**. 
{: .prompt-warning }

Mục tiêu chính của Arkenfox luôn là bảo mật, quyền riêng tư và giảm thiểu các hình thức theo dõi thực tế và quan trọng như `state` (_tạm dịch:_ theo dõi nhận dạng) và `navigational` (_tạm dịch:_ theo dõi điều hướng), thay vì ưu tiên mối đe dọa tiềm ẩn của tập lệnh lấy dấu vân tay nâng cao phổ biến rộng rãi. 

> `Stateful tracking` sử dụng thông tin nhận dạng được lưu trữ trong máy tính cục bộ của người dùng, để nhận dạng duy nhất máy tính của khách truy cập trên internet.[^rfp-stf-tracking]
{: .prompt-info }

Ví dụ: Cookie HTTP lưu giữ các phiên đăng nhập và thông tin người dùng

> `Stateless tracking` không lưu trữ bất kỳ thông tin nhận dạng nào trên máy tính của người dùng. Sự kết hợp của các chữ ký duy nhất về mỗi máy tính được lưu trữ trong máy chủ theo dõi, có thể xác định máy tính với độ chính xác tương đối cao nhưng không chính xác bằng các phương pháp `stateful tracking`.[^rfp-stl-tracking].Stateless tracking cho phép các công ty theo dõi người dùng duyệt web, bất kể họ có muốn bị theo dõi hay không; và (phần đáng lo ngại) gần như không thể chặn hoặc tránh được nó. [^rfp-stl-tracking-2]
{: .prompt-info }

Ví dụ: Sử dụng các footprint/fingerprint của trình duyệt để đối ứng các tham số, từ đó định danh người dùng cụ thể.

> `Navigational tracking` đề cập đến việc sử dụng chung một hoặc nhiều điều hướng để xác định rằng người dùng trên một trang web là cùng một người với người dùng trên một trang web khác. Điều hướng truyền thông tin giữa các trang web theo một số cách khác nhau, bao gồm cả trong URL mục tiêu, có thể được trang trí và theo thời gian của yêu cầu.[^rfp-nav-tracking]
{: .prompt-info }

Ví dụ: Facebook thêm parameter `?fbcid=` link ngoài Facebook, ví dụ: _https://l.facebook.com/l.php?u=<span style="color:yellow">example.com</span>%2F%3F`fbclid`%3DIwAR00o17-6BL5g9TBd9F6k0hygx-wvY4PWQAAGEAxLC8EgIE8QHAinHqZ9AM&h=AT1A85IQOXJn9627-nYImCSwJt0MFetGcvuNFcP2LpHZOF0hleBEh24M62EnJf0_gXXMEIlr2hfEsmBRvJs-jJYf3AYzDIF1-8kEqoI-Q1WuVNionMkWGuO8k7OEjloxtdMR&__tn__=-UK-R&c[0]=AT0lohZkHEyEqJWkXcZYI8NMTs0wznpqergspOap68rJWPPUqNORq7t4vZMV4oYy5vUmkdRFHZpMVDX_zDGaKNAe_8dRBxHZjTMtGykj2alODDKtWMBQ8wx-D_Cj6OsSX6slgVWaucNjxfJzX-YwBXIcLvAA1Nm3m1W3wORDMGvAca9proYhMEtyX0y5dh7hU-bw6A1cj-ypeK0zDqY_ Khi người dùng click vào link thì phía server sẽ biết được là người đang truy cập `example.com` là cùng một người. Từ phía người dùng sẽ không biết mình bị theo dõi bí mật, hay nói cách khác là người dùng không biết và không đồng thuận với hành vi này.

Nhắc đến `động thuận` thì phải nhắc đến Term of Use (hay Term of SErvice - Điều khoản sử dụng). Phần lớn mọi người (**kể cả mình**) đều không bao giờ đọc cái này mà mặc định cứ đồng ý hết. Nhưng trong cái mớ dài dằng dặc đấy lại có cả cái phần cho phép tracking

Trích trong Chính sách quyền riêng tư của Whatsapp
: _Thông tin liên lạc về dịch vụ của chúng tôi và các công ty Meta:_ Chúng tôi sử dụng thông tin chúng tôi có để liên lạc với bạn về Dịch vụ của chúng tôi và cho bạn biết về các điều khoản, chính sách của chúng tôi và các cập nhật quan trọng khác. Chúng tôi có thể cung cấp cho bạn hoạt động tiếp thị về Dịch vụ của chúng tôi và của các Công ty Meta. 
: _Không có quảng cáo của bên thứ ba:_ Chúng tôi vẫn không cho phép quảng cáo biểu ngữ của bên thứ ba trên Dịch vụ của mình. Chúng tôi không có ý định giới thiệu chúng, nhưng nếu có, chúng tôi sẽ cập nhật Chính sách quyền riêng tư này.
: > Tóm lại là ừ thì tao sẽ chưa bán cho các bên dịch vụ quảng cáo khác mà chỉ dùng cho quảng cáo của bọn tao. Nhưng bọn tao thì cũng là công ty quảng cáo. À mà thêm nữa là tương lai có thể tao sẽ bán, lúc đấy tao sẽ viết lại điều khoản này thôi! **Và mày đã Đọc và ấn Đồng Ý rồi thì đừng ý kiến**


Điều đó nói lên rằng, `arkenfox` chống lại `stateless tracking`
: Vì vậy, nếu một tập lệnh lấy dấu vân tay chạy, nó sẽ cần phải phổ cập hoặc phổ biến (tức là nó sử dụng cùng một các thử nghiệm canvas, âm thanh và webgl trong số những thử nghiệm khác - hầu hết là không), được chia sẻ bởi một nhà môi giới dữ liệu (hầu hết là không), không vô tri (hầu hết là như vậy) và không chỉ là bên thứ nhất hoặc chỉ được sử dụng để phát hiện bot và ngăn chặn gian lận (hầu hết là như vậy).
: Nhưng điều đó không có nghĩa là việc lấy dấu vân tay không phải là mối đe dọa và sẽ không trở nên phổ biến và tinh vi hơn.

> Không liệt kê ảnh hưởng của RFP rõ ràng hơn đọc code của `arkenfox`
>
> Link: <https://github.com/arkenfox/user.js/blob/master/user.js>
{: .prompt-info }

``` javascript
/*** [SECTION 4500]: RFP (RESIST FINGERPRINTING)
   RFP covers a wide range of ongoing fingerprinting solutions.
   It is an all-or-nothing buy in: you cannot pick and choose what parts you want
   [TEST] https://arkenfox.github.io/TZP/tzp.html

   [WARNING] DO NOT USE extensions to alter RFP protected metrics

    418986 - limit window.screen & CSS media queries (FF41)
   1281949 - spoof screen orientation (FF50)
   1330890 - spoof timezone as UTC0 (FF55)
   1360039 - spoof navigator.hardwareConcurrency as 2 (FF55)
 FF56
   1369303 - spoof/disable performance API
   1333651 - spoof User Agent & Navigator API
      version: android version spoofed as ESR
      OS: JS spoofed as Windows 10, OS 10.15, Android 10, or Linux | HTTP Headers spoofed as Windows or Android
   1369319 - disable device sensor API
   1369357 - disable site specific zoom
   1337161 - hide gamepads from content
   1372072 - spoof network information API as "unknown" when dom.netinfo.enabled = true
   1333641 - reduce fingerprinting in WebSpeech API
 FF57
   1369309 - spoof media statistics
   1382499 - reduce screen co-ordinate fingerprinting in Touch API
   1217290 & 1409677 - enable some fingerprinting resistance for WebGL
   1382545 - reduce fingerprinting in Animation API
   1354633 - limit MediaError.message to a whitelist
 FF58+
   1372073 - spoof/block fingerprinting in MediaDevices API (FF59)
      Spoof: enumerate devices as one "Internal Camera" and one "Internal Microphone"
      Block: suppresses the ondevicechange event
   1039069 - warn when language prefs are not set to "en*" (also see 0210, 0211) (FF59)
   1222285 & 1433592 - spoof keyboard events and suppress keyboard modifier events (FF59)
      Spoofing mimics the content language of the document. Currently it only supports en-US.
      Modifier events suppressed are SHIFT and both ALT keys. Chrome is not affected.
   1337157 - disable WebGL debug renderer info (FF60)
   1459089 - disable OS locale in HTTP Accept-Language headers (ANDROID) (FF62)
   1479239 - return "no-preference" with prefers-reduced-motion (FF63)
   1363508 - spoof/suppress Pointer Events (FF64)
   1492766 - spoof pointerEvent.pointerid (FF65)
   1485266 - disable exposure of system colors to CSS or canvas (FF67)
   1494034 - return "light" with prefers-color-scheme (FF67)
   1564422 - spoof audioContext outputLatency (FF70)
   1595823 - return audioContext sampleRate as 44100 (FF72)
   1607316 - spoof pointer as coarse and hover as none (ANDROID) (FF74)
   1621433 - randomize canvas (previously FF58+ returned an all-white canvas) (FF78)
   1506364 - return "no-preference" with prefers-contrast (FF80)
   1653987 - limit font visibility to bundled and "Base Fonts" (Windows, Mac, some Linux) (FF80)
   1461454 - spoof smooth=true and powerEfficient=false for supported media in MediaCapabilities (FF82)
    531915 - use fdlibm's sin, cos and tan in jsmath (FF93, ESR91.1)
   1756280 - enforce navigator.pdfViewerEnabled as true and plugins/mimeTypes as hard-coded values (FF100)
   1692609 - reduce JS timing precision to 16.67ms (previously FF55+ was 100ms) (FF102)
   1422237 - return "srgb" with color-gamut (FF110)
   1794628 - return "none" with inverted-colors (FF114)
***/
user_pref("_user.js.parrot", "4500 syntax error: the parrot's popped 'is clogs");
/* 4501: enable privacy.resistFingerprinting
 * [SETUP-WEB] RFP can cause some website breakage: mainly canvas, use a canvas site exception via the urlbar
 * RFP also has a few side effects: mainly timezone is UTC0, and websites will prefer light theme
 * [NOTE] pbmode applies if true and the original pref is false
 * [1] https://bugzilla.mozilla.org/418986 ***/
user_pref("privacy.resistFingerprinting", true); // [FF41+]
   // user_pref("privacy.resistFingerprinting.pbmode", true); // [FF114+]
/* 4502: set new window size rounding max values [FF55+]
 * [SETUP-CHROME] sizes round down in hundreds: width to 200s and height to 100s, to fit your screen
 * [1] https://bugzilla.mozilla.org/1330882 ***/
user_pref("privacy.window.maxInnerWidth", 1600);
user_pref("privacy.window.maxInnerHeight", 900);
/* 4503: disable mozAddonManager Web API [FF57+]
 * [NOTE] To allow extensions to work on AMO, you also need 2662
 * [1] https://bugzilla.mozilla.org/buglist.cgi?bug_id=1384330,1406795,1415644,1453988 ***/
user_pref("privacy.resistFingerprinting.block_mozAddonManager", true); // [HIDDEN PREF FF57-108]
/* 4504: enable RFP letterboxing [FF67+]
 * Dynamically resizes the inner window by applying margins in stepped ranges [2]
 * If you use the dimension pref, then it will only apply those resolutions.
 * The format is "width1xheight1, width2xheight2, ..." (e.g. "800x600, 1000x1000")
 * [SETUP-WEB] This is independent of RFP (4501). If you're not using RFP, or you are but
 * dislike the margins, then flip this pref, keeping in mind that it is effectively fingerprintable
 * [WARNING] DO NOT USE: the dimension pref is only meant for testing
 * [1] https://bugzilla.mozilla.org/1407366
 * [2] https://hg.mozilla.org/mozilla-central/rev/6d2d7856e468#l2.32 ***/
user_pref("privacy.resistFingerprinting.letterboxing", true); // [HIDDEN PREF]
   // user_pref("privacy.resistFingerprinting.letterboxing.dimensions", ""); // [HIDDEN PREF]
/* 4505: experimental RFP [FF91+]
 * [WARNING] DO NOT USE unless testing, see [1] comment 12
 * [1] https://bugzilla.mozilla.org/1635603 ***/
   // user_pref("privacy.resistFingerprinting.exemptedDomains", "*.example.invalid");
/* 4510: disable using system colors
 * [SETTING] General>Language and Appearance>Fonts and Colors>Colors>Use system colors ***/
user_pref("browser.display.use_system_colors", false); // [DEFAULT: false NON-WINDOWS]
/* 4511: enforce non-native widget theme
 * Security: removes/reduces system API calls, e.g. win32k API [1]
 * Fingerprinting: provides a uniform look and feel across platforms [2]
 * [1] https://bugzilla.mozilla.org/1381938
 * [2] https://bugzilla.mozilla.org/1411425 ***/
user_pref("widget.non-native-theme.enabled", true); // [DEFAULT: true]
/* 4512: enforce links targeting new windows to open in a new tab instead
 * 1=most recent window or tab, 2=new window, 3=new tab
 * Stops malicious window sizes and some screen resolution leaks.
 * You can still right-click a link and open in a new window
 * [SETTING] General>Tabs>Open links in tabs instead of new windows
 * [TEST] https://arkenfox.github.io/TZP/tzp.html#screen
 * [1] https://gitlab.torproject.org/tpo/applications/tor-browser/-/issues/9881 ***/
user_pref("browser.link.open_newwindow", 3); // [DEFAULT: 3]
/* 4513: set all open window methods to abide by "browser.link.open_newwindow" (4512)
 * [1] https://searchfox.org/mozilla-central/source/dom/tests/browser/browser_test_new_window_from_content.js ***/
user_pref("browser.link.open_newwindow.restriction", 0);
/* 4520: disable WebGL (Web Graphics Library)
 * [SETUP-WEB] If you need it then override it. RFP still randomizes canvas for naive scripts ***/
user_pref("webgl.disabled", true);
```

> Vậy là RFP là thứ chắc chắn nên bật! Nhắc đến RFP vì RFP nó sẽ ưu tiên hiển thị website ở light theme `websites will prefer light theme`: màu sáng nền trắng dễ chói mắt. Mà trend bây giờ là phải dark theme cho nó ngầu với không mỏi mắt! _Dù rằng dark theme chỉ là khái niệm của mấy ông dev website mà ra_, chứ chả có ông bác sĩ nhãn khoa nào khuyến cáo là có lợi cho mắt hết :))
{: .prompt-info }

## Các tùy chọn dark theme trên Firefox

### Dark mode nửa mùa pha ke

Firefox có cái tính năng là set màu nền (`background`), màu chữ (`foreground`), màu link chưa vào (`anchor`) và đã vào (`visited`) ngay trong trình duyệt. Nên là chỉ cần set background màu tối, foreground màu sáng là đã được 1 cái dark theme cũng giống giống

Ưu điểm
: Nhanh, nhẹ - Vì tự Firefox làm hết, chỉ có Firefox mới biết chính xác nhất đâu là nền, đâu là chữ, đâu là link (ví dụ, `<a>` là link, nhưng có những lúc `<span>` cũng là link, `<ul>` cũng là link...)

Nhược điểm
: **Không chơi với `privacy.resistFingerprinting`:** Nếu đặt `true` thì sẽ không có tác dụng đổi màu
: Dễ nát cái website: vì website không phải chỉ có 1 lớp `background` mà nhiều lớp đè lên nhau, Firefox nó đổi hết về 1 màu toang luôn cái web
: Xấu

Tắt `privacy.resistFingerprinting` theo 1 trong 2 cách sau
: Cách 1: Vào `about:config`
: > Tìm `privacy.resistFingerprinting` và đặt giá trị `false`
: Cách 2: Thêm dòng trong file `<PROFILE_DIR>/user.js`

```javascript
// Resist Fingerprint (RFP)
user_pref("privacy.resistFingerprinting", true);
```
{: file="user.js"}


Cài `CanvasBlocker` (_Tùy chọn - Theo khuyến cáo của `arkenfox`_)
: Link: <https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/>

> Chọn 1 trong 3 cách set màu cho firefox
{: .prompt-info }

Set màu cho Firefox trong giao diện của Firefox
: > ![](https://voz.vn/attachments/1683797100190-png.1828267/)

(Hoặc) Thêm dòng trong file `<PROFILE_DIR>/user.js`
: Vào `about:support` click nút `Open Profile Dir`

```javascript
// Phake native Darkmode
user_pref("browser.display.use_system_colors", false );
user_pref("browser.display.background_color", "#000000" );
user_pref("browser.display.foreground_color", "#ffffff" );
user_pref("browser.visited_color", "#cc99ff" );
user_pref("browser.anchor_color", "#ffcc99" );
user_pref("browser.display.document_color_use", 2 );
```
{: file="user.js"}

(Hoặc) Sửa `about:config`
: Tìm tham số và đặt giá trị tương ứng

| browser.display.use_system_colors | false |
| browser.display.background_color | #000000 |
| browser.display.foreground_color | #ffffff |
| browser.visited_color | "#cc99ff |
| browser.anchor_color | #ffcc99 |
| browser.display.document_color_use" | 2 |

### Addon `Dark Background and Light Text` by Mikhail Khvoinitsky

> Link: <https://addons.mozilla.org/en-US/firefox/addon/dark-background-light-text/>
{: .prompt-info }

Ưu điểm:
: Không cần tắt `privacy.resistFingerprinting`
: Nhẹ (về cơ bản là nó chèn thêm CSS `!important`)

Nhược điểm
: Tốn thêm 1 addon (đồng nghĩa với tốn tài nguyên: ram, cpu...)
: Xấu (_như native pha-ke ở trên_)
: Dễ toang website (_như đồ pha-ke ở trên_)

### UserChromeCSS

> Link: _để sau_
{: .prompt-info }

Ưu điểm:
: Không cần tắt `privacy.resistFingerprinting`
: Nhẹ (về cơ bản là nó chèn thêm CSS `!important`)
: Nhẹ hơn addon `Dark Background and Light Text` ở trên, vì nó không tốn tài nguyên cho add-on
: Cho phép tùy biến nhiều hơn 2 cái trên (`<table>` 1 màu, `<ul>` 1 màu, `<span>` 1 màu...)

Nhược điểm
: Xấu (_như 2 cái ở trên_)
: Dễ toang website (_như 2 cái ở trên_)
: Dễ toang luôn cả Firefox (vì UserChromeCSS cũng dùng để mod giao diện Firefox)

Bật `userChrome.CSS` trong `about:config`:
: | toolkit.legacyUserProfileCustomizations.stylesheets | true |

( Hoặc Thêm dòng trong file `<PROFILE_DIR>/user.js`)
: Vào `about:support` click nút `Open Profile Dir`
```javascript
// Enable UserChrome CSS
user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);
```
{: file="user.js"}

Trong thư mục `<PROFILE_DIR>`
: Tạo thư mục con `chrome` (_nếu chưa có_)
: Mở thư mục `chrome`, tạo file `userContent.css` (_nếu chưa có_)

```css


:root {
    --bg-default: #333333;
    --fg-default: #cccccc;
    --fg-header: #ea9a97;

    --link-fg-default: #ffcc99;
    --link-fg-hover: #9ccfd8;
    --link-fg-visited: #cc99ff;

    --button-bg-default:  #2b2a33;
    --button-bg-hover:  #6b697f;
    --button-bg-action:  #6b697f;

    --border-default: #cccccc;
    --overlay-default: #23213680;
    --placeholder-default: #c4a7e780;
}

@-moz-document regexp("^http(s|):\/\/.*") {
    
    html,
    body {
        background-color: var(--bg-default) !important;
        color: var(--fg-default) !important;
        * {
            border-radius: 0px !important;
        }

        div:first-child:not(*),
        header,
        nav,
        article *:not(a, a *, button),
        div[class*='container'],
        div[class*='section'],
        div[class*='wrapper'],
        div[class*='Wrapper'],
        div[class*='page'],
        div[class*='nav'],
        div#top_nav,
        div#extabar,
        div#slim_appbar,
        div#kp-wp-tab-overview > div,
        [role="navigation"],
        a {
            background-color: var(--bg-default) !important;
            color: var(--fg-default) !important;
        }

        a {
            color: var(--link-fg-default) !important;
            background-image: none !important;
            &:hover {
                color: !important;
                text-decoration: underline !important;
            }
            &:active, &:focus {
                color: var(--link-fg-hover:) !important;
            }
            &:visited {
                color: var(--link-fg-visited) !important;
            }
        }

        input, textarea, button, [role="button"] {
            background-color: var(--button-bg-default)!important;
            * {
                background-color: var(--button-bg-default) !important;
            }
            &:hover {
                background-color: var(--button-bg-hover) !important;
                * {
                    background-color: var(--button-bg-hover) !important;
                }
            }
            &:active,
            &:focus {
                background-color: var(--button-bg-action) !important;
                * {
                    background-color: var(--button-bg-action) !important;
                }
            }
        }

        h1, h2, h3, h4, h5, h6, cite {
            color: var(--fg-header) !important;
        }

        :not([style*="border-color:"]),
        ::before,
        ::after {
            border-color: var(--border-default) !important;
        }

        div:empty,
        [class*="expand"],
        .sr-reader *,
        .sr-backdrop {
            background-color: transparent !important;
            
        }

        div[aria-hidden="true"]{
            background-color: transparent !important;
            background-image: none !important;
        }

        img {
            z-index: 2 !important;
            background-color: transparent !important;
        }
        input::placeholder,
        textarea::placeholder {
            color: var(--placeholder-default) !important;
        }
        input:not([style*="background-image:"]),
        textarea:not([style*="background-image:"]) {
            background-image: none !important;
        }
    }
}
```
{: file="<PROFILE_DIR>/chrome/userContent.css"}

### Addon `Dark Reader` by Alexander Shutau

> Link: <https://addons.mozilla.org/en-US/firefox/addon/darkreader/>
{: .prompt-info }

Ưu điểm:
: Không cần tắt `privacy.resistFingerprinting`
: Đơn giản, dễ dùng
: Đẹp hơn 3 cái ở trên
: Không sợ bị toang trang web

Nhược điểm
: Nặng hơn 3 cái ở trên

Dark Reader sử dụng rất nhiều CSS và JS để thay đổi màu sắc từng vùng trên trang web (thực sự là addon này phức tạp hơn rất nhiều người nghĩ là cứ cài vào nó biến trang web thành màu đen, nó còn phân tích màu sắc của font, các thẻ HTML lân cận để đưa ra quyết định có thay đổi màu sang đen hay không) khiến trang web phải render liên tục.

Nếu trang web nào nhìn không hợp lý thì chuyển qua chế độ khác như `Static` (mặc định là `Dynamic` nhìn đẹp trên đa phần trang web, `Static` hiệu năng tốt nhất, `Filter` và `Filter+` hiệu năng rất tệ, nên tránh nếu có thể), sau đó chọn `Only for ...` để nó áp vào đúng trang hiện tại:

### UserScript

Ở đây có 2 userscript làm được việc, cơ chế cũng hao hao nhau nên để chung

> Change Background Color (Author: lidada): <https://greasyfork.org/en/scripts/2054-change-background-color/code>
>
> Browser Background Color Controller (Author: mapplewizard): <https://greasyfork.org/en/scripts/447138-browser-background-color-controller>
{: .prompt-info }

Ưu điểm
: Không cần tắt `privacy.resistFingerprinting`
: Đẹp hơn `userContent.css` và addon `Dark Background and Light Text` (2 cái này thay hàng loạt style `!important`, còn script này nó chỉ thay style sau khi trình duyệt đã tính toán bằng hàm javascript `window.getComputedStyle()`)
: Nhẹ hơn mấy cái addon (thực ra là ăn gian vì vẫn phải có 1 cái addon để load script như là GreesyMonkey, TamperMonkey hay ViolentMonkey)

Nhược điểm
: Xấu hơn Dark Reader (dù sau vẫn chỉ là cơ chế thay màu đơn giản)
: Chậm hơn native pha-ke (phải chờ website render xong mới đổi được màu - **tức là lúc site đang load dở thì sẽ là màu trắng, load xong mới đen**)

Ở trên đầu script sẽ có đoạn

```JavaScript
var Gr1 = 240; //RGB中的R值...当网页的背景颜色的rgb值分别大于Gr1,Gg1,Gb1时此脚本将把颜色改成目标颜色color
var Gg1 = 240; //RGB中的G值
var Gb1 = 240; //RGB中的B值
var color = "#CDC9C9" //改变后的背景颜色,默认值为网上那个所谓的眼科专家说的对眼睛最好的颜色
```

Thì Gr1, Gg1, Gb1 là cái ngưỡng RGB của màu để được coi là màu sáng (ví dụ RGB(255, 255, 255) thì 255 > 240 nên sẽ là màu sáng), nếu màu sáng sẽ đổi hết về màu trong cái biến color thì đang là màu xám (#CDC9C9).

## Bonus - "Dark" Download manager

![](/assets/img/firefox-rfp-darktheme/dark-mdm.png)

Mở Options của Multithreaded Download Manager
: Vào tab `Interface` > `Custom CSS`
: _Chú ý để `background-color` giống với config trong Addon/CSS tương ứng đang dùng_

```css
body:not(section) {
	background-color: #FDF6E3;
}

.summary-row>button:active,
.summary-row>button:focus,
#toolbar>button:active,
#toolbar>button:focus {
	outline: none !important;
}

.progress-canvas {
	background-color: #D5D2C1;
	filter: brightness(1.1) contrast(0.9);
	border: 1px solid #A3A08F;
	border-radius: 3px;
}

.task {
	color: #2F2F2F;
	padding: 10px 8px;
	border-bottom: 2px solid #E3E4E6;
}

.task:hover {
	background-color: #EDEDED;
}

.summary-row {
	margin-bottom: 4px;
}

.summary-row>button {
	color: #525252;
	padding: 4px;
	margin-left: 2px;
	border-radius: 3px;
}

.summary-row>button:not([disabled]):hover {
	background-color: #4285F4;
}

#toolbar {
	background-color: #E3E4E6;
}

#toolbar>button {
	color: #525252;
	background-color: #E3E4E6;
}

button.task-action:hover {
	color: #FFFFFF;
}

button.task-action:last-child:hover {
	background-color: #EA4949;
	color: #FFFFFF;
}
```

## Nguồn:
[^rfp-1]: <https://github.com/arkenfox/user.js/wiki/3.3-Overrides-[To-RFP-or-Not]>
[^rfp-tracking-rate-research]: <https://www.ndss-symposium.org/ndss2017/ndss-2017-programme/cross-browser-fingerprinting-os-and-hardware-level-features/>
[^rfp-vpn-guide]: <https://educatedguesswork.org/posts/traffic-relaying/>
[^rfp-technical-wiki]: <https://wiki.mozilla.org/Security/Fingerprinting>
[^rfp-stl-tracking]: <https://www.igi-global.com/dictionary/crookies/82858>
[^rfp-stf-tracking]: <https://www.igi-global.com/dictionary/crookies/82857>
[^rfp-stl-tracking-2]: <https://www.booitjie.com/post/144704961797/what-is-stateless-tracking-and-why-should-i-care>
[^rfp-nav-tracking]: <https://privacycg.github.io/nav-tracking-mitigations/>