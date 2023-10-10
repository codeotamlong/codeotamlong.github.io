---
title: "[Firefox Awesome] Các add-on hay ho"
date: 2023-09-30 11:33:00 +0700
categories: [firefox, awesome]
tags: [firefox, awesome]
---
> Linh vật của công ty là một khủng long (`Mozilla`), biểu tượng thì là một con cáo (`fire fox`), nhưng thực chất lại là gấu trúc (`red panda`), và sử dụng engine là một con tác kè (`gecko`)
{: .prompt-info }

## [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin) (uBO) - Chặn quảng cáo, tăng cường bảo mật, riêng tư[^ff-addon-voz]

Đây là add-on chặn quảng cáo đạt tới mức độ chân - thiện - mỹ với thuật toán Regex được tối ưu cho tốc độ và thuật toán nhúng CSS để ẩn nội dụng được chau chuốt, đó là lý do tại sao add-on này tốt hơn nhiều lần Adblock Plus với thuật toán tệ hơn cho hiệu năng tệ hơn.

> Với người dùng Việt Nam thì tất nhiên sau khi cài xong uBlock các bạn vào Dashboard rồi kéo xuống dưới tìm ABPVN rồi bật lên để chặn quảng cáo Việt Nam hiệu quả.
{: .prompt-tip }

Ngoài ra việc chặn quảng cáo sẽ giúp các bạn tránh khỏi những trường hợp dính virus (như đồng chí NFT_God dính virus mất sạch coin do search Google rồi ấn nhầm vào quảng cáo Google).

Cũng như tăng cường sự riêng tư vì các tracker bị chặn luôn, khiến các trang web không theo dõi được bạn.

### Các bộ lọc đáng dùng không lỗi cho uBlock[^ff-ubo-2][^ff-ubo-8]

| Tính năng | Phân loại | Link |
|:-|-|-|
| Chặn quảng cáo Facebook | đối tượng | <https://raw.githubusercontent.com/ethan-xd/ethan-xd.github.io/master/fb.txt> |
| Bypass Paywall Clean | tính năng | <https://gitlab.com/magnolia1234/bypass-paywalls-clean-filters/-/raw/main/bpc-paywall-filter.txt> |
| LegitimateURLShortener | tính năng | <https://gitlab.com/DandelionSprout/adfilt/-/raw/master/LegitimateURLShortener.txt> |
| Bỏ kết quả trùng lặp<br>trên Google, Duck, Bing... | đối tượng | <https://raw.githubusercontent.com/quenhus/uBlock-Origin-dev-filter/main/dist/all_search_engines/global.txt> |
| PrivacyEnhanced<br>_(@Fioren giới thiệu)_ | chặn | <https://github.com/stephenhawk8054/PrivacyExtended> |
| Ẩn hộp thoại bắt đăng nhập | tính năng | <https://github.com/DandelionSprout/adfilt/blob/master/BrowseWebsitesWithoutLoggingIn.txt> |
| Anti-Paywall Cleaner | tính năng | <https://github.com/liamengland1/miscfilters/blob/master/antipaywall.txt> |
| Ẩn elements khó chịu/thừa<br>_(của tác giả Betterfox)_ | tính năng | <https://github.com/yokoffing/filterlists/blob/main/annoyance_list.txt> |

> Bổ sung:
> : [ABPVN](https://abpvn.com/get): <https://abpvn.com/filter/abpvn-PeImlF.txt?ublock>
> : [FMSF2](https://nmtrung.com/fmsf-2/): <https://raw.githubusercontent.com/nmtrung/FMSF-2.0/master/fmsf_2.0.txt>
{: .prompt-info }



### Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^ff-ubo-3]

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

Mặc định uBlock cứ 7 tiếng cập nhập filter một lần[^ff-ubo-4], thêm vào là xong chả cần làm gì thêm nữa.

### Sử dụng uBlock thay thế NoScript/RequestPolicy để chặn script/ảnh/iframe bằng 2 cái nháy chuột[^ff-ubo-5] và Cơ bản cách sử dụng Dynamic Filtering[^ff-ubo-6]

Bạn có thể tiết kiệm một add-on Noscript bằng cách dùng uBlock, bật Advanced features lên:
![](https://voz.vn/attachments/1684062491489-png.1834001/)

Ấn vào biểu tượng uBlock sau đó nháy vào More liên tọi, cứ thấy More là nháy nó sẽ hiện ra bảng điều khiển nội dung web, ấn vào một trong ba phần trên để chặn:

- Script dạng chữ
- Script từ chính trang web
- Script từ bên thứ 3

Ngoài ra còn hỗ trợ chặn iframe, ảnh (chặn những trang thấy ảnh tải chậm, ví dụ những trang tiểu thuyết thì chặn ảnh, script, iframe đi cho nó max tốc độ tải trang)...

Rất dễ dùng một khi đã ép nó phải lòi cái bảng điều khiển ra, 2 chạm là xong.

![](https://voz.vn/attachments/1684061807548-png.1833979/)

Tiện đây mình làm một bài hướng dẫn chi tiết cách sử dụng tính năng gọi là `Dynamic Filtering` có thể dịch nôm na là `Lọc cơ động`:

![](https://voz.vn/attachments/1685289976728-png.1862304/){: width="972" height="589" }

Nó chia ra hai cột chủ đạo:

- Cột bên tay trái: Tắt bật trên toàn bộ trang web (thường là không bao giờ dùng đến trừ khi bạn muốn bật chế độ khổ dâm)
- Cột bên tay phải: Tắt bật chỉ trên trang đang mở (cái này là cái cần quan tâm)

Ngoài ra khi ấn Ctrl 2 lần khi mở giao diện Lọc cơ động này thì nó sẽ chia ra 3 cột con bên trong:

- <span style="color:LIGHTGREEN">**Cột XANH LÁ**</span>: Cho phép, khiến các kết nối mà bình thường bị chặn sẽ được du di ngoại lệ
- <span style="color:GREY">**Cột GHI**</span> Không làm gì cả
- <span style="color:RED">**Cột ĐỎ:**</span> Chặn, kể cả kết nối đã được ngoại lệ trong bộ lọc rồi

Mục đích sử dụng:
: Nhanh chóng xử lý quảng cáo mà không muốn phải đợi bộ lọc cập nhập
: Ép trang web load nhanh hết mức có thể bằng cách chặn đi gần hết nội dung trang web không cần thiết

Thực tế:
: Ví dụ vào một trang web đọc tiểu thuyết, nghĩa là trang web toàn chữ thì nên chặn hết script, iframe, ảnh.. để trang web tải hết tốc độ
: Ví dụ những trang tin tức cũng toàn chữ và ảnh, có thể chặn iframe, script để trang web chỉ còn mỗi chữ và ảnh, ví dụ như VnExpress, DanTri...
: Ví dụ những trang web động, cái mà nó thể hiện rõ ràng nhất là khi tải trang, trang web nó hiện từng phần từng phần một thì không nên chặn script, vì những trang này khả năng lớn nó cần dùng script để hiển thị nội dung

> Xem thêm: <https://github.com/gorhill/uBlock/wiki/Dynamic-filtering:-quick-guide>
{: .prompt-info }
## Góc drama - Nano Defenders: The shit hits the fan[^ff-ubo-7] _Tạm dịch_

> _TL;DR_:  Trình chặn quảng cáo (_ad-blocker_) nguồn mở được bán cho “các dev Thổ Nhĩ Kỳ” gần như ngay lập tức bị biến thành phần mềm độc hại và giành được quyền truy cập vào tài khoản Instagram của mọi người. dev cho rằng đây nên là một “bài học kinh nghiệm”, nhưng không nghĩ họ đã làm sai quá sai.
>
> Chi tiết: <https://www.reddit.com/r/HobbyDrama/comments/jo9wxn/open_source_development_the_fall_of_nano_defender/>
{: .prompt-info }

Tôi không chắc liệu phát triển nguồn mở có được coi là một sở thích hay không, nhưng này, mọi người làm việc đó vào thời gian rảnh rỗi, vì vậy...

### Giới thiệu

`Nano Adblock` và `Nano Defender` là các ad-blocker nguồn mở. Có thể đây là các add-on không quá phổ biến (với tổng cộng khoảng hơn 250 nghìn người dùng trên Chrome Web Store), nhưng phần lớn người dùng đã nghe nói về dự án gốc: **uBlock Origin**. Mặc dù các dự án `Nano` có phiên bản trên các trình duyệt khác nhau (như Chrome, Firefox và Edge...) nhưng nội dung này sẽ tập trung vào Chrome.

Các dự án nguồn mở, cho những người chưa biết, là các dự án được cung cấp miễn phí cho cộng đồng sửa đổi và phân phối: Có thể tạo ra ad-blocker mới từ mã nguồn uBlock Origin hoặc `Nano`, trong khi không thể lấy mã nguồn của Microsoft Word và sử dụng nó để tạo ra một trình soạn thảo văn bản mới. Trong khi các công ty lớn có thư viện nguồn mở, rất nhiều công việc được thực hiện bởi các nhóm hoặc cá nhân nhỏ, đó là trường hợp của `Nano`.

Do tính chất nguồn mở của dự án, hầu hết những người duy trì nó đều làm việc với nó trong thời gian rảnh rỗi và miễn phí. Đây là khối lượng công việc khổng lồ và có thể gây căng thẳng cho ai đó. Điều đó dẫn tôi đến...

### Nhà sáng lập bỏ đi

Vào ngày 3 tháng 10, người tạo ra các dự án Nano (@jspenguin2017, gọi tắt là JS) thông báo trên [GitHub](https://github.com/NanoAdblocker/NanoCore/issues/362) rằng vì lý do mất nhiều thời gian để bảo trì dự án nên họ sẽ chuyển nó cho chủ sở hữu mới. Trong thế giới nguồn mở, điều này là bình thường. Duy trì miễn phí phần mềm cấp doanh nghiệp thực sự vất vả và rắc rối. Mọi người đều (muốn) có cuộc sống riêng. Nó vốn là như thế.

Những gì đã không bình thường là sự mơ hồ trong các phát ngôn. Hãy xem, với tư cách là một ad-blocker, các dự án Nano có khả năng truy cập sâu vào những gì bạn nhìn thấy và thao tác trực tuyến. Điều quan trọng là phải biết ai sẽ có quyền truy cập vào dữ liệu đó (_trừ khi bạn là một công ty công nghệ lớn, rõ ràng là vậy, nhưng điều đó dành cho cuộc thảo luận vào một ngày khác_).

Đáng chú ý, một số thông tin quan trọng bị thiếu:
: Thông báo không thực sự nói Ai đã mua lại các dự án.
: Trên thực tế, thông báo dường như không cho biết có bao nhiêu người sẽ tham gia vào đội mới.
: Thông báo không đề cập đến việc liệu đây có phải là một đợt mua bán hay các bên quan tâm có phải là thành viên của cộng đồng hiện tại hay không.

Vậy rõ ràng là chuyện này sẽ diễn ra quá tốt đẹp.

### Mọi chuyện không suôn sẻ

Cộng đồng không hài lòng với thông báo này. Không hề.

JS khiến mọi thứ trở nên tồi tệ hơn khi đơn thuần giới thiệu nhóm phát triển mới là “nhóm gồm các dev Thổ Nhĩ Kỳ”, trong khi không muốn tiết lộ thêm thông tin. Sau đó, họ thông báo với cộng đồng rằng họ sẽ “giải quyết các bình luận của [cộng đồng] khi có nhiều thời gian hơn”. Nhưng cuộc thảo luận không mấy tốt đẹp. (_Nguyên văn: "Not great optics". "optic": quang học, "topic": chủ đề thảo luận - chắc tác giả gõ nhầm_)

[Ai đó tìm thấy tên của dev mới](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-704014156): Đây không phải là doxxing (_tiếng lóng: được hiểu là các hành động tìm kiếm, thu thập và công khai thông tin cá nhân của một người trên internet mà không được sự cho phép của người đó._), những người này theo nghĩa đen là không tồn tại. Điều đó không tốt chút nào.

Tại thời điểm này, dev uBlock Origin (dự án gốc của Nano), Raymond Hill, đã vào cuộc. với một [nhận xét mang tính tiên đoán](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-704278531).

> "Hai dev"[1] không có hồ sơ theo dõi về việc từng đóng góp cho dự án hiện tại hoặc bất kỳ dự án liên quan nào ít nhất thể hiện bất kỳ mối quan tâm nào đến việc chặn nội dung hoặc quyền riêng tư hoặc thậm chí các chủ đề liên quan lỏng lẻo và không có sự hiện diện rõ ràng trên internet cho đến ngày nay , đã trả một số tiền không được tiết lộ để đổi lấy cơ sở người dùng và quyền kiểm soát kho GitHub. 
> 
> Tính đến thời điểm hiện tại, cơ sở người dùng đã được chuyển giao (theo danh sách cửa hàng Chrome) và rất có thể phần lớn những người dùng đó sẽ không biết rằng các tiện ích mở rộng đã cài đặt của họ không còn được duy trì bởi người mà họ tin tưởng ban đầu nữa, ít nhất là ngầm hiểu, khi họ cài đặt những tiện ích mở rộng đó. Các liên kết đến chính sách bảo mật đã bị xóa khỏi danh sách cửa hàng Chrome (tại đây và tại đây). 
>
> Không cần phải nói rằng mục tiêu của "hai dev" này là kiếm tiền từ hai tiện ích mở rộng. "Hai dev" đó có thể sẽ tiếp tục nhập tất cả công việc từ thượng nguồn, tức là uBO, là kết quả của những tình nguyện viên lâu năm đầu tư thời gian và công sức rảnh rỗi của mình ngày này qua ngày khác trong nhiều năm, điều này cũng góp phần biến Nano AdBlocker trở thành thứ nó là. 
>
> [1] Sử dụng dấu ngoặc kép vì không ai biết rằng thực sự có hai dev thực sự vì cho đến nay vẫn chưa có gì có thể xác minh được.

JS trả lời ông Hill về cơ bản là “Chà, đây là một trải nghiệm đáng học hỏi”. Có lẽ đó không phải là thái độ cần có khi bạn nắm giữ hơn 250 nghìn dữ liệu của người dùng.

Ngoài ra, rõ ràng là ngay cả những thành viên cộng đồng có địa vị cao hơn cũng không được thông báo. Người phụ trách phần mở rộng Firefox của dự án Nano @LiCybora [không biết chuyện gì đang xảy ra](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-703614519). Bạn sẽ nghĩ rằng bạn muốn gợi ý cho họ về điều đó.

> Với tư cách là maintainer bản port Firefox, tôi muốn biết liệu "các dev Thổ Nhĩ Kỳ" cũng sẽ tiếp quản bản port trên Firefox hay chỉ phần Chrome(ium)/Edge. Tôi trung lập với quyết định này, nhưng nếu dev upstream bị thay đổi, tôi cần suy nghĩ xem liệu mình có nên tách khỏi upstream và đổi tên dự án, ~~maintain cho các dev mới~~ hay chỉ từ bỏ port Firefox. Không chắc tôi sẽ tiếp tục maintain cho các dev mới mà không biết lập trường của họ. 
>
> Động lực ban đầu của tôi khi maintain dự án này là tôi nhận thấy đây là một dự án hữu ích và không muốn nó chết trên Firefox (tác giả gốc trước đây và một số maintainer khác vẫn duy trì trên Firefox một thời gian). Tôi cố gắng hết sức để biến mình từ user bình thường thành maintainẻ. Tôi vẫn còn quá xa để có thể đủ điều kiện làm dev. Nhưng trong trường hợp tôi vẫn cần dự án này và các dev mới không tiếp quản port (hoặc trong trường hợp tôi không thích quan điểm của họ), tôi sẽ cố gắng hết sức để tự mình phát triển ~~(hoặc duy trì cho chúng nếu tôi đồng ý với các dev mới)~~.
>
> Tuy nhiên, vì uBO có syntax-highlighter và Firefox Mobile mới không hỗ trợ các tiện ích bổ sung bên ngoài danh sách Recommended Extension, tôi thậm chí còn bối rối rằng liệu Nano Adblocker có còn cần thiết trên Firefox hay không nếu không có report issue (hoặc những nghi vấn rằng mọi người đang lo ngại). ~~Tốt nhất thì các dev mới đều giỏi (có thể giỏi hơn tôi) và họ sẽ duy trì các cổng trên Firefox tốt hơn trước.~~ Tệ nhất là tôi sẽ từ từ tự phát triển hoặc chỉ sử dụng uBO và từ bỏ nó. 
>
> Cập nhật: Tôi từ chối port cho dự án này nữa.

### Vãi cả c*t (Nguyên văn: "Sh-t Hits the Fan")

> Nguyên văn tiêu đề: "Sh*t Hits the Fan", là thành ngữ miêu tả, một cách rất rất thô thiển, về một tình huống bất ngờ mà gây rắc rối cho nhiều người, giống như khi có 1 bãi c.t bay vào cánh quạt. `Fan` vừa có nghĩa là `quạt`, vừa là `người hâm mộ`. Một cục c.t bay thẳng về phía người dùng.
{: .prompt-info }

Kể cả trong trường hợp tốt nhất, các phát ngôn của JS đều rất tệ. Mọi người đang tức giận. JS đang cố gắng thuyết phục mọi người rằng đây là [“vì lợi ích tốt nhất của người dùng”](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-706731325), mặc dù cộng đồng đang cảm thấy không tốt. Một dev khác chỉ ra rằng [JS bị chỉ trích thậm tệ khi rút lui khỏi một dự án tương tự](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-706676653).

Nhưng nếu đúng như vậy thì đó sẽ chỉ là một vụ lộn xộn khác của GitHub. Cộng đồng nguồn mở giống như một phiên bản chuyên nghiệp hơn của máy chủ discord, mọi người đều biết thế.

Như đã nói, phần này có tiêu đề “Shit Hits the Fan”.

Đầu tiên, mặc dù JS cố gắng né tránh nhưng rõ ràng là họ đã bán các dự án Nano. Họ cũng thừa nhận không biết họ đã bán nó cho ai, nhưng họ biết rằng các dev mới có kế hoạch kiếm tiền từ nó. Điều này hơi mờ ám vì họ đang kiếm tiền từ công việc của các tình nguyện viên, bao gồm cả các tình nguyện viên của uBlock Origin, những người không biết gì về thỏa thuận này.

Thứ hai, mọi người tức giận về việc một nhóm người chưa xác định đang xử lý dữ liệu nhạy cảm. Mọi người gọi các dự án Nano là phần mở rộng về “bảo mật và quyền riêng tư”. JS về cơ bản [bỏ đi, từ chối tiếp tục phản hồi](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-707435432). Nói rằng cơn thịnh nộ bỏ đi không kéo dài.

Thứ ba, người ta phát hiện ra rằng trang web mới dành cho các dự án được kết hợp với nhau một cách kém chất lượng và các trang cửa hàng mới trên Chrome App Store không có chính sách bảo mật. Chính sách quyền riêng tư cuối cùng đã được thêm vào, nhưng nó chỉ là [một mẫu ngẫu nhiên](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-707747710).

Thứ tư, mặc dù JS cho biết các dev mới sẽ tham gia cuộc trò chuyện nhưng họ chưa bao giờ làm vậy. Tôi đã kiểm tra tất cả các chủ đề và đến hôm nay vẫn chưa có. Tài khoản GitHub được cho là của họ không còn tồn tại nữa, vì vậy có điều đó.

Tại thời điểm này, mọi người đang hoảng sợ, bởi vì rõ ràng, điều này rất mờ ám. Và đây là một ứng dụng, nếu rơi vào tay kẻ xấu,  có thể đọc mật khẩu của bạn Và kiểm soát trình duyệt của bạn, Trong số những thứ khác.

### Ôi! Tất cả phần mềm độc hại

Ba ngày sau bài đăng gốc, tiện ích mở rộng Nano Chrome cập nhật lần đầu tiên kể từ khi chuyển. Giống như hầu hết các bản cập nhật phần mềm, một số code mới được thêm vào.

Thật không may, code mới đó đang gửi dữ liệu người dùng đến nguồn của bên thứ ba. Thế là đủ để được coi là phần mềm độc hại.

[Đây là chi tiết kỹ thuật về điều đó.](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-709428210)

> The extension is now designed to lookup specific information from your outgoing network requests according to an externally configurable heuristics and send it to https://def.dev-nano.com/.
{: .prompt-info }

Người ta buộc tội JS [“đặt người dùng vào tình thế nguy hiểm để kiếm tiền nhanh chóng”](https://github.com/NanoAdblocker/NanoCore/issues/362#issuecomment-709666762). JS bác bỏ điều này bởi vì họ [“không tìm thấy điều gì xấu cả”](https://github.com/jspenguin2017/Snippets/issues/2#issuecomment-709715355).

Bởi vì _hoàn toàn không có sự hiện diện trực tuyến_ rõ ràng không phải là một dấu hiệu nguy hiểm.

### Hậu quả

Với số lượng người bị ảnh hưởng, [một số](https://www.ghacks.net/2020/10/16/time-to-remove-nano-adblocker-and-defender-from-your-browsers-except-firefox/) [bài báo](https://arstechnica.com/information-technology/2020/10/popular-chromium-ad-blockers-caught-stealing-user-data-and-accessing-accounts/) được xuất bản. JS kiên quyết rằng đây là tất cả [“điều gì đó chúng ta nên học hỏi"](https://github.com/jspenguin2017/Snippets/issues/2#issue-722783061).

Ars Technica xác nhận rằng tiện ích mở rộng hiện có khả năng truy cập tài khoản Instagram của người dùng bị ảnh hưởng và tự động thích các bài đăng trên Instagram. Nhiều tài khoản khác có thể đã bị ảnh hưởng, nhưng điều này chưa được xác nhận.

Người ta cố gắng giải thích tại sao cách JS xử lý việc này lại không tốt). [JS không đồng ý, mặc dù có thừa nhận rằng có lẽ nên tham khảo ý kiến chuyên gia](https://github.com/jspenguin2017/Snippets/issues/2#issuecomment-711033337. Điều đó đang được nói, ý kiến ​​​​chính thức của họ dường như là vì đây là một dự án cá nhân, ai quan tâm đến cách họ xử lý mọi việc (họ cũng có vẻ tin rằng phần lớn những người bất đồng chính kiến ​​​​là những kẻ troll, điều đó không tuyệt vời).

### Tôi có nên kiểm tra tiện ích mở rộng của mình không?

> CÓ
{: .prompt-tip }

Đây không phải là lần đầu tiên chuyện như thế này xảy ra và cũng không phải là lần cuối cùng. [The Great Suspender](https://github.com/greatsuspender/thegreatsuspender/issues/1175), với hai triệu người dùng, có thể đang bắt đầu cho một kịch bản tương tự. ([_Đính chính: Ừ thì nó có phức tạp hơn một chút._](https://www.reddit.com/r/HobbyDrama/comments/jouwq7/open_source_development_the_great_suspender_saga/))

Bản chất của các dự án nguồn mở là chúng có thể bị hỏng, bị mua lại hoặc có chúa mới biết là gì. Vì vậy, nếu bạn tin tưởng, hãy đảm bảo rằng bạn biết mình đang tải xuống những gì.

Đó là toàn bộ Drama. Thương hiệu Nano- bị hư hỏng không thể khắc phục được và các extension đã bị xóa khỏi Chrome và Edge. Tương lai của tiện ích mở rộng Firefox vô tội vẫn chưa rõ ràng.

Kiểm tra tiện ích mở rộng của bạn nhé mọi người.

### Cập nhật muộn

Hóa ra Nano không phải là phần mềm độc hại mạo đa ad-blocker duy nhất trên Chrome App Store. Những ứng dụng này có hơn 80 triệu người dùng kết hợp.

Vì vậy, như tôi đã nói, hãy kiểm tra extensions của bạn. 

## [Auto Tab Discard](https://addons.mozilla.org/en-US/firefox/addon/auto-tab-discard/): Tự động unload tab không hoạt động[^footnote] 
### Unload tab có sẵn (native) trên Firefox[^ff-tabunloader]

_Tạm dịch_
: Tab Unloading là một tính năng tự động tắt các tab để ngăn Firefox bị crash do thiếu bộ nhớ, gồm hai thành phần: `nhận diện thiếu tài nguyên` và `unload tabs`. Trình duyệt sẽ tự động unload tab khi phát hiện bộ nhớ xuống thấp: xếp hang ưu tiên và lựa chọn unload các tab; nếu không có tab nào có thể unload, trình duyệt sẽ kích hoạt cảnh báo nội bộ cho phép các modules giảm lượng sử dụng bộ nhớ của chúng.
:
: Thứ tự ưu tiên các tab cụ thể:
:
: 1. Firefox cơ bản tắt các tab theo thứ tự `đã lâu chưa sử dụng nhất`, _ngoại trừ các tab đang phát multimedia, sử dụng Picture-in-Picture hoặc sử dụng WebRTC_. Các tab được ghim sẽ được ưu tiên thấp hơn và ít có khả năng bị tắt.
:
: 2. Khi có nhiều tab được mở hơn, trong hầu hết các trường hợp khi có `hơn mười một tab`, Firefox sẽ thực hiện các tính toán bổ sung để `xác định các tiến trình lưu trữ tab` và ước tính mức sử dụng bộ nhớ của mỗi tab, sau đó `tắt các tab tốn nhiều bộ nhớ hơn`, và nhiều tiến trì sx kết thúc sau khi unload tab

> Tuy không được trình bày cụ thể, nhưng trong `about:config` có tham số `browser.tabs.min_inactive_duration_before_unload: 600000`, nếu đơn vị tính là mili-giây thì tương đương 10 phút. Đây (chắc?) là thời gian để bị coi là _lâu chưa sử dụng_
{: .prompt-info }

Theo giang hồ phàn nàn thì cái tính năng này đã yếu (chỉ unload nếu bộ nhớ dưới 400MB - máy 16Gigs RAM thì bao giờ nó mới chạy?) lại còn không ổn định, nên là tắt luôn đi cho lành: `browser.tabs.unloadOnLowMemory = false`

| browser.tabs.unloadOnLowMemory | false |

```javascript
// Disable native tab unloader
user_pref("browser.tabs.unloadOnLowMemory", false );
```
{: file="user.js"}

<https://www.reddit.com/r/firefox/comments/co6xng>
: I believe the native tab unloading is only activated when available memory is critically low. Auto Tab Discard has many more options to discard tabs either manually or via other conditions automatically.
: > Starting with Firefox 93, Firefox will monitor available system memory and, should it ever become so critically low that a crash is imminent, Firefox will respond by unloading memory-heavy but not actively used tabs.
    
<https://www.reddit.com/r/firefox/comments/co6xng>
: Unloading of tabs should happen when available memory is below 400MB when that preference is set to true.
: That preference has been set to false as default since v68 as it does not work as intended, were it will unload tabs even if there is more than 400MB of available memory.
: - Bug 1558930: Turn off tab unloading on release
: - Bug 1558554: Tabs are suspending above the low memory threshold
: - Bug 1558554: Tabs are suspending above the low memory threshold #5

### Add-on Auto Tab Discard[^ff-addon-voz][^ff-auto-tab-discard]

Tải và cài đặt: <https://addons.mozilla.org/en-US/firefox/addon/auto-tab-discard/>
: Vào chỉnh `When the number of inactive tabs exceeds:` là `1` (cứ có 1 tab không hoạt động là tắt)
: Thỉnh thoảng dọn rác
: - Vào `about:memory`, chọn `GC`: để Firefox giải phóng bớt RAM thừa đi
: - Vào `about:unloads`: click `Unload` nếu như muốn tự tay unload tab
: - Vào `about:config`: xóa sạch trong `extensions.webextensions.restrictedDomains` để unload không vùng cấm

```javascript
// Add-on run no exception
user_pref("extensions.webextensions.restrictedDomains", "");
```
{: file="user.js"}

## [ProxySwitchy Omega](https://addons.mozilla.org/en-US/firefox/addon/switchyomega/) - Fake IP theo tên miền[^ff-proxy-switchy-1]

### Vượt Deep Packet Inspector (DPI) của nhà mạng để vào tên miền bị chặn[^fn-proxy-switchy-2]

Tuy sử dụng HTTPS được mã hóa, nhưng giữa client và server vẫn trao đổi một số thông tin trong quá trình bắt tay TLS ban đầu để thỏa thuận mã hóa. Trong quá trình bắt tay ban đầu này, client sẽ _gửi tên của máy chủ mà nó đang liên hệ dưới dạng văn bản rõ_ (gói ClientHello) để máy chủ biết chứng chỉ nào cần cung cấp. Các hệ thống Kiểm tra Gói sâu (DPI) có thể chặn kết nối bằng cách chặn giao tiếp này. Để tránh bị phát hiện, Demergi phân đoạn và sửa đổi gói ban đầu này.

> Có những giải pháp đầy hứa hẹn cho vấn đề ẩn giấu càng nhiều thông tin càng tốt trong quá trình bắt tay ban đầu của kết nối TLS, một trong số đó là Encrypted Client Hello (ECH). Tuy nhiên, cho đến khi các giải pháp này được triển khai đầy đủ, các công cụ như Demergi có thể hữu ích như các cơ chế trốn tránh.
{: .prompt-info }

> Demergi là một công cụ mạnh mẽ có thể được sử dụng để bỏ qua DPI, nhưng nó không phải là một giải pháp bảo mật hoàn toàn. Một số nhà cung cấp dịch vụ Internet có thể phát hiện và chặn Demergi.
{: .prompt-warning }

Ưu điểm
: Hoạt động trên 100% trang web thậm chí không cần ECH, không quan tâm là Medium, Bonhup hay ẾchVid...
: Giải pháp mang tính toàn tổng hơn sử dụng cách thức băm nhỏ gói tin ClientHello ra để vượt cạn
: KHÔNG HỀ fake IP, nghĩa là tốc độ sẽ nguyên 100%, không tốn 1 xu, không dựa dẫm vào một ai cả
: Không gây lỗi web như GoodbyeDPI vì nó chỉ hoạt động trên những trang cần thiết chứ không toàn bộ hệ thống

#### Cài đặt

- Với Windows: Tải Demergi: <https://github.com/hectorm/demergi>, giải nén, bật lên
- Với MacOS:

```bash
npm install -g demergi
demergi --help
```

> Sử dụng NSSM (<https://nssm.cc/download>) để chạy Demergi như service (chạy ngầm không hiện cửa sổ):
>
> Cách 1: mở `cmd` gõ `nssm install` cho nó hiện cái giao diện ra:
> : Path: D:\demergi\demergi-win-x64.exe
> : Startup directory:D:\demergi
> : Arguments: (để trống)
> : Service name: Demergi
>
> Cách 2: gõ luôn `cmd` dài
> : nssm install Demergi D:\demergi\demergi-win-x64.exe 
{: .prompt-tip }

Vào phần config của `ProxySwitchy Omega` tạo một `Proxy Profile` tên `Demergi`, điền vào là `127.0.0.1` port `8080` rồi `Apply`
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-demergi.png)
: _Pofile Demergi_

Tạo tiếp một `Switch Profile` tên `Auto` rồi `Add condition` rồi chọn Type là `Host regex`, Details là `^.*?(?:medium.com|pornhub.com|xvideos.com)` chọn Profile là `ChunkRust` rồi Apply
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-auto.png)
: _Profile Auto_

> Chú ý: Muốn thêm trang nào thì tự thêm vào phần Details
{: .prompt-info }

Chọn proxy là `Auto` trên thanh toolbar của ProxySwitchy Omega, và thế là xong.
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-toolbar.png)
: _Chọn Auto trên toolbar_

### Truy cập  `.onion` với Tor Control Panel (chỉ có trên Windows) [^fn-proxy-switchy-3]

Ưu điểm
: Không bao giờ khiến trang web hàng ngày hay vào chậm đi
: Chọn được quốc gia nên không có chuyện dùng máy chủ Tor tận châu Phi gây chậm, mà dùng hẳn Singapore, Hong Kong

Yêu cầu
: SwitchyOmega ở #1
: Tor Control Panel (TCP) ở mục SwitchyOmega #1

#### Cài đặt Tor Control Panel

Tải về cài đặt: <https://github.com/abysshint/tor-control-panel/releases>
: chạy rồi Start, đợi một lúc, sau đó đặt proxy mà nó hiện ra ở phần mềm thường là `127.0.0.1:9050` hoặc `127.0.0.1:9051` vào socks của ProxySwitchy là xong thôi. Cụ thể port nó nằm ở:
: ![](https://voz.vn/attachments/1695470625450-png.2088817/)

Sau đó muốn chọn quốc gia thì vào `Settings` chọn `Filter`:
: Bỏ đánh dấu tất cả mấy cái ngôi sao nhìn thấy đi cho đến khi `Entry, Middle, Exit` đều là `0, 0, 0` (cứ click chuột vào ngôi sao đen) sau đó chọn một quốc gia ưa thích, đánh 3 dấu sao vào như hình dưới, chọn `Apply` rồi `Change Circuit`.

Muốn nhanh chọn các nước có ping thấp và gần Việt Nam
: Thông số tốc độ có hết trong mục `Filter`, các bạn cứ mạnh dạn ấn vào để sắp xếp theo thứ tự như Ping, Alive (thời gian sống, sống càng lâu càng tốt), Country (quốc gia) rồi chọn một cái ưng ý.
: ![](https://voz.vn/attachments/1682008215021-png.1791084/)

#### Config Proxy Switchy Omega

Ấn vào biểu tượng Switchy rồi `Options` -> `New Profile`
: Đặt tên là `Tor Control Panel`, phân loại `Proxy Profile`
: Ở phần Protocol chọn `SOCKS5`, Server `127.0.0.1`, Port `9050` hoặc `9051`, tùy theo cái port mà TCP phân cho rồi Save.
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-tor-control-panel.png)
: _Profile Tor Control Panel_

Chọn Switch Profile đã có (hoặc tạo mới)
: Chọn `Host regex` (bật `Advanced` settings nếu không thấy), điền vào là `^.*?\.onion`
: Phần profile chỉnh thành `Tor`, Save
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-auto.png)
: _Profile Auto_


Chọn proxy là `Auto` trên thanh toolbar của ProxySwitchy Omega, và thế là xong.
: ![](../../assets/img/firefox-addon-p2/proxyswitchy-toolbar.png)
_Chọn Auto trên toolbar_

> Sau đó vào các trang `.onion` rồi hưởng thụ thành quả, mấy trang này chứa rất nhiều hàng hiếm (có thể tham khảo bài bên trên có chia sẻ vài trang căn bản), thậm chí là chống lại nhân loại, nói chung là tiết chế để tránh bản thân trở nên sa sút
{: .prompt-warning}

## [Header Editor](https://addons.mozilla.org/en-US/firefox/add-on/header-editor/) - Đổi User-Agent/Language, tùy ý thay đổi nội dung trang web[^ff-addon-voz]
`Header Editor` là  add-on cực mạnh giúp phá và sửa trang web, tính năng:
: Thêm/xóa/sửa header (User-Agent, Referer...) của Request và Response
: Thêm/xóa/sửa source (HTML) response của server để thay đổi hiển thị trước khi trình duyệt render

### Tùy biến Youtube

#### Không chuyển hướng Youtube Mobile về PC

- Click vào dấu `+` (New)
- Rule type: `Modify request header`
- Match type: `Domain`
- Match Rules: `m.youtube.com`
- Execute type: `normal`
- Header name: `user-agent`
- Header value: `Mozilla/5.0 (Android 12; Mobile; rv:109.0) Gecko/113.0 Firefox/113.0`
- `Save`

![](../../assets/img/firefox-addon-p3/yt-inject-ua.png)
_Config trên HE_

#### Chuyển hướng từ Youtube PC sang Mobile

- Click vào dấu `+` (New)
- Rule type: `Redirect request`
- Match type: `Regular expression`
- Match Rules: `^https://www.youtube.com/(.*?$)`
- Execute type: `normal`
- Redirect to: `https://m.youtube.com/$1`

![](../../assets/img/firefox-addon-p3/yt-pc-to-mobile.png)
_Config trên HE_

#### Tắt Hovering to Play (Playback Inline)

- Click vào dấu `+` (New)
- Rule type: `Modify response header`
- Match type: `Regular expression`
- Match Rules: `.*?youtube.*?/`
- Execute type: `Custom function`
- Code:
```javascript
for (const a in val) {
    if (val[a].name.toLowerCase() === 'set-cookie') {
        val[a].value+='\nPREF=f7=1';
    }
}
```

![](../../assets/img/firefox-addon-p3/yt-disable-hover-to-play.png)
_Config trên HE_

### Tùy biến Facebook
#### Không chuyển hướng từ Facebook Touch về PC

- Click vào dấu `+` (New)
- Rule type: `Modify request header`
- Match type: `Domain`
- Match Rules: `touch.facebook.com`
- Execute type: `normal`
- Header name: `user-agent`
- Header value: `Mozilla/5.0 (Android 12; Mobile; rv:109.0) Gecko/113.0 Firefox/113.0`
- `Save`

![](../../assets/img/firefox-addon-p3/fb-inject-ua.png)
_Config trên HE_

#### Chuyển hướng từ Facebook PC sang Touch

- Click vào dấu `+` (New)
- Rule type: `Redirect request`
- Match type: `Regular expression`
- Match Rules: `^https://www.facebook.com/(.*?$)`
- Execute type: `normal`
- Redirect to: `https://touch.facebook.com/$1`

![](../../assets/img/firefox-addon-p3/fb-pc-to-touch.png)
_Config trên HE_

> Đó là sức mạnh của Header Editor (HE), khi mà đẩy giới hạn của nó lên mức cao nhất.
{: .prompt-info }

## FileCentipede - Tải đa luồng, bắt link như IDM

> Download: <https://github.com/filecxx/FileCentipede/releases>
{: .prompt-info }

Nếu các bạn xài Firefox Portable hay Floorp thì vào trang add-on cài **<https://addons.mozilla.org/vi/firefox/addon/filecxx/>** hoặc tải file `firefox.xpi` [**tại đây**](https://github.com/filecxx/FileCentipede/releases) rồi kéo thả nó vào để cài đặt là xong nếu nó không tự cài đặt, thường thì khi xài Firefox cài đặt là nó tự cài.

Tính năng thì:
: Y như IDM (đa luồng, thời gian biểu (schedule), bắt link video, hàng loạt...)
: Hơn IDM (kéo Torrent, ED2K)
: KHÔNG GHÉP FILE mà tạo ra một file ảo sau đó ghi liên tiếp vào file ảo trên, không nghẽn ổ đĩa


![](https://voz.vn/attachments/1694834094700-png.2074664/)
![](https://voz.vn/attachments/1694834115777-png.2074665/)


### Thuốc @Fioren[^ff-file-centipede-1]

Thoát hoàn toàn app
: ![](https://voz.vn/attachments/1695663665411-png.2092288/)

Tải DB Browser for SQLite Portable, giải nén và chạy
: Link: <https://portableapps.com/apps/development/sqlite_database_browser_portable>

Vào File > Open database
: Chọn file `filecxx_xxxxx\lib\data_windows.db`

Click phải vào table `local` > Delete Table
: ![](https://voz.vn/attachments/1666550072889-png.1456757/)

Save lại
: Ctrl + S

Mở lại File Centipede check reset trial lại 3 ngày sử dụng chưa.
: Help > Activation code

Thoát hẳn như bước 1
: File > Fully Shutdown

Mở lại cửa sổ SQLite Portable
: Ấn F5 hiển thị lại table `local`, 

Chuyển tab Browser Data chọn `local`
: ![](https://voz.vn/attachments/1666550198563-png.1456758/)

Dòng số 1,2 là 2 dãy chữ số giống nhau
: Ấn đè kéo cái 2 dòng đó để edit được.
: Đổi chữ cái **gần cuối cùng thành chữ a**. Ví dụ: FdyQ764Gih**<span style="color:RED;">k</span>**Y thành FdyQ764Gih**<span style="color:RED;">a</span>**Y
: ![](https://voz.vn/attachments/1666550471799-png.1456764/)

Save lại
: Ctrl + S

Mở lại File Centipede thấy ngày đã tăng
: ![](https://voz.vn/attachments/1666550349246-png.1456763/)

> [File ăn sẵn dành cho ai lười](https://voz.vn/attachments/data_windows-zip.2092290/):
> <br>Giải nén copy đè file `data_windows.db` vào `filecxx_xxxxx\lib`
{: .prompt-info}

## Multi-Threaded Download Manager - Tải đa luồng như IDM, bắt link video, tải hàng loạt như IDM!

> Link: <https://addons.mozilla.org/en-US/firefox/addon/multithreaded-download-manager/>
{: .prompt-info }

Tính năng
: Tải đa luồng như IDM hoạt động nhé, cơ mà mặc định giới hạn 6 luồng (đủ dùng và tốt nhất nên để 6 luồng thậm chí thấp hơn tầm 3-4 luồng sẽ xanh sạch đẹp cho server hơn) bằng với `network.http.max-persistent-connections-per-server` và `network.http.max-persistent-connections-per-proxy` trong `about:config` vì nó dùng API network của Firefox tải file:
: ![](https://i.imgur.com/7oxGDlB.jpg)
: Hỗ trợ bắt link video như IDM nhé, mà nó hoạt động trong Firefox nên không quan tâm tới Referer hay Cookies
: ![](https://i.imgur.com/CCPLqbM.jpg)
: Có tính năng Queue để giới hạn số lượng tải về trong cùng một thời điểm nhé:
: ![](https://i.imgur.com/C49vsrH.jpg)

> Nên dùng kết hợp với script bắt link video của bạn @boscofz sẽ rất tiện, script nhỏ nhẹ và tương thích mọi trang web: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23935535>
{: .prompt-tip }
> Kết hợp với yt-dlp như hướng dẫn này của mình thì IDM gọi bằng cụ nhé :D <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23288076>
{: .prompt-tip }

Tổng kết lại tính năng so với IDM:
: Tải đa luồng: Có
: Pause/Resume file đang tải dở: Có
: Quản lý tải về: Có
: Tải giới hạn số lượng tải cùng lúc: Có
: Bắt link video: Có (tốt hơn IDM do nó dùng cookies/referer từ Firefox)
: Tải hàng loạt: Có (tốt hơn IDM do nó dùng cookies/referer từ Firefox)

Tính năng mà IDM không có:
: Hoạt động ngay trong trình duyệt nên nó sử dụng cookies/referer tốt hơn, chia sẻ đăng nhập với Firefox nên không cần đăng nhập lại account premium. Nếu trang nào tải khoai quá vì một số lý do nó ghét phân luồng thì chọn `Continue in browser` tải trong Firefox là xong.
: Không cần ghép file như IDM làm quá tải ổ cứng, thằng này sử dụng thuật toán file ảo hiện đại, nó tạo ra một file ảo sử dụng Storage API của Firefox, ví dụ tải file 4GB thì nó tạo ra một file rỗng 4GB, sau đó tải nhồi dữ liệu vào file đó luôn nên không ghép file như IDM (đòi gấp 2 dung lượng)
: Tải những thứ mà IDM không tải được do nó hoạt động trong Firefox, cái gì Firefox thấy là nó thấy, và nó thấy là nó tải được. 
: Không thể bị phát hiện do nó dùng TLS Fingerprint của Firefox, nghĩa là Firefox chia luồng ra Firefox tải, nếu trang web muốn chặn là phải chặn cả Firefox, còn IDM thì nó có Fingerprint riêng (kể cả để HTTP Header y hệt trình duyệt trang web vẫn phát hiện được qua TLS Fingerprint.

> Các trang web tài file thường là ghét bị chia luồng vì nó tốn tài nguyên ổ đĩa I/O (cứ hiểu là đọc ghi ổ đĩa) gấp N lần số luồng, chia làm 16 luồng thì ổ cứng của họ phải làm việc gấp 16 lần gây nghẽn đọc ghi, Google Drive mặc định là nó không cho chia luồng vì nó không gửi trả `Accept-Ranges`, mình cứ bỏ qua chia thì nó đáp trả vậy đó. Nhìn chung cứ Continue in browser nếu file bự quá.
{: .prompt-info }

### Bản mod ngon hơn hỗ trợ tải đa luồng Google Drive và nhiều trang hơn[^ff-mdm-2]

Tải về, giải nén quăng vào `about:addons`.

Nếu báo không cài được: 
: Vào `about:config`
: Tìm `xpinstall.signatures.required` chuyển thành `false`
: Tìm `xpinstall.whitelist.required` chuyển thành `false`

| xpinstall.signatures.required | false |
| xpinstall.whitelist.required | false |

```javascript
// Un-check singature extension
user_pref("xpinstall.signatures.required", false);
user_pref("xpinstall.whitelist.required", false);
```
{: file="user.js"}


> Tải ở đây: <https://voz.vn/attachments/mdm-zip.1779202/>
{: .prompt-info }

>Vậy là không phải do tác giả viết sai kỹ thuật đâu bác, mà là viết quá tuân thủ kỹ thuật. Lẽ ra phải lươn lẹo như mấy thằng khác, có accept-range hay không cũng kệ, thấy content-length là chia luồng tải trước, lỗi thì quay lại 1 luồng.
{: .prompt-info }

Có 2 file `connection.js` và `monitor.js`, dùng Find tìm acceptRanges rồi chuyển tất cả cái gì là false thành true là xong.

Cách học lỏm code của bất kỳ ai nhanh nhất là dùng Notepad++, cài Compare Plus rồi mở cá 2 dự án đã được sửa và gốc lên rồi so sánh toàn bộ file, như vậy nó sẽ lộ ra phần đã chỉnh sửa nằm ở đâu file nào.

![https://i.imgur.com/iqA6i5Q.png](https://i.imgur.com/iqA6i5Q.png)

### Tùy chỉnh

Trong tab General
: Bật `Enable prompt for links without multithreading support`: `Audio` và `Video`
: ![](../../assets/img/firefox-addon-p4/mdm-general.png)

Trong tab Network
: Đặt `Minimum chunk` là `307200 KB` (_tương đương 300 MB_ - tránh MDM chia luồng tải dung lượng quá bé)
: Đặt `Maximum retries` là `Umlimited` (_xóa số mặc định đi là thành Unlimited_)
: ![](../../assets/img/firefox-addon-p4/mdm-network.png)

# Violentmonkey/Greasymonkey/Tampermonkey[^ff-addon-voz]

Violentmonkey
: Link: <https://addons.mozilla.org/en-US/firefox/addon/violentmonkey/>
: Có tính tương thích cao, mã nguồn mở

Greasymonkey
: Link: <https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/>
: Tthủy tổ của tất cả, tính tương thích tàm tạm, tính năng đã lỗi thời

Tampermonkey
: Link: <https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/>
: Có tính tương thích rất cao, tuy nhiên là _mã nguồn đóng_ <https://github.com/Tampermonkey/tampermonkey/issues/1515]

Firemonkey
: Trẻ trâu mới vào làng, rất nhanh và nhẹ 
: Tính tương thích kiểu lúc được lúc không, nên tạm thời cho xuống Thùng Rác

## Linguist/TWP - Dịch trang web, bôi đen với >100 ngôn ngữ (hỗ trợ dịch offline)"[^ff-addon-voz]
[**Linguist**](https://addons.mozilla.org/addon/linguist-translator/): Chrome có tính năng tự động dịch trang web mà nhiều người chết mê chết mệt, vậy Linguist mang đến cho Firefox tính năng dịch tương tự và nhiều hơn vì Linguist hỗ trợ dịch bôi đen, tính năng đặt ngoại lệ, tính năng dịch ngôn ngữ bất kỳ trên trang bất kỳ ví dụ trang tiếng Nhật thì dịch sang Anh thay vì sang Việt. Thậm chí Linguist còn hỗ trợ dịch offline hoàn toàn không dùng tới kết nối internet dựa trên dự án [**Bergamot**](https://github.com/browsermt/bergamot-translator) của Firefox.

Ngoài ra [**TWP - Translate This Page**](https://addons.mozilla.org/en-US/firefox/addon/traduzir-paginas-web/) cũng là một lựa chọn tương đối.

### Cách để dịch theo quy luật ngôn ngữ / trang web bất kì[^ff-linguist]

Ấn vào biểu tượng toolbar, chọn Nguồn -> Đích, sau đó phần `Preferences for xxx` chọn `Always translate`, kết quả nó thành thế này.

![](https://voz.vn/attachments/1686573899994-png.1891148/)

Thế là F5 cái Đen Vâu.vn tự dịch từ Việt -> Anh.

![](https://voz.vn/attachments/1686573966841-png.1891151/)

## Search by Image - Tìm kiếm ảnh, dịch trong ảnh[^ff-addon-voz]
[**Search by Image**](https://addons.mozilla.org/en-US/firefox/addon/search_by_image/): Dùng để tìm ảnh trùng lặp trên RẤT nhiều nguồn từ Google tới Tung Của rồi Nga Ngố, đủ thể loại, rất nhẹ cài vào chả dùng tí tài nguyên nào cả, chỉ là cái Context Menu cực đơn giản nhưng đa năng, và tính năng mà rất nhiều người sẽ thèm muốn là OCR dùng để xuất chữ ra từ ảnh dựa trên Google Lens. Vào Options của nó bật Google Lens lên là có tính năng OCR ngon lành cành đào:

![](https://voz.vn/attachments/1685429291909-png.1865315/)

## Progressive Web Application for Firefox - Tạo ứng dụng web như Zalo, Discord,..[^ff-addon-voz][^ff-pwa-1]

> [Zalo điếm thúi](https://voz.vn/t/zalo-diem-thui.726670/)
{: .prompt-info}

Câu nói quen thuộc của người dùng khi sử dụng lợn Zalo, bản PC thì chậm, ngốn tài nguyên, ngốn ổ đĩa, khởi động cùng hệ thống một cách vô lý... Bản web cũng chả kém cạnh gây chậm trình duyệt do lưu trữ một lượng IndexDB lớn [ảnh](https://voz.vn/attachments/1679844766285-png.1741371/). Cơ mà ở Việt Nam mà không dùng Zalo thì khỏi nghĩ tới:

- Tán gái, gái Việt dùng Zalo, không có khỏi tán gái
- Nhiều công ty ép nhân viên dùng Zalo, không có khỏi làm việc
- Xã hội dùng Zalo, không có khỏi giao tiếp


Vậy nên mấy hôm trước mình lặn lội thân cò tìm đường cứu nước, và giải pháp ở đây là biến thằng Zalo này thành ứng dụng web (PWA/Progressive Web Application), để nó tách biệt với trình duyệt và hoạt động như một ứng dụng web kiểu Electron có hẳn một biểu tượng riêng để mở ở Desktop, và đặc biệt khác với Zalo thường, thằng PWA này biến Zalo thành Portable, nghĩa là bê đi đâu cũng được mở phát lên dùng như khi ở nhà. Sau vài hôm sử dụng và nghiên cứu để có thể viết hướng dẫn mà ai cũng có thể làm được dù lấy não đặt sang một bên. :D

Addon này nhìn chung giống với PWA của Chrome, cơ mà ngon hơn nhiều về tính năng.

Vậy thì vào việc thôi.

Vậy đầu tiên đối tượng nào phù hợp để biến thành PWA ? Vào Settings -> Manage Cookies and Site Data, thấy thằng nào dùng tầm 1-2GB thì nghĩa là phù hợp, ví dụ:

![](https://voz.vn/attachments/1679844766285-png.1741371/)


- Cài đặt [**Progressive Web Application**](https://addons.mozilla.org/en-US/firefox/addon/pwas-for-firefox/) vào Firefox.
- Vào trang này tìm file kiểu `firefoxpwa_x.x.x_online.paf.exe` rồi cài vào: <https://github.com/filips123/PWAsForFirefox/releases>
- Chạy `PWAsForFirefoxPortable.exe`
- Chuột phải vào file `PWAsForFirefoxPortable.exe` rồi Copy
- Win + R, mở `%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup`
- Paste Shortcut vào để nó khởi động cùng hệ thống
- Quay lại Firefox, mở <https://chat.zalo.me/> lên, đăng nhập các kiểu rồi ấn vào biểu tượng PWA đỏ đỏ bên trên -> Install current site -> Install Web App là xong thôi. Nếu muốn sửa lại tên ứng dụng thì cứ sửa.
- Chọn Launch Web App hoặc cứ mở <https://chat.zalo.me/> là nó mở thẳng qua PWA như một ứng dụng Zalo điện thoại, kết quả:

![](https://i.imgur.com/2dXsrKZ.png)

Còn nếu muốn copy toàn bộ dữ liệu Zalo từ Firefox đang dùng theo nhu cầu của @wuwu_999 thì đầu tiên cứ đăng nhập vào cái Zalo App mới này, ở Firefox chính vào `about:support` -> Open Profile Folder rồi copy cả folder `storage` rồi vào folder kiểu `PWAsForFirefoxPortable\Data\profiles\00000000000000000000000000` của PWA rồi ghi đè lên là ok.

Kiểm tra lại xem có ok không, nếu đã ok rồi thì cứ mạnh dạn xóa sạch IndexDB trong Cookies and Site Data của Firefox chính là xong, thế là trả lại cho Firefox chính một bầu trời bình yên và thằng Zalo cuốn xéo sang một nơi khác ở. :D

Nếu thích cứ tạo Shortcut mà mở từ Desktop là giống y chang thằng Zalo PC, mà không bị ba cái vụ ba xàm kia. Áp dụng tương tự cho nhiều trang web khác nhé, ví dụ Photopea (biến thành offline luôn), Discord...

Đã cho lên #1, add-on ngon và tương lai sẽ có thêm tính năng Minimize to Tray như tác giả hứa.

### Cách Pin PWA vào Taskbar[^ff-pwa-2][^ff-pwa-3]

Cái này phải lấy command line từ cái process `firefox.exe` sau đó New shortcut -> Paste vào (cố gắng để folder PWA càng ngắn càng tốt vì shortcut có giới hạn 256 ký tự thôi), thế là xong ez, làm tương tự với Linux/Mac:

![](https://voz.vn/attachments/1691331024652-png.1999356)
![](https://voz.vn/attachments/1691331127251-png.1999362)

Nếu muốn Pin vào Taskbar thì chuột phải vào cái Shortcut mới tạo, chọn Pin to Taskbar là xong nhé.

### Tạo Template cho PWA

Hôm nay có nhắc tới vụ tạo Template cho PWA, sau một thời gian hỏi han tìm hiểu mình đã ngộ ra được chân lý nên phải viết ngay.

Ví dụ là **ép cho PWA tiết kiệm RAM bằng cách tắt Fission đi nha.**

- Tạo một folder rỗng ở đâu thì tùy, ví dụ `pwat`
- Tạo một file `user.js` trong thư mục trên, copy toàn bộ đoạn dưới vào:

```
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
```

- Save lại
- Từ cửa sổ Firefox/Floorp, ấn vào biểu tượng PWA
- Ấn vào cái bánh răng
- Dán đường dẫn tới thư mục `pwat` vừa tạo ban nãy:

![](https://voz.vn/attachments/1693494174928-png.2047205/)

Và thế là xong, từ nay mỗi khi bạn tạo một ứng dụng PWA mới, nó sẽ thừa hưởng file `user.js` và tắt Fission đi tiết kiệm rất nhiều RAM, các bạn có thể tham khảo #2 phần `Tối ưu Firefox` mình có để rất nhiều tối ưu, hoàn toàn có thể áp dụng một số tối ưu để tăng tốc PWA lên được như nglayout, tắt chạy nền, ví dụ đây là một file `user.js` hịn tắt Fission, tối ưu nglayout, tắt chạy nền:

```javascript
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
// Enable Multi-Account Container
user_pref("privacy.userContext.enabled", true); //enable Multi-Account Container
user_pref("privacy.userContext.ui.enabled", true); //enable Multi-Account Container

/*** [SECTION 0200]: GEOLOCATION / LANGUAGE / LOCALE ***/
user_pref("_user.js.parrot", "0200 syntax error: the parrot's definitely deceased!");
/* 0201: use Mozilla geolocation service instead of Google if permission is granted [FF74+]
 * Optionally enable logging to the console (defaults to false) ***/
user_pref("geo.provider.network.url", "https://location.services.mozilla.com/v1/geolocate?key=%MOZILLA_API_KEY%");
   // user_pref("geo.provider.network.logging.enabled", true); // [HIDDEN PREF]
/* 0202: disable using the OS's geolocation service ***/
user_pref("geo.provider.ms-windows-location", false); // [WINDOWS]
user_pref("geo.provider.use_corelocation", false); // [MAC]
user_pref("geo.provider.use_gpsd", false); // [LINUX]
user_pref("geo.provider.use_geoclue", false); // [FF102+] [LINUX]

/*** [SECTION 0300]: QUIETER FOX ***/
user_pref("_user.js.parrot", "0300 syntax error: the parrot's not pinin' for the fjords!");
/** RECOMMENDATIONS ***/
/* 0320: disable recommendation pane in about:addons (uses Google Analytics) ***/
user_pref("extensions.getAddons.showPane", false); // [HIDDEN PREF]
/* 0321: disable recommendations in about:addons' Extensions and Themes panes [FF68+] ***/
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
/* 0322: disable personalized Extension Recommendations in about:addons and AMO [FF65+]
 * [NOTE] This pref has no effect when Health Reports (0331) are disabled
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to make personalized extension recommendations
 * [1] https://support.mozilla.org/kb/personalized-extension-recommendations ***/
user_pref("browser.discovery.enabled", false);

/** TELEMETRY ***/
/* 0330: disable new data submission [FF41+]
 * If disabled, no policy is shown or upload takes place, ever
 * [1] https://bugzilla.mozilla.org/1195552 ***/
user_pref("datareporting.policy.dataSubmissionEnabled", false);
/* 0331: disable Health Reports
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send technical... data ***/
user_pref("datareporting.healthreport.uploadEnabled", false);
/* 0332: disable telemetry
 * The "unified" pref affects the behavior of the "enabled" pref
 * - If "unified" is false then "enabled" controls the telemetry module
 * - If "unified" is true then "enabled" only controls whether to record extended data
 * [NOTE] "toolkit.telemetry.enabled" is now LOCKED to reflect prerelease (true) or release builds (false) [2]
 * [1] https://firefox-source-docs.mozilla.org/toolkit/components/telemetry/telemetry/internals/preferences.html
 * [2] https://medium.com/georg-fritzsche/data-preference-changes-in-firefox-58-2d5df9c428b5 ***/
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false); // see [NOTE]
user_pref("toolkit.telemetry.server", "data:,");
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.newProfilePing.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.shutdownPingSender.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.updatePing.enabled", false); // [FF56+]
user_pref("toolkit.telemetry.bhrPing.enabled", false); // [FF57+] Background Hang Reporter
user_pref("toolkit.telemetry.firstShutdownPing.enabled", false); // [FF57+]
/* 0333: disable Telemetry Coverage
 * [1] https://blog.mozilla.org/data/2018/08/20/effectively-measuring-search-in-firefox/ ***/
user_pref("toolkit.telemetry.coverage.opt-out", true); // [HIDDEN PREF]
user_pref("toolkit.coverage.opt-out", true); // [FF64+] [HIDDEN PREF]
user_pref("toolkit.coverage.endpoint.base", "");
/* 0334: disable PingCentre telemetry (used in several System Add-ons) [FF57+]
 * Defense-in-depth: currently covered by 0331 ***/
user_pref("browser.ping-centre.telemetry", false);
/* 0335: disable Firefox Home (Activity Stream) telemetry ***/
user_pref("browser.newtabpage.activity-stream.feeds.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry", false);

/** STUDIES ***/
/* 0340: disable Studies
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to install and run studies ***/
user_pref("app.shield.optoutstudies.enabled", false);
/* 0341: disable Normandy/Shield [FF60+]
 * Shield is a telemetry system that can push and test "recipes"
 * [1] https://mozilla.github.io/normandy/ ***/
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");

/** CRASH REPORTS ***/
/* 0350: disable Crash Reports ***/
user_pref("breakpad.reportURL", "");
user_pref("browser.tabs.crashReporting.sendReport", false); // [FF44+]
   // user_pref("browser.crashReports.unsubmittedCheck.enabled", false); // [FF51+] [DEFAULT: false]
/* 0351: enforce no submission of backlogged Crash Reports [FF58+]
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send backlogged crash reports  ***/
user_pref("browser.crashReports.unsubmittedCheck.autoSubmit2", false); // [DEFAULT: false]

/** OTHER ***/
/* 0360: disable Captive Portal detection
 * [1] https://www.eff.org/deeplinks/2017/08/how-captive-portals-interfere-wireless-security-and-privacy ***/
user_pref("captivedetect.canonicalURL", "");
user_pref("network.captive-portal-service.enabled", false); // [FF52+]
/* 0361: disable Network Connectivity checks [FF65+]
 * [1] https://bugzilla.mozilla.org/1460537 ***/
user_pref("network.connectivity-service.enabled", false);

/*** [SECTION 0400]: SAFE BROWSING (SB)
   SB has taken many steps to preserve privacy. If required, a full url is never sent
   to Google, only a part-hash of the prefix, hidden with noise of other real part-hashes.
   Firefox takes measures such as stripping out identifying parameters and since SBv4 (FF57+)
   doesn't even use cookies. (#Turn on browser.safebrowsing.debug to monitor this activity)

   [1] https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/
   [2] https://wiki.mozilla.org/Security/Safe_Browsing
   [3] https://support.mozilla.org/kb/how-does-phishing-and-malware-protection-work
   [4] https://educatedguesswork.org/posts/safe-browsing-privacy/
***/
user_pref("_user.js.parrot", "0400 syntax error: the parrot's passed on!");
/* 0401: disable SB (Safe Browsing)
 * [WARNING] Do this at your own risk! These are the master switches
 * [SETTING] Privacy & Security>Security>... Block dangerous and deceptive content ***/
   // user_pref("browser.safebrowsing.malware.enabled", false);
   // user_pref("browser.safebrowsing.phishing.enabled", false);
/* 0402: disable SB checks for downloads (both local lookups + remote)
 * This is the master switch for the safebrowsing.downloads* prefs (0403, 0404)
 * [SETTING] Privacy & Security>Security>... "Block dangerous downloads" ***/
   // user_pref("browser.safebrowsing.downloads.enabled", false);
/* 0403: disable SB checks for downloads (remote)
 * To verify the safety of certain executable files, Firefox may submit some information about the
 * file, including the name, origin, size and a cryptographic hash of the contents, to the Google
 * Safe Browsing service which helps Firefox determine whether or not the file should be blocked
 * [SETUP-SECURITY] If you do not understand this, or you want this protection, then override this ***/
user_pref("browser.safebrowsing.downloads.remote.enabled", false);
   // user_pref("browser.safebrowsing.downloads.remote.url", ""); // Defense-in-depth
/* 0404: disable SB checks for unwanted software
 * [SETTING] Privacy & Security>Security>... "Warn you about unwanted and uncommon software" ***/
   // user_pref("browser.safebrowsing.downloads.remote.block_potentially_unwanted", false);
   // user_pref("browser.safebrowsing.downloads.remote.block_uncommon", false);
/* 0405: disable "ignore this warning" on SB warnings [FF45+]
 * If clicked, it bypasses the block for that session. This is a means for admins to enforce SB
 * [TEST] see https://github.com/arkenfox/user.js/wiki/Appendix-A-Test-Sites#-mozilla
 * [1] https://bugzilla.mozilla.org/1226490 ***/
   // user_pref("browser.safebrowsing.allowOverride", false);
```

### Template giảm RAM cho PWA[^ff-pwa-4]

Cập nhập tiếp bài này, <span style="color:rgb(226, 80, 65);">**chú ý một điều là cái file `user.js` trên chỉ dành cho PWA vì tính bảo mật nó thấp hơn**</span>, không dùng cho trình duyệt chính mà có dùng phải bỏ tất những thứ liên quan tới tắt Fission đi.

Cập nhập giảm tiếp đọc ghi ổ đĩa, CPU bằng cách tăng sessionstore delay:

|:---------------------------------------------------|---------|
| browser.sessionstore.idleDelay	                 | 3600000 |
| browser.sessionstore.interval	                     | 3600000 |
| browser.sessionstore.collect_zoom	                 | false   |
| browser.sessionstore.privacy_level                 | 2       |
| browser.sessionstore.restore_pinned_tabs_on_demand | true    |

Giảm RAM bằng cách tắt Fast Back cache mà PWA không bao giờ dùng đến nên tự dưng ôm đồm nó phí RAM:

|:-----------------------------------------|---|
| browser.sessionhistory.max_total_viewers | 0 |

File `user.js` cuối, có vẻ lần này là hết cỡ thật trừ khi trong tương lai mình nhào nặn ra cái gì khác:

```javascript
user_pref("browser.sessionstore.idleDelay", 3600000);
user_pref("browser.sessionstore.interval", 3600000);
user_pref("browser.sessionstore.collect_zoom", false);
user_pref("browser.sessionstore.privacy_level", 2);
user_pref("browser.sessionstore.restore_pinned_tabs_on_demand", true);
user_pref("browser.sessionhistory.max_total_viewers", 0);

user_pref("dom.ipc.processCount.webIsolated", 1);
user_pref("fission.webContentIsolationStrategy", 0);
user_pref("identity.fxaccounts.enabled", false);
user_pref("extensions.pocket.enabled", false);
user_pref("accessibility.force_disabled", 1);
user_pref("fission.autostart", false);
user_pref("dom.ipc.processCount", 1);
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
// Enable Multi-Account Container
user_pref("privacy.userContext.enabled", true); //enable Multi-Account Container
user_pref("privacy.userContext.ui.enabled", true); //enable Multi-Account Container

/*** [SECTION 0200]: GEOLOCATION / LANGUAGE / LOCALE ***/
user_pref("_user.js.parrot", "0200 syntax error: the parrot's definitely deceased!");
/* 0201: use Mozilla geolocation service instead of Google if permission is granted [FF74+]
 * Optionally enable logging to the console (defaults to false) ***/
user_pref("geo.provider.network.url", "https://location.services.mozilla.com/v1/geolocate?key=%MOZILLA_API_KEY%");
   // user_pref("geo.provider.network.logging.enabled", true); // [HIDDEN PREF]
/* 0202: disable using the OS's geolocation service ***/
user_pref("geo.provider.ms-windows-location", false); // [WINDOWS]
user_pref("geo.provider.use_corelocation", false); // [MAC]
user_pref("geo.provider.use_gpsd", false); // [LINUX]
user_pref("geo.provider.use_geoclue", false); // [FF102+] [LINUX]

/*** [SECTION 0300]: QUIETER FOX ***/
user_pref("_user.js.parrot", "0300 syntax error: the parrot's not pinin' for the fjords!");
/** RECOMMENDATIONS ***/
/* 0320: disable recommendation pane in about:addons (uses Google Analytics) ***/
user_pref("extensions.getAddons.showPane", false); // [HIDDEN PREF]
/* 0321: disable recommendations in about:addons' Extensions and Themes panes [FF68+] ***/
user_pref("extensions.htmlaboutaddons.recommendations.enabled", false);
/* 0322: disable personalized Extension Recommendations in about:addons and AMO [FF65+]
 * [NOTE] This pref has no effect when Health Reports (0331) are disabled
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to make personalized extension recommendations
 * [1] https://support.mozilla.org/kb/personalized-extension-recommendations ***/
user_pref("browser.discovery.enabled", false);

/** TELEMETRY ***/
/* 0330: disable new data submission [FF41+]
 * If disabled, no policy is shown or upload takes place, ever
 * [1] https://bugzilla.mozilla.org/1195552 ***/
user_pref("datareporting.policy.dataSubmissionEnabled", false);
/* 0331: disable Health Reports
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send technical... data ***/
user_pref("datareporting.healthreport.uploadEnabled", false);
/* 0332: disable telemetry
 * The "unified" pref affects the behavior of the "enabled" pref
 * - If "unified" is false then "enabled" controls the telemetry module
 * - If "unified" is true then "enabled" only controls whether to record extended data
 * [NOTE] "toolkit.telemetry.enabled" is now LOCKED to reflect prerelease (true) or release builds (false) [2]
 * [1] https://firefox-source-docs.mozilla.org/toolkit/components/telemetry/telemetry/internals/preferences.html
 * [2] https://medium.com/georg-fritzsche/data-preference-changes-in-firefox-58-2d5df9c428b5 ***/
user_pref("toolkit.telemetry.unified", false);
user_pref("toolkit.telemetry.enabled", false); // see [NOTE]
user_pref("toolkit.telemetry.server", "data:,");
user_pref("toolkit.telemetry.archive.enabled", false);
user_pref("toolkit.telemetry.newProfilePing.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.shutdownPingSender.enabled", false); // [FF55+]
user_pref("toolkit.telemetry.updatePing.enabled", false); // [FF56+]
user_pref("toolkit.telemetry.bhrPing.enabled", false); // [FF57+] Background Hang Reporter
user_pref("toolkit.telemetry.firstShutdownPing.enabled", false); // [FF57+]
/* 0333: disable Telemetry Coverage
 * [1] https://blog.mozilla.org/data/2018/08/20/effectively-measuring-search-in-firefox/ ***/
user_pref("toolkit.telemetry.coverage.opt-out", true); // [HIDDEN PREF]
user_pref("toolkit.coverage.opt-out", true); // [FF64+] [HIDDEN PREF]
user_pref("toolkit.coverage.endpoint.base", "");
/* 0334: disable PingCentre telemetry (used in several System Add-ons) [FF57+]
 * Defense-in-depth: currently covered by 0331 ***/
user_pref("browser.ping-centre.telemetry", false);
/* 0335: disable Firefox Home (Activity Stream) telemetry ***/
user_pref("browser.newtabpage.activity-stream.feeds.telemetry", false);
user_pref("browser.newtabpage.activity-stream.telemetry", false);

/** STUDIES ***/
/* 0340: disable Studies
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to install and run studies ***/
user_pref("app.shield.optoutstudies.enabled", false);
/* 0341: disable Normandy/Shield [FF60+]
 * Shield is a telemetry system that can push and test "recipes"
 * [1] https://mozilla.github.io/normandy/ ***/
user_pref("app.normandy.enabled", false);
user_pref("app.normandy.api_url", "");

/** CRASH REPORTS ***/
/* 0350: disable Crash Reports ***/
user_pref("breakpad.reportURL", "");
user_pref("browser.tabs.crashReporting.sendReport", false); // [FF44+]
   // user_pref("browser.crashReports.unsubmittedCheck.enabled", false); // [FF51+] [DEFAULT: false]
/* 0351: enforce no submission of backlogged Crash Reports [FF58+]
 * [SETTING] Privacy & Security>Firefox Data Collection & Use>Allow Firefox to send backlogged crash reports  ***/
user_pref("browser.crashReports.unsubmittedCheck.autoSubmit2", false); // [DEFAULT: false]

/** OTHER ***/
/* 0360: disable Captive Portal detection
 * [1] https://www.eff.org/deeplinks/2017/08/how-captive-portals-interfere-wireless-security-and-privacy ***/
user_pref("captivedetect.canonicalURL", "");
user_pref("network.captive-portal-service.enabled", false); // [FF52+]
/* 0361: disable Network Connectivity checks [FF65+]
 * [1] https://bugzilla.mozilla.org/1460537 ***/
user_pref("network.connectivity-service.enabled", false);

/*** [SECTION 0400]: SAFE BROWSING (SB)
   SB has taken many steps to preserve privacy. If required, a full url is never sent
   to Google, only a part-hash of the prefix, hidden with noise of other real part-hashes.
   Firefox takes measures such as stripping out identifying parameters and since SBv4 (FF57+)
   doesn't even use cookies. (#Turn on browser.safebrowsing.debug to monitor this activity)

   [1] https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/
   [2] https://wiki.mozilla.org/Security/Safe_Browsing
   [3] https://support.mozilla.org/kb/how-does-phishing-and-malware-protection-work
   [4] https://educatedguesswork.org/posts/safe-browsing-privacy/
***/
user_pref("_user.js.parrot", "0400 syntax error: the parrot's passed on!");
/* 0401: disable SB (Safe Browsing)
 * [WARNING] Do this at your own risk! These are the master switches
 * [SETTING] Privacy & Security>Security>... Block dangerous and deceptive content ***/
   // user_pref("browser.safebrowsing.malware.enabled", false);
   // user_pref("browser.safebrowsing.phishing.enabled", false);
/* 0402: disable SB checks for downloads (both local lookups + remote)
 * This is the master switch for the safebrowsing.downloads* prefs (0403, 0404)
 * [SETTING] Privacy & Security>Security>... "Block dangerous downloads" ***/
   // user_pref("browser.safebrowsing.downloads.enabled", false);
/* 0403: disable SB checks for downloads (remote)
 * To verify the safety of certain executable files, Firefox may submit some information about the
 * file, including the name, origin, size and a cryptographic hash of the contents, to the Google
 * Safe Browsing service which helps Firefox determine whether or not the file should be blocked
 * [SETUP-SECURITY] If you do not understand this, or you want this protection, then override this ***/
user_pref("browser.safebrowsing.downloads.remote.enabled", false);
   // user_pref("browser.safebrowsing.downloads.remote.url", ""); // Defense-in-depth
/* 0404: disable SB checks for unwanted software
 * [SETTING] Privacy & Security>Security>... "Warn you about unwanted and uncommon software" ***/
   // user_pref("browser.safebrowsing.downloads.remote.block_potentially_unwanted", false);
   // user_pref("browser.safebrowsing.downloads.remote.block_uncommon", false);
/* 0405: disable "ignore this warning" on SB warnings [FF45+]
 * If clicked, it bypasses the block for that session. This is a means for admins to enforce SB
 * [TEST] see https://github.com/arkenfox/user.js/wiki/Appendix-A-Test-Sites#-mozilla
 * [1] https://bugzilla.mozilla.org/1226490 ***/
   // user_pref("browser.safebrowsing.allowOverride", false);
```

## Quick Cookie Manager - Thêm, sửa, xóa, ghim, backup, chia sẻ Cookies[^ff-addon-2]
[**Quick Cookie Manager**](https://addons.mozilla.org/en-US/firefox/addon/cookie-quick-manager/): Tính năng chính là cho phép thêm, sửa, xóa cookie mà hiện tại nhiều người vẫn dùng nó để chơi trò share account premium đấy.
Firefox thì có rất nhiều add-on quản lý cookie, tuy nhiên add-on quản lý cookie này mình đánh giá rất cao tại vì:

- Hỗ trợ quản lý cookie trong cả Container
- Hỗ trợ export ra file cookies.txt có thể chia sẻ cho nhau tài khoản Premium hay dùng cho yt-dlp mà trước [Chrome từng có thằng Save cookies.txt mà cả một subreddit cài vào là malware đó](https://i.reddit.com/r/youtubedl/comments/11i5vyq/psa_the_get_cookiestxt_extension_is_now_actively/)
- Hỗ trợ ghim cookie để ép cho cookie không bị xóa và đây là một tính năng hay và đi đầu
- GIao diện dễ sử dụng, nhẹ cài vào chả dùng nổi vài MB RAM

## Dark Reader - Ép "Chế độ ban đêm" cho trang web (kèm hướng dẫn tối ưu)[^ff-addon-2][^ff-darkreader-1]

Thấy nhu cầu của nhiều người dùng cần Chế độ ban đêm (Dark Reader), mà ở thời điểm hiện tại Firefox không có giải pháp tốt nhất cho chế độ này nghĩa là [**native (dùng chính engine WebRender để tạo màu đen cho web, hiệu năng cao nhất)**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25194758) nên mình sẽ viết một bài chi tiết cách sử dụng add-on này sao cho hiệu năng cao nhất.

[**Dark Reader**](https://addons.mozilla.org/en-US/firefox/addon/darkreader/) thì là add-on quá nổi tiếng rồi, trong các add-on ép Chế độ ban đêm cho trang web thì thằng này là số một, đa năng nhất, lâu đời nhất, hiệu quả nhất, hiệu năng cũng nhất tuy nhiên vẫn chậm một chút, để nó hoạt động hiệu quả các bạn nên làm phần hướng dẫn bên dưới chỉnh giá trị [**nglayout.initialpaint.delay**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23570551)[^ff-darkreader-2] để tăng hiệu năng của nó lên hết cỡ.

**Cài đặt: <https://addons.mozilla.org/en-US/firefox/addon/darkreader/>**

![](https://voz.vn/attachments/1685504097681-png.1867022/)
_Trang web sẽ đen xì như cục than như thế này đây_

Để Dark Reader có hiệu năng tốt hơn, làm theo bài này:
: [**`nglayout.initialpaint.delay` khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23570551)[^ff-darkreader-2] ([**Nguyên nhân**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22949373)[^ff-darkreader-3])

Chỉ vậy thôi là Dark Reader sẽ hoạt động trơn tru hơn. Nếu trang web nào nhìn không hợp lý thì chuyển qua chế độ khác như <span style="COLOR:rgb(65, 168, 95)">**Static</span>** (mặc định là <span style="color:rgb(41, 105, 176)">**Dynamic**</span> nhìn đẹp trên đa phần trang web, **<span style="color:rgb(65, 168, 95)">Static</span>** hiệu năng tốt nhất, **<span style="color:rgb(226, 80, 65)">Filter</span>** và <span style="color:rgb(226, 80, 65)">**Filter+**</span> hiệu năng rất tệ, nên tránh nếu có thể), sau đó chọn `Only for ...` để nó áp vào đúng trang hiện tại:

![](https://voz.vn/attachments/1685503710124-png.1867003/)

### **`nglayout.initialpaint.delay` khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU**[^ff-darkreader-2]

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

### Nguyên nhân[^ff-darkreader-3]

Mặc định là tức thì đó và giá trị tính là mili giây, 1 giây là 1000 mili giây.

Firefox hiện tại để giá trị này là 5ms, Chrome là 0ms, của mình 2000ms nghĩa là 2s render một lần, tuy nhiên nếu trang web tải xong trước 2s thì render luôn nên không ảnh hưởng đến tốc độ tải trang đâu, Firefox giờ nó khôn lắm không lãng phí thời gian render đâu.

![](https://i.imgur.com/ljX3Fwv.png)

Còn đây là cách Firefox mình render trang web (trang web luôn hiện ra ở trạng thái 100%): <https://gfycat.com/AggressiveDimpledAntarcticgiantpetrel>

Cũng bài viết trên này và áp dụng với người dùng của Dark Reader (<https://addons.mozilla.org/vi/firefox/addon/darkreader/>):

> I rather like the popular Dark Reader extension — an extension which forces "dark" versions of webpages via looking at the colors used. This is useful to reduce power usage on OLED displays and for more comfortable viewing in dark environments — but it causes significant rendering slowdown on my Android phone and causes the phone to heat up.
?
> Instructing Firefox to delay incremental redraw appears to have done a great deal to resolve the pain of this for me.
>
> Ordinarily, if Firefox has not downloaded a full webpage in 250 milliseconds, it tries to start rendering what it has pulled down anyway. This is a great idea if the page can be rendered quickly and not such a great idea if it's expensive to render, since it means that it has to render a webpage multiple times. Presently, it doesn't look like Firefox has any sort of automatic tuning of this value.
>
> I increased the time to 2000 milliseconds.
>
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

## Bitwarden - Tiện ích lưu mật khẩu mã hóa đáng tin cậy![^ff-addon-2]
[**Bitwarden - Tiện ích lưu mật khẩu mã hóa đáng tin cậy!**](https://addons.mozilla.org/en-US/firefox/addon/bitwarden-password-manager/): Thật ra bình thường mình sẽ không giới thiệu một tiện ích lưu mật khẩu online và mình sẽ chỉ nói rằng đặt Master Password là thừa bảo mật, cơ mà Bitwarden khá đáng dùng nếu bạn cần một tiện ích giúp quản lý và đồng bộ mật khẩu trên máy bàn qua lại giữa Windows -> Linux -> Mac -> Android -> iOS và được mã hóa một chiều trên máy chủ (theo những gì người ta nói) nên dù hacker có hack được cục database thì nó cũng như một cục đất vô tri vô giác. Ngoài ra BItwarden còn hỗ trợ việc chạy máy chủ lưu mật khẩu offline luôn qua Bitwarden Vault hay Vaultwarden, và đây là lý do tại sao mình giới thiệu nó chứ không phải Lasspass.

## FastForward - Bỏ qua thời gian chờ trên một số dịch vụ web[^ff-addon-2]
[**FastForward**](https://addons.mozilla.org/en-US/firefox/addon/fastforwardteam/): Bỏ qua bộ đếm bắt chờ kiểu đợi 30-60s mới được tải và bỏ qua link rút gọn trên mấy trang phổ biến, khá tiện cho ai có sở thích tải ứng dụng được chia sẻ bởi mấy ông chơi kiếm tiền online mà không muốn bị hành xác tốn thời gian.

> ~~**Chú ý:**Addon đã bị xóa khỏi Mozilla do bị report DMCA chơi xấu, chi tiết và cách khắc phục <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24177537>~~
{: .prompt-info }

## New Tab Override - Chuyển hướng trang New Tab
[New Tab Override](https://addons.mozilla.org/en-US/firefox/addon/new-tab-override/) là một tiện ích mở rộng dành cho trình duyệt Firefox, thường được sử dụng để thay đổi trang tab mới (New Tab page) của trình duyệt. Điều này cho phép bạn thay đổi cách trang tab mới được hiển thị và hoạt động, tùy chỉnh nội dung hiển thị trên trang tab mới theo ý muốn của bạn.

# Nguồn:
[^ff-addon-voz]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/>
[^ff-ubo-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24996350>
[^ff-ubo-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24961417>
[^ff-ubo-4]: <https://github.com/gorhill/uBlock/wiki/Advanced-settings#autoupdateperiod>
[^ff-ubo-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25261196>
[^ff-ubo-6]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25582594>
[^ff-ubo-7]: <https://www.reddit.com/r/HobbyDrama/comments/jo9wxn/open_source_development_the_fall_of_nano_defender/>
[^ff-ubo-8]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-376#post-28159390>
[^ff-tabunloader]: <https://firefox-source-docs.mozilla.org/browser/tabunloader/>
[^ff-auto-tab-discard]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24609843>
[^fn-proxy-switchy-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25233313>
[^fn-proxy-switchy-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24766263>
[^fn-proxy-switchy-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27899373>
[^ff-file-centipede-1]: <https://voz.vn/t/tong-hop-software-can-thiet-cho-may-tinh.2974/post-21105427>
[^ff-mdm-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24638856>
[^ff-mdm-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27468734>
[^ff-mdm-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24525109>
[^ff-mdm-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24867468>
[^ff-linguist]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25895858>
[^ff-pwa-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24276732>
[^ff-pwa-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-254#post-27298594>
[^ff-pwa-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-234#post-26996596>
[^ff-pwa-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-280#post-27524899>
[^ff-addon-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/#post-22174347>
[^ff-darkreader-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25633915>
[^ff-darkreader-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-38#post-23570551>
[^ff-darkreader-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-16#post-22949373>
