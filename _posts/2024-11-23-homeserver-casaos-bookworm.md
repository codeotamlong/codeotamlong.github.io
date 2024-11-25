---
title: "[Home Server] Hôm nào!!!"
date: 2024-11-23 8:00:00 +0700
categories: [home, server, debian, bookworm, casaos]
tags: [home, server, debian, bookworm, casaos]
---

## CasaOS là cái gì

CasaOS là một phần mềm mã nguồn mở được xây dựng trên hệ sinh thái docker. Nó có thể đơn giản hóa quá trình triển khai và quản lý ứng dụng container.

CasaOS được phát hành bởi IceWhale Technology vào năm 2021. CasaOS nhằm mục đích xác định lại trải nghiệm kỹ thuật số đám mây riêng cho người dùng và nhà phát triển thông qua dân chủ hóa dữ liệu và cho phép mọi người đưa mục tiêu đó lên một quy mô mới.

Tính năng của CasaOS
: Quản lý tất các tệp trong FILES.
: Chia sẻ file qua mạng.
: Dễ dàng cài đặt và quản lý nhiều các docker container.
: Tự do thêm ổ đĩa và không gian mở rộng.
: Bảo vệ dữ liệu riêng tư của bạn

## Phần cứng
- Main Celeron cùi xin được
- Card Wifi mSata cũng xin được
- SSD mSata ORICO phải mua
- Case cũng phải mua
- HDD SATA vẫn là đồ đi xin
- Và 1 đường truyền internet cắm dây vì nhiều lí do linh tinh _Tí nữa sẽ giải thích_

## Phần mềm
### Cài Debian Bookworm

> Dùng Debian 12 vì đây là hàng `Official Support`, `Tested` và `Recommended`
{: .prompt-info}

Desktop Environment thì chọn `XFCE` cho nhẹ, hoặc `KDE` cho nhiều tính năng. Máy cùi Celeron thì chọn `XFCE` thôi

Nên cài = file ISO `netinstall`, chứ cài bằng file full lại phải vào `/etc/apt/sources.list` tắt cái source DVD đi. Không tắt thì `apt update` nó lại báo lỗi thiếu source, lằng nhằng lắm

### Thêm user chính vào `sudo`

```bash
su -
sudo usermod -aG sudo codeotamlong
```

`codeotamlong` là username đã tạo lúc cài Debian
{: .prompt-info}

### Cài driver Wifi

> Cái card wifi xin được kia lại dùng chip `Broadcom BCM43142 (PCI ID 14e4:4365)`, và đáng buồn là phải cài driver wifi chứ Debian không tự nhận
{: .prompt-info}

```bash
sudo nano /etc/apt/sources.list
```

Thêm `non-free` vào. Lúc sửa thì tìm đúng dòng để sửa: Thực ra thêm vào cuối file cũng được, nhưng mà sau này lúc nào `apt update` nó cũng báo trùng nhìn khó chịu lắm.

```
deb http://deb.debian.org/debian bookworm main contrib non-free-firmware non-free
```

Update dữ liệu gói và cài gói cần thiết `linux-image` tương ứng, `linux-headers` và `broadcom-sta-dkms`:

```bash
sudo apt-get update
sudo apt-get install linux-image-$(uname -r|sed 's,[^-]*-[^-]*-,,') linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms
```

> Nếu chẳng may cài lỗi
```bash
sudo apt-get install -f
sudo dpkg-reconfigure broadcom-sta-dkms
```
{: .prompt-tip}

> Kiểm tra kết quả: Có `wl.ko` trong danh sách
```bash
find /lib/modules/$(uname -r)/updates
```
{: .prompt-tip}

Tắt module xung đột
```bash
sudo modprobe -r b44 b43 b43legacy ssb brcmsmac bcma
```

Nạp module `wl`
```bash
sudo modprobe wl
```

Dùng giao diện DE để kết nối wifi!

### Cài `tailscale`

Tailscale là một dịch vụ VPN cho phép kết nối các thiết bị và ứng dụng của bạn ở khắp mọi nơi trên thế giới tạo thành một mạng LAN ảo. Các kết nối giữa hai thiết bị được mã hóa dựa trên giao thức WireGuard, bảo đảm chỉ có các thiết bị nằm trong hệ thống mạng riêng ảo có thể giao tiếp với nhau.

Tailscale kết nối các thiết bị tạo thành hệ thống mạng dạng lưới ngang hàng (peer-to-peer mesh network), được gọi là tailnet. Nhờ vậy giúp cải thiện tốc độ kết nối, giảm độ trễ và tăng sự ổn định cho hệ thống mạng.

> Quan trọng là `tailscale` có kèm theo `MagicDNS`, cho đặt tên miền (gọi là `tailname`) đối với máy trong mạng _Thế là không cần nhớ IP_
{: .prompt-tip}

Nhưng `MagicDNS` và `tailname` không hoạt động với subdomain: Tình cờ làm sao mà CasaOS truy cập tất cả các app là qua port! 

> Cosmos Cloud thì mặc định là dùng subdomain (_đương nhiên là vẫn đặt port làm phương án phụ được_) Nhưng cái này để lúc khác nói
{: .prompt-info}

#### Tự động

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

#### Thủ công

Thêm repo và chữ ký `tailscale` vào nguồn

```bash
curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```


Cài `Tailscale`:

```bash
sudo apt-get update
sudo apt-get install tailscale
```

Kết nối vào mạng Tailnet

```bash
sudo tailscale up
```

Kiểm tra IP

```bash
tailscale ip -4
```

### Cài `CasaOS`

Thao tác đơn giản, nhanh gọn

```bash
wget -qO- https://get.casaos.io | sudo bash
```

Hoặc

```bash
curl -fsSL https://get.casaos.io | sudo bash
```

Sau khi cài xong, sẽ hiển thị link để truy cập có dạng `http://<ip_lan>/`. Truy cập và tạo tài khoản mới

> CasaOS hiện chỉ cho lập 1 tài khoản: _Nên là ta chỉ dùng để làm home-server_
{: .prompt-info}

## Các ứng dụng theo yêu cầu

### Thêm nguồn cho AppStore

### MeTube

#### Xóa quảng cáo với `SponsorBlock`

Thêm Environment Variables

Key
: `YTDL_OPTIONS`

Value
: `{postprocessors:[{key:SponsorBlock,categories:[sponsor]},{key:ModifyChapters,remove_sponsor_segments:[sponsor]}]}`


```
{postprocessors:[{key:SponsorBlock,categories:[sponsor]},{key:ModifyChapters,remove_sponsor_segments:[sponsor]}]}
```

#### `docker-compose` export từ CasaOS

```yaml
name: metube-youtubedl
services:
  app:
    cpu_shares: 90
    command: []
    deploy:
      resources:
        limits:
          memory: 3811M
    environment:
      - DARK_MODE=true
      - GID=1000
      - UID=1000
      - YTDL_OPTIONS={postprocessors:[{key:SponsorBlock,categories:[sponsor]},{key:ModifyChapters,remove_sponsor_segments:[sponsor]}]}
    image: alexta69/metube:latest
    labels:
      icon: https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Images/ytdlm.png
    ports:
      - target: 8081
        published: "8081"
        protocol: tcp
    restart: unless-stopped
    volumes:
      - type: bind
        source: /mnt/Storage1/Downloads/metube
        target: /downloads
    x-casaos:
      envs: []
    devices: []
    cap_add: []
    networks:
      - default
    privileged: false
    container_name: ""
    hostname: ""
networks:
  default:
    name: metube-youtubedl_default
x-casaos:
  architectures:
    - amd64
    - arm
    - arm64
  author: WisdomSky
  category: Coolstore
  description:
    en_us: Web GUI for youtube-dl with playlist support. Allows you to download
      videos from YouTube and dozens of other sites
      (https://ytdl-org.github.io/youtube-dl/supportedsites.html).
  developer: ""
  hostname: ""
  icon: https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Images/ytdlm.png
  index: /
  is_uncontrolled: false
  main: app
  port_map: "8081"
  scheme: http
  store_app_id: metube-youtubedl
  tagline:
    en_us: Web Gui For Youtube-dl With Playlist Support. Allows You To Download
      Videos From Youtube And Dozens Of Other Sites
      (https://ytdl-org.github.io/youtube-dl/supportedsites.html).
  thumbnail: https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Images/ytdlm.png
  title:
    custom: ""
    en_us: Metube
```

### Modipy
#### Cài thẳng vào Debian chạy nền `service`

Ưu điểm
: Cập nhật mới nhất
: Nhanh, gọn, dễ cài, tài liệu đầy đủ
: Bắt kênh âm thanh dễ, dùng DE để chỉnh trực quan

Nhược điểm
: Nhanh quá _Chạy trước cả `docker` nên không load được các thue viện chạy trên CasaOS _Phải khởi động lại dịch vụ_
: Khó quản lý: Tự cưng lại có 1 thằng nằm ngoài CasaOS

Cài thôi nào

```bash
sudo mkdir -p /etc/apt/keyrings
sudo wget -q -O /etc/apt/keyrings/mopidy-archive-keyring.gpg https://apt.mopidy.com/mopidy.gpg
sudo wget -q -O /etc/apt/sources.list.d/mopidy.list https://apt.mopidy.com/bullseye.list
sudo apt update
sudo apt install mopidy
```

Chạy nền nào

```bash
sudo dpkg-reconfigure mopidy
```

Quản lý dịch vụ chạy nền

```bash
sudo service mopidy start
sudo service mopidy stop
sudo service mopidy restart
sudo service mopidy status
```

Cài phần mở rộng

```bash
sudo apt install python3-pip
sudo apt install mopidy-mpd
sudo apt install mopidy-local
sudo python3 -m pip install Mopidy-Jellyfin --break-system-packages
sudo python3 -m pip install Mopidy-Iris
sudo python3 -m pip install Mopidy-YouTube
sudo python3 -m pip install --upgrade "yt-dlp[default]"
```

Tùy chỉnh

```conf
# For information about configuration values that can be set in this file see:
#
#   https://docs.mopidy.com/en/latest/config/
#
# Run `sudo mopidyctl config` to see the current effective config, based on
# both defaults and this configuration file.
[http]
enabled = true
hostname = 0.0.0.0
port = 6680
zeroconf = Mopidy HTTP server on $hostname
allowed_origins =
csrf_protection = true
default_app = mopidy

[local]
enabled = true
media_dir = /mnt/Storage1/Music

[file]
enabled = true
media_dirs =
        /mnt/Storage1/Music

[mpd]
enabled = true
hostname = 0.0.0.0

[youtube]
enabled = true
autoplay_enabled = true
youtube_dl_package = yt_dlp

[jellyfin]
hostname = 127.0.0.1:8097
username = <username_jellyfin>
password = <password_jellyfin>
```
{: file='/etc/mopidy/mopidy.conf'}

#### Chạy `docker`

Ưu điểm
: Load được thư viện `jellyfin` mà không cần khởi động lại
: Cài nhanh, không phụ thuộc vào Debian nền

Nhược điểm
: Bản trên `dockerhub` cũ rồi: Không chạy được `Youtube` _Dù là dùng homeserver để load nhạc từ Youtube thì hơi ngu, nhưng có thì vẫn hơn_
: Tương thích phần cứng hên xui

Compose export từ CasaOS

```yaml
name: affectionate_dylan
services:
  main_app:
    cpu_shares: 10
    command:
      - ""
    container_name: mopidy
    deploy:
      resources:
        limits:
          memory: 256M
    devices:
      - /dev/snd:/dev/snd
    hostname: mopidy
    image: wernight/mopidy:latest
    labels:
      icon: https://icon.casaos.io/main/all/mopidy.png
    ports:
      - target: 6680
        published: "6681"
        protocol: tcp
      - target: 6600
        published: "6601"
        protocol: tcp
    restart: unless-stopped
    volumes:
      - type: bind
        source: /mnt/Storage1/Music
        target: /var/lib/mopidy/media
      - type: bind
        source: /DATA/AppData/Mopidy
        target: /var/lib/mopidy/local
    cap_add: []
    environment: []
    network_mode: bridge
    privileged: false
x-casaos:
  author: self
  category: self
  hostname: ""
  icon: https://icon.casaos.io/main/all/mopidy.png
  index: /
  is_uncontrolled: false
  port_map: "6681"
  scheme: http
  store_app_id: affectionate_dylan
  title:
    custom: mopidy
```
{: .file='mopidy-casaos-export.yaml'}