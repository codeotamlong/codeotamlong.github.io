---
title: "[Firefox Awesome] Các userChromeJS/CSS hay ho: Extension Option Panel"
date: 2023-10-01 10:30:00 +0700
categories: [awesome, firefox, add-on, userchromejs, extension option panel]
tags: [awesome, firefox, add-on, userchromejs, extension option panel]     ## TAG names should always be lowercase
---

## userChrome.JS[^ff-userchrome]
Giải thích ngắn gọn: `Inject code JavaScript`, chạy trên ngữ cảnh của Firefox browser. Tức là can thiệp trực tiếp vào code logic của Firefox.
Để so sánh thì các script chạy trên *monkey chỉ hoạt động trên ngữ cảnh của trang web, không tác động được vào browser.
Các Addon thì chỉ sử dụng những API mà Firefox expose ra, nên tác động hạn chế.

Về cơ bản các userChromeJS script sẽ không có hạn chế gì cả. Tác động được vào tất cả các phần viết bằng JavaScript của Firefox (còn các phần khác viết bằng C++ hay các ngôn ngữ khác thì không được). 

> Ngoài ra các script này còn có toàn quyền đọc/ghi trên ổ cứng của bạn. **Cực kỳ nguy hiểm. Phải kiểm tra rất cẩn thận trước khi sử dụng.**
{: .prompt-danger }

### Cài fx-autoconfig (_userChrome.js manager_)

> Link: <https://github.com/MrOtherGuy/fx-autoconfig>
{: .prompt-info }

Tải về, giải nén (hoặc `git clone`)
: Chú ý 2 thư mục `profile` và `program`

```
.
├── profile
│   └── chrome
│       ├── CSS
│       ├── JS
│       ├── resources
│       └── utils
└── program
    ├── config.js
    └── defaults
        └── pref
```

Copy **nội dung bên trong** thư mục `program` (gồm file `config.js` và cả thư mục `defaults`) vào thư mục cài đặt Firefox
: Windows
: > Thường là `C:\Program Files\Mozilla Firefox\`: cả `config.js` và thư mục `defaults` sẽ nằm cạnh `firefox.exe`
: MacOS
: > Thường là `/Applications/Firefox.app/Contents/MacOS/` hoặc` /Applications/Firefox Nightly.app/Contents/MacOS/`
: Linux
: > Thường là `/usr/lib/firefox/` hoặc `/usr/lib64/firefox/`: `config.js` nằm cùng thư mục với tập nhị phân `firefox`

Copy **nội dung bên trong** thư mục `profile` (gồm cả thư mục `chrome`) vào thư mục profile đang dùng của Firefox
: Merge nếu đã có thư mục `chrome`

> Để tìm thư mục cài đặt và profile của Firefox nhanh
>
> Mở `about:support`
> - Thư mục cài đặt nằm ở dòng `Application Binary`
> - Thư mục profile nằm ở dòng `Profile Folder` (_Có nút `Open Profile Folder` trên Windows, `Show in Finder` trên MacOS để mở nhanh_)
{: .prompt-tip }

> Bộ loader `fx-autoconfig` của @MrOtherGuy sẽ tự động load các file `*.uc.js`, `*.uc.mjs`, `*.sys.mjs` (trong thư mục `chrome/JS/`) và các file `*.uc.css` (trong thư mục `chrome/CSS/`). Chú ý đổi tên file để load được script. (_Không hiểu sao riêng FLoorP thì lại tự động load hết, không cần đổi tên - hên xui!_)
{: .prompt-tip }

> Có repo userChromeJS đáng chú ý:
> `firefox-scripts` của @xiaoxiaoflood
> : Link: <https://github.com/xiaoxiaoflood/firefox-scripts>
>
> `fx-autoconfig`của @MrOtherGuy
> : Link: <https://github.com/MrOtherGuy/fx-autoconfig> 
> : Cũng là tác giả của nhiều tweak css tại <https://github.com/MrOtherGuy/firefox-csshacks>
>
> `userChrome.js` của @alice0775, người Nhật nên đọc comment code cũng vất vả xíu.
> : Link: <https://github.com/alice0775/userChrome.js>
>
> `uc.css.js` của @aminomancer.
> : Link: <https://github.com/aminomancer/uc.css.js>
>
> _Script viết theo loader của MrOtherGuy, alice0775 và aminimancer khá tương thích với nhau, còn bộ loader số 1 của @xiaoxiaoflood cần viết theo cấu trúc khác hẳn. Nhưng nói chung nếu bỏ công sức ra thì cũng port qua lại được._
{: .prompt-info }

> Sau khi cài UserChrome JS/CSS mới, restart lại Firefox: 
> :`about:support` -> `Clear startup cache...` (_xóa cache cũ_)
{: .prompt-info }

### Extension Option Panel (nút quản lý addon)[^ff-js-1] (Tác giả @aminomancer)

> Link: <https://github.com/aminomancer/uc.css.js/#extension-options-panel>
> : Copy vào thư mục `PROFILE_DIR/chrome/JS/`
{: .prompt-info }

### about:userchrome - giao diện quản lý userChrome.JS (Tác giả @aminomancer)

> Link: <https://github.com/aminomancer/uc.css.js/>
{: .prompt-info }

Tải cả repo kia về
: Cách 1: `Code` => `Download ZIP`, giải nén, mở ra
: ![](../../assets/img/firefox-userchrome/github-code-download.png)
: Cách 2: `git clone https://github.com/aminomancer/uc.css.js/`

Cấu trúc thư mục `uc.css.js`
: Chú ý 2 thư mục con `CSS`, `JS`, `resources`, `utils`
: _(cấu trúc tương tự fx-autoconfig bên trên )_

```
.
├── CSS
├── JS
├── resource
├── utils
...
```
{: file="/uc.css.js/."}

Mở thư mục `uc.css.js/JS`
: Tìm và copy file `aboutUserChrome.sys.mjs` vào thư mục `PROFILE_DIR/chrome/JS` của Firefox

Mở thư mục `uc.css.js/resources/aboutuserchrome`
: Tìm và copy thư mục `aboutuserchrome` vào thư mục `PROFILE_DIR/chrome/resources` của Firefox

Cấu trúc thư mục `PROFILE_DIR\chrome\` mới
: _Các file/folder đã có vẫn giữ nguyên_

```
.
├── CSS
│   └── ...
├── JS
│   └── aboutUserChrome.sys.mjs
├── resources
│   ├── aboutuserchrome
│   │   ├── aboutuserchrome.css
│   │   ├── aboutuserchrome.html
│   │   ├── aboutuserchrome.js
│   │   ├── chrome
│   │   ├── modules
│   │   └── src
|   └── ...
└── utils
    └── ...
```
{: file="PROFILE_DIR/chrome/."}

## userChrome.CSS [^ff-css-1]

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

Mở folder `PROFILE_DIR/chrome`:
: Tạo một file `userContent.css`
: Copy tất cả đoạn bên dưới vào, sau đó khởi động lại Firefox:
    
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
{: file = "PROFILE_DIR/chrome/userContent.css"}

Test thử ở trang này, nếu cục `CSS` màu xanh lá không chạy animation là thành công: <https://www.w3schools.com/css/css3_animations.asp>

### Thanh tìm kiếm Findbar phía bên trên trình duyệt (giống Chrome)

> Link: <https://github.com/MrOtherGuy/firefox-csshacks/blob/master/chrome/floating_findbar_on_top.css>
> : Copy vào thư mục `PROFILE_DIR/chrome/CSS/`
{: .prompt-info }

Nếu muốn để thanh Findbar nằm góc trên bên phải
: `about:config` => tạo key mới:
: > Tên: `userchrome.floating-findbar-on-right.enabled`
: > Kiểu: `Boolean`
: > Giá trị: `true`

| userchrome.floating-findbar-on-right.enabled | true |

```javascript
// UserChrome.CSS Findbar floating on Top-Right (as Google Chrome)
user_pref("userchrome.floating-findbar-on-right.enabled", true);
```
{: file="user.js"}

### Tùy biến menu quản lý add-on mặc định của Firefox (biểu tượng miếng xếp hình)

#### Ẩn/ Đổi màu icon

Khi sử dụng userChrome.JS Extension Option Panel ở trên, trên thanh toolbar sẽ có 2 biểu tượng quản lý add-on: 1 của Firefox, 1 của script. Có thể ẩn hoặc đổi màu cái biểu tượng mặc định cho đỡ nhầm. Nhưng mà vì cái manifest V3 nên cái quản lý addon mặc định dùng để mở menu và pin add-on lên toolbar, nên hay nhất là đổi màu cho cái biểu tượng đấy

Tắt hẳn Firefox
: Mở thư mục `PROFILE_DIR/chrome/CSS/`:
: Tạo file `custom_puzzle_addon_icon.uc.css`
: Copy đoạn CSS ở  dưới vào, muốn ẩn/đổi màu thì xóa (hoặc đặt comment /* */) cái còn lại
: Lưu lại, khởi động lại Firefox

```css
/*
** REMOVE
*/

/*#unified-extensions-button,
#unified-extensions-button > .toolbarbutton-icon{
	width: 0px !important;
	padding: 0px !important;
}*/

/*
** CHANGE COLOR
*/
#unified-extensions-button {
    color: red!important;
	fill: red !important;
}
```
{: file="PROFILE_DIR/chrome/CSS/custom_puzzle_addon_icon.uc.css"}

#### Thu nhỏ danh sách add-on

> Link: <https://github.com/datguypiko/Firefox-Mod-Blur/tree/master/EXTRA%20MODS/Compact%20extensions%20menu/Style%202>
{: .prompt-info }

Tắt hẳn Firefox
: Mở thư mục `PROFILE_DIR/chrome/CSS/`:
: Tải thẳng file `cleaner_extensions_menu.css` đã tải ở Link trên vào đây
: Đổi tên `cleaner_extensions_menu**.uc**.css`
: Lưu lại, khởi động lại Firefox

Kết quả
: ![](https://github.com/datguypiko/Firefox-Mod-Blur/blob/master/EXTRA%20MODS/Compact%20extensions%20menu/Style%202/preview.png?raw=true)

> Nếu không thích cái gạch chia menu thì mở thư mục `No Seperate Line` tải file `cleaner_extension_menu.css` về là làm tương tự
> : ![](https://github.com/datguypiko/Firefox-Mod-Blur/blob/master/EXTRA%20MODS/Compact%20extensions%20menu/Style%202/No%20separator%20line/preivew.jpg?raw=true)
{: .prompt-tip }

## Nguồn:
[^ff-userchrome]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-172#post-25670849>
[^ff-js-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27662606>
[^ff-css-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-160#post-25566309>
[^fn-nth-4]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-160#post-25566309>