---
title: "[Firefox Awesome] Tối ưu Firefox (P3): OCSP, DNS và HTTP3"
date: 2023-10-03 21:45:00 +0700
categories: [awesome, firefox, optimize]
tags: [awesome, firefox, optimize]     ## TAG names should always be lowercase
---
> Có **02*- cách chính để thay đổi các tham số của Firefox:
> 1. Vào `about:config`, tìm và sửa tham số theo nhu cầu
> 2. Sửa file `user.js` (**khuyến khích*- để có thể theo dõi thay đổi và backup):
>       + Mở `about:support` => Open Profile Folder
>       + Đóng Firefox (tắt hẳn - _chú ý với MacOS: Close khác với Quit_)
>       + Tạo mới nếu chưa có
>       + Thêm dòng mới `user_pref("<tham số>", <giá trị mới>);`
>       + Save và mở Firefox
{: .prompt-info }

> `user.js` là file javascript nên có thể sử dụng `//` và `/**/` để viết ghi chú
{: .prompt-tip }

## Tắt OCSP để tăng tốc kết nối tới trang web[^fn-nth-6] (ngoài ra có thể mở CRlite thay thế, @Bin_kutakoto_99)

Do thám bằng [vài post về chủ đề tốc độ cho Firefox](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24223961)  xong thấy các bợn có vẻ cũng hứng thú với tăng tốc Firefox, vậy hôm nay tiếp tục chia sẻ một mẹo tăng tốc Firefox, đó là tắt OCSP.

Đầu tiên cần hiểu OCSP là gì, nó hoạt động ra sao thì Firefox cứ mỗi khi các bạn kết nối với một trang web, nó sẽ gửi cái chứng chỉ đến máy chủ OCSP (máy chủ xác thực trạng thái chứng chỉ) để kiểm tra độ tin cậy của chứng chỉ, xem nó đã hết hạn hay bị giả mạo hay không thì sẽ bị buộc thu hồi, đó gọi là OCSP.

Thế nhưng việc kết nối tới máy chủ để kiểm tra như vậy có nhiều nhược điểm:

- Thứ nhất là ảnh hưởng tới tốc độ kết nối tới trang web của Firefox, nhanh thì tốn nửa giây, chậm thì hơn, đứt cáp thì còn hơn nữa vì máy chủ đặt xa tít mù khơi
- Tự dưng đi khoe với một thằng ất ơ mình vào gần như tất cả mọi trang web, trừ HTTP ra, ảnh hưởng tới tính riêng tư
- Nếu máy chủ OCSP sập thì khỏi vào web
- Có thể dễ dàng bị hacker quay như chong chóng nếu nó khiến bạn không kết nối vào máy chủ OCSP được rồi chuyển hướng tới máy chủ của nó (MITM)

> Firefox bật OCSP mặc định, Chrome đã tắt OCSP đi từ rất lâu rồi.
{: .prompt-info }

Vậy với những nhược điểm bên trên mà ưu điểm chẳng thấy đâu tốt nhất là nên tắt, ngoài ra mình là chuột bạch kể từ ngày Firefox thêm OCSP vào từ 3.x 4.x nào đó đến nay mà chưa thấy bị hack bao giờ cả, vậy nên cứ mạnh dạn tắt thôi.

Cách thức:

- Vào `about:config`
- Tìm `security.OCSP.enabled`
- Chuyển thành `0`

```javascript
// Disable OSCP
user_pref("security.OCSP.enabled", 0);
```
{: file="user.js"}
Đó, chỉ đơn giản vậy thôi, một bài viết dài quan trọng để giải thích cách thức hoạt động của nó, ưu nhược của nó, như vậy sẽ hiểu sâu được nguyên nhân dẫn đến kết quả.

Triết lý tối ưu Firefox của mình là vậy, hiểu rõ, hiểu sâu nên một bài chỉ một mẹo duy nhất.

Sẽ còn nữa nhé, chủ đề sắp tới sẽ thú vị và độc, lạ hơn, có thể sẽ chưa bao giờ thấy mẹo tối ưu sắp tới. :D

### Mở CrLite thay thế [^fn-nth-7]

Tắt OCSP và mở CrLite. Nhanh hơn và bảo mật hơn

```javascript
// Enable CrLite
user_pref("security.remote_settings.crlite_filters.enabled", true);
user_pref("security.pki.crlite_mode", 2);
```
{: file="user.js"}


Link:
: <https://bugzilla.mozilla.org/buglist.cgi?bug_id=1429800,1670985,1753071>
: <https://blog.mozilla.org/security/tag/crlite/>

## Tối ưu DNS và (HTTP3+QUICv2 do bạn @Bin_kutakoto_99 chia sẻ) [^fn-nth-8]

Chậm cũng có thể do Microsoft trả về CDN ở tận trời Tây, nên sử dụng NextDNS/GoogleDNS (gửi ECS) để Tây nó trả về máy chủ gần Việt Nam, đặc biệt tránh dùng 1.1.1.1 cùi bắp vì nó trả về CDN tận Mỹ cuồng râm, cứ hiểu là 1.1.1.1 chỉ dành cho người Mỹ bản địa.

Vào thread NextDNS cài YogaDNS là dễ nhất, còn muốn mã mở dùng dnsproxy/dnscrypt.

Hoặc có thể đặt DNS Firefox thành NextDNS bằng cách `about:config`:

| network.trr.uri | <https://doh3.dns.nextdns.io/> |
| network.trr.custom_uri | <https://doh3.dns.nextdns.io/> |
| network.trr.mode | 2 |

```javascript
// Next DNS
user_pref("network.trr.uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.mode", 2);
```
{: file="user.js"}

> Nếu muốn dùng profile NextDNS của riêng, sửa thành `https://doh3.dns.nextdns.io/ID_NEXTDNS`, ví dụ `https://doh3.dns.nextdns.io/75a58e` nghĩa là ID_NEXTDNS không chặn quảng cáo, tracking của [thread NextDNS\](https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/), các bạn nên sử dụng ID này hoặc ID của riêng cá nhân với thiết lập tương đương để tăng tính ổn định cho Firefox bởi uBlock bao khoản chặn quảng cáo rồi, nếu dùng ID có chặn quảng cáo thì sẽ gây lỗi web hay bị phát hiện chặn quảng cáo bởi nhiều trang web khác, `nghĩa là các bạn chỉ dùng NextDNS để lấy ECS kiếm máy chủ gần Việt Nam nhất có thể cho Firefox - và để chặn các trang độc hại, lừa đảo`, cụ thể:
>
> | network.trr.uri | https://dns.nextdns.io/b7b3b7 |
> | network.trr.custom_uri | https://dns.nextdns.io/b7b3b7 |
> | network.trr.mode | 2 |
>
> ```javascript
> // Next DNS - ECS
> user_pref("network.trr.uri", "https://doh3.dns.nextdns.io/");
> user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io/");
> user_pref("network.trr.mode", 2);
> ```
> {: file="user.js"}
{: .prompt-info }


### Bật QUICv2

Cách thức
: <https://github.com/kelmenhorst/quic-censorship/blob/main/browsers.md>
: <https://datatracker.ietf.org/doc/draft-duke-httpbis-quic-version-alt-svc/>)

| network.http.http3.alt-svc-mapping-for-testing | doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1" |

```javascript
// Enable QUICv2
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1"');
```
{: file="user.js"}

### Tiện tay bật luôn ECH lên để hiệu lực Encrypted Client Hello tránh nhà mạng dòm ngó [^fn-nth-13]

> Chú ý ở thời điểm hiện tại ECH đang là bản nháp, khi bật lên mạng sẽ bị trễ đi một chút
{: .prompt-warning }


> Nếu dùng GoogleDNS:
> | network.trr.disable-ECS | false |
>
> Để ép Firefox gửi ECS cho trả về CDN gần.
> 
> | network.trr.uri | <https://dns.google/dns-query> |
> | network.trr.custom_uri | <https://dns.google/dns-query> |
> | network.trr.mode | 2 |
>
> ```javascript
> // GoogleDNS - ECS
> user_pref("network.trr.uri", "https://dns.google/dns-query");
> user_pref("network.trr.custom_uri", "https://dns.google/dns-query");
> user_pref("network.trr.mode", 2);
> ```
> {: file="user.js"}

> Hoặc nếu bạn không muốn dùng NextDNS+GoogleDNS thì có thể thử Cloudflare Zero Trust: [Hướng dẫn dùng Cloudflare Zero Trust\](https://voz.vn/t/huong-dan-dung-cloudflare-zero-trust.822971/)
{: .prompt-info }


### Sử dụng NextDNS hợp lý[^fn-nth-9]

Tiện đây mình cũng chia sẻ một thói quen tốt khi dùng NextDNS, đó là: **<span style="color:RED">Hai tay hai súng</span>**

Nghĩa là làm sao ?

Một tay (`profile`) không chặn quảng cáo mà chỉ chặn (chú ý đánh tích đúng):
: **Tên miền mới (cực quan trọng)**
: Mã độc
: Lừa đảo
: Bật ECS

> Sử dụng profile _chặn quảng cáo_ trên router/ncpa.cpl hay native Secure DNS của Android/iOS: Vậy là cả hộ gia đình sẽ được bảo vệ bởi việc chặn quảng cáo dù họ chả biết gì về công nghệ cả, giúp tránh những trường hợp ấn linh tinh vào virus hay vào web cá độ cược bay luôn sổ đỏ hay bị nhà tôi ba đời lừa đảo
{: .prompt-info }

Một tay (`profile`) chặn quảng cáo (dùng càng ít list càng tốt sẽ giảm nguy cơ bị phát hiện chặn quảng cáo):
: Tất cả những cái bên trên
: List ABPVN
: List mobile để xử lý quảng cáo trong ứng dụng Android/iOS

> Sử dụng profile _không chặn quảng cáo_ trong trình duyệt web: giống bài này vì thứ tư ưu tiên trình duyệt web luôn dùng DNS mình đặt trong trình duyệt và dùng kèm addon chặn quảng cáo như uBlock/Adguard
{: .prompt-info }

Như vậy trải nghiệm sẽ là tốt nhất, vì trình duyệt web sợ anti-adblock, cơ mà dùng kiểu này anti-adblock bị uBlock chém rồi nên NextDNS chỉ phải lo đảm bảo an toàn không gian mạng cho mình.

### Tool để kiểm tra traceroute hiển thị cả quốc gia[^fn-nth-10]

Dùng tool chuyên dụng chạy tracert, nếu thấy toàn Việt Nam là ngon: <https://www.nirsoft.net/utils/country_traceroute.html>

![https://www.nirsoft.net/utils/countrytraceroute.png](https://www.nirsoft.net/utils/countrytraceroute.png)

Cái hay của tool này là nó hiện quốc gia luôn, biết ngay mình bị cho du lịch sang đâu.

### Sự hữu ích khi dùng DNS có ECS[^fn-nth-11]

- Ping lần đầu vào DNS thì nó cache lại được, vì đây là ping lấy IP máy chủ, lần tiếp theo thì sẽ là 0ms
- Tuy nhiên khoảng thời gian trả dữ liệu lại từ máy chủ thì **thứ duy nhất làm giảm ping là máy chủ gần vị trí mình đang đặt đít, **và đó là lý do tại sao ECS cần thiết nên NextDNS và GoogleDNS+ECS/Quad9 (bản <https://dns11.quad9.net/dns-query>) tốt hơn
- Còn lý do tại sao nên dùng NextDNS đó là ECH nữa, hiện tại chỉ NextDNS và 1.1.1.1 hỗ trợ bản ghi TYPE65 giúp trình duyệt web lên được ECH, giúp vượt vũ môn vào Bonhup, Ếch Vít, Medium...
- Ngoài ra NextDNS hỗ trợ chặn web độc hại/lừa đảo (giúp người thân thoát dính họa sát thân vào trang các cược cược tung cái nhà, hay bị nhà tôi ba đời lừa mua thuốc trị bách bệnh...), web mới tạo (đa phần là virus) giúp giảm tối thiểu khả năng sẽ chết vì virus vì thường nếu nó chặn tên miền mới nó chặn luôn tên miền thằng hacker nó dùng để gửi thông tin mà spyware lấy được, chặn thì nó không lấy được gì

Vậy nên nếu không dùng NextDNS thì ít nhất cũng dùng GoogleDNS+ECS chứ tội gì dùng AdguardDNS. :D

Nói chung vấn đề Greencloud hay bị chập chờn chắc do đội của ông tay to @bedepver1 đang chỉnh chọt định tuyến, các bạn hỏi han tinh hình thì cứ hỏi, còn giải pháp:

- Dùng Anexia
- Dùng GoogleDNS+ECS

### Tối ưu HTTP3 [^fn-nth-12]

#### Tối ưu HTTP3:

| network.http.http3.send_background_tabs_deprioritization|true |
| network.http.http3.version_negotiation.enabled | true |
| security.tls.ech.grease_http3 | true |

```javascript
// Optimize HTTP3:
user_pref("network.http.http3.send_background_tabs_deprioritization", true );
user_pref("network.http.http3.version_negotiation.enabled", true );
user_pref("security.tls.ech.grease_http3", true );
```
{: file="user.js"}

#### Ép NextDNS chạy HTTP3 và QUICv2 bằng chỉnh altsvc:

| network.http.http3.alt-svc-mapping-for-testing | doh3.dns.nextdns.io;h3=":443"; quicv="6b3343cf,1" |

```javascript
// Force NextDNS on HTTP3 and QUICv2 by altsvc:
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io;h3=":443"; quicv="6b3343cf,1"' );
```
{: file="user.js"}

#### Trr:

| network.dns.skipTRR-when-parental-control-enabled | false |
| network.trr.async_connInfo | true |
| network.trr.confirmation_telemetry_enabled | false |
| network.trr.custom_uri | <https://doh3.dns.nextdns.io> |
| network.trr.disable-ECS | false |
| network.trr.mode | 3 |
| network.trr.uri | <https://doh3.dns.nextdns.io> |

```javascript
// Trr
user_pref("network.dns.skipTRR-when-parental-control-enabled", false );
user_pref("network.trr.async_connInfo", true );
user_pref("network.trr.confirmation_telemetry_enabled", false );
user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io" );
user_pref("network.trr.disable-ECS", false );
user_pref("network.trr.mode", 3 );
user_pref("network.trr.uri", "https://doh3.dns.nextdns.io" );
```
{: file="user.js"}

- Chỉnh không giới hạn dns cache queries:

| network.dnsCacheEntries | -1 |

```javascript
// Unlimited DNS queries
user_pref("network.dnsCacheEntries", -1 );
```
{: file="user.js"}


## Nguồn:
[^fn-nth-6]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-69#post-24344300>
[^fn-nth-7]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24344471>
[^fn-nth-8]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-85#post-24688026>
[^fn-nth-9]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-27558297>
[^fn-nth-10]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-25489531>
[^fn-nth-11]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-25454142>
[^fn-nth-12]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24688423>
[^fn-nth-13]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24916883>