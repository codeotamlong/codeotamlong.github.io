---
title: "[Firefox Awesome] Tối ưu Firefox (P2): Kháng Tracking, tắt tác vụ chạy nền"
date: 2023-10-03 21:00:00 +0700
categories: [awesome, firefox, optimize]
tags: [awesome, firefox, optimize]     ## TAG names should always be lowercase
---
> Có **02*- cách chính để thay đổi các tham số của Firefox:
> 1. Vào `about:config`, tìm và sửa tham số theo nhu cầu
> 2. Sửa file `user.js` (**khuyến khích*- để có thể theo dõi thay đổi và backup):
>       + Mở `about:support` => Open Profile Folder
>       + Đóng Firefox (tắt hẳn - _chú ý với MacOS: Close khác với Quit_)
>       + Tạo mới nếu chưa có
>       + Thêm dòng mới `user_pref("<tham số>", <giá trị mới>);`
>       + Save và mở Firefox
{: .prompt-info }

> `user.js` là file javascript nên có thể sử dụng `//` và `/**/` để viết ghi chú
{: .prompt-tip }

## Kháng Tracking + Canvas Fingerprint + Font Fingerprint với RFP + FluxFont [^fn-nth-2]

Cái này tí mình quên tại ban đầu là viết cho addon JShelter+Fluxfonts, chữa cháy tạm với RFP+Fluxfonts nên quên vụ ghi đè font của RFP này luôn, cảm ơn bạn đã chia sẻ. Vậy mình sẽ sử dụng post này để làm một bài về chống fingerprint rồi cho lên #1 cho dễ tra cứu.

> **Lưu ý nhỏ:***- Riêng tư và bảo mật luôn đi kèm sự thay đổi hoặc bất tiện, cân nhắc kỹ trước khi làm theo.
{: .prompt-warning }

Chi tiết những thay đổi khi dùng RFP: <https://librewolf.net/docs/faq/#what-are-the-most-common-downsides-of-rfp-resist-fingerprinting>**

Bài này sẽ hướng dẫn sử dụng cả Resist Fingerprint (RFP) và Fluxfonts:

- Bật Resist Fingerprint (RFP) trong Firefox bằng cách vào `about:config`
- Tìm `privacy.resistFingerprinting` chuyển thành true
- Tìm `layout.css.font-visibility.resistFingerprinting` chỉnh thành 3 (ép Firefox hiển thị Font hệ thống+gói ngôn ngữ+người dùng cài) để Fluxfonts phát huy tác dụng

```javascript
// Resist Fingerprint (RFP)
user_pref("privacy.resistFingerprinting", true);
user_pref("layout.css.font-visibility.resistFingerprinting", 3)
```
{: file="user.js"}

Cài Fluxfonts: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24027291>

> Nếu trường hợp Fluxfonts không hoạt động, dùng Font Fingerprint Defender thay thế: <https://addons.mozilla.org/vi/firefox/addon/font-fingerprint-defender/>**
{: .prompt-tip}

Vậy là xong, Resist Fingerprint sẽ giải quyết khá trọn vẹn một vấn đề đáng quan ngại là Canvas Fingerprint, còn Fluxfonts thì cứ 40 phút (hoặc ít hơn tùy ý chỉnh) sẽ đổi font một lần, kháng hoàn toàn Font Fingerprint.

Kiểm tra tại:

- Cho Canvas Fingerprint: <https://browserleaks.com/canvas>
- Cho Font Fingerprint: <https://browserleaks.com/fonts>
- Vài bài test khác: <https://browserleaks.com/> và <https://coveryourtracks.eff.org/>

## Tắt sạch tác vụ chạy nền, chia sẻ trải nghiệm của Firefox (an toàn 1000%) [^fn-nth-5]

100% tắt hết telemetry, không bao giờ hỏng dù một tính năng của Firefox.

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

Copy tất, tạo ra một file tên là `user.js` rồi ném thẳng vào folder profile Firefox tìm trong `about:support` -> `Open Profile Folder` -> Khởi động lại Firefox.

Nếu muốn tự update, vào link chính chủ copy mục `0330` tới mục `0405` y như trên, chú ý không copy toàn bộ vì cái Arkenfox này khiến Firefox khó dùng gấp trăm lần <https://github.com/arkenfox/user.js/blob/master/user.js>. Chi tiết:

Chi tiết
: * TELEMETRY
:  0330: disable new data submission [FF41+]
:  0331: disable Health Reports
:  0332: disable telemetry
:  0333: disable Telemetry Coverage
:  0334: disable PingCentre telemetry (used in several System Add-ons) [FF57+]
:  0335: disable Firefox Home (Activity Stream) telemetry
: * STUDIES
:  0340: disable Studies
:  0341: disable Normandy/Shield [FF60+]
: * CRASH REPORTS
:  0350: disable Crash Reports
:  0351: enforce no submission of backlogged Crash Reports [FF58+]
: * OTHER
:  0360: disable Captive Portal detection
:  0361: disable Network Connectivity checks [FF65+]
: ** [SECTION 0400]: SAFE BROWSING (SB)
:  0401: disable SB (Safe Browsing)
:  0402: disable SB checks for downloads (both local lookups + remote)
:  0403: disable SB checks for downloads (remote)
:  0404: disable SB checks for unwanted software
:  0405: disable "ignore this warning" on SB warnings [FF45+]

## Nguồn:
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-97#post-24757875>
[^fn-nth-5]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-17#post-22955672>