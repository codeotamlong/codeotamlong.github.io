---
title: "[Firefox Awesome] Các add-on hay ho (P1): uBlock Origin"
date: 2023-09-29 16:00:00 +0700
categories: [awesome, firefox, add-on]
tags: [awesome, firefox, add-on, ublock, ublock origin]     ## TAG names should always be lowercase
---
## [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin) (uBO) - Chặn quảng cáo, tăng cường bảo mật, riêng tư[^footnote]

Đây là add-on chặn quảng cáo đạt tới mức độ chân - thiện - mỹ với thuật toán Regex được tối ưu cho tốc độ và thuật toán nhúng CSS để ẩn nội dụng được chau chuốt, đó là lý do tại sao add-on này tốt hơn nhiều lần Adblock Plus với thuật toán tệ hơn cho hiệu năng tệ hơn.

> Với người dùng Việt Nam thì tất nhiên sau khi cài xong uBlock các bạn vào Dashboard rồi kéo xuống dưới tìm ABPVN rồi bật lên để chặn quảng cáo Việt Nam hiệu quả.
{: .prompt-tip }

Ngoài ra việc chặn quảng cáo sẽ giúp các bạn tránh khỏi những trường hợp dính virus (như đồng chí NFT_God dính virus mất sạch coin do search Google rồi ấn nhầm vào quảng cáo Google).

Cũng như tăng cường sự riêng tư vì các tracker bị chặn luôn, khiến các trang web không theo dõi được bạn.

### Các bộ lọc đáng dùng không lỗi cho uBlock[^fn-nth-2]

Tiếp tục chủ đề về uBlock, add-on #1 ở thread nên phải tiếp tục mở rộng công năng của nó, sau đây là những filter (bộ lọc) hay cho uBlock mà không gây lỗi web, bởi nó là bộ lọc tính năng hoặc chỉ dành cho một đối tượng nhất định nào đó:

- Chặn quảng cáo với Facebook (đối tượng): <https://raw.githubusercontent.com/ethan-xd/ethan-xd.github.io/master/fb.txt>
- Xem các trang đòi trả tiền không tốn xu nào với Bypass Paywall Clean (tính năng): <https://gitlab.com/magnolia1234/bypass-paywalls-clean-filters/-/raw/main/bpc-paywall-filter.txt>
- Nhảy link rút gọn, link theo dõi người dùng với LegitimateURLShortener (tính năng): <https://gitlab.com/DandelionSprout/adfilt/-/raw/master/LegitimateURLShortener.txt>
- Loại bỏ các trang web trùng lặp khỏi kết quả tìm kiếm Google, Duck, Bing... (đối tượng): <https://raw.githubusercontent.com/quenhus/uBlock-Origin-dev-filter/main/dist/all_search_engines/global.txt>

Và không quên lưu ý, luật bất thành văn khi thêm bộ lọc vào uBlock là **luôn thêm bộ lọc `đối tượng` và `tính năng,` tránh xa bộ lọc `chặn`**.

> Bổ sung:
>- [ABPVN](https://abpvn.com/get): <https://abpvn.com/filter/abpvn-PeImlF.txt?ublock>
>- [FMSF2](https://nmtrung.com/fmsf-2/): <https://raw.githubusercontent.com/nmtrung/FMSF-2.0/master/fmsf_2.0.txt>
{: .prompt-info }

### Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^fn-nth-3]

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

Mặc định uBlock cứ 7 tiếng cập nhập filter một lần[^fn-nth-4], thêm vào là xong chả cần làm gì thêm nữa.

### Sử dụng uBlock thay thế NoScript/RequestPolicy để chặn script/ảnh/iframe bằng 2 cái nháy chuột[^fn-nth-5] và Cơ bản cách sử dụng Dynamic Filtering[^fn-nth-6]

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
## Góc drama - Nano Defenders: The shit hits the fan[^fn-nth-7] _Tạm dịch_

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

## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24996350>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24961417>
[^fn-nth-4]: <https://github.com/gorhill/uBlock/wiki/Advanced-settings#autoupdateperiod>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25261196>
[^fn-nth-6]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25582594>
[^fn-nth-7]: <https://www.reddit.com/r/HobbyDrama/comments/jo9wxn/open_source_development_the_fall_of_nano_defender/>