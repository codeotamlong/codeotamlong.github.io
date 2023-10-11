---
title: "[Firefox Awesome] Tối ưu Firefox"
date: 2023-09-30 20:00:00 +0700
categories: [awesome, firefox, optimize]
tags: [awesome, firefox, optimize]     ## TAG names should always be lowercase
---
> Có **02** cách chính để thay đổi các tham số của Firefox:
> 1. Vào `about:config`, tìm và sửa tham số theo nhu cầu
> 2. Sửa file `user.js` (**khuyến khích** để có thể theo dõi thay đổi và backup):
>       + Mở `about:support` => Open Profile Folder
>       + Đóng Firefox (tắt hẳn - _chú ý với MacOS: Close khác với Quit_)
>       + Tạo mới nếu chưa có
>       + Thêm dòng mới `user_pref("<tham số>", <giá trị mới>);`
>       + Save và mở Firefox
{: .prompt-info }

> `user.js` là file javascript nên có thể sử dụng `//` và `/**/` để viết ghi chú
{: .prompt-tip }

## Tổng hợp `user.js`, cách sử dụng:[^ff-optimize-aio]

Mở thư mục `profile`
: Tải link dưới vào thẳng thư mục `profile`
: _hoặc_ Tạo fie `user.js` rồi paste hết đoạn javascript này vào đấy, lưu lại

> Download: <https://github.com/codeotamlong/awesome/blob/main/firefox/user.js>
{: .prompt-tip }
       
```javascript
/*
** PERSONALIZE
*/

// Un-check singature extension
user_pref("xpinstall.signatures.required", false);
user_pref("xpinstall.whitelist.required", false);

// No exception on extension
user_pref("extensions.webextensions.restrictedDomains", "");

// Enable userChrome.css
user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);

// UserChrome FindBar Floating Top - Right
user_pref("userchrome.floating-findbar-on-right.enabled", true);

/*
** SPEED-UP
*/

// Delay to first render
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);

// Force RAM cache
//user_pref("browser.cache.disk.enable", false);
//user_pref("browser.cache.memory.enable", true);
//user_pref("browser.cache.memory.capacity", 524288);
//user_pref("browser.cache.memory.max_entry_size", 512000);

// Force RAM cache - Disable RCWN
user_pref("network.http.rcwn.enabled", false);

// Disable SkeletonUI
user_pref("browser.startup.preXulSkeletonUI", false );

// Disable Accessibility
user_pref("accessibility.force_disabled", 1 );

/*
** UX/UI
*/

// Compact mode (slim toolbar)
user_pref("browser.compactmode.show", true );

// Enable Early hints
user_pref("network.early-hints.enabled", true);
user_pref("network.early-hints.preconnect.enabled", true);
user_pref("network.early-hints.preconnect.max_connections", 20);

// Bypass Cookie Banners: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPT - to remove banner);
user_pref("cookiebanners.service.mode", 2 );
user_pref("cookiebanners.service.mode.privateBrowsing", 2 );

// Bypass Cookie Banners - emulator CLICK, cookie INJECTOR: 
user_pref("cookiebanners.bannerClicking.enabled", true );
user_pref("cookiebanners.cookieInjector.enabled", true );

// Smooth scroll
user_pref("apz.overscroll.enabled", true);
user_pref("general.smoothScroll", true);
user_pref("mousewheel.enable_pixel_scrolling", false );
user_pref("mousewheel.default.delta_multiplier_y", 275 );
user_pref("general.smoothScroll.mouseWheel.durationMaxMS", 250 );
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 200 );

/*
** NETWORK
*/

// Disable OSCP
user_pref("security.OCSP.enabled", 0);

// Enable CrLite
user_pref("security.remote_settings.crlite_filters.enabled", true);
user_pref("security.pki.crlite_mode", 2);

// Next DNS
user_pref("network.trr.uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.mode", 2);

// Enable QUICv2
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1"');

/*
** PRIVACY - SECURITY
*/

// Resist Fingerprint (RFP)
user_pref("privacy.resistFingerprinting", true);

// Enable punnycode
user_pref("network.IDN_show_punycode", true);

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
{: file="user.js"}

## Các tham số cá nhân hóa (_optional - có thể bỏ qua_)

```javascript
/*
** PERSONALIZE
*/

// Un-check singature extension
user_pref("xpinstall.signatures.required", false);
user_pref("xpinstall.whitelist.required", false);

// No exception on extension
user_pref("extensions.webextensions.restrictedDomains", "");

// Enable userChrome.css
user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);

// UserChrome FindBar Floating Top - Right
user_pref("userchrome.floating-findbar-on-right.enabled", true);
```
{: file="user.js"}

## Hiệu năng phần mềm
### Windows Defenders vs Firefox [^ff-nglayout]

> Link: <https://bugzilla.mozilla.org/show_bug.cgi?id=1441918> 
{: .prompt-info }

Trích bình luận đáng chú ý <https://bugzilla.mozilla.org/show_bug.cgi?id=1441918#c61>
> With browser.cache.disk.enable = false, MsMpEng is around 3% CPU with the same test case, similar to other browsers (also observed in comment 53 with private windows). Excluding the profile's cache folder in Windows Defender has a similar effect.
>
> Using Process Monitor to count MsMpEng events for 30 seconds after reloading youtube.com (Ctrl+F5) I get the following (numbers are very rough):
>
> - Firefox (disk cache on): 1300 total events, 800 cache events, 50 files, 3MB
> - Firefox (disk cache off): 300 total events, 0 cache events, 0 files, 0MB
> - Chrome: 500 total events, 90 cache events, 10 files, 2MB
> - Edge: 400 total events, 0 cache events (800 ignored), 45 files, 7MB 

Theo như ông dev của Firefox test thì Firefox bị Windows Defendrs scan cache gấp chục lần so với Chrome và Edge. Nhìn chung Windows Defenders nó ưu ái Edge nhất. (cạnh tranh bẩn)

Hình như phía Firefox cũng bó tay rồi, 5 năm rồi không sửa nổi 5 năm bị đì đọt trên Windows. Kiểu cảm giác là lẽ ra Firefox phải hoạt động tầm 30-50% nhanh hơn nhưng vì bị thằng Windows Defender nó ghìm lại nên không hoạt động hết công suất được cũng đau. Cũng phần nào lý giải tại sao mình thấy nhiều người chê Firefox chậm hơn Chrome trong khi mình dùng cả hai thì thấy Firefox nhẹ hơn Chrome.

> Đặt ngoại lệ cho Windows Defenders không scan thư mục `profile`
> : Vào `about:support`, copy đường dẫn ở `Profile Folder`, cho vào `Exclusion` của Windows Defenders
> : ![](/assets/img/firefox-optimize/windows-defenders-exclusion.jpg)
{: .prompt-tip }

### `nglayout.initialpaint.delay` [^ff-nglayout]

Firefox nói riêng, và các ứng dụng Mozzila nói chung, có cơ chế render website dần dần - tức là nhận được phần nào hiển thị phần đấy. Tuy nhiên, vì phần đầu của website thường không có nhiều thông tin, Firefox sẽ chờ một khoảng thời gian delay trước khi render lần đầu tiên. Tham số `nglayout.initialpaint.delay` và `nglayout.initialpaint.delay_in_oopif` thiết lập số migi-giây Firefox chờ tải các thành phần của trang web trước khi render lần đầu tiên (Mặc địch: 250). Giá trị thấp hơn sẽ làm cho trang ban đầu hiển thị nhanh hơn nhưng sẽ khiến trang mất nhiều thời gian hơn để hoàn tất hiển thị. Giá trị cao hơn sẽ có tác dụng ngược lại.

> Tăng giá trị `nglayout.initialpaint.delay` sẽ cực kỳ hiệu quả khi dùng add-on như Dark Reader, [chi tiết](../firefox-addon/#nguy%C3%AAn-nh%C3%A2n).
{: .prompt-tip }

Mở `about:cònig`
: Đặt `nglayout.initialpaint.delay` = `2000`
: Đặt `nglayout.initialpaint.delay_in_oopif` = `2000`

| nglayout.initialpaint.delay | 2000 |
| nglayout.initialpaint.delay_in_oopif | 2000 |

```javascript
// Delay to first render
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
```
{: file="user.js"}

### Lưu cache trên RAM [^ff-ram-cache]

Mở `about:config`
: Đặt `browser.cache.disk.enable` = `false`
: Đặt `browser.cache.memory.enable` = `true`.
: Đặt `browser.cache.memory.capacity`(_nếu chưa có: ấn chọn kiểu `Number` rồi ấn `+` để tạo mới_) theo giá trị tương ứng (_tính theo KB - Kilobytes):
: - An toàn: `1048576` (tương đương 1GB)
: - Firefox 32bit: `524288` (512MB) thôi vì ứng dụng 32bit có giới hạn số RAM (xấp xỉ 4GB) mà cứ vượt ngưỡng là sẽ treo ứng dụng (vì ở đây còn phải tính tới số RAM mà trang web đòi hỏi để render trang nữa, có những trang web siêu nặng như Youtube hay Facebook chỉ mở một tab là đi tong 1GB RAM nếu không dùng uBlock chặn quảng cáo)
: - Firefox 64bit + nhà đẻ ra RAM (tầm 16GB+): `2097152` - `4194304` (tầm 2-4GB)
: Đặt `browser.cache.memory.max_entry_size` = `512000` (mặc định là 5120 _quá ít_) 

```javascript
// Force RAM cache
user_pref("browser.cache.disk.enable", false);
user_pref("browser.cache.memory.enable", true);
user_pref("browser.cache.memory.capacity", 524288);
user_pref("browser.cache.memory.max_entry_size", 512000);
```
{: file="user.js"}

### Tắt Race Cache With Network (_RCWN_) [^ff-disable-rcwn]

> Kể từ phiên bản 59, Firefox có một tính năng gọi là Race Cache With Network (_RCWN_). Nếu phát hiện ổ đĩa chậm(như _HDD đời Tống_ - Firefox 59 release năm 2018), Firefox có thể quyết định bắt đầu yêu cầu mạng ngay lập tức mà không cần chờ bộ đệm. 
{: .prompt-info }

Đó là một sự đánh đổi: 
: Nếu các yêu cầu mạng nhanh hơn, độ trễ sẽ được cải thiện; 
: Nếu cache nhanh hơn thì băng thông mạng đã bị lãng phí.

Vào `about:config`
: Đặt `network.http.rcwn.enabled` = `false`

| network.http.rcwn.enabled | false |

```javascript
// Force RAM cache - Disable RCWN
user_pref("network.http.rcwn.enabled", false);
```
{: file="user.js"}

### Tắt SkeletonUI

Do cấu hình của Floorp tắt SkeletonUI đi mặc Firefox/tete/Mercury đều bật mặc định, vào config chỉnh. Cái SkeletonUI này giúp bật phát hiện luôn Firefox, nên không có lý do gì để mà tắt cả và nó hữu ích cho người già, vì họ thường nhấp liên tục vào biểu tượng trình duyệt nếu chưa thấy cửa sổ hiện lên, nhiều khi bật hàng trăm hàng nghìn Firefox lên gây tràn luôn cả RAM:

| browser.startup.preXulSkeletonUI | false |

```javascript
// Disable SkeletonUI
user_pref("browser.startup.preXulSkeletonUI", false );
```
{: file="user.js"}

Xem thêm
: <https://firefox-source-docs.mozilla.org/dom/ipc/process_model.html>
: <https://searchfox.org/mozilla-central/source/dom/ipc/ProcessIsolation.cpp>

### Tắt Accessibility

> Accessibility giúp các ứng dụng ngoài (Screen Reader, Antivirus, ứng dụng trợ năng..) can thiệp sâu vào Firefox để cải thiện trải nghiệm
{: .prompt-info }

Mở `about:config`
: Đặt `accessibility.force_disabled` = `1`

| accessibility.force_disabled| 1 |

```javascript
// Disable Accessibility
user_pref("accessibility.force_disabled", 1 );
```
{: file="user.js"}

### Giảm RAM _(đánh đổi bằng bảo mật)_ (Chi tiết về cách thức hoạt động và các cấp độ của Fission)

> Dưới đây là tối ưu giảm RAM, đặc biệt hiệu quả khi dùng [Progressive Web Application](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24276732) do đặc thù chỉ dùng 1 trang web của nó.
{: .prompt-info }

Làm theo những cái bôi đen trong mục Tối ưu Firefox: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-22174347>

| dom.ipc.processCount | 1 |
| fission.autostart | false |

```javascript
// Reduce RAM usage (lower security)
user_pref("dom.ipc.processCount", 1 );
user_pref("fission.autostart", false );
```
{: file="user.js"}

#### Các cấp độ Fission

1. Không giới hạn số tiến trình: *Chính là cài đặt mặc định*
: Nội dung (bao gồm: page, iframe, ...) đến từ mỗi root domain được xử lý bởi tiến trình riêng (dù là trong cùng 1 tab). VD: mở cái link sau đây sẽ thấy Firefox dùng 9 "Isolated web content process" và 1 "Isolated service worker process" cho riêng tab đó: <https://voz.vn/u/haidangtueba.1457647/>. Check tại `about:processes` hoặc `about:support#remote-processes`.
: Nội dung trong nhiều tab nhưng đến từ cùng 1 root domain được dùng không quá 4 tiến trình (giá trị mặc định của *dom.ipc.processCount.webIsolated*).

2. Giới hạn bởi số root domain: `dom.ipc.processcount.webisolated = 1`
: Nội dung trong nhiều tab nhưng đến từ cùng 1 root domain được dùng 1 tiến trình. VD: mở 7 tab [www.google.com](https://www.google.com), mail.google.com, docs.google.com, drive.google.com[COLOR=rgb(44, 130, 201)], cloud.google.com[COLOR=rgb(44, 130, 201)], translate.google.com[COLOR=rgb(44, 130, 201)], bard.google.com[/COLOR] [/COLOR][/COLOR] chỉ tốn 1 "Isolated web content process".

3. Giới hạn bởi content value: `fission.webContentIsolationStrategy = 2`
: Chỉ những *high value content* mới chạy trong tiến trình riêng (không rõ Mozilla coi những trang nào là high value, chắc là các trang payment, email...), các Nội dung còn lại sẽ được xử lý bởi các "Shared web content process", số process này chính là giá trị của *dom.ipc.processCount*.

4. Không tách biệt Nội dung: `fission.webContentIsolationStrategy = 0`
: Gần giống với tắt Fission vì hầu hết Nội dung đều được xử lý bởi "Shared web content processes" nhưng vẫn có các tiến trình riêng để xử lý service workers.

5. Tắt Fission: `fission.autostart = false`
: Mọi nội dung đều được xử lý bởi "Shared web content processes".

Có thể thấy từ **cấp độ 3** trở xuống thì `dom.ipc.processCount` mới có ý nghĩa.

Thói quen, sở thích duyệt web kết hợp với cấu hình máy của thím sẽ giúp thím tìm được setup phù hợp. :sexy_girl:



## Tối ưu giao diện, trải nghiệm sử dụng

### Mở Early Hints để tăng tốc độ tải trang[^ff-enable-early-hints]

> `HTTP 103 Early Hints` là phản hồi của server ngay từ lúc đang xử lý yêu cầu, bao gồm các gợi ý về các tài nguyên _được cho là_ sẽ sử dụng. Điều này cho phép trình duyệt bắt đầu `tải trước tài nguyên` trước khi server xử lý xong và trả về kết quả.
>
> _Xem thêm:_ <https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/103>
{: .prompt-info }

```javascript
// Enable Early hints
user_pref("network.early-hints.enabled", true);
user_pref("network.early-hints.preconnect.enabled", true);
user_pref("network.early-hints.preconnect.max_connections", 20);
```
{: file="user.js"}

### Chế độ Compact (gọn gàng) có sẵn của Firefox[^ff-enable-compact-ui]

| browser.compactmode.show | true |

```javascript
// Compact mode (slim toolbar)
user_pref("browser.compactmode.show", true );
```
{: file="user.js"}

Sử dụng
: Chuột phải vào thanh toolbar
: Chọn `Customize` ![](https://voz.vn/attachments/1685073662176-png.1857635/)
: Chọn `Compact`

Kết quả nó sẽ gọn như này
: ![](https://voz.vn/attachments/1685073724165-png.1857641/)

### Chế độ bỏ qua Cookie Banner[^ff-remove-cookie-banner]

#### Bỏ qua tuy nhiên nếu cần thiết Chấp nhận:

| cookiebanners.service.mode | 2 |
| cookiebanners.service.mode.privateBrowsing | 2 |

#### Bỏ qua hết (nếu không cho bỏ qua thì không ẩn được):

| cookiebanners.service.mode | 1 |
| cookiebanners.service.mode.privateBrowsing | 1 |

```javascript
// Bypass Cookie Banners: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPT - to remove banner);
user_pref("cookiebanners.service.mode", 2 );
user_pref("cookiebanners.service.mode.privateBrowsing", 2 );
```
{: file="user.js"}

Test trên Firefox 113, hoạt động cực tốt. Đỉnh nhất trong các sự lựa chọn ẩn cookie vì nó dùng 2 thuật toán chính, click như người thật (tốt hơn add-on là click máy) và nhúng cookie:

| cookiebanners.bannerClicking.enabled | true |
| cookiebanners.cookieInjector.enabled | true |

```javascript
// Bypass Cookie Banners - emulator CLICK, cookie INJECTOR: 
user_pref("cookiebanners.bannerClicking.enabled", true );
user_pref("cookiebanners.cookieInjector.enabled", true );
```
{: file="user.js"}

Các trang test:
: <https://stackoverflow.com/questions/37365561/flexbox-row-inside-flexbox-column>

### Smooth scroll

```javascript
// Smooth scroll
user_pref("apz.overscroll.enabled", true);
user_pref("general.smoothScroll", true);
user_pref("mousewheel.enable_pixel_scrolling", false );
user_pref("mousewheel.default.delta_multiplier_y", 275 );
user_pref("general.smoothScroll.mouseWheel.durationMaxMS", 250 );
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 200 );
```
{: file="user.js"}

## Tối ưu kết nối mạng
### Tắt OCSP, mở CRlite thay thế [^ff-disable-ocsp][^ff-enable-crlite]

> OCSP (máy chủ xác thực trạng thái chứng chỉ) Firefox cứ mỗi khi các bạn kết nối với một trang web, nó sẽ gửi cái chứng chỉ đến OSCP để kiểm tra độ tin cậy của chứng chỉ, xem nó đã hết hạn hay bị giả mạo hay không thì sẽ bị buộc thu hồi.
>
> Nhược điểm của OCSP
> : Ảnh hưởng tới tốc độ kết nối tới trang web của Firefox
> : Tiết lộ thói quen sử dụng với bên thứ 3
> : Không thể truy cập web nếu máy chủ OCSP lỗi
{: .prompt-info }

> Firefox bật OCSP mặc định, Chrome đã tắt OCSP đi từ rất lâu rồi.
{: .prompt-info }

#### Tắt OSCP

Vào `about:config`
: Đặt `security.OCSP.enabled` = `0`

```javascript
// Disable OSCP
user_pref("security.OCSP.enabled", 0);
```
{: file="user.js"}
#### Mở CrLite thay thế [^ff-enable-crlite]

```javascript
// Enable CrLite
user_pref("security.remote_settings.crlite_filters.enabled", true);
user_pref("security.pki.crlite_mode", 2);
```
{: file="user.js"}

Link:
: <https://bugzilla.mozilla.org/buglist.cgi?bug_id=1429800,1670985,1753071>
: <https://blog.mozilla.org/security/tag/crlite/>

### Tối ưu DNS [^ff-dns-http3-quicv2]

#### Nếu dùng NextDNS

Vào `about:config`:
: Đặt `network.trr.uri` là `https://doh3.dns.nextdns.io/`
: Đặt `network.trr.custom_uri` là `https://doh3.dns.nextdns.io/`
: Đặt `network.trr.mode` là `2`

| network.trr.uri | https://doh3.dns.nextdns.io/ |
| network.trr.custom_uri | https://doh3.dns.nextdns.io/ |
| network.trr.mode | 2 |

```javascript
// Next DNS
user_pref("network.trr.uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io/");
user_pref("network.trr.mode", 2);
```
{: file="user.js"}

> Nếu muốn dùng profile NextDNS của cá nhân, sửa thành `https://doh3.dns.nextdns.io/ID_NEXTDNS`, ví dụ `https://doh3.dns.nextdns.io/abc123`. Nên sử dụng profile cá nhân với thiết lập `không chặn quảng cáo` để tăng tính ổn định cho Firefox bởi uBlock bao khoản chặn quảng cáo rồi, nếu chặn thêm bằng NextDNS thì sẽ gây lỗi web hay bị phát hiện. 
>
> Nói cách khác là _chỉ dùng NextDNS để lấy ECS kiếm máy chủ gần Việt Nam nhất cho Firefox_ - và để chặn các trang độc hại, lừa đảo.
{: .prompt-info }

#### Nếu dùng GoogleDNS:

| network.trr.disable-ECS | false |

Để ép Firefox gửi ECS cho trả về CDN gần.
 
| network.trr.uri | <https://dns.google/dns-query> |
| network.trr.custom_uri | <https://dns.google/dns-query> |
| network.trr.mode | 2 |

```javascript
// GoogleDNS - ECS
user_pref("network.trr.uri", "https://dns.google/dns-query");
user_pref("network.trr.custom_uri", "https://dns.google/dns-query");
user_pref("network.trr.mode", 2);
```
{: file="user.js"}

> Hoặc nếu bạn không muốn dùng NextDNS+GoogleDNS thì có thể thử Cloudflare Zero Trust: [Hướng dẫn dùng Cloudflare Zero Trust](https://voz.vn/t/huong-dan-dung-cloudflare-zero-trust.822971/)
{: .prompt-info }

#### Bật QUICv2

Cách thức
: <https://github.com/kelmenhorst/quic-censorship/blob/main/browsers.md>
: <https://datatracker.ietf.org/doc/draft-duke-httpbis-quic-version-alt-svc/>)

| network.http.http3.alt-svc-mapping-for-testing | doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1" |

```javascript
// Enable QUICv2
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1"');
```
{: file="user.js"}

### Sự hữu ích khi dùng DNS có ECS[^info-dns-ecs]

Ping lần đầu vào DNS thì nó cache lại được, vì đây là ping lấy IP máy chủ, lần tiếp theo thì sẽ là 0ms

Tuy nhiên khoảng thời gian trả dữ liệu lại từ máy chủ thì **thứ duy nhất làm giảm ping là máy chủ gần vị trí mình đang đặt đít**, và đó là lý do tại sao ECS cần thiết nên NextDNS và GoogleDNS+ECS/Quad9 (bản <https://dns11.quad9.net/dns-query>) tốt hơn

Còn lý do tại sao nên dùng NextDNS đó là ECH nữa, hiện tại chỉ NextDNS và 1.1.1.1 hỗ trợ bản ghi TYPE65 giúp trình duyệt web lên được ECH, giúp vượt vũ môn vào Bonhup, Ếch Vít, Medium...

Ngoài ra NextDNS hỗ trợ chặn web độc hại/lừa đảo (giúp người thân thoát dính họa sát thân vào trang các cược cược tung cái nhà, hay bị nhà tôi ba đời lừa mua thuốc trị bách bệnh...), web mới tạo (đa phần là virus) giúp giảm tối thiểu khả năng sẽ chết vì virus vì thường nếu nó chặn tên miền mới nó chặn luôn tên miền thằng hacker nó dùng để gửi thông tin mà spyware lấy được, chặn thì nó không lấy được gì

Vậy nên nếu không dùng NextDNS thì ít nhất cũng dùng GoogleDNS+ECS chứ tội gì dùng AdguardDNS. :D

Nói chung vấn đề Greencloud hay bị chập chờn chắc do đội của ông tay to @bedepver1 đang chỉnh chọt định tuyến, các bạn hỏi han tinh hình thì cứ hỏi, còn giải pháp:

- Dùng Anexia
- Dùng GoogleDNS+ECS

### Sử dụng NextDNS hợp lý[^guide-nextdns]

Tiện đây mình cũng chia sẻ một thói quen tốt khi dùng NextDNS, đó là: **Hai tay hai súng**

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

> Sử dụng profile _không chặn quảng cáo_ trong trình duyệt web: giống bài này vì thứ tư ưu tiên trình duyệt web luôn dùng DNS mình đặt trong trình duyệt và dùng kèm add-on chặn quảng cáo như uBlock/Adguard
{: .prompt-info }

Như vậy trải nghiệm sẽ là tốt nhất, vì trình duyệt web sợ anti-adblock, cơ mà dùng kiểu này anti-adblock bị uBlock chém rồi nên NextDNS chỉ phải lo đảm bảo an toàn không gian mạng cho mình.

### Tool để kiểm tra traceroute hiển thị cả quốc gia[^tool-traceroute]

Dùng tool chuyên dụng chạy tracert, nếu thấy toàn Việt Nam là ngon: <https://www.nirsoft.net/utils/country_traceroute.html>

![https://www.nirsoft.net/utils/countrytraceroute.png](https://www.nirsoft.net/utils/countrytraceroute.png)

Cái hay của tool này là nó hiện quốc gia luôn, biết ngay mình bị cho du lịch sang đâu.

## Bảo vệ riêng tư, bảo mật

### Kháng Tracking + Canvas Fingerprint + Font Fingerprint với RFP + FluxFont [^ff-anti-tracking]

> **Lưu ý nhỏ:** Riêng tư và bảo mật luôn đi kèm sự thay đổi hoặc bất tiện, cân nhắc kỹ trước khi làm theo.
{: .prompt-warning }

> Chi tiết những thay đổi khi dùng RFP: <https://librewolf.net/docs/faq/#what-are-the-most-common-downsides-of-rfp-resist-fingerprinting>
> _Trích lược_: 
> Các vấn đề trong quá trình sử dụng có thể gặp:
> : Ảnh hiển thị bị sọc
> : Sai múi giờ 
> : Light theme
> : Kích thước cửa sổ nhỏ hơn và cố định khi khởi động. 
> : Chặn các sự kiện sửa đổi bàn phím bằng phím Alt.
{: .prompt-info }

Vào `about:config`
: Đặt `privacy.resistFingerprinting` = `true`

```javascript
// Resist Fingerprint (RFP)
user_pref("privacy.resistFingerprinting", true);
```
{: file="user.js"}
### Bật `punycode` để miễn nhiễm với tên miền giả mạo

Bảo mật và riêng tư luôn đi liền với bất tiện, nhìn chung nên xác định điều này và Firefox mặc định nó đủ bảo mật và riêng tư rồi, chỉ cái:

| network.IDN_show_punycode | true |

Là ai cũng nên bật vì nó sẽ phá mấy trang web dùng unicode thành dạng `xn--abcxyz` giúp mấy trang lừa đảo giả tên miền kiểu `google.com` không còn linh nữa.

Ví dụ `フラワーナイトガール.攻略wiki.com` khi bật punycode sẽ bị buộc thành `xn--eckq7fg8cygsa1a1je.xn--wiki-4i9hs14f.com`

Hoặc ngoạn mục là `GOOGᒪE.com` được sửa thành `xn--googe-bkz.com`, `𝐠𝐨𝐨𝐠ʟ𝐞.𝐜𝐨𝐦` thành `xn--googe-hxc.com`

Đó là sự đáng sợ của tên miền giả mạo, và tụi hacker tụi nó không nhân từ như mình mà nó y hệt `google.com` luôn.

```javascript
// Enable punnycode
user_pref("network.IDN_show_punycode", true);
```
{: file="user.js"}

### Tắt sạch tác vụ chạy nền bằng code của ArkenFox [^ff-disable-telementry]

> Link: <https://github.com/arkenfox/user.js/blob/master/user.js>
{: .prompt-info }

Vào link chính chủ ở trên <https://github.com/arkenfox/user.js/blob/master/user.js>
: copy mục `0330` tới mục `0405` 

> **Chú ý** không copy toàn bộ vì cái Arkenfox này khiến Firefox khó dùng gấp trăm lần .
{: .prompt-warning }

```javascript
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
{: file="user.js"}

## Nguồn:
[^ff-optimize-aio]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-280#post-27527209>
[^ff-nglayout]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-38#post-23570551>
[^ff-ram-cache]: <https://voz.vn/t/cach-ep-firefox-luu-cache-tren-ram-ma-khong-can-ramdisk.664955/>
[^ff-disable-rcwn]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-262#post-27409530>
[^ff-anti-tracking]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-97#post-24757875>
[^ff-disable-telementry]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-17#post-22955672>
[^ff-disable-ocsp]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-69#post-24344300>
[^ff-enable-crlite]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24344471>
[^ff-dns-http3-quicv2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-85#post-24688026>
[^guide-nextdns]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-27558297>
[^tool-traceroute]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-25489531>
[^info-dns-ecs]: <https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/post-25454142>
[^ff-http3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24688423>
[^ff-enable-ech]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24916883>
[^ff-enable-early-hints]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-188#post-25845776>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-194#post-25938099>
[^ff-remove-cookie-banner]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-106#post-24935068>
[^ff-enable-compact-ui]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-157#post-25530119>