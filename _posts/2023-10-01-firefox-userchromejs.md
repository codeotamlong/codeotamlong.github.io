---
title: "[Firefox Awesome] Các userChromeJS hay ho: Extension Option Panel"
date: 2023-10-01 10:30:00 +0700
categories: [awesome, firefox, add-on, userchromejs, extension option panel]
tags: [awesome, firefox, add-on, userchromejs, extension option panel]     ## TAG names should always be lowercase
---
## userChromeJS scripts[^footnote]
Giải thích ngắn gọn: `Inject code JavaScript`, chạy trên ngữ cảnh của Firefox browser. Tức là can thiệp trực tiếp vào code logic của FIrefox.
Để so sánh thì các script chạy trên *monkey chỉ hoạt động trên ngữ cảnh của trang web, không tác động được vào browser.
Các Addon thì chỉ sử dụng những API mà Firefox expose ra, nên tác động hạn chế.

Về cơ bản các userChromeJS script sẽ không có hạn chế gì cả. Tác động được vào tất cả các phần viết bằng JavaScript của Firefox (còn các phần khác viết bằng C++ hay các ngôn ngữ khác thì không được). 

> Ngoài ra các script này còn có toàn quyền đọc/ghi trên ổ cứng của bạn. **Cực kỳ nguy hiểm. Phải kiểm tra rất cẩn thận trước khi sử dụng.**
{: .prompt-danger }

Có 3 bộ autoconfig để load userChromeJS mà theo mình là đáng chú ý:
1. [firefox-scripts](https://github.com/xiaoxiaoflood/firefox-scripts) của xiaoxiaoflood
2. [fx-autoconfig](https://github.com/MrOtherGuy/fx-autoconfig) của MrOtherGuy, cũng là tác giả của nhiều [tweak css](https://github.com/MrOtherGuy/firefox-csshacks). Có nhiều scripts dựa trên loader này nằm trên repo [uc.css.js](https://github.com/aminomancer/uc.css.js) của aminomancer.
3. [userChrome.js](https://github.com/alice0775/userChrome.js) của alice0775, người Nhật nên đọc comment code cũng vất vả xíu.

Script viết theo loader 2 và 3 khá tương thích với nhau, còn bộ loader số 1 của xiaoxiaoflood cần viết theo cấu trúc khác hẳn. Nhưng nói chung nếu bỏ công sức ra thì cũng port qua lại được.

Dự định của mình là viết một scripts làm vertical tab cho FIrefox, giống kiểu của Edge (có bật/tắt autohide). Các giải pháp sử dụng addon (Tree Style Tab, Sidebery, etc.) + CSS không thể bật tắt autohide được. Tiện tay thì vertical tab này sẽ dùng native tab (thay đổi vị trí ngang/dọc) thay vì clone lại tab vào sidebar.
Cơ mà đấy là dự định, làm còn lâu mới xong.

Giờ share 2 script vừa và nhỏ:
1. [URLBar show domain](https://github.com/vufly/foxinity/blob/master/src/js/urlbar-show-domain.uc.js):
Cũng không có gì đặc biệt. Gọt hết phần protocol (https://) và www. và path (t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/), chỉ để lại subdomain.domain
Nói chung là bắt chước URLBar của Safari.

2. [Sidebar easy switch](https://github.com/vufly/foxinity/blob/master/src/js/sidebar-easy-switch.uc.js):
Nói chung là bắt chước side panel của Vivaldi.

* Bỏ giới hạn chiều rộng tối thiểu/tối đa của sidebar.
* Các options trong dropdown chọn sidebar được đưa ra một panel bên ngoài. Tiết kiệm 1 click và vài cm kéo chuột chọn.
* Thu gọn/phóng to sidebar.

Ai dùng nhiều sidebar khác nhau sẽ thấy tiện hơn chút. Tất nhiên cái này không tương thích với ai đang dùng các giải pháp autohide sidebar bằng CSS.: <https://imgur.com/fHIoQPx>

À quên, mình dùng fx-autoconfig, nên cách cài cũng tương tự như [aminomancer hướng dẫn](https://github.com/aminomancer/uc.css.js#installation).

## Cài cái userChrome.js Extension Option Panel (nút quản lý addon)[^fn-nth-2]
Để làm lại bài về cài cái userChrome.js Extension Option Panel (nút quản lý addon) này.

Đầu tiên là cách cài Loader của MrOtherGuy:

* Vào: <https://github.com/MrOtherGuy/fx-autoconfig>
* Ấn vào nút `Code`, sau đó `Download`, giải nén ra đâu cũng được
* Vào folder tên `program`, bôi đen folder `defaults` và file `config.js`, rồi Copy
* Từ Firefox gõ `about:support` rồi nhìn ở phần `Application Binary`, mở cái folder chứa `firefox.exe` đó lên
* Paste
* Vào folder tên `profile` và bôi đen folder `chrome`, rồi Copy
* `about:support`
* Open Profile Folder
* Paste


Rồi, đơn giản lắm giờ cài script Extension Option Panel thôi:

* `about:support``
* Open Profile Folder
* Vào thư mục `chrome`
* Vào thư mục `JS`
* Vào <https://github.com/aminomancer/uc.css.js#extension-options-panel>
* Tải thẳng vào folder `JS` bên trên
* Save


Khởi động lại là xong (tốt nhất là dùng `about:support` -> `Clear startup cache...` để Firefox đào thải cache cũ khiến Loader không nạp được), kết quả y như bài bên trên: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27662443>

Ngoài ra đọc bài [**giới thiệu các script userChrome.js này để kiểm script ngon**]('https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27662881')**.**



## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-172#post-25670849>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27662606>