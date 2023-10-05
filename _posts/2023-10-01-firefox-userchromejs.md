---
title: "[Firefox Awesome] Các userChromeJS/CSS hay ho: Extension Option Panel"
date: 2023-10-01 10:30:00 +0700
categories: [awesome, firefox, add-on, userchromejs, extension option panel]
tags: [awesome, firefox, add-on, userchromejs, extension option panel]     ## TAG names should always be lowercase
---

## userChromeJS[^footnote]
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

Ngoài ra đọc bài [**giới thiệu các script userChrome.js này để kiểm script ngon**\](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-292#post-27662881)**.**

## userContent.css [^fn-nth-3]

> Có **02** cách chính để Bật userChrome.CSS:
> 1. Sửa trong `about:config`:
> | toolkit.legacyUserProfileCustomizations.stylesheets | true |
>
> 2. Sửa file `user.js` (**khuyến khích** để có thể theo dõi thay đổi và backup):
>       + Mở `about:support` => Open Profile Folder
>       + Đóng Firefox (tắt hẳn - _chú ý với MacOS: Close khác với Quit_)
>       + Tạo mới nếu chưa có
>       + Thêm dòng mới `user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);`
>       + Save và mở Firefox
{: .prompt-info }

> `user.js` là file javascript nên có thể sử dụng `//` và `/**/` để viết ghi chú
{: .prompt-tip }

### Tắt CSS3 Animation [^fn-nth-4]

> Trong `about:config` có tham số `ui.prefersReducedMotion` để bắt trang web nó không dùng animation, tuy nhiên hỏi là một chuyện người ta đồng ý hay không lại là một chuyện khác vì nó đòi hỏi trang web phải sử dụng CSS `@media (prefers-reduced-motion) {/* styles to apply if a user's device settings are set to reduced motion */}`
{: .prompt-tip }

> Ngoài ra nếu sử dụng thêm [Header Editor](../firefox-addon-p3) để gửi thêm header [`Sec-CH-Prefers-Reduced-Motion: "reduce"`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-Prefers-Reduced-Motion) thì sẽ hiệu quả hơn vì sẽ khiến trang web hiểu điều này để trả về trang web không dùng animation.
{: .prompt-tip }

Thật ra để tắt animation, mình có cái "Tối ưu CSS" này đã dùng 7-8 năm liên tục và cải thiện nó đến mức nó khá an toàn và ổn định, đoạn code dưới đây tắt sạch CSS3 nặng nề đi khiến các trang web chạy nhẹ hơn, ít dùng CPU hơn.

Sau đó mở folder `chrome`, tạo một file `userContent.css` rồi copy tất cả đoạn bên dưới vào, sau đó khởi động lại Firefox:
    
```css
*, *:before, *:after {
    border-radius:unset!important;
    box-shadow:unset!important;
    text-shadow:unset!important;
    text-transform:unset!important;
    animation-iteration-count:1!important;
    scroll-behavior:unset!important;
    moz-animation-iteration-count:1!important;
    webkit-animation-iteration-count:1!important;
    backdrop-filter:unset!important;
    filter:unset!important;
    animation-timing-function: step-start !important;
    transition-timing-function: step-start !important;
    filter:none!important;
    text-rendering:none!important;
}
```
{: file = "PROFILE/chrome/userContent.css"}

Test thử ở trang này, nếu cục `CSS` màu xanh lá không chạy animation là thành công: <https://www.w3schools.com/css/css3_animations.asp>


## Nguồn:
[^footnote]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-172#post-25670849>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27662606>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-160#post-25566309>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-160#post-25566309>