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

> Download: <https://github.com/codeotamlong/awesome/blob/main/firefox/user.js>
{: .prompt-tip }
       
```javascript    
/*
** ADD-ONS - CUSTOMIZE UI
*/

// Un-check singature extension
user_pref("xpinstall.signatures.required", false);
user_pref("xpinstall.whitelist.required", false);

// No exception on extension
user_pref("extensions.webextensions.restrictedDomains", "");

// Enable userChrome.css
user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);

// Compact mode
user_pref("browser.compactmode.show", true);

// Native Dark mode (?)
//user_pref("browser.display.use_system_colors", false );
//user_pref("browser.display.background_color", "#c0c0c0" );
//user_pref("browser.display.foreground_color", "#000000" );
//user_pref("browser.visited_color", "#aa3700" );
//user_pref("browser.anchor_color", "#800040" );
//user_pref("browser.display.document_color_use", 2 );

// Native Font
user_pref("font.name.serif.x-western", "Tahoma" );
user_pref("browser.display.use_document_fonts", 0 );

// Smooth scroll
user_pref("apz.overscroll.enabled", true);
user_pref("general.smoothScroll", true);
user_pref("mousewheel.enable_pixel_scrolling", false );
user_pref("mousewheel.default.delta_multiplier_y", 275 );
user_pref("general.smoothScroll.mouseWheel.durationMaxMS", 200 );
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 50 );

/*
** SPEED
*/

// Reduce render rate
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);

// Force RAM cache, uncomment // to enable
// user_pref("browser.cache.disk.enable", false);
// user_pref("browser.cache.memory.enable", true);
// user_pref("browser.cache.memory.capacity", 524288);
// user_pref("browser.cache.memory.max_entry_size", 512000);

// Force RAM cache - Disable RCWN
user_pref("network.http.rcwn.enabled", false);

// Disable SkeletonUI
user_pref("browser.startup.preXulSkeletonUI", false );

// Reduce disk read/write
user_pref("browser.sessionstore.idleDelay", 3600000);
user_pref("browser.sessionstore.interval", 3600000);
user_pref("browser.sessionstore.collect_zoom", false);
user_pref("browser.sessionstore.privacy_level", 2);
user_pref("browser.sessionstore.restore_pinned_tabs_on_demand", true);
user_pref("browser.sessionhistory.max_total_viewers", 0);

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

// Optimize HTTP3:
user_pref("network.http.http3.send_background_tabs_deprioritization", true );
user_pref("network.http.http3.version_negotiation.enabled", true );
user_pref("security.tls.ech.grease_http3", true );

// Force NextDNS on HTTP3 and QUICv2 by altsvc:
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io;h3=":443"; quicv="6b3343cf,1"' );

// Trr
user_pref("network.dns.skipTRR-when-parental-control-enabled", false );
user_pref("network.trr.async_connInfo", true );
user_pref("network.trr.confirmation_telemetry_enabled", false );
// user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io" );
user_pref("network.trr.disable-ECS", false );
user_pref("network.trr.mode", 3 );
// user_pref("network.trr.uri", "https://doh3.dns.nextdns.io" );

// Unlimited DNS queries
user_pref("network.dnsCacheEntries", -1 );



/*
** MISC
*/

// Enable Early Hints
user_pref("network.early-hints.enabled", true);
user_pref("network.early-hints.preconnect.enabled", true);
user_pref("network.early-hints.preconnect.max_connections", 20);

// Enable punycode
user_pref("network.IDN_show_punycode", true);

// Bypass Cookie Banners: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPTS - to remove banner);
user_pref("cookiebanners.service.mode", 2 );
user_pref("cookiebanners.service.mode.privateBrowsing", 2 );
// Bypass Cookie Banners - emulator CLICK, cookie INJECTOR:
user_pref("cookiebanners.bannerClicking.enabled", true );
user_pref("cookiebanners.cookieInjector.enabled", true );

// UserChrome.CSS Floating Findbar on Right (as Google Chrome)
user_pref("userchrome.floating-findbar-on-right.enabled", true);

/*
** PRIVACY
*/

// Anti Tracking+Canvas Fingerprint+Font Fingerprint
user_pref("privacy.resistFingerprinting", true);

// Disable Pocket and Accessibility
user_pref("extensions.pocket.enabled", false);
user_pref("accessibility.force_disabled", 1);

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

## Đặt ngoại lệ antivirus để Firefox không bị hãm tốc độ[^ff-nglayout]

Không hề bình thường, vì antivirus thường có thói quen scan linh tinh, virus thì chả thấy đâu nhưng tài nguyên hệ thống thì tốn thấy rõ nên mình bỏ dùng antivirus 10 năm nay rồi, chưa từng nhiễm virus một lần kể từ đó lại còn không bao giờ gặp phải lỗi không tương thích do antivirus tụi nó tì đè vào ứng dụng đang hoạt động nữa. (một vài ví dụ rõ nhất là vụ antivirus chặn giao thức QUIC, khiến nhiều người không dùng được DNS over QUIC)

Giải pháp:
: Cho Firefox (cả folder chứa firefox.exe và folder profile) vào ngoại lệ của WD để nó không bao giờ động chạm vào Firefox nữa
: Tắt tính năng thời gian thực của WD
: Tắt hoàn toàn WD


Nguồn đây: <https://bugzilla.mozilla.org/show_bug.cgi?id=1441918> (có cái bình luận này <https://bugzilla.mozilla.org/show_bug.cgi?id=1441918#c61> đáng chú ý, tắt cache trên ổ đĩa đi thì CPU hạ hẳn, cũng dễ hiểu vì WD chắc chắn scan cache của Firefox, làm theo bài này mình chỉ cách tắt cache đĩa và dùng cache RAM <https://voz.vn/t/cach-ep-firefox-luu-cache-tren-ram-ma-khong-can-ramdisk.664955/>)

> Trích <https://www.reddit.com/r/reddit/firefox/comments/zpz2aj>
>> Using Process Monitor to count MsMpEng events for 30 seconds after reloading youtube.com (Ctrl+F5) I get the following (numbers are very rough):
>> 
>> Firefox (disk cache on): 1300 total events, 800 cache events, 50 files, 3MB
>> Firefox (disk cache off): 300 total events, 0 cache events, 0 files, 0MB
>> Chrome: 500 total events, 90 cache events, 10 files, 2MB
>> Edge: 400 total events, 0 cache events (800 ignored), 45 files, 7MB 

Theo những gì ông dev của Firefox test, chỉ có duy nhất Firefox là bị WD scan cache và bị scan nhiều gấp chục lần với 2100 lần với 800 lần bị scan cache, Chrome 590 lần với 90 lần scan cache, Edge 400 lần và không hề bị scan cache, Chrome và Edge không bị nên có thể 30% CPU khi mở tab của bạn là do đây. Nhìn chung WD nó ưu ái Edge nhất. (cạnh tranh bẩn)

Hình như phía Firefox cũng bó tay rồi, 5 năm rồi không sửa nổi 5 năm bị đì đọt trên Windows. Kiểu cảm giác là lẽ ra Firefox phải hoạt động tầm 30-50% nhanh hơn nhưng vì bị thằng Windows Defender nó ghìm lại nên không hoạt động hết công suất được cũng đau. Cũng phần nào lý giải tại sao mình thấy nhiều người chê Firefox chậm hơn Chrome trong khi mình dùng cả hai thì thấy Firefox nhẹ hơn Chrome.

Hướng dẫn: <https://www.thegioididong.com/hoi-dap/cach-sua-loi-windows-defender-chiem-qua-nhieu-tai-nguyen-1322722>
Chú ý: Đoạn đặt ngoại lệ thư mục thì mở about:support trong Firefox rồi Open Profile Folder sau đó copy đường dẫn folder vào mục ngoại lệ của WD để ngoại lệ hoàn toàn vụ scan cache (cache chả bao giờ nhiễm virus vào máy được đâu nên không lo, vì nó còn chả có đuôi file).

Nói chung kinh nghiệm để sống khỏe với antivirus:
- Tắt hết tính năng thời gian thực (scan mạng, scan driver..) mà chỉ bật duy nhất tính năng tự động scan khi mở thư mục (tính năng siêu căn bản của antivirus cho những ai cẩn trọng, cứ mở folder cái nó scan toàn bộ folder) và thấy file lạ thì chuột phải vào rồi cho antivirus scan, còn an toàn hơn thì ném vô sandbox.

Chỉ cần như trên là quá an toàn rồi, để nó scan lưu lượng mạng chỉ tốn tài nguyên hệ thống mà chả bao giờ ra virus.

P/s: Sắp tới bài viết về tối ưu Firefox của mình sẽ phải có vụ đặt ngoại lệ folder Firefox trong antivirus rồi, không ngoại lệ thì chả khác gì chấp Edge với Chrome 30% CPU.

## nglayout.initialpaint.delay khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU[^ff-nglayout]

Ngày xưa hồi mà các bài báo Việt Nam đăng ồ ạt về tối ưu Firefox ấy, thì cái `nglayout.initialpaint.delay` là một trong những tối ưu sai rất sai khi họ khuyên người dùng hạ xuống thấp hơn 250, thực ra để giá trị này cải thiện hiệu năng thì nên tăng lên vì Firefox giờ rất thông minh rồi, tăng lên 1000000000000 thì khi trang tải xong Firefox cũng render một chạm cả trang luôn, cơ mà mình toàn để 2000 (nghĩa là nhắc Firefox cứ làm sao thì làm, sau 2s phải hiển thị trang web dựa trên những gì đã tải được) vì nhỡ sao trang web nó bị chậm có vài file css, js tải mãi không xong thì đợi dài cổ :D

Tăng giá trị `nglayout.initialpaint.delay` sẽ cực kỳ hiệu quả khi dùng add-on như Dark Reader, [chi tiết](../firefox-addon/#nguy%C3%AAn-nh%C3%A2n).

**Cách thức:**
- Mở `about:config`, tìm và sửa lại:

| nglayout.initialpaint.delay | 2000 |
| nglayout.initialpaint.delay_in_oopif | 2000 |

```javascript
// Reduce render rate
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
```
{: file="user.js"}

_Xem thêm_

: [Một cái nhìn khái quát hơn về cách Firefox render trang web cũng như tối ưu xa hơn giữa `nglayout.initialpaint.delay` và `content.notify.interval`.](../firefox-addon/#m%E1%BB%99t-c%C3%A1i-nh%C3%ACn-kh%C3%A1i-qu%C3%A1t-h%C6%A1n-v%E1%BB%81-c%C3%A1ch-firefox-render-trang-web-c%C5%A9ng-nh%C6%B0-t%E1%BB%91i-%C6%B0u-xa-h%C6%A1n-gi%E1%BB%AFa-nglayoutinitialpaintdelay-v%C3%A0-contentnotifyinterval)
: [Nguyên nhân](../firefox-addon/#nguy%C3%AAn-nh%C3%A2n)

## Ép Firefox lưu cache trên RAM mà không cần RAMDisk [^ff-ram-cache]

Chào cả nhà, cá nhân là một người đã dùng Firefox từ hồi 3.x, cũng học được khá nhiều mẹo mà đảo qua thấy anh em ngày nay toàn chê Firefox chuộng Chrome mà chưa hiểu hết những cái hay của Firefox nên tiện đây mình làm một thread khởi đầu cho series chia sẻ thủ thuật Firefox trong tương lai, mục đích nữa là muốn phổ biến Firefox hơn để ngăn thế độc quyền của Chrome khiến Google tuỳ ý cắt xén, bóp méo thế giới web (ví dụ: ManifestV3 gần như giết chết AdBlock, 1st Party Sets sau này biến trang bên thứ 3 thành bên thứ nhất, giúp theo dõi người dùng dễ dàng...).

Mở đầu là cách chuyển cache (bộ nhớ đệm) của Firefox lên RAM hết. Như cái bạn biết khi các bạn vào Facebook, Youtube hay gì gì thì trình duyệt sẽ tải các file .js, .css, .json, ảnh... vào thư mục cache, điều này không thực sự tốt cho ổ cứng SSD, cũng như RAM thời nay rẻ như bèo, nên chuyển hết cache lên RAM thì sẽ đạt hiệu năng cao hơn.

Mà Firefox thì hay hơn Chrome rất nhiều vì có thể bê nguyên cache lên RAM mà KHÔNG cần phải cài RAMDisk, để làm được như vậy các bạn làm như sau, rất ngắn thôi vì là thread khởi đầu series:

Trên thanh địa chỉ gõ:

`about:config`

Rồi chọn Tổi hiểu/I Understand gì gì đó, sau đó ở khung tìm kiếm gõ cache rồi tìm `browser.cache.disk.enable`- chuyển giá trị thành `false`, tiện đó kiểm tra xem `browser.cache.memory.enable`- đã là `true`- chưa, nếu chưa `true` - thì chuyển thành `true`.

Tiếp theo ấn chuột phải vào giữa `about:config`, `Add` -> `Integer` và tạo một khoá tên `browser.cache.memory.capacity`- (nếu có sẵn, các bạn search `browser.cache.memory.capacity` - rồi nháy đúp vào rồi thay giá trị thay vì tạo mới như mình nhé) và gắn cho nó một con số nào đấy như:

- An toàn: 1048576 (giá trị này tính bằng KB, nghĩa là 1GB)
- Firefox 32bit: nếu dùng Firefox bản 32bit thì đặt là 524288 (512MB) thôi vì ứng dụng 32bit có giới hạn số RAM (xấp xỉ 4GB) mà cứ vượt ngưỡng là sẽ treo ứng dụng (vì ở đây còn phải tính tới số RAM mà trang web đòi hỏi để render trang nữa, có những trang web siêu nặng như Youtube hay Facebook chỉ mở một tab là đi tong 1GB RAM nếu không dùng uBlock chặn quảng cáo)
- Firefox 64bit + nhà đẻ ra RAM: Nếu có nhiều RAM tầm 16GB+  đặt 2-4GB (2097152-4194304)

Và tìm tiếp `browser.cache.memory.max_entry_size` - chuyển thành 512000 (mặc định là 5120 quá ít, vô dụng) để nó tính số lượng file cache được lưu vô RAM nhé.

Vậy là xong rồi, vào đại một trang web nào đó rồi mở about:cache lên sẽ thấy tất cả cache được chuyển qua RAM hết, vậy là từ nay SSD sẽ không bị đọc ghi bởi Firefox nữa, cũng như tốc độ tải cache cũng sẽ tăng đặc biệt nếu bạn dùng HDD mà có nhiều RAM.

> Chú ý là tối ưu cho cache lên RAM sẽ hiệu quả nhất nếu bạn tạo thói quen không tắt Firefox thường xuyên, dữ liệu trên RAM tuy nhanh hơn cả SSD nhưng khi tắt Firefox sẽ mất hết, hiện tại Firefox đã tối ưu cho việc mở hàng tháng trời không cần tắt nên tắt đi bật lại không khiến Firefox nhanh hơn mà chỉ phí thời gian bật lên lại.
{: .prompt-info }

Vì một hệ sinh thái Firefox xanh sạch đẹp.

```javascript
// Force RAM cache
user_pref("browser.cache.disk.enable", false);
user_pref("browser.cache.memory.enable", true);
user_pref("browser.cache.memory.capacity", 524288);
user_pref("browser.cache.memory.max_entry_size", 512000);
```
{: file="user.js"}

### Tắt RCWN để Firefox chung thủy với RAM cache [^ff-disable-rcwn]

Kể từ phiên bản 59, Firefox có một tính năng gọi là Race Cache With Network (_RCWN_). Nếu phát hiện ổ đĩa chậm(như _HDD đời Tống_ - Firefox 59 release năm 2018), Firefox có thể quyết định bắt đầu yêu cầu mạng ngay lập tức mà không cần chờ bộ đệm. 

Đó là một sự đánh đổi: 
: Nếu các yêu cầu mạng nhanh hơn, độ trễ sẽ được cải thiện; 
: Nếu cache nhanh hơn thì băng thông mạng đã bị lãng phí.

Để vô hiệu hóa: Vào `about:config` chỉnh:

| network.http.rcwn.enabled | false |

```javascript
// Force RAM cache - Disable RCWN
user_pref("network.http.rcwn.enabled", false);
```
{: file="user.js"}

Vậy là từ nay Firefox sẽ chỉ chung thủy sắt son với RAM thôi chứ không có ý định ngoại tình với mạng.

## Kháng Tracking + Canvas Fingerprint + Font Fingerprint với RFP + FluxFont [^ff-anti-tracking]

Cái này tí mình quên tại ban đầu là viết cho add-on JShelter+Fluxfonts, chữa cháy tạm với RFP+Fluxfonts nên quên vụ ghi đè font của RFP này luôn, cảm ơn bạn đã chia sẻ. Vậy mình sẽ sử dụng post này để làm một bài về chống fingerprint rồi cho lên #1 cho dễ tra cứu.

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

## Tắt sạch tác vụ chạy nền, chia sẻ trải nghiệm của Firefox (an toàn 1000%) [^ff-disable-telementry]

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

## Tắt OCSP để tăng tốc kết nối tới trang web[^ff-disable-ocsp] (ngoài ra có thể mở CRlite thay thế[^ff-enable-crlite], @Bin_kutakoto_99)

Do thám bằng [vài post về chủ đề tốc độ cho Firefox](https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24223961)  xong thấy các bợn có vẻ cũng hứng thú với tăng tốc Firefox, vậy hôm nay tiếp tục chia sẻ một mẹo tăng tốc Firefox, đó là tắt OCSP.

Đầu tiên cần hiểu OCSP là gì, nó hoạt động ra sao thì Firefox cứ mỗi khi các bạn kết nối với một trang web, nó sẽ gửi cái chứng chỉ đến máy chủ OCSP (máy chủ xác thực trạng thái chứng chỉ) để kiểm tra độ tin cậy của chứng chỉ, xem nó đã hết hạn hay bị giả mạo hay không thì sẽ bị buộc thu hồi, đó gọi là OCSP.

Thế nhưng việc kết nối tới máy chủ để kiểm tra như vậy có nhiều nhược điểm:

- Thứ nhất là ảnh hưởng tới tốc độ kết nối tới trang web của Firefox, nhanh thì tốn nửa giây, chậm thì hơn, đứt cáp thì còn hơn nữa vì máy chủ đặt xa tít mù khơi
- Tự dưng đi khoe với một thằng ất ơ mình vào gần như tất cả mọi trang web, trừ HTTP ra, ảnh hưởng tới tính riêng tư
- Nếu máy chủ OCSP sập thì khỏi vào web
- Có thể dễ dàng bị hacker quay như chong chóng nếu nó khiến bạn không kết nối vào máy chủ OCSP được rồi chuyển hướng tới máy chủ của nó (MITM)

> Firefox bật OCSP mặc định, Chrome đã tắt OCSP đi từ rất lâu rồi.
{: .prompt-info }

Vậy với những nhược điểm bên trên mà ưu điểm chẳng thấy đâu tốt nhất là nên tắt, ngoài ra mình là chuột bạch kể từ ngày Firefox thêm OCSP vào từ 3.x 4.x nào đó đến nay mà chưa thấy bị hack bao giờ cả, vậy nên cứ mạnh dạn tắt thôi.

Cách thức:

- Vào `about:config`
- Tìm `security.OCSP.enabled`
- Chuyển thành `0`

```javascript
// Disable OSCP
user_pref("security.OCSP.enabled", 0);
```
{: file="user.js"}
Đó, chỉ đơn giản vậy thôi, một bài viết dài quan trọng để giải thích cách thức hoạt động của nó, ưu nhược của nó, như vậy sẽ hiểu sâu được nguyên nhân dẫn đến kết quả.

Triết lý tối ưu Firefox của mình là vậy, hiểu rõ, hiểu sâu nên một bài chỉ một mẹo duy nhất.

Sẽ còn nữa nhé, chủ đề sắp tới sẽ thú vị và độc, lạ hơn, có thể sẽ chưa bao giờ thấy mẹo tối ưu sắp tới. :D

### Mở CrLite thay thế [^ff-enable-crlite]

Tắt OCSP và mở CrLite. Nhanh hơn và bảo mật hơn

```javascript
// Enable CrLite
user_pref("security.remote_settings.crlite_filters.enabled", true);
user_pref("security.pki.crlite_mode", 2);
```
{: file="user.js"}


Link:
: <https://bugzilla.mozilla.org/buglist.cgi?bug_id=1429800,1670985,1753071>
: <https://blog.mozilla.org/security/tag/crlite/>

## Tối ưu DNS và (HTTP3+QUICv2 do bạn @Bin_kutakoto_99 chia sẻ) [^ff-dns-http3-quicv2]

Chậm cũng có thể do Microsoft trả về CDN ở tận trời Tây, nên sử dụng NextDNS/GoogleDNS (gửi ECS) để Tây nó trả về máy chủ gần Việt Nam, đặc biệt tránh dùng 1.1.1.1 cùi bắp vì nó trả về CDN tận Mỹ cuồng râm, cứ hiểu là 1.1.1.1 chỉ dành cho người Mỹ bản địa.

Vào thread NextDNS cài YogaDNS là dễ nhất, còn muốn mã mở dùng dnsproxy/dnscrypt.

Hoặc có thể đặt DNS Firefox thành NextDNS bằng cách `about:config`:

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

> Nếu muốn dùng profile NextDNS của riêng, sửa thành `https://doh3.dns.nextdns.io/ID_NEXTDNS`, ví dụ `https://doh3.dns.nextdns.io/75a58e` nghĩa là ID_NEXTDNS không chặn quảng cáo, tracking của [thread NextDNS\](https://voz.vn/t/tat-tan-tat-ve-dich-vu-nextdns.522718/), các bạn nên sử dụng ID này hoặc ID của riêng cá nhân với thiết lập tương đương để tăng tính ổn định cho Firefox bởi uBlock bao khoản chặn quảng cáo rồi, nếu dùng ID có chặn quảng cáo thì sẽ gây lỗi web hay bị phát hiện chặn quảng cáo bởi nhiều trang web khác, `nghĩa là các bạn chỉ dùng NextDNS để lấy ECS kiếm máy chủ gần Việt Nam nhất có thể cho Firefox - và để chặn các trang độc hại, lừa đảo`, cụ thể:
>
> | network.trr.uri | https://dns.nextdns.io/b7b3b7 |
> | network.trr.custom_uri | https://dns.nextdns.io/b7b3b7 |
> | network.trr.mode | 2 |
>
> ```javascript
> // Next DNS - ECS
> user_pref("network.trr.uri", "https://dns.nextdns.io/b7b3b7");
> user_pref("network.trr.custom_uri", "https://dns.nextdns.io/b7b3b7");
> user_pref("network.trr.mode", 2);
> ```
> {: file="user.js"}
{: .prompt-info }


### Bật QUICv2

Cách thức
: <https://github.com/kelmenhorst/quic-censorship/blob/main/browsers.md>
: <https://datatracker.ietf.org/doc/draft-duke-httpbis-quic-version-alt-svc/>)

| network.http.http3.alt-svc-mapping-for-testing | doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1" |

```javascript
// Enable QUICv2
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io; h3=":443"; quicv="709a50c4,1", dns.google; h3=":443"; quicv="709a50c4,1"');
```
{: file="user.js"}

### Tiện tay bật luôn ECH lên để hiệu lực Encrypted Client Hello tránh nhà mạng dòm ngó [^ff-enable-ech]

> Chú ý ở thời điểm hiện tại ECH đang là bản nháp, khi bật lên mạng sẽ bị trễ đi một chút
{: .prompt-warning }


> Nếu dùng GoogleDNS:
> | network.trr.disable-ECS | false |
>
> Để ép Firefox gửi ECS cho trả về CDN gần.
> 
> | network.trr.uri | <https://dns.google/dns-query> |
> | network.trr.custom_uri | <https://dns.google/dns-query> |
> | network.trr.mode | 2 |
>
> ```javascript
> // GoogleDNS - ECS
> user_pref("network.trr.uri", "https://dns.google/dns-query");
> user_pref("network.trr.custom_uri", "https://dns.google/dns-query");
> user_pref("network.trr.mode", 2);
> ```
> {: file="user.js"}

> Hoặc nếu bạn không muốn dùng NextDNS+GoogleDNS thì có thể thử Cloudflare Zero Trust: [Hướng dẫn dùng Cloudflare Zero Trust](https://voz.vn/t/huong-dan-dung-cloudflare-zero-trust.822971/)
{: .prompt-info }


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

### Sự hữu ích khi dùng DNS có ECS[^info-dns-ecs]

- Ping lần đầu vào DNS thì nó cache lại được, vì đây là ping lấy IP máy chủ, lần tiếp theo thì sẽ là 0ms
- Tuy nhiên khoảng thời gian trả dữ liệu lại từ máy chủ thì **thứ duy nhất làm giảm ping là máy chủ gần vị trí mình đang đặt đít, **và đó là lý do tại sao ECS cần thiết nên NextDNS và GoogleDNS+ECS/Quad9 (bản <https://dns11.quad9.net/dns-query>) tốt hơn
- Còn lý do tại sao nên dùng NextDNS đó là ECH nữa, hiện tại chỉ NextDNS và 1.1.1.1 hỗ trợ bản ghi TYPE65 giúp trình duyệt web lên được ECH, giúp vượt vũ môn vào Bonhup, Ếch Vít, Medium...
- Ngoài ra NextDNS hỗ trợ chặn web độc hại/lừa đảo (giúp người thân thoát dính họa sát thân vào trang các cược cược tung cái nhà, hay bị nhà tôi ba đời lừa mua thuốc trị bách bệnh...), web mới tạo (đa phần là virus) giúp giảm tối thiểu khả năng sẽ chết vì virus vì thường nếu nó chặn tên miền mới nó chặn luôn tên miền thằng hacker nó dùng để gửi thông tin mà spyware lấy được, chặn thì nó không lấy được gì

Vậy nên nếu không dùng NextDNS thì ít nhất cũng dùng GoogleDNS+ECS chứ tội gì dùng AdguardDNS. :D

Nói chung vấn đề Greencloud hay bị chập chờn chắc do đội của ông tay to @bedepver1 đang chỉnh chọt định tuyến, các bạn hỏi han tinh hình thì cứ hỏi, còn giải pháp:

- Dùng Anexia
- Dùng GoogleDNS+ECS

### Tối ưu HTTP3 [^ff-http3]

#### Tối ưu HTTP3:

| network.http.http3.send_background_tabs_deprioritization|true |
| network.http.http3.version_negotiation.enabled | true |
| security.tls.ech.grease_http3 | true |

```javascript
// Optimize HTTP3:
user_pref("network.http.http3.send_background_tabs_deprioritization", true );
user_pref("network.http.http3.version_negotiation.enabled", true );
user_pref("security.tls.ech.grease_http3", true );
```
{: file="user.js"}

#### Ép NextDNS chạy HTTP3 và QUICv2 bằng chỉnh altsvc:

| network.http.http3.alt-svc-mapping-for-testing | doh3.dns.nextdns.io;h3=":443"; quicv="6b3343cf,1" |

```javascript
// Force NextDNS on HTTP3 and QUICv2 by altsvc:
user_pref("network.http.http3.alt-svc-mapping-for-testing", 'doh3.dns.nextdns.io;h3=":443"; quicv="6b3343cf,1"' );
```
{: file="user.js"}

#### Trr:

| network.dns.skipTRR-when-parental-control-enabled | false |
| network.trr.async_connInfo | true |
| network.trr.confirmation_telemetry_enabled | false |
| network.trr.custom_uri | <https://doh3.dns.nextdns.io> |
| network.trr.disable-ECS | false |
| network.trr.mode | 3 |
| network.trr.uri | <https://doh3.dns.nextdns.io> |

```javascript
// Trr
user_pref("network.dns.skipTRR-when-parental-control-enabled", false );
user_pref("network.trr.async_connInfo", true );
user_pref("network.trr.confirmation_telemetry_enabled", false );
user_pref("network.trr.custom_uri", "https://doh3.dns.nextdns.io" );
user_pref("network.trr.disable-ECS", false );
user_pref("network.trr.mode", 3 );
user_pref("network.trr.uri", "https://doh3.dns.nextdns.io" );
```
{: file="user.js"}

- Chỉnh không giới hạn dns cache queries:

| network.dnsCacheEntries | -1 |

```javascript
// Unlimited DNS queries
user_pref("network.dnsCacheEntries", -1 );
```
{: file="user.js"}

## Mở Early Hints để tăng tốc độ tải trang[^ff-enable-early-hints]

```javascript
// Enable Early hints
user_pref("network.early-hints.enabled", true);
user_pref("network.early-hints.preconnect.enabled", true);
user_pref("network.early-hints.preconnect.max_connections", 20);
```
{: file="user.js"}

Thông tin thêm <https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/103>
: `HTTP 103 Early Hints` là phản hồi của server ngay từ lúc đang xử lý yêu cầu, bao gồm các gợi ý về các tài nguyên _được cho là_ sẽ sử dụng. Điều này cho phép trình duyệt bắt đầu `tải trước tài nguyên` trước khi server xử lý xong và trả về kết quả.

## Bật `punycode` để miễn nhiễm với tên miền giả mạo

Bảo mật và riêng tư luôn đi liền với bất tiện, nhìn chung nên xác định điều này và Firefox mặc định nó đủ bảo mật và riêng tư rồi, chỉ cái:


| network.IDN_show_punycode | true |

Là ai cũng nên bật vì nó sẽ phá mấy trang web dùng unicode thành dạng `xn--abcxyz` giúp mấy trang lừa đảo giả tên miền kiểu `google.com` không còn linh nữa.

Ví dụ `フラワーナイトガール.攻略wiki.com` khi bật punycode sẽ bị buộc thành `xn--eckq7fg8cygsa1a1je.xn--wiki-4i9hs14f.com`

Hoặc ngoạn mục là `GOOGᒪE.com` được sửa thành `xn--googe-bkz.com`, `𝐠𝐨𝐨𝐠ʟ𝐞.𝐜𝐨𝐦` thành `xn--googe-hxc.com`

Đó là sự đáng sợ của tên miền giả mạo, và tụi hacker tụi nó không nhân từ như mình mà nó y hệt `google.com` luôn.

##  Tối ưu giảm RAM cho Firefox (đánh đổi bằng bảo mật) (Chi tiết về cách thức hoạt động và các cấp độ của Fission)

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

### Các cấp độ Fission

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

## Tối ưu tốc độ bật Firefox

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

## Bật chế độ bỏ qua hỏi han quấy rầy Cookie Banner[^ff-remove-cookie-banner]

### Bỏ qua tuy nhiên nếu cần thiết Chấp nhận:

| cookiebanners.service.mode | 2 |
| cookiebanners.service.mode.privateBrowsing | 2 |

### Bỏ qua hết (nếu không cho bỏ qua thì không ẩn được):

| cookiebanners.service.mode | 1 |
| cookiebanners.service.mode.privateBrowsing | 1 |

```javascript
// Bypass Cookie Banners: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPT - to remove banner);
user_pref("cookiebanners.service.mode", 2 );
user_pref("cookiebanners.service.mode.privateBrowsing, 2 );
```
{: file="user.js"}

Test trên Firefox 113, hoạt động cực tốt. Đỉnh nhất trong các sự lựa chọn ẩn cookie vì nó dùng 2 thuật toán chính, click như người thật (tốt hơn add-on là click máy) và nhúng cookie:

| cookiebanners.bannerClicking.enabled | true |
| cookiebanners.cookieInjector.enabled | true |

```javascript
// Bypass Cookie Banners - emulator CLICK, cookie INJECTOR: 
//      1 - Decline ALL (DECLINE - if FAILED, KEEP banner); 
//      2 - Hide ALL    (DECLINE - if FAILED, ACCEPTS - to remove banner);
user_pref("cookiebanners.bannerClicking.enabled", true );
user_pref("cookiebanners.cookieInjector.enabled", true );
```
{: file="user.js"}

Các trang test:
: <https://stackoverflow.com/questions/37365561/flexbox-row-inside-flexbox-column>

Chốt lại là sau này Firefox sẽ bật cái này mặc định thì dùng của Firefox sẽ tốt hơn dùng của uBlock (tốt hơn rất nhiều vì nó giúp tránh rất nhiều lỗi khó chịu mà trang web tạo ra nếu chỉ ẩn bằng CSS).

## Cách bật nhanh chế độ Compact (gọn gàng) có sẵn của Firefox[^ff-enable-compact-ui]

Thêm một bài rất đơn giản cơ mà hữu ích cho đa phần những ai thích giao diện nhỏ gọn cho Firefox, đó là bật giao diện "Compact" của Firefox mà không cần dùng userChrome.

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