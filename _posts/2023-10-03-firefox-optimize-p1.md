---
title: "[Firefox Awesome] Tối ưu Firefox (P1): Tăng hiệu năng Firefox "
date: 2023-10-03 20:00:00 +0700
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

## Tổng hợp tất cả tối ưu tốt nhất của thread trong một file `user.js`, cách sử dụng:[^fn-nth-1]
> Chú ý: Phần ép cache chạy trên RAM mình không bật mặc định, các bạn muốn bật thì bỏ `//` ở phần dưới của `// Force RAM cache, uncomment // to enable` để bật nhé.
{: .prompt-info }
Và thế là xong, chỉ một file `user.js` chứa tất cả tinh hoa bao đời nay của người dùng Firefox và của thread, thao tác chưa tới vài giây là xong.
        
```javascript    
//Instant start-up
user_pref("browser.startup.preXulSkeletonUI", false);

// Reduce disk read/write
user_pref("browser.sessionstore.idleDelay", 3600000);
user_pref("browser.sessionstore.interval", 3600000);
user_pref("browser.sessionstore.collect_zoom", false);
user_pref("browser.sessionstore.privacy_level", 2);
user_pref("browser.sessionstore.restore_pinned_tabs_on_demand", true);
user_pref("browser.sessionhistory.max_total_viewers", 0);

// Disable Pocket and Accessibility
user_pref("extensions.pocket.enabled", false);
user_pref("accessibility.force_disabled", 1);

// Optimize rendering speed
// https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-23570551
// https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27064564
user_pref("nglayout.initialpaint.delay", 2000);
user_pref("nglayout.initialpaint.delay_in_oopif", 2000);
user_pref("content.notify.backoffcount", 0);
user_pref("content.notify.interval", 2000000);
user_pref("content.notify.ontimer", true);

// Enable punycode
// https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-25938099
user_pref("network.IDN_show_punycode", true);

// GoogleDNS + ECS
// https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-24688026
user_pref("network.trr.uri", "https://dns.google/dns-query");
user_pref("network.trr.custom_uri", "https://dns.google/dns-query");
user_pref("network.trr.mode", 2);
user_pref("network.trr.disable-ECS", false);

// Reduce network request
// https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/post-27409530
user_pref("network.http.rcwn.enabled", false);

// Force RAM cache, uncomment // to enable
// https://voz.vn/t/cach-ep-firefox-luu-cache-tren-ram-ma-khong-can-ramdisk.664955/
//user_pref("browser.cache.disk.enable", false);
//user_pref("browser.cache.memory.enable", true);
//user_pref("browser.cache.memory.capacity", 524288);
//user_pref("browser.cache.memory.max_entry_size", 512000);

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

## Đặt ngoại lệ antivirus để Firefox không bị hãm tốc độ[^fn-nth-3]

Không hề bình thường, vì antivirus thường có thói quen scan linh tinh, virus thì chả thấy đâu nhưng tài nguyên hệ thống thì tốn thấy rõ nên mình bỏ dùng antivirus 10 năm nay rồi, chưa từng nhiễm virus một lần kể từ đó lại còn không bao giờ gặp phải lỗi không tương thích do antivirus tụi nó tì đè vào ứng dụng đang hoạt động nữa. (một vài ví dụ rõ nhất là vụ antivirus chặn giao thức QUIC, khiến nhiều người không dùng được DNS over QUIC)

Giải pháp:

- Cho Firefox (cả folder chứa firefox.exe và folder profile) vào ngoại lệ của WD để nó không bao giờ động chạm vào Firefox nữa
- Tắt tính năng thời gian thực của WD
- Tắt hoàn toàn WD


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

## nglayout.initialpaint.delay khiến Firefox render trang ít đi giảm tổng tiêu thụ CPU[^fn-nth-3]

Ngày xưa hồi mà các bài báo Việt Nam đăng ồ ạt về tối ưu Firefox ấy, thì cái `nglayout.initialpaint.delay` là một trong những tối ưu sai rất sai khi họ khuyên người dùng hạ xuống thấp hơn 250, thực ra để giá trị này cải thiện hiệu năng thì nên tăng lên vì Firefox giờ rất thông minh rồi, tăng lên 1000000000000 thì khi trang tải xong Firefox cũng render một chạm cả trang luôn, cơ mà mình toàn để 2000 (nghĩa là nhắc Firefox cứ làm sao thì làm, sau 2s phải hiển thị trang web dựa trên những gì đã tải được) vì nhỡ sao trang web nó bị chậm có vài file css, js tải mãi không xong thì đợi dài cổ :D

Tăng giá trị `nglayout.initialpaint.delay` sẽ cực kỳ hiệu quả khi dùng add-on như Dark Reader, [chi tiết](../firefox-addon-p7/#nguy%C3%AAn-nh%C3%A2n).

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

: [Một cái nhìn khái quát hơn về cách Firefox render trang web cũng như tối ưu xa hơn giữa `nglayout.initialpaint.delay` và `content.notify.interval`.](../firefox-addon-p7/#m%E1%BB%99t-c%C3%A1i-nh%C3%ACn-kh%C3%A1i-qu%C3%A1t-h%C6%A1n-v%E1%BB%81-c%C3%A1ch-firefox-render-trang-web-c%C5%A9ng-nh%C6%B0-t%E1%BB%91i-%C6%B0u-xa-h%C6%A1n-gi%E1%BB%AFa-nglayoutinitialpaintdelay-v%C3%A0-contentnotifyinterval)
: [Nguyên nhân](../firefox-addon-p7/#nguy%C3%AAn-nh%C3%A2n)

## Ép Firefox lưu cache trên RAM mà không cần RAMDisk [^fn-nth-4]

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

### Tắt RCWN để Firefox chung thủy với RAM cache [^fn-nth-2]

Kể từ phiên bản 59, Firefox có một tính năng gọi là Race Cache With Network (_RCWN_). Nếu phát hiện ổ đĩa chậm(như _HDD đời Tống_ - Firefox 59 release năm 2018), Firefox có thể quyết định bắt đầu yêu cầu mạng ngay lập tức mà không cần chờ bộ đệm. 

Đó là một sự đánh đổi: 
: Nếu các yêu cầu mạng nhan hơn, độ trễ sẽ được cải thiện; 
: Nếu cache nhanh hơn thì băng thông mạng đã bị lãng phí.

Để vô hiệu hóa: Vào `about:config` chỉnh:

| network.http.rcwn.enabled | false |

```javascript
// Force RAM cache - Disable RCWN
user_pref("network.http.rcwn.enabled", false);
```
{: file="user.js"}

Vậy là từ nay Firefox sẽ chỉ chung thủy sắt son với RAM thôi chứ không có ý định ngoại tình với mạng.

## Nguồn:
[^fn-nth-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-280#post-27527209>
[^fn-nth-3]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-38#post-23570551>
[^fn-nth-4]: <https://voz.vn/t/cach-ep-firefox-luu-cache-tren-ram-ma-khong-can-ramdisk.664955/>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-262#post-27409530>