---
title: "[Firefox Awesome] Tại sao lại là Firefox?"
date: 2023-08-28 11:33:00 +0700
categories: [firefox, awesome]
tags: [firefox, awesome]
---
> Linh vật của công ty là một khủng long (`Mozilla`), biểu tượng thì là một con cáo (`fire fox`), nhưng thực chất lại là gấu trúc (`red panda`), và sử dụng engine là một con tác kè (`gecko`)
{: .prompt-info }
## Chrome không tốt như thế: "Do be evil!" [^footnote]

Tốc độ của Chrome _có vẻ_ nhanh hơn Firefox, thực chất là do thuật toán học máy để đoán trước trang web, ví dụ: Bạn vừa gõ `goo`, nó đã biết là `google` rồi và tải sẵn luôn trang web vào bộ nhớ. Tính năng này *đánh lừa* người dùng là Chrome nhanh hơn Firefox: nếu cùng load một nội dung thì cả 02 trình duyệt đều giống nhau, nhưng Chrome giống như bắt đầu chạy từ giữa đường trong khi đối thủ đang đứng từ vạch xuất phát. 

> Vấn đề ở đây cần phải làm rõ là Chrome không hề nhanh hơn Firefox, mà nó có nhiều chiêu trò đánh lừa người dùng khiến họ nghĩ Chrome nhanh hơn.
{: .prompt-warning }

Với Chrome:
: or instance, Chrome, predicts what the user is typing and fires the request even before the user has done typing and hitting enter. By the time they hit enter, the page is ready to load front the cache. This is done with some fair amount of ML.
: _Tạm dịch_
: Ví dụ, trình duyệt Chrome có khả năng dự đoán những gì người dùng đang gõ và gửi yêu cầu trước cả khi người dùng đã gõ xong và nhấn Enter. Khi họ nhấn Enter, **trang web đã sẵn sàng để tải từ bộ nhớ cache**. Điều này được thực hiện thông qua một lượng lớn thuật toán học máy.


Với Firefox (ý nói là Firefox không tải trước trang như Chrome) [^fn-nth-2] [^fn-nth-3]
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

## uBlock Origin làm việc tốt nhất trên Firefox (uBO works best on Firefox) [^fn-nth-4] _Tạm dịch - Đọc bản gốc để hiểu rõ hơn_
Truy nguyên CNAME
: ![Desktop View](https://user-images.githubusercontent.com/585534/103416937-b623c400-4b56-11eb-8e94-b4851a2248b7.png)
: _Nguồn: "Characterizing CNAME Cloaking-Based Tracking on the Web"[^fn-nth-5], Asia Pacific Network Information Centre[^fn-nth-6], August 2020._ (Cao hơn là tốt hơn)

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

## Manifest V3 triệt hạ khả năng chặn quảng cáo của trình duyệt. Tham khảo: Sự khác biệt của uBlock Firefox vs Chrome vs Manifest V3 vs Adguard[^fn-nth-7]

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
: - **Không thể có nhiều hơn 30.000 rule** (dòng chặn, chi tiết: [MV3: overcoming the 30000 rules limit](https://old.reddit.com/r/uBlockOrigin/comments/xlw1wi/mv3_overcoming_the_30000_rules_limit/)), trong khi số lượng trang web tăng không ngừng mỗi ngày, ngoài ra adblock còn được dùng để chặn các trang có nội dung malware nữa nên thậm chí để an toàn thì một người dùng cần dùng tới hàng triệu rule, ví dụ như chỉ để chặn các tên miền mới tạo ra trong vòng 31 ngày đã ngốn nguyên 3 triệu rule: Cách chặn các tên miền mới tạo (thường là lừa bịp, virus) bằng uBlock[^fn-nth-3]
: - **Dừng hoạt động sau khi trang tải xong một thời gian** ([5 phút](https://old.reddit.com/r/learnjavascript/comments/10jmkc4/how_to_prevent_service_worker_from_going_inactive/)), nghĩa là sẽ vô dụng với các trang web động sử dụng AJAX như Youtube/Facebook vì một lúc sau khi tải xong sẽ không còn chặn quảng cáo nữa, khiến quảng cáo hiện ra

Còn đây là thông tin do chính `gorhill` cung cấp.[^fn-nth-7]: 

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
## Privacy Sandbox quảng cáo bằng cách địa lịch sử duyệt web của người dùng.[^fn-nth-8][^fn-nth-11]

[Google Chrome vừa chính thức bật tính năng `Privacy Sandbox` lên tất cả phiên bản Chrome mới](https://arstechnica.com/gadgets/2023/09/googles-widely-opposed-ad-platform-the-privacy-sandbox-launches-in-chrome/), tính năng này chính là FLoC[^fn-nth-12](Federated Learning of Cohorts, chạy trong trình duyệt Chrome của Google và theo dõi hành vi trực tuyến, cho phép dịch vụ quảng cáo xác định tệp khách hàng dựa trên hành vi mà không cần cookie) cải biên do trước định thực hiện nhưng người dùng chửi cho nát mặt nên giờ lươn lẹo đổi tên thành `Privacy Sandbox`, nghe tên rất chi là riêng tư cơ mà nó ngược lại hoàn toàn,cho phép trình duyệt web lấy lịch sử duyệt web của người dùng, tóm tắt lại rồi gửi cho trang web để họ tạo quảng cáo, ví dụ:

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

## Widevine triệt hạ trình duyệt web mới nối bên thứ ba [^fn-nth-9]

> Nghĩa là để xem được các trang Netflix, Spotify... thì tác giả trình duyệt mới phải quỳ lạy, van xin Google cấp cho, mà thường thì 1-2 năm không có phản hồi, dù rằng các trình duyệt web này đều tốt hơn Chrome gốc (Cromite, Ungoogled, Floorp...). 
{: .prompt-warning}

Nghe nói thằng này mới cải thiện hiệu năng, nhìn chung đã chơi nhân Chromium thì cứ fork mà táng thôi chứ Chrome mới chính ra là thằng cùi bắp nhất hội.

Cái khó là bị vụ WebDRM (Widevine) nghĩa là mấy bản fork sẽ không xem được Netflix hay Spotify, dù nó ngon như Cromite/Ungoogled. Quy trình cấp phép Widevine của Google cũng nhiêu khê lắm, phải chìa tay ra xin Google và đợi họ ban ơn. :D
 
## Environment Intergrity[^fn-nth-10]

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

# Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22179155>
[^fn-nth-2]: <https://old.reddit.com/r/firefox/comments/gjuqwz/does_firefox_preload_websites_on_search/>
[^fn-nth-3]: <https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections#w_prefetching>
[^fn-nth-4]: <https://github.com/gorhill/uBlock/wiki/uBlock-Origin-works-best-on-Firefox>
[^fn-nth-5]: <https://blog.apnic.net/2020/08/04/characterizing-cname-cloaking-based-tracking/>
[^fn-nth-6]: <https://www.apnic.net/about-apnic/>
[^fn-nth-7]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25474057>
[^fn-nth-8]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27638662>
[^fn-nth-9]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27693869>
[^fn-nth-10]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27482337>
[^fn-nth-11]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27693391>
[^fn-nth-12]: <https://www.howtogeek.com/724441/what-is-googles-floc-and-how-will-it-track-you-online/>