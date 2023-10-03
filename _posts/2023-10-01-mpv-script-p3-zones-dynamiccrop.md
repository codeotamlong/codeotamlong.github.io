---
title: "[MPV Awesome] Script hay ho cho MPV (P3): Zones, Dynamic crop, SmartCopyPaste"
date: 2023-10-01 21:45:00 +0700
categories: [awesome, mpv, youtube, zones, dynamic crop, smart copy paste]
tags: [awesome, mpv, zones, dynamic crop, smart copy paste]     ## TAG names should always be lowercase
---

## [zones.lua](https://github.com/wiiaboo/mpv-scripts/blob/master/zones.lua) - Điều khiển dựa trên `thao tác` và `vị trí` chuột
### Cài đặt

- Vào <https://github.com/wiiaboo/mpv-scripts/>
  + Tải `zones.lua` vào `./portable_config/scripts`

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
--  # input.conf example of use:
--  #    wheel up/down with mouse
-- MOUSE_BTN3 script_message_to zones commands "top-right: add brightness  1" "top: add contrast  1" "*-left: add volume  5" "default: seek  10"
-- MOUSE_BTN4 script_message_to zones commands "top-right: add brightness -1" "top: add contrast -1" "*-left: add volume -5" "default: seek -10"
```

## Dynamic crop - Tự động crop các dải đen xung quanh video
### Cài đặt

- Vào <https://github.com/Ashyni/mpv-scripts/>
    * Tải `dynamic-crop.lua` vào `./portable_config/scripts`

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

> SmartCopyPaste - Copy mọi thứ (file ảnh, file phim, link youtube, link magnet, phụ đề...) và paste trực tiếp vào mpv, cũng như là copy từ cửa sổ `mpv` này sang cửa sổ `mpv` khác
{: .prompt-info}

![SmartCopyPaste Demo](https://raw.githubusercontent.com/Eisa01/mpv-scripts/master/.misc/smartcopypaste_demo1.webp)
_SmartCopyPaste_

> SmartCopyPaste_II - Y hệt SmartCopyPaste nhưng có thêm clipboard log
{: .prompt-info}

![SmartCopyPaste_II Demo](https://raw.githubusercontent.com/Eisa01/mpv-scripts/master/.misc/smartcopypaste_ii_demo1.webp)
_SmartCopyPaste-II_

### Cài đặt

- Vào <https://github.com/Eisa01/mpv-scripts>
    + Tải `scripts/SmartCopyPaste.lua` (_hoặc_ `scripts/SmartCopyPaste_II.lua`) vào `./portable_config/scripts`
    + Tải `script-opts/SmartCopyPaste.conf` (_hoặc_ `script-opts/SmartCopyPaste_II.conf`) vào `./portable_config/script-opts`

### Sử dụng

| Keybind                        | Name                            | Description                                             |
|--------------------------------|---------------------------------|:--------------------------------------------------------|
| `ctrl+c` / `ctrl+C` /<br> `meta+c` / `meta+C` | copy                 | Copy đường dẫn/link<br> **có** mốc thời gian           |
| `ctrl+v` / `ctrl+V` /<br> `meta+v` / `meta+V` | paste                | Paste vào `mpv` và chạy                                 |
| `ctrl+alt+c` / `ctrl+alt+C` /<br> `meta+alt+c` / `meta+alt+C` | copy-specific  | Copy đường dẫn/link<br> **không có** mốc thời gian|
| `ctrl+alt+v` / `ctrl+alt+V` /<br> `meta+alt+v` / `meta+alt+V` | paste-specific | Thêm vào playlist|
| `c` / `C`_(đối với SmartCopyPaste-II)_| open-list | Mở Clipboard list<br> [(LogManager)](https://github.com/Eisa01/mpv-scripts#logmanager) |

## Nguồn:
[^fn-nth-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-112#post-25012334>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-156#post-25522101>