---
title: "[Firefox Awesome] Part 2a: Các addon hay ho - uBlock Origin"
date: 2023-09-29 16:00:00 +0700
categories: [awesome, firefox, addon]
tags: [awesome, firefox, addon, ublock, ublock origin]     ## TAG names should always be lowercase
---
## [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin) (uBO)- Chặn quảng cáo, tăng cường bảo mật, riêng tư[^footnote]

Đây là addon chặn quảng cáo đạt tới mức độ chân - thiện - mỹ với thuật toán Regex được tối ưu cho tốc độ và thuật toán nhúng CSS để ẩn nội dụng được chau chuốt, đó là lý do tại sao addon này tốt hơn nhiều lần Adblock Plus với thuật toán tệ hơn cho hiệu năng tệ hơn, với người dùng Việt Nam thì tất nhiên **sau khi cài xong uBlock các bạn vào Dashboard rồi kéo xuống dưới tìm ABPVN** rồi bật lên để chặn quảng cáo Việt Nam hiệu quả.

Ngoài ra việc chặn quảng cáo sẽ giúp các bạn tránh khỏi những trường hợp dính virus (như đồng chí NFT_God dính virus mất sạch coin do search Google rồi ấn nhầm vào quảng cáo Google).

Cũng như tăng cường sự riêng tư vì các tracker bị chặn luôn, khiến các trang web không theo dõi được bạn.

### 1. Các bộ lọc đáng dùng không lỗi cho uBlock[^fn-nth-2]

Tiếp tục chủ đề về uBlock, addon #1 ở thread nên phải tiếp tục mở rộng công năng của nó, sau đây là những filter (bộ lọc) hay cho uBlock mà không gây lỗi web, bởi nó là bộ lọc tính năng hoặc chỉ dành cho một đối tượng nhất định nào đó:

- Chặn quảng cáo với Facebook (đối tượng): <https://raw.githubusercontent.com/ethan-xd/ethan-xd.github.io/master/fb.txt>
- Xem các trang đòi trả tiền không tốn xu nào với Bypass Paywall Clean (tính năng): <https://gitlab.com/magnolia1234/bypass-paywalls-clean-filters/-/raw/main/bpc-paywall-filter.txt>
- Nhảy link rút gọn, link theo dõi người dùng với LegitimateURLShortener (tính năng): <https://gitlab.com/DandelionSprout/adfilt/-/raw/master/LegitimateURLShortener.txt>
- Loại bỏ các trang web trùng lặp khỏi kết quả tìm kiếm Google, Duck, Bing... (đối tượng): <https://raw.githubusercontent.com/quenhus/uBlock-Origin-dev-filter/main/dist/all_search_engines/global.txt>

Cách thêm bộ lọc tham khảo bài này: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24961417>

Và không quên lưu ý, luật bất thành văn khi thêm bộ lọc vào uBlock là **luôn thêm bộ lọc `đối tượng` và `tính năng,` tránh xa bộ lọc `chặn`**.

> Bổ sung:
>- [ABPVN](https://abpvn.com/get): <https://abpvn.com/filter/abpvn-PeImlF.txt?ublock>
>- [FMSF2](https://nmtrung.com/fmsf-2/): <https://raw.githubusercontent.com/nmtrung/FMSF-2.0/master/fmsf_2.0.txt>
{: .prompt-info }

### 2. Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^fn-nth-3]

NextDNS có cái tính năng chặn tên miền mới (NRD) rất hay, tuy nhiên NextDNS thì cũng có giới hạn nếu xài miễn phí, vậy nên mình tìm hiểu xem có giải pháp thay thế nào không và kết quả là hóa ra uBlock cũng làm được tương tự.

Đây là một list chặn NRD rất hay vì đa phần các tên miền mới đều là lừa đảo, virus... Vậy nên chặn tụi nó đi giúp tránh được rất nhiều tai họa. Và list này là một list dạng tính năng, không khiến trang dùng anti-adblock để phát hiện và quấy rối người dùng như việc thêm một lô một lốc các list phục vụ mục đích chặn quảng cáo.

Vào `Settings` của `uBlock`, chọn `Custom` rồi copy thẳng vào nhé:

Chặn các tên miền mới tạo dưới 32 ngày: <https://nocdn.nrd-list.com/1/nrd-list-32-days.txt>
Chặn các tên miền mới tạo dưới 7 ngày: <https://nocdn.nrd-list.com/1/nrd-list-7-days.txt>

![](https://voz.vn/attachments/1682834413912-png.1807635/){: width="972" height="589" }
_Giao diện uBO_

Nguồn: <https://nrd-list.com/downloads/>
> List trên hỗ trợ cả `DNSCrypt` và `YogaDNS`, nếu các bạn dùng được DNSCrypt thật ra (chuẩn bài, hiệu năng) thì nên thêm vào DNSCrypt, còn YogaDNS thì mình không rõ vì nó phải trả phí mới cho chạy làm dịch vụ Windows
{: .prompt-info}

Cơ mà DNSCrypt thì các bạn hỏi @Bin_kutakoto_99 cho chính xác. Làm sao cho DNSCrypt nó tự động cập nhập list trên mới khó, vậy nên uBlock cũng ngon chán, mình cài vào thấy hiệu năng y xì như trước khi cài dù rằng list này chứa đến 3 triệu filter (tham khảo bài viết [Bóc phốt Adguard tốt hơn uBlock sẽ thấy uBlock hiệu năng tốt gấp 3x Adguard](https://github.com/gorhill/uBlock/wiki/Debunking-%22uBlock-Origin-is-less-efficient-than-Adguard%22-claims) {uBlock Origin (top): 4,662.3 ms (3,403.6 ms + 1,258.7 ms), Adguard (bottom): 14,424 ms (11,638.8 ms + 2,785.2 ms)}, mình sẽ có một bài chi tiết về vụ này sau tại vào thread ABPVN thấy mấy đồng chí bốc phét Adguard này Adguard nọ :D).

Chọn cái nào là tùy ý cơ mà chỉ nên chọn 1 trong 2, nói chung cứ 32 ngày mà táng, tên miền tầm 1 năm mới đáng tin, còn nếu nó chặn nhầm mấy trang hay đổi tên miền thì ngoại lệ tay lấy.

Mặc định **uBlock cứ 7 tiếng cập nhập filter một lần**[^fn-nth-4], thêm vào là xong chả cần làm gì thêm nữa.

### 3. Sử dụng uBlock thay thế NoScript/RequestPolicy để chặn script/ảnh/iframe bằng 2 cái nháy chuột[^fn-nth-5] và Cơ bản cách sử dụng Dynamic Filtering[^fn-nth-6]

Bạn có thể tiết kiệm một addon Noscript bằng cách dùng uBlock, bật Advanced features lên:
![](https://voz.vn/attachments/1684062491489-png.1834001/){: width="972" height="589" }


Ấn vào biểu tượng uBlock sau đó nháy vào More liên tọi, cứ thấy More là nháy nó sẽ hiện ra bảng điều khiển nội dung web, ấn vào một trong ba phần trên để chặn:

Script dạng chữ
Script từ chính trang web
Script từ bên thứ 3

Ngoài ra còn hỗ trợ chặn iframe, ảnh (chặn những trang thấy ảnh tải chậm, ví dụ những trang tiểu thuyết thì chặn ảnh, script, iframe đi cho nó max tốc độ tải trang)...

Rất dễ dùng một khi đã ép nó phải lòi cái bảng điều khiển ra, 2 chạm là xong.

![](https://voz.vn/attachments/1684061807548-png.1833979/){: width="972" height="589" }

Tiện đây mình làm một bài hướng dẫn chi tiết cách sử dụng tính năng gọi là `Dynamic Filtering` có thể dịch nôm na là `Lọc cơ động`, trước tiên nếu chưa biết qua tính năng này thì nên đọc bài:

> [Sử dụng uBlock thay thế NoScript/RequestPolicy để chặn script/ảnh/iframe bằng 2 cái nháy chuột](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25261196)[^fn-nth-5]

![](https://voz.vn/attachments/1685289976728-png.1862304/){: width="972" height="589" }

Nó chia ra hai cột chủ đạo:

- Cột bên tay trái: Tắt bật trên toàn bộ trang web (thường là không bao giờ dùng đến trừ khi bạn muốn bật chế độ khổ dâm)
- Cột bên tay phải: Tắt bật chỉ trên trang đang mở (cái này là cái cần quan tâm)

Ngoài ra khi ấn Ctrl 2 lần khi mở giao diện Lọc cơ động này thì nó sẽ chia ra 3 cột con bên trong:

- <span style="color:LIGHTGREEN">**Cột XANH LÁ**</span> Cho phép, nghĩa là khi chọn nó sẽ khiến các kết nối mà bình thường bị chặn sẽ được du di ngoại lệ
- <span style="color:GREY">**Cột GHI**</span> Không làm gì cả
- <span style="color:RED">**Cột ĐỎ:**</span> Chặn, nghĩa là khi chọn nó sẽ chặn kể cả kết nối đã được ngoại lệ trong bộ lọc rồi

#### Mục đích sử dụng:

Mục đích khi dùng là để nhanh chóng xử lý quảng cáo mà không muốn phải đợi bộ lọc cập nhập
Hoặc để ép trang web load nhanh hết mức có thể bằng cách chặn đi gần hết nội dung trang web không cần thiết

#### Thực tế:

- Ví dụ vào một trang web đọc tiểu thuyết, nghĩa là trang web toàn chữ thì nên chặn hết script, iframe, ảnh.. để trang web tải hết tốc độ
- Ví dụ những trang tin tức cũng toàn chữ và ảnh, có thể chặn iframe, script để trang web chỉ còn mỗi chữ và ảnh, ví dụ như VnExpress, DanTri...
- Ví dụ những trang web động, cái mà nó thể hiện rõ ràng nhất là khi tải trang, trang web nó hiện từng phần từng phần một thì không nên chặn script, vì những trang này khả năng lớn nó cần dùng script để hiển thị nội dung

> **Xem thêm**: <https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-quick-guide>
{: .prompt-info }

### 4. Sự khác biệt của `uBlock Firefox` vs `Chrome` vs `Manifest V3` vs `Adguard`[^fn-nth-7]

Tiện nhắc tới uBlock mình viết một bài phân tích sự khác biệt giữa:
- uBlock của Firefox và uBlock của Chrome
- uBlock Manifest V2 vs uBlock Manifest V3
- uBlock và Adguard

#### a. uBlock của Firefox và uBlock của Chrome
##### Hiệu năng:

- Biến code thành mã máy: uBlock của Firefox nhanh hơn rất nhiều lần uBlock của Chrome (cũng như Adguard), vì uBlock của Firefox hỗ trợ WebAssembly, nghĩa là khi lọc trang web, uBlock biến code từ Javascript thành mã máy, khiến tăng tốc quá trình lọc lên rất rất nhiều lần. Để nói về hiệu năng của Web Assembly so với Javascript thì nếu bạn học lập trình bạn sẽ thấy nó có ngôn ngữ thông dịch (interpreted language) và ngôn ngữ biên dịch (compiled language), sự khác biệt về hiệu năng giữa Web Assembly và Javascript như so sánh trời với đất, nó gấp rất rất nhiều lần, cũng y như so trình xem HTML của Firefox/Chrome (viết bằng HTML5=HTML+Javascript) với MPV (viết bằng C nguyên chất) vậy.
- Sử dụng IndexedDB thay vì localStorage: IndexedDB có hiệu năng tốt hơn nhiều localStorage nên khi mở Firefox lên, uBlock hoạt động ngay lập tức sau 0.5s (đối với con máy cùi bép của mình), nhưng với Chrome thì nếu bạn mở ngay trang web, khả năng lớn là quảng cáo sẽ lọt vì Chrome dùng localStorage chứa các bộ lọc của uBlock, nhiều người từng trải nghiệm uBlock trên Chrome tốn 15 phút để load xong các bộ lọc.

> Tham khảo: 
> - <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#browser-launch> 
> - <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#storage-compression>
{: .prompt-info }

> Chi tiết:
> - <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#webassembly>
{: .prompt-info }

##### Tính năng:

- uBlock của Firefox hỗ trợ bóc tách CNAME của tên miền, giúp tìm ra những tên miền con cùng là một bố mẹ đẻ ra rồi chặt luôn một thể, nên kết quả là uBlock nghiễm nhiên chặn nhiều quảng cáo hơn mà không tốn công sức: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#cname-uncloaking>
- uBlock của Firefox hỗ trợ lọc nội dung web, giúp thoải mái cắt xén trang web, chặn những quảng cáo mà bình thường không thể chặn được.

> Tham khảo: 
> - <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#html-filtering>
> - [Cách sửa mọi thứ trong trang web, phá tan nát trang web, chặn những quảng cáo gần như khó nhất với Header Editor](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25473236)

#### b. uBlock (Adblock) Manifest V2 vs uBlock (Adblock) Manifest V3 - Áp dụng cho mọi tiện ích chặn quảng cáo viết bằng Manifest V3

- AdBlock Manifest V3 sẽ không thể tự động cập nhập bộ lọc, trong khi thế giới web các trang web thay đổi cứ vài giây một lần, thêm sửa quảng cáo, không tự động cập nhập được nghĩa là thành phế
- AdBlock Manifest V3 sẽ không thể có nhiều hơn 30.000 rule (dòng chặn, chi tiết: [MV3: overcoming the 30000 rules limit](https://old.reddit.com/r/uBlockOrigin/comments/xlw1wi/mv3_overcoming_the_30000_rules_limit/)), trong khi số lượng trang web tăng không ngừng mỗi ngày, ngoài ra adblock còn được dùng để chặn các trang có nội dung malware nữa nên thậm chí để an toàn thì một người dùng cần dùng tới hàng triệu rule, ví dụ như chỉ để chặn các tên miền mới tạo ra trong vòng 31 ngày đã ngốn nguyên 3 triệu rule: Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^fn-nth-3]
- AdBlock Manifest V3 sẽ ngưng hoạt động sau khi trang tải xong một thời gian ([5 phút](https://old.reddit.com/r/learnjavascript/comments/10jmkc4/how_to_prevent_service_worker_from_going_inactive/)), nghĩa là sẽ vô dụng với các trang web động sử dụng AJAX như Youtube/Facebook vì một lúc sau khi tải xong sẽ không còn chặn quảng cáo nữa, khiến quảng cáo hiện ra

Còn đây là thông tin do chính `gorhill` cung cấp.[^fn-nth-7]: 

> uBO Lite:
> - Filter lists update only when the extension updates (no fetching up to date lists from servers)
> - Many filters are [dropped at conversion time](https://github.com/gorhill/uBlock/blob/master/dist/mv3/log.txt) due to MV3's limited filter syntax
> - No [crafting your own filters](https://github.com/gorhill/uBlock/wiki/Dashboard:-My-filters) (thus no [element picker](https://github.com/gorhill/uBlock/wiki/Element-picker))
> - No [strict-blocked](https://github.com/gorhill/uBlock/wiki/Strict-blocking) pages
> - No [per-site switches
> - No [dynamic filtering
> - No importing external lists

#### c. uBlock và Adguard
Gần như giống nhau, thích dùng gì thì dùng, nhưng uBlock hơn ở hiệu năng do sử dụng Web Assembly (chỉ Firefox), đã được xác nhận đóng dấu trên trang liệt kê các ứng dụng sử dụng Web Assembly (WASM) trên kèm benchmark hiệu năng: <https://madewithwebassembly.com/showcase/ublock-origin/>

> uBlock Origin is a very popular add-on, and uses WebAssembly for multiple parts of it's codebase. The most notable being, uBlock Origin uses Wasm for hostname lookup for it's data structures that contain the list of origins it intends to block. This is a great use of WebAssembly, as it offered them better performance, compared to a JavaScript implementation, in the web browser for doing computationally intensive processing tasks over a large set of data. This can be tested in your own browser, by checking out the benchmark.

uBlock hỗ trợ HTML Filtering (chỉ Firefox), một tính năng giúp lọc và xóa triệt để nội dung web, giúp trị những quảng cáo khó nhằn nhất cũng như xóa triệt để nội dung web thì sẽ loại bỏ được kết nối ngầm, từ đó tối đa tốc độ tải trang:

> [Chặn quảng cáo kiểu triệt hạ với uBlock sử dụng tính năng HTML Filtering](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27879329) (chỉ hỗ trợ uBlock cho Firefox) (Ví dụ: [Xóa triệt thanh sidebar ở trang chủ Voz khiến trang load nhanh như điện](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27879524))
{: .prompt-tip }

Nhìn kỹ số lượng kết nối ở 2 cái spoiler.

![](https://voz.vn/attachments/1695314107674-png.2085528/)
_Ẩn_
VS
![](https://voz.vn/attachments/1695314749241-png.2085538/)
_Xóa_

Ngoài ra mã nguồn Scriptlets của uBlock nuột hơn Adguard do Adguard dùng Webpack, là kiểu đóng gói code Javascript nhưng hiệu năng luôn kém hơn uBlock là native Javascript, và mặc định cả Adguard và uBlock đều sử dụng Scriptlets để trị quảng cáo khó nhằn như Youtube, Twitch...

Vậy chốt lại là uBlock trên Firefox hơn Adguard ở những điểm:

> - Biến mã thông dịch Javascript thành mã máy WebAssembly, tăng tốc độ lọc
> - Lọc và xóa triệt để nội dung web ở cấp độ mã nguồn, nghĩa là trước khi nó xuất hiện trên màn hình
> - Lọc CNAME một cách tự động, không cần phụ thuộc vào một bộ lọc thủ công nào cả

Nghĩa là nếu dùng **Firefox thì uBlock có nhiều tính năng hơn**, còn dòng Chrome thì cả hai như nhau như đã nói bên trên, thích dùng gì thì dùng.

### Góc drama - Nano Defenders: The shit hits the fan
<https://www.reddit.com/r/HobbyDrama/comments/jo9wxn/open_source_development_the_fall_of_nano_defender/>

## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24996350>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24961417>
[^fn-nth-4]: <https://github.com/gorhill/uBlock/wiki/Advanced-settings#autoupdateperiod>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25261196>
[^fn-nth-6]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25582594>
[^fn-nth-7]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25474057> 
[^fn-nth-8]: <https://old.reddit.com/r/uBlockOrigin/comments/1067als/eli5_ublock_lite_vs_ublock_origin/j3h00xj/>
