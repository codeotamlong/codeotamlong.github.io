---
title: "[MPV Awesome] Script hay ho cho MPV (P2): Youtube và hơn thế nữa!"
date: 2023-10-01 21:45:00 +0700
categories: [awesome, mpv, youtube, sponsorblock, youtube-search, youtube-upnext]
tags: [awesome, mpv, youtube, sponsorblock, youtube-search, youtube-upnext]     ## TAG names should always be lowercase
---
## Cài cURL
### Windows
- Tải `cURL` về, giải nén, mở thư mục `/bin/`

```
.
├── BUILD-HASHES.txt
...
├── bin
│   ├── curl-ca-bundle.crt
│   ├── curl.exe
│   ├── libcurl-x64.def
│   └── libcurl-x64.dll
...
```
{: file="./curl-win64-mingw/bin"}

- Copy file `curl.exe` và `curl-ca-bundle.crt` vào cùng thư mục với `mpv.exe`

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

### MacOS

MacOS đã có sẵn `cURL`, nhưng nếu muốn cập nhật thì chạy lệnh

```bash
brew install curl
```

> Cần `API key` của Youtube, có thể tạo miễn phí ở <https://console.developers.google.com/apis/api/youtube.googleapis.com/>
{: .prompt-info }

## [youtube-search.lua](https://github.com/CogentRedTester/mpv-scripts/) - Tìm kiếm video trên Youtube
### Cài đặt

- Vào <https://github.com/CogentRedTester/mpv-scripts/>
    + Tải `youtube-search.lua` vào `./portable_config/scripts`
    + Tải `script-opts/youtube-search.lua` vào `./portable_config/script-opts`
- Vào https://github.com/CogentRedTester/mpv-user-input
    + Tải `user-input.lua` vào `./portable_config/scripts`
    + Tải `user-input-module.lua` vào `./portable_config/script-modules`
- Vào https://github.com/CogentRedTester/mpv-scroll-list
    + Tải `scroll-list.lua` vào `./portable_config/scripts`

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
#       script-binding yt          			   		#! Open > Youtube > Search
#       script-binding youtube-search          		#! Open > Youtube > Result
```
{: file="./portable_config/input.conf"}

## [youtube-upnext.lua](https://github.com/cvzi/mpv-youtube-upnext) - Tự động chuyển tiếp video theo You>tube Recommendation

> Cần `API key` của Youtube, có thể tạo miễn phí ở <https://console.developers.google.com/apis/api/youtube.googleapis.com/>
> <br>Cần `cURL`, tải miễn phí cho Windows ở `https://curl.se/windows/`
{: .prompt-info }

### Cài đặt

- Vào <https://github.com/cvzi/mpv-youtube-upnext>
    + Tải `youtube-upnext.lua` vào `./portable_config/scripts`
    + Tải `youtube-upnext.conf` vào `./portable_config/script-opts`

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

## SponsorBlock - Bỏ qua quảng cáo tài trợ trong video [^fn-nth-1]

### Cài đặt

- Tải thằng này thẳng và folder `scripts` trong `portable_config`: <https://codeberg.org/jouni/mpv_sponsorblock_minimal/raw/branch/master/sponsorblock_minimal.lua>

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

Kết quả: <https://streamable.com/qhfgb3>

Vậy là xong thôi, thằng này dùng webAPI nên không bao giờ hết đát, luôn  luôn cập nhập theo thời gian thực. Tác giả viết nó cho Linux cơ mà chắc chắn hoạt động trên Windows vì Windows cũng có Cù.

## PhantomJS - phá `nsig` đánh lừa Youtube mình không phải bot [^fn-nth-2]

Cái này mình quên béng mất là hiện tại phía yt-dlp họ có cách dùng PhantomJS để phá `nsig` của Youtube, khiến Youtube nó nghĩ rằng người dùng xem từ trình duyệt web, tác dụng thì mình cũng không rõ cơ mà cứ nên thử:

- Vào: <https://phantomjs.org/download.html>
- Tải file zip rồi giải nén file `phantomjs.exe` vào folder chứa `mpv.exe` và `yt-dlp.exe`

Thế là xong, không cần làm gì thêm `yt-dlp` sẽ tự động biết cách sử dụng `phantomjs` khi nó cảm thấy cần thiết.

Ngoài ra các bạn cũng nên cập nhập `yt-dlp` sang bản Nightly vì hiện tại bản stable đã rất lâu không cập nhập, mình đang xài Nightly và nó vá rất nhiều lỗi so với stable, ông tác giả chưa ra stable là vì hiện tại Youtube đang thay đổi rất nhiều nên ông ấy ngâm dấm để tránh phía Youtube nằm vùng phá hoại. (cách đây tầm 2 tháng Youtube thay đổi liên tục gây lỗi `yt-dlp`)

Tải tại: <https://github.com/yt-dlp/yt-dlp-nightly-builds/releases>

## Nguồn:
[^fn-nth-1]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-112#post-25012334>
[^fn-nth-2]: <https://voz.vn/t/tong-hop-nhung-addon-chat-cho-firefox-pc-mobile.682181/page-156#post-25522101>