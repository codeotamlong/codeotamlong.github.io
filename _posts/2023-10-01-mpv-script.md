---
title: "[MPV Awesome] Script hay ho cho MPV"
date: 2023-10-01 21:45:00 +0700
categories: [awesome, mpv, uosc, thumbfast, quality-menu]
tags: [awesome, mpv, uosc, thumbfast, quality-menu]     ## TAG names should always be lowercase
---
## Các thành phần phụ

### cURL

#### Windows:

Tải `cURL` ở đây: <https://curl.se/windows/>
: Giải nén, mở thư mục `/bin/`

```
.
├── BUILD-HASHES.txt
...
├── bin
│   ├── curl-ca-bundle.crt
│   ├── curl.exe
...
```
{: file="./curl-win64-mingw/bin"}

Copy file `curl.exe` và `curl-ca-bundle.crt` vào cùng thư mục với `mpv.exe`
: Cấu trúc thư mục `mpv`

```
.
│
├── mpv.exe
├── curl.exe
├── curl-ca-bundle.crt
|  
...
```
{: file="./mpv"}

#### MacOS

MacOS đã có sẵn `cURL`, nhưng nếu muốn cập nhật thì chạy lệnh

```bash
brew install curl
```

### yt-dlp

> `yt-dlp` có 2 phiên bản là `stable` một (vài?) tháng release 1 lần; và `nightly` release liên tục tự động khi có code mới
>
> Release `stable`: <https://github.com/yt-dlp/yt-dlp/releases/latest>
>
> Release `nightly`: <https://github.com/yt-dlp/yt-dlp-nightly-builds/releases/latest>
>
> _Dùng cái nào cũng được_
{: .prompt-info}

#### Windows

Vào link phiên bản muốn cài tương ứng ở trên tải file `yt-dlp.exe`.
: | yt-dlp.exe | Windows (Win7 SP1+) standalone x64 binary _(recommended for Windows)_ |
: | yt-dlp_x86.exe | Windows (Vista SP2+) standalone x86 (32-bit) binary |
: | yt-dlp_min.exe | Windows (Win7 SP1+) standalone x64 binary built with py2exe _(NOT recommended)_|

Copy file `yt-dlp.exe` vào cùng thư mục với `mpv.exe`
: Cấu trúc thư mục `mpv`

```
.
│
├── mpv.exe
├── yt-dlp.exe
|  
...
```
{: file="./mpv"}

#### MacOS

> Để cài `brew.sh`, chạy lệnh
> `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
{: .prompt-info }

Cài đặt
: `brew install yt-dlp`

```bash
brew install yt-dlp
```

Cập nhật
: `brew upgrade yt-dlp`

```bash
brew upgrade yt-dlp
```

### PhantomJS [^mpv-phantomjs]

Hiện tại phía yt-dlp họ có cách dùng PhantomJS để phá `nsig` của Youtube, khiến Youtube nó nghĩ rằng người dùng xem từ trình duyệt web, tác dụng thì không rõ cơ mà cứ nên thử:

Windows
: Vào: <https://phantomjs.org/download.html>
: Tải file `phantomjs-x.x.x-windows.zip` rồi giải nén file `phantomjs.exe` vào folder chứa `mpv.exe` và `yt-dlp.exe`

```
.
│
├── mpv.exe
├── yt-dlp.exe
|  
...
```
{: file="./mpv/."}

MacOS
: Chạy lệnh Terminal `brew install phantomjs`

### ffmpeg

> Link: 
{: .prompt-info}

Mở link <https://github.com/yt-dlp/FFmpeg-Builds/releases/latest/>
: Tải file `ffmpeg-master-latest-win64-gpl.zip`, giải nén

```
.
├── LICENSE.txt
├── bin
│   ├── ffmpeg.exe
│   ├── ffplay.exe
│   └── ffprobe.exe
└── doc
     └── ...
```
{: file="./ffmpeg-master-latest-win64-gpl/"}

Tìm trong thư mục `bin` 2 file `ffmpeg.exe` and `ffprobe.exe`
: Copy vào cùng thư mục `mpv.exe`

```
.
├── mpv.exe
├── yt-dlp.exe
├── yt-dlp.conf
├── ffmpeg.exe
├── ffprobe.exe
├── phantomjs.exe
└── portable_config
        ├── input.conf
        ├── mpv.conf
        ├── fonts
        ├── scripts
        ├── script-opts
        ├── script-modules
        └── shaders 
```
{: file='./mpv/'}

## UOSC - Feature-rich minimalist proximity-based UI for MPV player [^mpv-uosc]

> Link: <https://github.com/tomasklaen/uosc/releases>
{: .prompt-info }

Download các thành phần
: Tải file `uosc.zip`, giải nén được 2 thư mục `fonts` và `scripts`
: Tải file `uosc.conf`


Copy các thành phần vào `/mpv/portable_config/`
: Copy 2 thư mục `fonts` và `scripts` vào `/mpv/portable_config/`
: Copy `uosc.conf` vào `/mpv/portable_config/scrips-opts`

```
.
├── fonts
│   ├── uosc_icons.otf
│   └── uosc_textures.ttf
├── script-opts
│   └── uosc.conf
└── scripts
    ├── uosc.lua
    └── uosc_shared
        ├── elements
        ├── lib
        └── main.lua
```
{: file='./portable_config/'}

Mở file `/mpv/portable_config/mpv.conf` (tạo mới nếu chưa có)
: Copy toàn bộ đoạn dưới này vào rồi Save:

```
#uosc
## required so that the 2 UIs don't fight each other
osc=no
## uosc provides its own seeking/volume indicators, so you also don't need this
osd-bar=no
## uosc will draw its own window controls if you disable window border
border=no
```
{: file='./portable_config/mpv.conf'}
    
## thumbfast - High-performance on-the-fly thumbnailer for mpv [^mpv-thumbfast-1][^mpv-thumbfast-2]

> Link: <https://github.com/po5/thumbfast>
{: prompt-info }

Vào <https://github.com/po5/thumbfast>
: Download `thumbfast.lua` vào `/mpv/portable_config/scripts`
: Download `thumbfast.conf` `/mpv/portable_config/scrips-opts/`

```
.
├── script-opts
│   └── thumbfast.conf
└── scripts
    └── thumbfast.lua
```
{: file="/mpv/portable_config/"}

> _Nếu dùng giao diện gốc `mpv` (hoặc `mpv.net`):_ Download `osc.lua` và copy vào thư mục `portable_config/scripts`
> Link: <https://raw.githubusercontent.com/po5/thumbfast/vanilla-osc/player/lua/osc.lua>
> : Sau đó thêm `osc=no` vào `mpv.conf`
{: .prompt-tip }

## quality-menu - Change the streamed video and audio quality (ytdl-format) on the fly [^mpv-quality-menu]

> Link: <https://github.com/christoph-heinrich/mpv-quality-menu>
{: .prompt-info }

Vào <https://github.com/christoph-heinrich/mpv-quality-menu>
: Download `quality-menu.lua` vào `/mpv/portable_config/scripts`
: Download `quality-menu.conf` vào `/mpv/portable_config/scrips-opts/`

```
.
├── script-opts
│   └── quality-menu.conf
└── scripts
    └── quality-menu.lua
```
{: file="/mpv/portable_config/"}

> _Nếu dùng giao diện gốc `mpv` (hoặc `mpv.net`):_ Download thêm file `quality-menu-osc.lua` và copy vào thư mục `portable_config/scripts`
> : Sau đó thêm `osc=no` vào `mpv.conf`
{: .prompt-tip }


## youtube-search - Tìm kiếm video trên Youtube

> Link: <https://github.com/CogentRedTester/mpv-scripts/>
{: .prompt-info }

> Cần `API key` của Youtube, có thể tạo miễn phí ở <https://console.developers.google.com/apis/api/youtube.googleapis.com/>
{: .prompt-info }

### Cài đặt

Vào <https://github.com/CogentRedTester/mpv-scripts/>
: Download `youtube-search.lua` vào `./portable_config/scripts`
: Download `script-opts/youtube-search.lua` vào `./portable_config/script-opts`

Vào <https://github.com/CogentRedTester/mpv-user-input>
: Download `user-input.lua` vào `./portable_config/scripts`
: Download `user-input-module.lua` vào `./portable_config/script-modules`

Vào <https://github.com/CogentRedTester/mpv-scroll-list>
: Download `scroll-list.lua` vào `./portable_config/scripts`

### Sử dụng

- `Y`: Kết quả tìm kiếm, `ấn lần nữa` mở Thanh tìm kiếm.
- `Ctrl+y`: Mở Thanh tìm kiếm.
- `Esc`: Tắt giao diện.
- `Up/Down`: Chọn kết quả
- `Enter`: Mở lựa chọn
- `Shift+Enter`: Thêm vào playlist.

### Tích hợp vào `uosc`

Thêm vào `./portable_config/input.conf`
```
##       script-binding yt          			   		#! Open > Youtube > Search
##       script-binding youtube-search          		#! Open > Youtube > Result
```
{: file="./portable_config/input.conf"}

## youtube-upnext - Tự động chuyển tiếp video theo Youtube Recommendation

> Link: <https://github.com/cvzi/mpv-youtube-upnext>
{: .prompt-info }

> Cần `API key` của Youtube, có thể tạo miễn phí ở <https://console.developers.google.com/apis/api/youtube.googleapis.com/>
{: .prompt-info }

### Cài đặt

Vào <https://github.com/cvzi/mpv-youtube-upnext>
: Download `youtube-upnext.lua` vào `./portable_config/scripts`
: Download `youtube-upnext.conf` vào `./portable_config/script-opts`

### Sử dụng

- `Ctrl+u`: Mở danh sách.
- `Up/Down`: Chọn kết quả
- `Enter`: Mở lựa chọn
- `Space`: Thêm vào playlist.
- `Esc` hoặc `Ctrl+u`: Tắt giao diện (hoặc sẽ tự động tắt sau 10s).

### Tích hợp vào `uosc`

Thêm vào `./portable_config/input.conf`
```
#		script-message-to youtube_upnext menu					#! Open > Youtube > Next
```
{: file="./portable_config/input.conf"}

## SponsorBlock - Bỏ qua quảng cáo tài trợ trong video [^mpv-sponsorblock]

> Link: <https://codeberg.org/jouni/mpv_sponsorblock_minimal/>
{: .prompt-info }

### Cài đặt

Vào <https://codeberg.org/jouni/mpv_sponsorblock_minimal/>
: Download `sponsorblock_minimal.lua` vào `./portable_config/scripts`

```
.
│
...
└── scripts
|  ├── sponsorblock_minimal.lua
|  ...
...
```
{: file="./portable_config/scripts"}

### Sử dụng

`b`: Bật / Tắt

> Tự động kích hoạt: Mở file `sponsorblock_minimal.lua` chỉnh `local ON = false` thành `local ON = true`
{: .prompt-tip }

## [zones.lua](https://github.com/wiiaboo/mpv-scripts/blob/master/zones.lua) - Điều khiển dựa trên `thao tác` và `vị trí` chuột

> Link: <https://github.com/wiiaboo/mpv-scripts/>
{: .prompt-info }

### Cài đặt

Vào <https://github.com/wiiaboo/mpv-scripts/>
: Download `zones.lua` vào `./portable_config/scripts`

### Sử dụng

- `Y`: Kết quả tìm kiếm, `ấn lần nữa` mở Thanh tìm kiếm.
- `Ctrl+y`: Mở Thanh tìm kiếm.
- `Esc`: Tắt giao diện.
- `Up/Down`: Chọn kết quả
- `Enter`: Mở lựa chọn
- `Shift+Enter`: Thêm vào playlist.

### Tùy chỉnh

Ví dụ đối với thao tác lăn chuột, sửa file `./portable_config/input.conf`

``` python
WHEEL_UP    script_message_to zones commands "top-*: playlist-prev" "*-left: add brightness 1" "*-right: add volume 5" "bottom-*: seek  10"
WHEEL_DOWN 	script_message_to zones commands "top-*: playlist-next" "*-left: add brightness -1" "*-right: add volume -5" "bottom-*: seek -10"
```
{: file='./portable_config/input.conf'}

_Xem thêm_

```
--  Vertical positions can be top, middle, bottom or "*" to represent the whole column.
--  Horizontal positions can be left, middle, bottom or "*" to represent the whole row.
--  If you only use one position, it'll only represent the middle slot of that position.
--    ex: "top" == "top-middle", "right" == "middle-right", "middle" == "middle-middle"
--  "default" will be the fallback command to be used if no command is assigned to that area.
--  "" (empty), "*-*" and "*" are synonyms for "default"
--
--  ## input.conf example of use:
--  ##    wheel up/down with mouse
-- MOUSE_BTN3 script_message_to zones commands "top-right: add brightness  1" "top: add contrast  1" "*-left: add volume  5" "default: seek  10"
-- MOUSE_BTN4 script_message_to zones commands "top-right: add brightness -1" "top: add contrast -1" "*-left: add volume -5" "default: seek -10"
```

## Dynamic crop - Tự động crop các dải đen xung quanh video

> Link <https://github.com/Ashyni/mpv-scripts/>
{: .prompt-info }

### Cài đặt

Vào <https://github.com/Ashyni/mpv-scripts/>
: Tải `dynamic-crop.lua` vào `./portable_config/scripts`

### Sử dụng

- `Y`: Kết quả tìm kiếm, `ấn lần nữa` mở Thanh tìm kiếm.
- `Ctrl+y`: Mở Thanh tìm kiếm.
- `Esc`: Tắt giao diện.
- `Up/Down`: Chọn kết quả
- `Enter`: Mở lựa chọn
- `Shift+Enter`: Thêm vào playlist.

### Tùy chỉnh (chỉnh sửa `dynamic-crop.lua`)

```lua
local options = {
    -- behavior
    mode = 4, -- [0-4] more details above
    start_delay = 0, -- delay in seconds used to skip intro (usefull with mode 2)
    prevent_change_timer = 0, -- seconds
    prevent_change_mode = 2, -- [0-2], disable with 'prevent_change_timer = 0'
    resize_windowed = true,
    fast_change_timer = 0.1, -- seconds, minimum 0 = 1 frame
    new_known_ratio_timer = 5, -- seconds
    new_fallback_timer = 30, -- seconds, >= 'new_known_ratio_timer', disable with 0
    ratios = "2.4 2.39 2.35 2.2 2 1.85 16/9 5/3 1.5 4/3 1.25 9/16", -- list separated by space
    segmentation = 0.5, -- %, 0 will approved only a continuous metadata (strict)
    -- filter, see https://ffmpeg.org/ffmpeg-filters.html#cropdetect for details
    detect_limit = 26, -- is the maximum use, increase it slowly if lighter black are present
    detect_round = 2, -- even number
    detect_reset = 1, -- minimum 1
    detect_skip = 2, -- mininum 1 (ffmpeg build since 12/2020), more details above
    -- verbose
    debug = false
}
```
_Trong đó_
`mode = 4`
: có 04 chế độ, trong đó: `0` - Tắt, còn lại:

    |          | Một lần | Liên tục |
    |----------|---------|----------|
    | Thủ công |    1    |    3     |
    | Tự động  |    2    |    4     |

> Đối với các chế độ Thủ công `1` và `3` cần kích hoạt bằng phím tắt mặc định `Shift + c`. Sau khi kích hoạt, script sẽ ở trạng thái sẵn sàng, chờ đến khung hình thích hợp để tự động crop
{: .prompt-info}

`start_delay = 0`
: Delay từ thời điển bắt đầu video đến khi bắt đầu tính toán crop _Thường kết hợp với `mode = 2` để bỏ qua không crop quảng cáo_

> Cần đảm bảo tham số `hwdec=` là  `no` (mặc định) hoặc một trong các giá trị `*-copy`, nẾu không, script sẽ không thể hoạt động. Xem thêm về tham số `hwdec` [tại đây](https://mpv.io/manual/stable/#options-hwdec)
{: .prompt-info }

> Chạy lệnh `mpv --hwdec=help` để xem danh sách hardware decoding api của máy
{: .prompt-tip }

_Ví dụ:_
```bash
$ mpv --hwdec=help
Valid values (with alternative full names):
  videotoolbox (h263-videotoolbox)
  videotoolbox (h263p-videotoolbox)
  videotoolbox (h264-videotoolbox)
  videotoolbox (hevc-videotoolbox)
  videotoolbox (mpeg1video-videotoolbox)
  videotoolbox (mpeg2video-videotoolbox)
  videotoolbox (mpeg4-videotoolbox)
  videotoolbox (prores-videotoolbox)
  videotoolbox (vp9-videotoolbox)
  videotoolbox-copy (h263-videotoolbox-copy)
  videotoolbox-copy (h263p-videotoolbox-copy)
  videotoolbox-copy (h264-videotoolbox-copy)
  videotoolbox-copy (hevc-videotoolbox-copy)
  videotoolbox-copy (mpeg1video-videotoolbox-copy)
  videotoolbox-copy (mpeg2video-videotoolbox-copy)
  videotoolbox-copy (mpeg4-videotoolbox-copy)
  videotoolbox-copy (prores-videotoolbox-copy)
  videotoolbox-copy (vp9-videotoolbox-copy)
  auto (yes '')
  no
  auto-safe
  auto-copy
  auto-copy-safe
```

> Nếu script không hoạt động, kiểm tra lại phiêm bản `mpv` có build cùng libavfilter `crop` và `cropdetect`. Chạy lệnh `mpv --vf=help | grep crop`
{: .prompt-info }

_Ví dụ_:
```bash
$ mpv --vf=help | grep crop
  crop             Crop the input video.
  cropdetect       Auto-detect crop size.
```
## [SmartCopyPaste - SmartCopyPaste_II](https://github.com/Eisa01/mpv-scripts) - Paste mọi thứ trực tiếp vào mpv


> Link: <https://github.com/Eisa01/mpv-scripts>
>
> `SmartCopyPaste` - Copy mọi thứ (file ảnh, file phim, link youtube, link magnet, phụ đề...) và paste trực tiếp vào mpv, cũng như là copy từ cửa sổ `mpv` này sang cửa sổ `mpv` khác
>
> ![SmartCopyPaste Demo](https://raw.githubusercontent.com/Eisa01/mpv-scripts/master/.misc/smartcopypaste_demo1.webp) _SmartCopyPaste_
>
> `SmartCopyPaste_II` - Y hệt SmartCopyPaste nhưng có thêm clipboard log
>
>![SmartCopyPaste_II Demo](https://raw.githubusercontent.com/Eisa01/mpv-scripts/master/.misc/smartcopypaste_ii_demo1.webp) _SmartCopyPaste-II_
{: .prompt-info}

### Cài đặt

Vào <https://github.com/Eisa01/mpv-scripts>
: Tải `scripts/SmartCopyPaste.lua` (_hoặc_ `scripts/SmartCopyPaste_II.lua`) vào `./portable_config/scripts`
: Tải `script-opts/SmartCopyPaste.conf` (_hoặc_ `script-opts/SmartCopyPaste_II.conf`) vào `./portable_config/script-opts`

### Sử dụng

| Keybind                        | Name                            | Description                                             |
|--------------------------------|---------------------------------|:--------------------------------------------------------|
| `ctrl+c` / `ctrl+C` /<br> `meta+c` / `meta+C` | copy                 | Copy đường dẫn/link<br> **có** mốc thời gian           |
| `ctrl+v` / `ctrl+V` /<br> `meta+v` / `meta+V` | paste                | Paste vào `mpv` và chạy                                 |
| `ctrl+alt+c` / `ctrl+alt+C` /<br> `meta+alt+c` / `meta+alt+C` | copy-specific  | Copy đường dẫn/link<br> **không có** mốc thời gian|
| `ctrl+alt+v` / `ctrl+alt+V` /<br> `meta+alt+v` / `meta+alt+V` | paste-specific | Thêm vào playlist|
| `c` / `C`_(đối với SmartCopyPaste-II)_| open-list | Mở Clipboard list<br> [(LogManager)](https://github.com/Eisa01/mpv-scripts#logmanager) |

## Nguồn:
[^mpv-uosc]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-31#post-23246313>
[^mpv-thumbfast-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-51#post-23869287>
[^mpv-thumbfast-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-162#post-25597851>
[^mpv-quality-menu]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-354#post-28040183>
[^mpv-sponsorblock]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-112#post-25012334>
[^mpv-phantomjs]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-156#post-25522101>