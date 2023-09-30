---
title: "[Firefox Awesome] Part 2c: Các add-on hay ho - HeaderEditor"
date: 2023-09-30 21:30:00 +0700
categories: [awesome, firefox, add-on]
tags: [awesome, firefox, add-on, file centipede, multithreaded download manager, mdm]     # TAG names should always be lowercase
---
## FileCentipede - Tải đa luồng, bắt link như IDM và hơn thế

### Hướng dẫn cách cài con vịt pede xòe ra hai cái cánh để bắt link và tải đa luồng như IDM:

- Tải tại đây: <https://github.com/filecxx/FileCentipede/releases>
- Hướng dẫn cách để con vịt hết pede đi bởi @Fioren: <https://voz.vn/t/tong-hop-software-can-thiet-cho-may-tinh.2974/post-21105427>

Nếu các bạn xài Firefox Portable hay Floorp thì vào trang addon cài **<https://addons.mozilla.org/vi/firefox/addon/filecxx/>** hoặc tải file `firefox.xpi` [**tại đây**](https://github.com/filecxx/FileCentipede/releases) rồi kéo thả nó vào để cài đặt là xong nếu nó không tự cài đặt, thường thì khi xài Firefox cài đặt là nó tự cài.

Tính năng thì:
: Y như IDM (đa luồng, thời gian biểu (schedule), bắt link video, hàng loạt...)
: Hơn IDM (kéo Torrent, ED2K)
: KHÔNG GHÉP FILE mà tạo ra một file ảo sau đó ghi liên tiếp vào file ảo trên, không nghẽn ổ đĩa


![](https://voz.vn/attachments/1694834094700-png.2074664/)
![](https://voz.vn/attachments/1694834115777-png.2074665/)


### Hướng dẫn cách để con vịt hết pede đi bởi @Fioren[^footnote]
mò mẫm cũng biết cách cr@ck con vịt này :sexy_girl:

Chọn chỗ này để thoát hoàn toàn app

![](https://voz.vn/attachments/1695663665411-png.2092288/)

Sau đó tải app này <https://portableapps.com/apps/development/sqlite_database_browser_portable>

Tải về giải nén các kiểu cài ra được app portabe, chạy nó.

Vào File > open database chọn file `filecxx_xxxxx\lib\data_windows.db`

Thấy cái table Local chuột phải > delete table

![](https://voz.vn/attachments/1666550072889-png.1456757/)

Ấn Ctrl + S để save lại

Sau đó bật lại con vịt vào Help > Activation code coi số ngày nó reset lại 3 ngày sử dụng chưa.

Rồi thoát hoàn toàn con vịt như bước đầu tiên

Mở lại cửa sổ SQL lite ấn F5 nó sẽ hiển thị lại table local

Tới đây bấm tab Browser data chọn Local

![](https://voz.vn/attachments/1666550198563-png.1456758/)

Dòng số 1,2 là 2 dãy chữ số giống nhau. Ấn đè kéo cái 2 dòng đó để edit được. Đổi chữ cái **gần cuối cùng thành chữ a**. VD: FdyQ764Gih**<span style="color:RED;">k</span>**Y thành FdyQ764Gih**<span style="color:RED;">a</span>**Y

![](https://voz.vn/attachments/1666550471799-png.1456764/)

Sau đó ấn Ctrl + S để save lại

Rồi mở con vịt lên và thấy số ngày tăng :sexy_girl:

![](https://voz.vn/attachments/1666550349246-png.1456763/)

> [File ăn sẵn dành cho ai lười](https://voz.vn/attachments/data_windows-zip.2092290/):
> <br>Giải nén copy đè file `data_windows.db` vào `filecxx_xxxxx\lib`
{: .prompt-info}

## Multi-Threaded Download Manager - Tải đa luồng như IDM, bắt link video, tải hàng loạt như IDM!

Tiếp tục bài trên này, sau khi phải dứt ruột ném thằng `TurboDownloadManager` vào sọt rác thì giờ hàng mới ngon đã được khai quật từ nơi cống rãnh nhé :D

Thằng [**Multi-Threaded Download Manager**](https://addons.mozilla.org/en-US/firefox/addon/multithreaded-download-manager/) (**>>>>**[**Bản mod ngon hơn hỗ trợ tải đa luồng Google Drive và nhiều trang hơn**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24638856)**<<<<**) này đã test thử, tính năng tải đa luồng như IDM hoạt động nhé, cơ mà mặc định giới hạn 6 luồng (đủ dùng và tốt nhất nên để 6 luồng thậm chí thấp hơn tầm 3-4 luồng sẽ xanh sạch đẹp cho server hơn) bằng với `network.http.max-persistent-connections-per-server` và `network.http.max-persistent-connections-per-proxy` trong `about:config` vì nó dùng API network của Firefox tải file:

![](https://i.imgur.com/7oxGDlB.jpg)

Link test nếu các bạn muốn tự tay thử: <https://speed.hetzner.de/>

Ngoài ra nó còn hỗ trợ bắt link video như IDM nhé, mà nó hoạt động trong Firefox nên không quan tâm tới Referer hay Cookies

![](https://i.imgur.com/CCPLqbM.jpg)

Link test nếu muốn kiểm nghiệm: <https://www.w3schools.com/html/html5_video.asp>

Có tính năng Queue để giới hạn số lượng tải về trong cùng một thời điểm nhé:

![](https://i.imgur.com/C49vsrH.jpg)

> Nên dùng kết hợp với script bắt link video của bạn @boscofz sẽ rất tiện, script nhỏ nhẹ và tương thích mọi trang web: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23935535>
{: .prompt-tip }
> Kết hợp với yt-dlp như hướng dẫn này của mình thì IDM gọi bằng cụ nhé :D <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23288076>
{: .prompt-tip }

Ngoài ra đã kiểm tra code, an toàn nhé và ông dev Tung Của này uy tín và có nghề phết, toàn code addon độc và lạ. :D

**Để Multithreaded Download Manager bắt link Drive thì xem post sau: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24525109>**

Tổng kết lại tính năng so với IDM:
- Tải đa luồng: Có
- Pause/Resume file đang tải dở: Có
- Quản lý tải về: Có
- Tải giới hạn số lượng tải cùng lúc: Có
- Bắt link video: Có (tốt hơn IDM do nó dùng cookies/referer từ Firefox)
- Tải hàng loạt: Có (tốt hơn IDM do nó dùng cookies/referer từ Firefox)

Tính năng mà IDM không có:
- Hoạt động ngay trong trình duyệt nên nó sử dụng cookies/referer tốt hơn, ví dụ khi tải những link premium thì IDM phải thêm vào mục Account thủ công, thằng này phang luôn trong Firefox vì nó chia sẻ đăng nhập với Firefox
- Vì MDM hoạt động ngay trong Firefox nên [**nếu trang nào tải khoai quá vì một số lý do nó ghét phân luồng thì chọn `Continue in browser` tải trong Firefox là xong**](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24848706)
> Kể cả IDM cũng bị, nhìn chung nó cũng có tí chống phân luồng cơ mà Google nó làm gì thì luôn âm thầm, người không biết quỷ không hay, các trang web tài file thường là ghét bị chia luồng vì nó tốn tài nguyên ổ đĩa IO (cứ hiểu là đọc ghi ổ đĩa) gấp N lần số luồng, chia làm 16 luồng thì ổ cứng của họ phải làm việc gấp 16 lần gây nghẽn đọc ghi, Google Drive mặc định là nó không cho chia luồng vì nó không gửi trả `Accept-Ranges`, mình cứ bỏ qua chia thì nó đáp trả vậy đó. Nhìn chung cứ Continue in browser nếu file bự quá.
> <br>Ít nhất MDM còn cho Continue in browser dễ dàng khắc phục 100% lỗi còn IDM hình như phải ấn tổ hợp phím gì đó mà người dùng cũng chả nhớ mấy đâu.
> <br> <https://voz.vn/t/loi-download-google-drive-bi-loi-giua-chung.720358/>
{: .prompt-info }
- Không cần ghép file như IDM làm quá tải ổ cứng, thằng này sử dụng thuật toán file ảo hiện đại, nó tạo ra một file ảo sử dụng Storage API của Firefox, ví dụ tải file 4GB thì nó tạo ra một file rỗng 4GB, sau đó tải nhồi dữ liệu vào file đó luôn nên **KHÔNG PHẢI GHÉP FILE** như IDM
- Tải những thứ mà IDM không tải được do nó hoạt động trong Firefox, cái gì Firefox thấy là nó thấy, và nó thấy là nó tải được. Ví dụ: Đố IDM tải được blob:, cơ mà nó tải được blob:
- Không thể bị phát hiện do nó dùng TLS Fingerprint của Firefox, nghĩa là Firefox chia luồng ra Firefox tải, nếu trang web muốn chặn là phải chặn cả Firefox, còn IDM thì nó có Fingerprint riêng (kể cả để HTTP Header y hệt trình duyệt trang web vẫn phát hiện được qua TLS Fingerprint. Test tại: <https://tls.browserleaks.com/json> hoặc <https://tls.peet.ws/api/all>) nên nói thẳng là trang web muốn chặn/giới hạn tốc độ IDM dễ như trở bàn tay, mà tác giả IDM cũng không đủ tuổi code để vượt qua TLS Fingerprint do thực tế chục năm rồi IDM vẫn còn ghép file gây nghẽn ổ cứng

Đã cho lên #1 ngay và luôn, với cái này thì IDM chả đáng dùng nữa, vừa miễn phí, vừa hoạt động trong Firefox nên tính gắn kết cao hơn, lại còn hỗ trợ đa luồng, giới hạn số lượng tải về, bắt link video (trong `+`, vào thẻ Media nó bắt hết link video trong trang không cần dùng BulkMediaDownloader), bắt link hàng loạt. :D



### Bản mod ngon hơn hỗ trợ tải đa luồng Google Drive và nhiều trang hơn[^fn-nth-2]

Tranh thủ tí rảnh rỗi buổi tối mình cập nhập bản MDM mới tải được đa luồng trên cả Google Drive (và rất rất nhiều trang khác nữa mà thuật toán cũ lỗi thời kiểm tra Accept-Ranges bỏ qua, phần mềm Download Manager mình tự viết bên trên không bao giờ kiểm tra Accept-Ranges vẫn ngon chả lỗi gì cả)

Tải về, giải nén quăng vào `about:addons`.

Nếu báo không cài được vào `about:config` tìm `xpinstall.signatures.required` chuyển thành false, tìm `xpinstall.whitelist.required` chuyển thành false

Kết quả: <https://streamable.com/ki69x4>
Link test: <https://drive.google.com/file/d/1bYHpARq45jEToKVecVES7v_hghb60yA6/view>

@Odoryanse @nhoxbuondkny @ngowuys: Hàng mới nóng hổi vừa thổi vừa đớp nhé :D

> Tải ở đây: <https://voz.vn/attachments/mdm-zip.1779202/>
{: .prompt-info }

### Tải hàng loạt ảnh/video/link với MDM:[^fn-nth-3] 
Tiện đây làm một bài hướng dẫn dùng MDM để tải hàng loạt nội dung web (ảnh, video, theo đuôi file bất kỳ), nó rất đơn giản thôi nhưng nếu các bạn tận dụng sẽ giúp ích cho việc tìm kiếm dữ liệu, ví dụ lấy ảnh/video hàng loạt cho AI nó ăn.

Ví dụ tải toàn bộ ảnh ở link này: <https://baodantoc.vn/loi-ich-tuyet-voi-cua-hoa-hoe-doi-voi-suc-khoe-1655093293060.htm>

- Ấn vào biểu tượng MDM ở toolbar
- Chọn dấu `+`

![](https://voz.vn/attachments/1693396553060-png.2045030)

- Sang thẻ Media (hoặc cũng có thể dùng thẻ Link cho trường hợp khác)
- Gõ vào phần search ví dụ `.jpg`, `.png`, `/uploads/` để lọc ra ảnh muốn tải
- Tích vào cái ô vuông trên cùng
- Download là xong

![](https://voz.vn/attachments/1693396818796-png.2045039)

Để mọi thứ nuột nà các bạn nên tắt hộp thoại xác nhận tải của Firefox để đỡ phải nháy chuột liên tọi:
![](https://voz.vn/attachments/1693396884544-png.2045040)

### Tối ưu cho MDM bắt link nhiều hơn[^fn-nth-4]

Trường hợp này bạn ấn vào dấu `+`, vào thẻ Media xem có bắt được không ?

Bạn thử vào Options đánh dấu vào như sau:

![](https://i.imgur.com/CjltAlU.jpg)

Có gì bạn đưa link mình test thử xem sao.

Mình test thấy nó bắt link Google Drive dạng tải (Click vô nút mũi tên hướng xuống đất) ngon lành, còn MKV thì hình như cũng là link tải vì trình duyệt đâu có hỗ trợ chạy MKV nhỉ :D ![](https://i.imgur.com/nX3MYZo.jpg)

### Tối ưu cho MDM thay đổi thuật toán tải chia luồng hiệu quả hơn để tránh bị máy chủ chặn[^fn-nth-5] 

Iêm cũng để ý là lúc 1 luồng bất kỳ nào tải xong nó sẽ mở tiếp luồng khác để down tiếp. Tính ra nó cũng quá là tham lam đi :))

Đã thành công tải file dung lượng lớn, thành công save. Cám ơn thím toilagay và thím nhoxbuondkny

![](https://voz.vn/attachments/1682417261241-png.1799862/)

![](https://voz.vn/attachments/1682417173799-png.1799860/)

# Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-software-can-thiet-cho-may-tinh.2974/post-21105427>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24638856>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27468734>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24525109>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24867468>