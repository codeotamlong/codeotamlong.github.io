---
title: "[Firefox Awesome] Tại sao lại là Firefox?"
date: 2023-08-28 11:33:00 +0700
categories: [firefox, awesome]
tags: [firefox, awesome]
---
> Linh vật của công ty là một khủng long (`Mozilla`), biểu tượng thì là một con cáo (`fire fox`), nhưng thực chất lại là gấu trúc (`red panda`), và sử dụng engine là một con tác kè (`gecko`)
{: .prompt-info }

## Chrome **KHÔNG** nhanh hơn Firefox [^ff-why-1]

Tốc độ của Chrome _có vẻ_ nhanh hơn Firefox, thực chất là do thuật toán học máy để đoán trước trang web, ví dụ: Bạn vừa gõ `goo`, nó đã biết là `google` rồi và tải sẵn luôn trang web vào bộ nhớ. Tính năng này *đánh lừa* người dùng là Chrome nhanh hơn Firefox: nếu cùng load một nội dung thì cả 02 trình duyệt đều giống nhau, nhưng Chrome giống như bắt đầu chạy từ giữa đường trong khi đối thủ đang đứng từ vạch xuất phát. 

> Vấn đề ở đây cần phải làm rõ là Chrome không hề nhanh hơn Firefox, mà nó có nhiều chiêu trò đánh lừa người dùng khiến họ nghĩ Chrome nhanh hơn.
{: .prompt-warning }

Với Chrome:
: or instance, Chrome, predicts what the user is typing and fires the request even before the user has done typing and hitting enter. By the time they hit enter, the page is ready to load front the cache. This is done with some fair amount of ML.
: _Tạm dịch_
: Ví dụ, trình duyệt Chrome có khả năng dự đoán những gì người dùng đang gõ và gửi yêu cầu trước cả khi người dùng đã gõ xong và nhấn Enter. Khi họ nhấn Enter, **trang web đã sẵn sàng để tải từ bộ nhớ cache**. Điều này được thực hiện thông qua một lượng lớn thuật toán học máy.


Với Firefox (ý nói là Firefox không tải trước trang như Chrome) [^ff-why-2] [^ff-why-3]
: - Firefox will prefetch certain links if any of the websites you are viewing uses the special prefetch-link tag.
: - In order to reduce latency, Firefox will proactively perform domain name resolution on links that the user may choose to follow as well as URLs for items referenced by elements in a web page. 
: - To improve the loading speed, Firefox will open predictive connections to sites when the user hovers their mouse over thumbnails on the New Tab page or the user starts to search in the Search Bar, or in the search field on the Home or the New Tab page. In case the user follows through with the action, the page can begin loading faster since some of the work was already started in advance.
: _Tạm dịch:_
: - Firefox sẽ tìm tải trước trước một số liên kết nhất định _nếu trang web đang truy cập sử dụng thẻ_ `prefetch-link`, ví dụ: `<link rel="prefetch" href="https://example.com/landing-page" />`
: - Để giảm độ trễ, Firefox sẽ chủ động thực hiện _phân giải tên miền_ trên các liên kết mà người dùng có thể chọn theo dõi cũng như URL của các mục được tham chiếu bởi các thành phần trong trang web, ví dụ `<link rel="dns-prefetch" href="https://example.com/" />`. Xem thêm: <https://bitsup.blogspot.com/2008/11/dns-prefetching-for-firefox.html>
: - Để cải thiện tốc độ tải, Firefox sẽ _mở các kết nối_ được dự đoán tới các trang web khi người dùng di chuột qua biểu tượng trên trang `New Tab` hoặc người dùng bắt đầu tìm kiếm trong `Thanh tìm kiếm` hoặc trong trường tìm kiếm trên `Homepage` hoặc trang `New Tab`. Nếu dự đoán đúng, trang có thể bắt đầu tải nhanh hơn vì một số công việc đã được bắt đầu trước.

Ngoài ra rất nhiều người dùng không muốn tính năng này vì nó không tôn trong bảo mật thông tin cá nhân của người dùng, vì chưa vào trang đã tải luôn rồi thì trang web mục tiêu nó đã ghi địa chỉ IP lại rồi, Firefox không thêm tính năng này vì hộ tôn trọng sự bảo mật thông tin người dùng.

Không có cách nào thêm vào Firefox cả vì tính năng này hoạt động khi đang gõ trên thanh địa chỉ, thứ duy nhất có thể khiến Firefox gần giống Chrome là add-on Load Faster này <https://addons.mozilla.org/en-US/firefox/addon/faster-pageload/>, nó khiến Firefox tải trang vào bộ nhớ khi đặt chuột lên link, Chrome cũng có tính năng này, bạn cứ dùng Chrome, đặt chuột lên một link bất kỳ, đợi 3s rồi ấn phát vào link là trang hiện ra tức thì không cần tải. Cơ mà như trên, tính năng này không tôn trọng quyền riêng tư của người dùng.

Tóm lại học được gì qua những gì mình nói:

> Chrome nó tải nguyên trang web (DNS, HTML) vào RAM ngay khi bạn chưa gõ xong tên trang web, khi đặt chuột lên link.
>
> Firefox mặc định chỉ tải trước DNS, không hề có HTML nên đó là lý do tại sao Firefox cảm giảc chậm hơn
{: .prompt-info }

## uBlock Origin làm việc tốt nhất trên Firefox (uBO works best on Firefox) [^ff-why-4] _Tạm dịch - Đọc bản gốc để hiểu rõ hơn_
Truy nguyên CNAME
: ![Desktop View](https://user-images.githubusercontent.com/585534/103416937-b623c400-4b56-11eb-8e94-b4851a2248b7.png)
: _Nguồn: "Characterizing CNAME Cloaking-Based Tracking on the Web"[^ff-why-5], Asia Pacific Network Information Centre[^ff-why-6], August 2020._ (Cao hơn là tốt hơn)

Lọc HTML (HTML filtering)
: HTML filtering là khả năng lọc nội dung phản hồi của HTML trả về trước khi trình duyệt xử lý, cho phép xóa các thẻ cụ thể trong HTML. Tính năng này yêu cầu API `webRequest.filterResponseData()`, hiện chỉ có trên `Firefox`.

Khởi chạy trình duyệt
: _Firefox sẽ đợi uBO sẵn sàng_ trước khi gửi yêu cầu mạng từ (các) tab đã mở khi khởi chạy trình duyệt. 

Nạp trước (Pre-fetching)
: uBO mặc định tắt tính năng pre-fetching.
: Tham khảo: <https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-prefetching>

WebAssembly
: Phiên bản Firefox của uBO sử dụng mã WebAssembly
: Thông tin thêm: <https://github.com/WebAssembly/content-security-policy/issues/7#issuecomment-441259729>

Nén lưu trữ
: Firefox uBO mặc định  sử dụng `nén LZ4` theo để lưu trữ. LZ4 yêu cầu sử dụng `IndexedDB`, điều này không hiệu quả với trình duyệt nền Chromium (xem [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399) ). `IndexedDB` là bắt buộc vì nó hỗ trợ lưu trữ Blob, `browser.storage.localAPI` không hỗ trợ.

> Chrome gần đây thì thể hiện thế độc quyền thấy rõ, mà mục tiêu chính là họ muốn biến trình duyệt web thành môi trường cho quảng cáo:
{: .prompt-info }

## Manifest V3 triệt hạ khả năng chặn quảng cáo của trình duyệt. Tham khảo: Sự khác biệt của uBlock Firefox vs Chrome vs Manifest V3 vs Adguard[^ff-why-7]

Tiện nhắc tới uBlock mình viết một bài phân tích sự khác biệt giữa:
- uBlock của Firefox và uBlock của Chrome
- uBlock Manifest V2 vs uBlock Manifest V3
- uBlock và Adguard

### uBlock của Firefox và uBlock của Chrome

Hiệu năng:
: - Biến code thành mã máy: uBlock của Firefox nhanh hơn rất nhiều lần uBlock của Chrome (cũng như Adguard), vì uBlock của Firefox hỗ trợ WebAssembly, nghĩa là khi lọc trang web, uBlock biến code từ Javascript thành mã máy, khiến tăng tốc quá trình lọc lên rất rất nhiều lần. Để nói về hiệu năng của Web Assembly so với Javascript thì nếu bạn học lập trình bạn sẽ thấy nó có ngôn ngữ thông dịch (interpreted language) và ngôn ngữ biên dịch (compiled language), sự khác biệt về hiệu năng giữa Web Assembly và Javascript như so sánh trời với đất, nó gấp rất rất nhiều lần, cũng y như so trình xem HTML của Firefox/Chrome (viết bằng HTML5=HTML+Javascript) với MPV (viết bằng C nguyên chất) vậy.
: - Sử dụng IndexedDB thay vì localStorage: IndexedDB có hiệu năng tốt hơn nhiều localStorage nên khi mở Firefox lên, uBlock hoạt động ngay lập tức sau 0.5s (đối với con máy cùi bép của mình), nhưng với Chrome thì nếu bạn mở ngay trang web, khả năng lớn là quảng cáo sẽ lọt vì Chrome dùng localStorage chứa các bộ lọc của uBlock, nhiều người từng trải nghiệm uBlock trên Chrome tốn 15 phút để load xong các bộ lọc.

> Tham khảo: 
>
> <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#browser-launch> 
>
> <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#storage-compression>
{: .prompt-info }

> Chi tiết:
>
> <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#webassembly>
{: .prompt-info }

Tính năng:
: uBlock của Firefox hỗ trợ bóc tách CNAME của tên miền, giúp tìm ra những tên miền con cùng là một bố mẹ đẻ ra rồi chặt luôn một thể, nên kết quả là uBlock nghiễm nhiên chặn nhiều quảng cáo hơn mà không tốn công sức: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#cname-uncloaking>
: uBlock của Firefox hỗ trợ lọc nội dung web, giúp thoải mái cắt xén trang web, chặn những quảng cáo mà bình thường không thể chặn được.

Tham khảo: 
: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox#html-filtering>
: [Cách sửa mọi thứ trong trang web, phá tan nát trang web, chặn những quảng cáo gần như khó nhất với Header Editor](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25473236)

### uBlock (Adblock) Manifest V2 vs uBlock (Adblock) Manifest V3 (_Áp dụng cho mọi tiện ích chặn quảng cáo viết bằng Manifest V3_)

AdBlock Manifest V3 
: - **Không thể tự động cập nhập bộ lọc**, trong khi thế giới web các trang web thay đổi cứ vài giây một lần, thêm sửa quảng cáo, không tự động cập nhập được nghĩa là thành phế
: - **Không thể có nhiều hơn 30.000 rule** (dòng chặn, chi tiết: [MV3: overcoming the 30000 rules limit](https://old.reddit.com/r/uBlockOrigin/comments/xlw1wi/mv3_overcoming_the_30000_rules_limit/)), trong khi số lượng trang web tăng không ngừng mỗi ngày, ngoài ra adblock còn được dùng để chặn các trang có nội dung malware nữa nên thậm chí để an toàn thì một người dùng cần dùng tới hàng triệu rule, ví dụ như chỉ để chặn các tên miền mới tạo ra trong vòng 31 ngày đã ngốn nguyên 3 triệu rule: Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^ff-why-3]
: - **Dừng hoạt động sau khi trang tải xong một thời gian** ([5 phút](https://old.reddit.com/r/learnjavascript/comments/10jmkc4/how_to_prevent_service_worker_from_going_inactive/)), nghĩa là sẽ vô dụng với các trang web động sử dụng AJAX như Youtube/Facebook vì một lúc sau khi tải xong sẽ không còn chặn quảng cáo nữa, khiến quảng cáo hiện ra

Còn đây là thông tin do chính `gorhill` cung cấp.[^ff-why-7]: 

> uBO Lite:
>
> - Filter lists update only when the extension updates (no fetching up to date lists from servers)
> - Many filters are [dropped at conversion time](https://github.com/gorhill/uBlock/blob/master/dist/mv3/log.txt) due to MV3's limited filter syntax
> - No [crafting your own filters](https://github.com/gorhill/uBlock/wiki/Dashboard:-My-filters) (thus no [element picker](https://github.com/gorhill/uBlock/wiki/Element-picker))
> - No [strict-blocked](https://github.com/gorhill/uBlock/wiki/Strict-blocking) pages
> - No [per-site switches](https://github.com/gorhill/uBlock/wiki/Per-site-switches)
> - No [dynamic filtering](https://github.com/gorhill/uBlock/wiki/Blocking-mode)
> - No [importing external lists](https://github.com/gorhill/uBlock/wiki/Dashboard:-Filter-lists#3rd-party-filter-lists)

### uBlock và Adguard

Gần như giống nhau, thích dùng gì thì dùng, nhưng uB0 trên Firefox:

- Hiệu năng tốt hơn do sử dụng Web Assembly, đã được xác nhận đóng dấu trên trang liệt kê các ứng dụng sử dụng Web Assembly (WASM) trên kèm benchmark hiệu năng: (https://madewithwebassembly.com/showcase/ublock-origin/)
: uBlock Origin is a very popular add-on, and uses WebAssembly for multiple parts of it's codebase. The most notable being, uBlock Origin uses Wasm for hostname lookup for it's data structures that contain the list of origins it intends to block. This is a great use of WebAssembly, as it offered them better performance, compared to a JavaScript implementation, in the web browser for doing computationally intensive processing tasks over a large set of data. This can be tested in your own browser, by checking out the [benchmark](https://raw.githack.com/gorhill/uBlock/master/docs/tests/hnset-benchmark.html).
: _Tạm dịch_
: uBlock Origin là một tiện ích bổ sung rất phổ biến và sử dụng WebAssugging cho nhiều phần của cơ sở mã của nó. Điều đáng chú ý nhất là uBlock Origin sử dụng Wasm để tra cứu tên máy chủ cho cấu trúc dữ liệu chứa danh sách nguồn gốc mà nó dự định chặn. Đây là một công dụng tuyệt vời của WebAssugging vì nó mang lại cho chúng hiệu suất tốt hơn so với việc triển khai JavaScript trong trình duyệt web để thực hiện các tác vụ xử lý chuyên sâu về mặt tính toán trên một tập hợp dữ liệu lớn. Điều này có thể được kiểm tra trong trình duyệt của riêng bạn, bằng cách kiểm tra điểm chuẩn.


- Hỗ trợ HTML Filtering, một tính năng giúp lọc và xóa triệt để nội dung web, giúp trị những quảng cáo khó nhằn nhất cũng như xóa triệt để nội dung web thì sẽ loại bỏ được kết nối ngầm, từ đó tối đa tốc độ tải trang:
: Xem thêm: [Chặn quảng cáo kiểu triệt hạ với uBlock sử dụng tính năng HTML Filtering](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27879329) (chỉ hỗ trợ uBlock cho Firefox) (Ví dụ: [Xóa triệt thanh sidebar ở trang chủ Voz khiến trang load nhanh như điện](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27879524))

Nhìn kỹ số lượng kết nối ở 2 cái spoiler.

![](https://voz.vn/attachments/1695314107674-png.2085528/)
_Ẩn (chỉ dùng bộ lọc thông thường)_
VS
![](https://voz.vn/attachments/1695314749241-png.2085538/)
_Xóa (sử dụng HTML Filtering)_

Vậy chốt lại là uBlock trên Firefox hơn Adguard ở những điểm:
: Biến mã thông dịch Javascript thành mã máy WebAssembly, tăng tốc độ lọc
: Lọc và xóa triệt để nội dung web ở cấp độ mã nguồn, nghĩa là trước khi nó xuất hiện trên màn hình
: Lọc CNAME một cách tự động, không cần phụ thuộc vào một bộ lọc thủ công nào cả

> Nghĩa là nếu dùng **Firefox thì uBlock có nhiều tính năng hơn**, còn dòng Chrome thì cả hai như nhau như đã nói bên trên, thích dùng gì thì dùng.
{: .prompt-info}

> Ngoài ra mã nguồn Scriptlets của uBlock nuột hơn Adguard do Adguard dùng Webpack, là kiểu đóng gói code Javascript nhưng hiệu năng luôn kém hơn uBlock là native Javascript, và mặc định cả Adguard và uBlock đều sử dụng Scriptlets để trị quảng cáo khó nhằn như Youtube, Twitch...
{: .prompt-tip }
## Privacy Sandbox quảng cáo bằng cách địa lịch sử duyệt web của người dùng.[^ff-why-8][^ff-why-11]

[Google Chrome vừa chính thức bật tính năng `Privacy Sandbox` lên tất cả phiên bản Chrome mới](https://arstechnica.com/gadgets/2023/09/googles-widely-opposed-ad-platform-the-privacy-sandbox-launches-in-chrome/), tính năng này chính là FLoC[^ff-why-12](Federated Learning of Cohorts, chạy trong trình duyệt Chrome của Google và theo dõi hành vi trực tuyến, cho phép dịch vụ quảng cáo xác định tệp khách hàng dựa trên hành vi mà không cần cookie) cải biên do trước định thực hiện nhưng người dùng chửi cho nát mặt nên giờ lươn lẹo đổi tên thành `Privacy Sandbox`, nghe tên rất chi là riêng tư cơ mà nó ngược lại hoàn toàn,cho phép trình duyệt web lấy lịch sử duyệt web của người dùng, tóm tắt lại rồi gửi cho trang web để họ tạo quảng cáo, ví dụ:

- Một ông hay vào web pỏn, hay xem bóng đá, hay vào sọp bee
- Google Chrome gửi cho trang web lịch sử duyệt web cho trang web sử dụng Privacy Sandbox
- Trang web phân tích lịch sử duyệt web và tạo ra quảng cáo cực kỳ khớp với sở thích bệnh hoạn của người dùng

Đó là Privacy Sandbox, một tính năng được quảng cáo là giúp loại bỏ 3rd party cookie, cơ mà các trình duyệt như Safari hay Firefox đều có phương pháp trị dạng cookie này (với Safari là tắt hoàn toàn, với Firefox thì cô lập bằng Total Cookie Protection) nên việc Chrome vẫn còn lưu luyến với 3rd party cookie là do họ muốn Chrome hỗ trợ quảng cáo tốt hơn (đây là mình giải thích cho hiểu tại sao hoàn toàn có thể tắt 3rd party cookie mà Chrome không làm).

> Câu hỏi là liệu Google có ép Firefox phải thêm tính năng này vào vì trước Firefox đã phải thêm Widevine (WebDRM, cứ vào Netflix, Spotify bằng Floorp/Ungoogled/Cromite sẽ hiểu) rồi? Bởi nên nhớ tiền mua sữa cho con của các kỹ sư Mozilla 500 củ đô la / 1 năm là do Google trả.
{: .prompt-danger }

![](https://cdn.arstechnica.net/wp-content/uploads/2023/09/image-5-980x1098.png)

> Nguồn:
>
> <https://arstechnica.com/gadgets/2023/09/googles-widely-opposed-ad-platform-the-privacy-sandbox-launches-in-chrome/>
>
> <https://www.reddit.com/r/browsers/comments/16cvuyk/>
{: .prompt-info}

Mặc định nó nằm trong nhân trình duyệt thủy tổ là Chromium rồi, phải xóa bằng tay
: Nghĩa là Google nó chơi bẩn ở mức tính năng này được cho vào là tính năng bản lề, là một phần của chuẩn web nên nó cho thẳng luôn vào Chromium (thằng mà từ đó sinh ra Brave, Cromite, Opera, Vivaldi và tất nhiên là cả **Edge** và **Chrome**).

Hiện tại chưa thấy Edge nói gì về việc xóa hay không, sợ là theo luôn Chrome cho tính năng này thành chuẩn web.

Chromium là mã nguồn mở mà không hề mở, nghĩa là những người được phép thêm thắt tính năng mới đương nhiên là nhân viên ruột của Google, còn mấy ông contributor chỉ tạo mấy cái sửa lỗi vớ va vớ vẩn và cũng phải bợ đít lắm mới được duyệt. Còn Google Chrome thì tất nhiên là **mã nguồn đóng** rồi, có rất nhiều code người dùng không thể đọc.

Mã nguồn chứng tỏ trình duyệt dựa trên Chromium phải xóa tay: <https://github.com/ungoogled-software/ungoogled-chromium/blob/master/patches/core/ungoogled-chromium/disable-privacy-sandbox.patch>

## Widevine triệt hạ trình duyệt web mới nối bên thứ ba [^ff-why-9]

> Nghĩa là để xem được các trang Netflix, Spotify... thì tác giả trình duyệt mới phải quỳ lạy, van xin Google cấp cho, mà thường thì 1-2 năm không có phản hồi, dù rằng các trình duyệt web này đều tốt hơn Chrome gốc (Cromite, Ungoogled, Floorp...). 
{: .prompt-warning}

Nghe nói thằng này mới cải thiện hiệu năng, nhìn chung đã chơi nhân Chromium thì cứ fork mà táng thôi chứ Chrome mới chính ra là thằng cùi bắp nhất hội.

Cái khó là bị vụ WebDRM (Widevine) nghĩa là mấy bản fork sẽ không xem được Netflix hay Spotify, dù nó ngon như Cromite/Ungoogled. Quy trình cấp phép Widevine của Google cũng nhiêu khê lắm, phải chìa tay ra xin Google và đợi họ ban ơn. :D
 
## Environment Intergrity[^ff-why-10]

> WebDRM nghĩa là trang web sẽ được phép cho phép một số trình duyệt vào ngoại lệ, còn không chặn hết, nghĩa là nếu lập trình viên web thấy Chrome phổ biến nhất sẽ chặn tất cả những cái khác và chỉ cho người dùng Chrome vào web của họ.
{: .prompt-warning }

Người tính không bằng Google tính, họ đã biết trước bối cảnh một ngày các trình duyệt ăn theo như Bromite/ Cromite/ Ungoogled/ Brave.. sẽ trở nên phổ biến và ăn thị phần của Chrome do Chrome liên tục ra các chính sách khiến người dùng xóa Chrome như MV3, Privacy Sandbox, Web Environment Intergrity... nên mới ra cái DRM này như đòn chí mạng khiến các trình duyệt trên không bao giờ sánh được với Chrome gốc, và mấu chốt ở đây muốn có DRM Widevine phải chìa tay ra xin Google - Còn Google **CHO hay KHÔNG** là do **GOOGLE**.

Thông tin chi tiết thì cả Firefox và Chrome đang dùng Widevine L3 (cấp độ 3 - không chua cay mặn ngọt), còn xịn nhất là Widevine L1 (cấp cao nhất - siêu cay) ở các thiết bị Android:

Trích <https://github.com/ungoogled-software/ungoogled-chromium/issues/2194>
: Hi so I followed #2124 but I'm on the portable version 108.0.5359.125 (Official Build, ungoogled-chromium) (64-bit) so I don't have this path %localappdata%\Chromium\Application the one I have is this : C:\Users\USER\AppData\Local\Chromium\User Data\WidevineCdm and I downloaded 4.10.2557.0-win-x64 of the Widevine CDM plugin and paste it as the guide suggested but when I go to chrome://components/ the version still 0.0.0.0 any i deas?
: **@PF4Public** closed this as not planned (won't fix, can't repro, duplicate, stale)


Trích comment của `u/LukaD-S` trên r/browsers <https://www.reddit.com/r/browsers/comments/15690l9/comment/jt04xdi/>
: I can watch/play those services in Floorp, albeit only with them capped at 720p max resolution / 192kbps audio. The Widevine license you guys use is the same as Firefox's which should be Widevine L3.
: Google doesn't easily provide Widevine L1, which is what enables on their services to play 4K and max audio quality due to licensing issues and weird stupid factors that they deem necessary. It's mostly present in partnered Smartphones / Smart TVs / Android TV Box / Android OS / etc.
:  To make things even funnier, Chrome on Desktop also only uses Widevine L3 even though it is a Google Product. 🤦
: On Windows only choice to watch 4K content / Max audio quality is to either use Edge (Hardware DRM PlayReady) or the App itself from Windows Store in case of Netflix or Spotify's App respectively
: PS: I hate DRM worst stupid thing ever created that gives unfair treatment to alternative browsers.

> Thread này không chỉ về Firefox mà còn chứa lượng kiến thức không nhỏ về thế giới web, ít nhất cũng hiểu được tại sao lại thế lọ thế chai. :D
{: .prompt-info }

# Các bản Firefox mod hay ho

## Lợi ích gì khi sử dụng các bản mod của Firefox? [^ff-mod-1]

Tốc độ
: Firefox zin mặc định không được biên dịch (compile) bằng các tập lệnh tối ưu, mà thực tế ra được biên dịch bằng các tập lệnh tối ưu khiến Firefox mượt lên rất nhiều mà tier list là SSE > SSE2 > SSE3 > AVX2, nhược điểm là càng lên cao độ tương thích phần cứng càng giảm, yêu cầu các hệ máy mới hơn.

Tính năng mới
: Tùy theo từng bản mod mà được tích hợp các tính năng hữu ích như Portable, ẩn địa chỉ IP, chống theo dõi...

## Các bản mod hay ho, uy tín của Firefox

| Thuật ngữ | Giải thích |
|:--------:|:----------|
| Privacy  | Riêng tư |
| Portable | Không cần cài đặt, không để lại rác, cho vào USB/mang sang máy khác giữ 100% dữ liệu|
| Adblock  | Chặn quảng cáo dạng native |
| SSE2/AVX/LTO<br>_các từ khóa đầu tiên_ | Tập lệnh tăng tốc biên dịch|

### Firefox Tete009 - SSE2/AVX2+Portable

Nếu như nói tới bản mod uy tín và lâu đời nhất (từ Firefox 2 nghĩa là 2006 tới nay), không thể không nói tới tete009, bản mod này được biên dịch tối ưu bằng tập lệnh SSE2 nên tương thích với đa phần hệ máy thời nay, giúp tăng tốc độ xử lý so với Firefox thường, ngoài ra tác giả áp dụng rất nhiều lệnh tối ưu PGO trong suốt mấy chục  năm trời nên nhìn chung về độ uy tín và an toàn là không có gì bản. Bản này không khác gì Firefox thường, tuy nhiên có thể biến thành Portable 100% không cần Launcher như Portableapps.

Hiện tại (14/9/23) Tete đã chính thức lên kệ AVX2.

Ngoài ra một điểm mạnh nữa của tete là bản này là bản stable nhưng lại là Nightly, nên nó có thể cài được Fastforward, Multi-Threaded Download Manager và iMacros.

> Download: <http://www1.plala.or.jp/tete009/en-US/software.html#FFDL>
{: .prompt-info }

> Folder chứa các bản cũ (có cả 32bit): <https://drive.google.com/drive/folders/0BwJVYWis62cRalRwX2tsZklqUkk>
{: .promtp-info }

#### Cách đặt Tete thành Firefox Portable xịn Pin được, đặt Default Browser được: [^ff-tete-1]

Tạo một file tên `tmemutil.ini` cùng folder với `firefox.exe`:

```
[General]
Portable=1
PortableDataPath=PortableData
CreateCrashDump=0
CrashDumpType=0
GdiBatchLimit=0
ProcessAffinityMask=0

[Env]
MOZ_LEGACY_PROFILES=1
```
{: file="tmemutil.ini"}

#### Cách đặt Tete Portable thành Default Browser:[^ff-tete-2]

Tạo file `firefox.vbs` cùng folder với `firefox.exe` rồi chạy:

```
'Registers Firefox Portable with Default Programs or Default Apps in Windows
'firefoxportable.vbs - created by Ramesh Srinivasan for Winhelponline.com
'v1.0 17-July-2022 - Initial release. Tested on Mozilla Firefox 102.0.1.0.
'v1.1 23-July-2022 - Minor bug fixes.
'v1.2 27-July-2022 - Minor revision. Cleaned up the code.
'Suitable for all Windows versions, including Windows 10/11.
'Tutorial: https://www.winhelponline.com/blog/register-firefox-portable-with-default-apps/

Option Explicit
Dim sAction, sAppPath, sExecPath, sIconPath, objFile, sbaseKey, sbaseKey2, sAppDesc
Dim sClsKey, ArrKeys, regkey
Dim WshShell : Set WshShell = CreateObject("WScript.Shell")
Dim oFSO : Set oFSO = CreateObject("Scripting.FileSystemObject")

Set objFile = oFSO.GetFile(WScript.ScriptFullName)
sAppPath = oFSO.GetParentFolderName(objFile)
sExecPath = sAppPath & "\firefox.exe"
sIconPath = sAppPath & "\firefox.exe"
sAppDesc = "Firefox delivers safe, easy web browsing. " & _
"A familiar user interface, enhanced security features including " & _
"protection from online identity theft, and integrated search let " & _
"you get the most out of the web."

'Quit if FirefoxPortable.exe is missing in the current folder!
If Not oFSO.FileExists (sExecPath) Then
   MsgBox "Please run this script from Firefox Portable folder. The script will now quit.", _
   vbOKOnly + vbInformation, "Register Firefox Portable with Default Apps"
   WScript.Quit
End If

If InStr(sExecPath, " ") > 0 Then
   sExecPath = """" & sExecPath & """"
   sIconPath = """" & sIconPath & """"
End If

sbaseKey = "HKCU\Software\"
sbaseKey2 = sbaseKey & "Clients\StartmenuInternet\Firefox Portable\"
sClsKey = sbaseKey & "Classes\"

If WScript.Arguments.Count > 0 Then
   If UCase(Trim(WScript.Arguments(0))) = "-REG" Then Call RegisterFirefoxPortable
   If UCase(Trim(WScript.Arguments(0))) = "-UNREG" Then Call UnRegisterFirefoxPortable
Else
   sAction = InputBox ("Type REGISTER to add Firefox Portable to Default Apps. " & _
   "Type UNREGISTER To remove.", "Firefox Portable Registration", "REGISTER")
   If UCase(Trim(sAction)) = "REGISTER" Then Call RegisterFirefoxPortable
   If UCase(Trim(sAction)) = "UNREGISTER" Then Call UnRegisterFirefoxPortable
End If

Sub RegisterFirefoxPortable 
   WshShell.RegWrite sbaseKey & "RegisteredApplications\Firefox Portable", _
   "Software\Clients\StartMenuInternet\Firefox Portable\Capabilities", "REG_SZ"
 
   'FirefoxHTML registration
   WshShell.RegWrite sClsKey & "FirefoxHTML2\", "Firefox HTML Document", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\EditFlags", 2, "REG_DWORD"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\FriendlyTypeName", "Firefox HTML Document", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\DefaultIcon\", sIconPath & ",1", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\shell\", "open", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\shell\open\command\", sExecPath & _
   " -url " & """" & "%1" & """", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\shell\open\ddeexec\", "", "REG_SZ"
 
   'FirefoxPDF registration
   WshShell.RegWrite sClsKey & "FirefoxPDF2\", "Firefox PDF Document", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxPDF2\EditFlags", 2, "REG_DWORD"
   WshShell.RegWrite sClsKey & "FirefoxPDF2\FriendlyTypeName", "Firefox PDF Document", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxPDF2\DefaultIcon\", sIconPath & ",5", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxPDF2\shell\open\", "open", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxPDF2\shell\open\command\", sExecPath & _
   " -url " & """" & "%1" & """", "REG_SZ"
 
   'FirefoxURL registration
   WshShell.RegWrite sClsKey & "FirefoxURL2\", "Firefox URL", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\EditFlags", 2, "REG_DWORD"
   WshShell.RegWrite sClsKey & "FirefoxURL2\FriendlyTypeName", "Firefox URL", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\URL Protocol", "", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\DefaultIcon\", sIconPath & ",1", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\shell\open\", "open", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\shell\open\command\", sExecPath & _
   " -url " & """" & "%1" & """", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxURL2\shell\open\ddeexec\", "", "REG_SZ" 
 
   'Default Apps Registration/Capabilities
   WshShell.RegWrite sbaseKey2, "Firefox Portable", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "Capabilities\ApplicationDescription", sAppDesc, "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "Capabilities\ApplicationIcon", sIconPath & ",0", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "Capabilities\ApplicationName", "Firefox Portable", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "Capabilities\FileAssociations\.pdf", "FirefoxPDF2", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "Capabilities\StartMenu", "Firefox Portable", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "DefaultIcon\", sIconPath & ",0", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "shell\open\command\", sExecPath, "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "shell\properties\", "Firefox &Options", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "shell\properties\command\", sExecPath & " -preferences", "REG_SZ"
   WshShell.RegWrite sbaseKey2 & "shell\safemode\", "Firefox &Safe Mode", "REG_SZ" 
   WshShell.RegWrite sbaseKey2 & "shell\safemode\command\", sExecPath & " -safe-mode", "REG_SZ"
 
   ArrKeys = Array ( _
   "FileAssociations\.avif", _
   "FileAssociations\.htm", _
   "FileAssociations\.html", _
   "FileAssociations\.shtml", _
   "FileAssociations\.svg", _
   "FileAssociations\.webp", _
   "FileAssociations\.xht", _
   "FileAssociations\.xhtml", _
   "URLAssociations\http", _
   "URLAssociations\https", _
   "URLAssociations\mailto" _
   )
 
   For Each regkey In ArrKeys
      WshShell.RegWrite sbaseKey2 & "Capabilities\" & regkey, "FirefoxHTML2", "REG_SZ"
   Next    
 
   'Override the default app name by which the program appears in Default Apps  (*Optional*)
   '(i.e., -- "Mozilla Firefox, Portable Edition" Vs. "Firefox Portable")
   'The official Mozilla Firefox setup doesn't add this registry key.
   WshShell.RegWrite sClsKey & "FirefoxHTML2\Application\ApplicationIcon", sIconPath & ",0", "REG_SZ"
   WshShell.RegWrite sClsKey & "FirefoxHTML2\Application\ApplicationName", "Firefox Portable", "REG_SZ"
 
   'Launch Default Programs or Default Apps after registering Firefox Portable 
   WshShell.Run "control /name Microsoft.DefaultPrograms /page pageDefaultProgram"
End Sub


Sub UnRegisterFirefoxPortable
   sbaseKey = "HKCU\Software\"
   sbaseKey2 = "HKCU\Software\Clients\StartmenuInternet\Firefox Portable" 
 
   On Error Resume Next
   WshShell.RegDelete sbaseKey & "RegisteredApplications\Firefox Portable"
   On Error GoTo 0
 
   WshShell.Run "reg.exe delete " & sClsKey & "FirefoxHTML2" & " /f", 0
   WshShell.Run "reg.exe delete " & sClsKey & "FirefoxPDF2" & " /f", 0
   WshShell.Run "reg.exe delete " & sClsKey & "FirefoxURL2" & " /f", 0
   WshShell.Run "reg.exe delete " & chr(34) & sbaseKey2 & chr(34) & " /f", 0
 
   'Launch Default Apps after unregistering Firefox Portable 
   WshShell.Run "control /name Microsoft.DefaultPrograms /page pageDefaultProgram" 
End Sub

```
{: file="firefox.vbs"}

### Floorp - LTO+Portable+Sidebar+VerticalTab+Workspace+UnloadTab+...

Bản Firefox mod của tác giả người Nhật mới nổi thời gian gần đây trên các trang Reddit như /r/browsers, /r/firefox bởi nó cũng khá là đặc sắc khi so với Firefox gốc, mà cái đặc sắc nằm ở:
: Sidebar bên tay phải để mở nhanh các tính năng như bookmark, history, add-ons... (native)
: Hỗ trợ giao diện đẹp như Lepton, Chrome, Edge (cứ vào Settings là thấy)
: Ngủ đông tab giống Auto Tab Discard cơ mà tốt hơn vì nó unload nhiều hơn, và là native
: Hỗ trợ tab dọc (native)
: Hỗ trợ đổi phím tắt tùy ý (native)
: Workspace giống Vivaldi để quản lý tab theo từng vùng một cho gọn, ví dụ chia ra cho: Công việc, Cá nhân, Ăn chơi... (native)
: Tối ưu bằng tập lệnh PGO+LTO nên nhanh hơn cả tete (SSE2+PGO) và thậm chí Mercury (AVX) mà vẫn giữ nguyên tính tương thích với hệ máy cũ chứ không như AVX kén hệ máy mới
: Và nhiều tùy chỉnh nhỏ khác nữa rất khó liệt kê hết vì nói chung nó nằm trong Settings ấy...

> Download: <https://github.com/Floorp-Projects/Floorp/releases>
{: .prompt-info }

## Cách nhảy các bản mod Firefox không lo mất dữ liệu [^ff-backup-restore]
1. Đầu tiên ở Firefox đang dùng, gõ `about:support` rồi xem phần `Application Binary`, mở thư mục chứa `firefox.exe` lên
2. Tải bản mod dạng nén như 7z, zip, rar... về rồi giải nén thẳng vào thư mục chứa `firefox.exe`
3. Nếu mở lên báo lỗi không tương thích thì vào folder `profile` xóa file `compatibility.ini` đi là xong

## Làm sao tạo mới profile mà vẫn giữ được 90% dữ liệu ?

Đây là một bài viết mà sau khi đọc xong bạn có một cái nhìn toàn tổng về profile của Firefox, giúp bạn xoay sở trong những tình huống khó nhất.

### Mục tiêu
- Giữ được bookmark, history
- Giữ được mật khẩu
- Giữ được đăng nhập
- Giữ được about:config
- Giữ được add-on đã cài (tuy nhiên mất hết tùy chỉnh của add-on)

### Sau lưu (Backup)

`about:support`
: => _Open Profile Folder_

Copy những file sau:
: Nén vào 1 file .zip cho nó không bị sót

|----------------------------------|-------------------|
| File/Folder                      | Tác dụng          |
|:---------------------------------|:------------------|
| places.sqlite                    | Bookmark; History |
| cookies.sqlite                   | Cookies           |
| - cert9.db<br> - key4.db<br> - logins.json | Mật khẩu|
| - extension-preferences.json<br> - extensions.json<br> - extension-settings.json<br> - Thư mục `extensions` | Add-ons |
| prefs.js                         | about:config      |
| Thư mục `storage`                | Tùy chỉnh add-on <br>*không đảm bảo 100%*|
| Thư mục `chrome`                 | Giao diện         |
| handlers.json                    | Protocol (_để sau mở Youtube bằng mpv_) |
| - prefsCleaner.bat<br> (- prefsCleaner.sh) | Reset `about:config` mặc đinh<br>(_tùy hệ điều hành_ - Đồ của @arkenfox) |

### Khôi phục (Restore)

`about:support`
: => _Open Profile Folder_

**Tắt hẳn** Firefox
: Copy **toàn bộ** các thứ đã lưu bên trên

Chạy `prefsCleaner.bat` (hoặc `prefsCleaner.sh` - tùy hệ điều hành)
: Reset lại `cài đặt`

#### Nếu muốn tạo profile mới

`about:profiles`
: Create a new profile -> Chọn thư mục -> Launch profile

`about:support`
: Open Profile Folder -> Tắt Firefox -> Paste vào.

> Đừng quên `Set as Default Profile` cho cái profile mới tạo để từ nay nó là profile chính.
{: .prompt-info }

> Chú ý trên MacOS phân biệt Quit (Tắt) và Close (Đóng), nên là cần chắc chắn là đã QUIT hẳn Firefox
{: .prompt-tip }

## Góc drama -  Giải "ảo" Adguard tốt hơn uBlock? [^ff-why-13] _Tạm dịch_ (Bài viết của @gorhill - Tác giả uBO)

Cụ thể hơn, việc vạch trần [@christianbute](https://twitter.com/christianbute) phát ngôn <https://twitter.com/christianbute/status/893462816270815232>. Hai tweet được trích dẫn nguyên văn:

> Theo thử nghiệm của tôi, trình chặn quảng cáo và phần mềm độc hại tốt nhất cho @MicrosoftEdge là AdGuard. Bất cứ điều gì khác chỉ làm cho hiệu suất tồi tệ hơn.
>
> Có, ngay cả uBlock Origin cũng làm chậm trải nghiệm duyệt web của tôi. Trên cài đặt chứng khoán hoặc danh sách tùy chỉnh, không thành vấn đề. Không muốn nhắc tới người khác

Rất tiếc, tôi không thể điều tra khiếu nại này trên Microsoft Edge vì tôi không có Windows. Tuy nhiên, cả hai extension đều sử dụng cùng một mã trên Microsoft Edge giống như trên Chrome, do đó ít nhất tôi có thể điểm chuẩn với Chrome.

Các phép đo khách quan của tôi, benchmark trên Chrome 59 trên Linux 64-bit:

uBO 1.13.8
: cài đặt/danh sách mặc định
: tất cả các danh sách được cập nhật

Adguard 2.6.7
: Bộ lọc tiếng Anh + phần mềm gián điệp
: tắt "Cho phép tự quảng cáo của quảng cáo tìm kiếm và trang web"
: tất cả các danh sách được cập nhật

### Các bước thực hiện

- Khởi chạy Chrome chỉ khi bật một trong các trình adblocker
   + với tab Extension được ghim + chỉ một tab mới
   + không có phần mở rộng nào khác
- Mở Task manager của riêng Chromium, đợi dọn rác extension
- Mở trang nền của extension, chọn khung "Performance"
- Nhấp vào nút "Record" trong khung Performance
- Chọn "New Tab" đã mở trong trình duyệt
- Nhấp chuột phải vào thư mục bookmark 20 tab (xem bên dưới) và chọn "Open all bookmarks"
- Đợi tất cả các tab được tải
- Kích hoạt lần lượt từng tab mới mở
- Nhấp vào nút "Stop" trong khung Hiệu suất
- Kết quả ảnh chụp màn hình trong ngăn "Performance"

Đối với điểm chuẩn "memory usage": tất cả các bước tương tự ngoại trừ các công cụ extension dành cho nhà phát triển không được mở và chỉ tính đến Task manager. Đợi ít nhất 2 phút sau bước 8. trước khi chụp ảnh màn hình Task manager.

20-tab thư mục dấu trang trong thanh dấu trang (được đọc từ các bài đăng hàng đầu trên Tin tức Hacker trong năm qua, do đó "sử dụng thực tế"):

```
http://www.hntoplinks.com/year/2
https://www.susanjfowler.com/blog/2017/2/19/reflecting-on-one-very-strange-year-at-uber
http://www.nature.com/news/these-seven-alien-worlds-could-help-explain-how-planets-form-1.21512?WT.mc_id=TWT_NatureNews
https://medium.com/@amyvertino/my-name-is-not-amy-i-am-an-uber-survivor-c6d6541e632f
https://www.nytimes.com/2017/06/21/technology/uber-ceo-travis-kalanick.html?_r=0
https://www.malwaretech.com/2017/05/how-to-accidentally-stop-a-global-cyber-Attacks.html
https://qz.com/937038/github-now-lets-its-workers-keep-the-ip-when-they-use-company-resources-for-personal-projects/?s=1
https://techcrunch.com/2017/01/09/atlassian-acquires-trello/
https://www.washingtonpost.com/news/the-fix/wp/2016/11/08/donald-trumps-path-to-victory-is-suddenly-Looking-much-much-wider/?hpid=hp_hp -bignews3_fix-electalmap-210am%3Ahomepage%2Fstory
https://news.mit.edu/2017/tim-berners-lee-wins-turing-award-0404
https://code.facebook.com/posts/1840075619545360
https://www.blog.google/topics/public-policy/net-neutrality-day-action-help-preserve-open-internet/
https://daringfireball.net/2017/06/fuck_facebook
https://josephg.com/blog/electron-is-flash-for-the-desktop/
https://privacylog.blogspot.ca/2017/04/what-happens-when-you-send-zero-day-to.html
http://www.groundup.org.za/article/why-were-dropping-google-ads/
http://www.sciencedirect.com/science/article/pii/S1525001617301107
https://twitter.com/GambleLee/status/862307447276544000
https://answers.microsoft.com/en-us/msoffice/forum/msoffice_onedrivefb-mso_o365brs/onedrive-for-business-open-is-very-slow-on-linux/3d33dc1b-3cc3-4c24-9998-9ab96bad31fc
https://www.theatlantic.com/magazine/archive/2017/06/lolas-story/524490/?single_page=true
https://www.theguardian.com/technology/2017/jan/13/whatsapp-design-feature-encrypted-messages
```

#### Kết quả:

Mức sử dụng CPU (xem ảnh):
: uBlock Origin (trên): 4.662,3 ms (3.403,6 ms + 1.258,7 ms)
: Adguard (dưới): 14.424 ms (11.638,8 ms + 2.785,2 ms)

![](https://user-images.githubusercontent.com/585534/28976229-1a45cc20-790b-11e7-83df-31372efd5e93.png)

Mức sử dụng bộ nhớ sau khi tải tất cả các tab (xem ảnh, trên cùng là sau khi khởi chạy trình duyệt + thu gom rác và trước khi mở tất cả các tab):
: uBlock Origin (trái): 1.254 MB
: Adguard (phải): 1.535 MB

![](https://user-images.githubusercontent.com/585534/28976324-6910e2c2-790b-11e7-9388-3591daaed7b6.png
)
#### Kết luận:

Về cơ bản, cả hai extension đều sử dụng cùng một mã trên Microsoft Edge giống như trên Chrome, vì vậy dự kiến ​​chúng sẽ có kết quả hiệu suất tương đối giống nhau. Kết quả chỉ ra rằng **uBlock Origin tiêu tốn 1/3 chu kỳ CPU để thực sự đạt được nhiều hơn Adguard** (mặc định của uBO bao gồm danh sách phần mềm độc hại và của Peter Lowe), việc tuyên bố rằng kết quả hoàn toàn bị đảo ngược trên Microsoft Edge là một tuyên bố khá đặc biệt và do đó cần phải được được chứng minh bằng nhiều điều hơn là chỉ đánh giá hoàn toàn chủ quan và không có dữ liệu, chẳng hạn như "phương pháp luận là cách sử dụng thực tế".

Rõ ràng, việc công bố kết quả được hỗ trợ bởi dữ liệu + phương pháp để vạch trần một tuyên bố vô căn cứ lại bị coi là ["công kích"](https://twitter.com/christianbute/status/893523529437765632). Tính chủ quan, Thiên kiến, hiệu ứng giả dược là thực tế, và cách để chống lại những điều này là bám vào dữ liệu khách quan, và đó là điều tôi đã làm ở trên.

## Nguồn:
[^ff-why-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22179155>
[^ff-why-2]: <https://old.reddit.com/r/firefox/comments/gjuqwz/does_firefox_preload_websites_on_search/>
[^ff-why-3]: <https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections#w_prefetching>
[^ff-why-4]: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox>
[^ff-why-5]: <https://blog.apnic.net/2020/08/04/characterizing-cname-cloaking-based-tracking/>
[^ff-why-6]: <https://www.apnic.net/about-apnic/>
[^ff-why-7]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25474057>
[^ff-why-8]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27638662>
[^ff-why-9]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27693869>
[^ff-why-10]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27482337>
[^ff-why-11]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27693391>
[^ff-why-12]: <https://www.howtogeek.com/724441/what-is-googles-floc-and-how-will-it-track-you-online/>
[^ff-why-13]: <https://github.com/gorhill/uBlock/wiki/Debunking-%22uBlock-Origin-is-less-efficient-than-Adguard%22-claims>
[^ff-mod-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-302#post-27777028>
[^ff-backup-restore]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-302#post-27777028>
[^ff-tete-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23354773>
[^ff-tete-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24612099>