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

## Thiết lập Debian 12 "Bookworm"

> Dùng Debian 12 vì đây là hàng `Official Support`, `Tested` và `Recommended`
{: .prompt-info}

Desktop Environment thì chọn `XFCE` cho nhẹ, hoặc `KDE` cho nhiều tính năng. Máy cùi Celeron thì chọn `XFCE` thôi

Nên cài = file ISO `netinstall`, chứ cài bằng file full lại phải vào `/etc/apt/sources.list` tắt cái source DVD đi. Không tắt thì `apt update` nó lại báo lỗi thiếu source, lằng nhằng lắm



> Cài Debian 12 đến bước chọn Desktop Environment có thể chọn luôn`XFCE`, `ssh server` và `standard system utilities` cho nhanh
{: .prompt-info }

> Chạy với quyền `su`
> ```bash
> su -
> ```
{: .prompt-warning}

### Debian 12 "Bookworm" và XFCE Minimal _(Vì tiết kiệm vài trăm MB mà ta thêm vài trăm bước thao tác)_

#### Cài Debian không có DE - Sau đấy cài `XFCE`[^minimal_bookworm_xfce]

![](assets/img/homeserver-casaos-bookworm/debian-bookworm-sw-selection.jpg)
_Vì 1 hệ thống tối giản_

> Debian chưa có gói `sudo` đâu nên vẫn phải chạy `su -` từ trước
{: .prompt-info}

```bash
nano /etc/apt/sources
```

Thêm `non-free` vào. Lúc sửa thì tìm đúng dòng để sửa: Thực ra thêm vào cuối file cũng được, nhưng mà sau này lúc nào `apt update` nó cũng báo trùng nhìn khó chịu lắm.


```
deb http://deb.debian.org/debian bookworm main contrib non-free-firmware non-free
```

Cập nhật nguồn và cài `xfce` và các gói bổ sung tính năng khác

```bash
sudo apt update
apt install sudo
apt install xfce4
apt install \
  libxfce4ui-utils \
  thunar \
  xfce4-appfinder \
  xfce4-panel \
  xfce4-session \
  xfce4-settings \
  xfce4-terminal \
  xfce4-power-manager \
  xfconf \
  xfdesktop4 \
  xfwm4\
  network-manager-gnome
```

Cài các phần mềm linh tinh khác _(Tùy sở thích)_

```bash
apt install \
  epiphany-browser \ # Simple yet powerful GNOME web browser targeted at non-technical users
  atril \ # simple multi-page document viewer: PostScript (PS), Encapsulated PostScript (EPS), DJVU, DVI, XPS and PDF
  ristretto \ #  image viewer for the Xfce desktop environment
```

```bash
reboot now
```

> Nếu sau khi khởi động lại mà Network Manager không hiển thị kết nối Ethernet/LAN dù vẫn có mạng:<br> 
> Chạy lệnh `sudo nano /etc/NetworkManager/NetworkManager.conf`<br>
> Sửa `[ifupdown] managed=false` thành `true`
> Thêm dòng này vào cuối
> ```conf
> [keyfile]
> unmanaged-devices=*,except:type:wifi,except:type:wwan,except:type:ethernet
> ```
> Khởi động lại service `sudo service network-manager restart`
> Hoặc khởi động lại `sudo reboot now`
{: .prompt-tip}

#### Cài Debian kèm XFCE - Sau đó xóa bớt[^minimal_bookworm_debloat]

```bash
cd ~
https://github.com/LostByteSoft/Debian-10
cd Debian-10
cd Debian_12
chmod +x *.sh
./remove ALL deb 12.5 excep zzz.sh
./remove zzz evince.sh
./remove zzz firefox-esr.sh
./remove zzz gimp.sh
./remove zzz libreoffice.sh
./remove zzz rhythmbox.sh
apt autoremove 
```

### Thêm user chính vào `sudo`

```bash
usermod -aG sudo <username>
```

### Cài driver Wifi

> Cái card wifi xin được kia lại dùng chip `Broadcom BCM43142 (PCI ID 14e4:4365)`, và đáng buồn là phải cài driver wifi chứ Debian không tự nhận
{: .prompt-info}

```bash
nano /etc/apt/sources.list
```

Thêm `non-free` vào. Lúc sửa thì tìm đúng dòng để sửa: Thực ra thêm vào cuối file cũng được, nhưng mà sau này lúc nào `apt update` nó cũng báo trùng nhìn khó chịu lắm.

```
deb http://deb.debian.org/debian bookworm main contrib non-free-firmware non-free
```

Thao tác
: Cập nhật danh sách gói <br>
: Cài gói cần thiết `linux-image` tương ứng, `linux-headers` và `broadcom-sta-dkms` <br>
: Vô hiệu hóa module xung đột
: Nạp module `wl`

```bash
apt-get update
apt-get install linux-image-$(uname -r|sed 's,[^-]*-[^-]*-,,') linux-headers-$(uname -r|sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms
modprobe -r b44 b43 b43legacy ssb brcmsmac bcma
modprobe wl
```

> Sửa nếu chẳng may cài lỗi
```bash
apt-get install -f
dpkg-reconfigure broadcom-sta-dkms
```
{: .prompt-tip}

> Kiểm tra kết quả: Có `wl.ko` trong danh sách
```bash
find /lib/modules/$(uname -r)/updates
```
{: .prompt-tip}

> Dùng giao diện DE để kết nối wifi!
{: .prompt-info}

### Tự động mount ổ cứng dữ liệu khi khởi động

> Nếu dùng các environment khác (ví dụ như `KDE`...) thì sẽ có giao diện đồ họa để config, nhưng XFCE rất là minimal nên phải dùng CLI thôi
{: .prompt-info}

![](assets/img/homeserver-casaos-bookworm/kde-partition-manager.png)
_KDE Partition Manager > Edit Mount Point_

#### Tìm đường dẫn phần cứng của ổ đĩa cần mount

```bash
lsblk
```

Kết quả: Phân vùng muốn mount là sda1

```bash
root@debian:~# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0 232.9G  0 disk 
└─sda1   8:1    0 232.9G  0 part 
```

#### Tìm UUID

```bash
ls -al /dev/disk/by-uuid/
```

![](assets/img/homeserver-casaos-bookworm/fstab-lsblk-uuid.png)
_Phân vùng cần mount là `/dev/sda1` và UUID của nó_

#### Mount thủ công

```bash
mkdir /media/storage1
mount /dev/sda1 /media/storage1
```

#### Mount tự động khi khởi động bằng `fstab`

```bash
nano /etc/fstab
```
Nội dung `/etc/fstab` sẽ thế này

```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sdb1 during installation
UUID=410e1383-d8a0-41f4-92c9-5070c0dd8870 /               ext4    errors=remount-ro 0       1
# swap was on /dev/sdb5 during installation
UUID=7ad24829-f7ec-472e-be88-0f007dc90b12 none            swap    sw              0       0
```
{: file='/etc/fstab/'}

Thêm vào `/etc/fstab`


```bash
# data drive
UUID=0cbe24cf-b0df-4753-b7a7-bc9f9f66b86e /media/storage1  ext4    defaults        0       0
```

Kiểm tra lỗi với `findmnt --verify`

```bash
root@debian:~# findmnt --verify
   [W] your fstab has been modified, but systemd still uses the old version;
       use 'systemctl daemon-reload' to reload

0 parse errors, 0 errors, 1 warning
root@debian:~# 
```

#### Unmount ổ đã mount thủ công (Optional)

```bash
umount /media/storage1
```

> Khởi động lại `sudo reboot now` để mount tự động
{: .prompt-info}

## Cài `CasaOS`

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

### Thêm nguồn cho AppStore

| Name | Link |
|-|-|
| Linux Server    | https://casaos-appstore.paodayag.dev/linuxserver.zip |
| Cool Store      | https://casaos-appstore.paodayag.dev/coolstore.zip |
| Home Automation | https://github.com/mr-manuel/CasaOS-HomeAutomation-AppStore/archive/refs/tags/latest.zip |
| Big Bear CasaOS | https://github.com/bigbeartechworld/big-bear-casaos/archive/refs/heads/master.zip |
| TMC Community   | https://github.com/mariosemes/CasaOS-TMCstore/archive/refs/heads/main.zip |
| Pentest Docker  | https://github.com/arch3rPro/Pentest-Docker/archive/refs/heads/master.zip |

### MeTube

#### Xóa quảng cáo với `SponsorBlock`

Thêm Environment Variables

Key
: `YTDL_OPTIONS`

Value
: `{"postprocessors":[{"key":"SponsorBlock","categories":["sponsor"]},{"key":"ModifyChapters","remove_sponsor_segments":["sponsor"]}]}`


```
{"postprocessors":[{"key":"SponsorBlock","categories":["sponsor"]},{"key":"ModifyChapters","remove_sponsor_segments":["sponsor"]}]}
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

Test audio, tự dưng thấy loa rú ầm lên là được

```bash
sudo docker run --rm \
  --user root --device /dev/snd \
  wernight/mopidy \
  gst-launch-1.0 audiotestsrc ! audioresample ! autoaudiosink
```

`Install a customized app`

```yaml
docker run -d \
  --user root --device /dev/snd \
  -v "/media/storage1/:/var/lib/mopidy/media:ro" \
  -v "/DATA/AppData/mopidy/local:/var/lib/mopidy/local" \
  -v "/DATA/AppData/mopidy/mopidy.conf:/config/mopidy.conf" \
  -p 6600:6600 -p 6680:6680 \
  wernight/mopidy
```

Title
: `wernight/mopidy`

Icon URL
: `https://raw.githubusercontent.com/mopidy/mopidy/refs/heads/main/docs/_static/mopidy.png`

**Web UI**

| http:// | | :6680 | /iris

**Port**

| Host | Container | Protocol |
|:-:|:-:|:-:|
| 6600 | 6600 | TCP |
| 6680 | 6680 | TCP |

**Volumes**

| Host | Container |
|:-|:-|
| /media/storage1/ | /var/lib/mopidy/media |
| /DATA/AppData/mopidy/local | /var/lib/mopidy/local |
| /DATA/AppData/mopidy/mopidy.conf | /config/mopidy.conf |

**Devices**

| Host | Container |
|:-|:-|
| /dev/snd | /dev/snd |


```config
[core]
data_dir = /var/lib/mopidy

[local]
media_dir = /var/lib/mopidy/media/Music

[file]
enabled = true
media_dirs =
    /var/lib/mopidy/media/Music|Music
    /var/lib/mopidy/media/Downloads/metube|Metube
    
[audio]
output = tee name=t ! queue ! autoaudiosink t. ! queue ! udpsink host=0.0.0.0 port=5555

[m3u]
playlists_dir = /var/lib/mopidy/playlists

[http]
hostname = 0.0.0.0

[mpd]
hostname = 0.0.0.0

[spotify]
username=USERNAME
password=PASSWORD

[gmusic]
username=USERNAME
password=PASSWORD

[soundcloud]
auth_token=TOKEN
```
{: file='/DATA/AppData/mopidy/mopidy.conf'}

**Cập nhật dữ liệu cho module Mopidy-Local**: Chạy trong Settings của App > **[>_]** Terminal and Logs

```bash
mopidy local scan
```

## Mở cửa ra cho internet đi vào

### TailScale

Tailscale là một dịch vụ VPN cho phép kết nối các thiết bị và ứng dụng của bạn ở khắp mọi nơi trên thế giới tạo thành một mạng LAN ảo. Các kết nối giữa hai thiết bị được mã hóa dựa trên giao thức WireGuard, bảo đảm chỉ có các thiết bị nằm trong hệ thống mạng riêng ảo có thể giao tiếp với nhau.

Tailscale kết nối các thiết bị tạo thành hệ thống mạng dạng lưới ngang hàng (peer-to-peer mesh network), được gọi là tailnet. Nhờ vậy giúp cải thiện tốc độ kết nối, giảm độ trễ và tăng sự ổn định cho hệ thống mạng.

> Quan trọng là `tailscale` có kèm theo `MagicDNS`, cho đặt tên miền (gọi là `tailname`) đối với máy trong mạng _Thế là không cần nhớ IP_
{: .prompt-tip}

Nhưng `MagicDNS` và `tailname` không hoạt động với subdomain: Tình cờ làm sao mà CasaOS truy cập tất cả các app là qua port! 

> Cosmos Cloud thì mặc định là dùng subdomain (_đương nhiên là vẫn đặt port làm phương án phụ được_) Nhưng cái này để lúc khác nói
{: .prompt-info}

Nguồn: <https://hub.docker.com/r/tailscale/tailscale>

Import `docker run` chạy agent vào CasaOS > :heavy_plus_sign: > Customized App

```bash
docker run -d --name=tailscaled -v /var/lib:/var/lib -v /dev/net/tun:/dev/net/tun --network=host --cap-add=NET_ADMIN --cap-add=NET_RAW tailscale/tailscale
```

Thêm biến môi trường

Key
: TS_AUTHKEY

Value _tự tạo mới trên website <https://login.tailscale.com/admin/settings/keys>_
: tskey-auth-ab1CDE2CNTRL-0123456789abcdef

> Lưu ý `--name=tailscaled` sẽ là tên thiết bị trên Dashboard của TailScale _Nếu thích thì có thể đổi tên khác_
{: .prompt-tip}

### Nginx Proxy Manager

Ưu điểm
: Docker: có tính đóng gói cao, xóa đi là sạch, không liên quan đến hệ thống
: Public Domain và DNS: Không cần chạy VPN như TailScale với ZeroTier

Nhược điểm
: Public: Mở cửa ra cho tất cả mọi người, dễ toang
: Cần 1 tên miền (phải mua hoặc xin)
: Không truy cập được App từ WebUI của CasaOS theo port, phải gán từng tên miền cho từng App

#### Thiết lập DNS

Mua/Xin 1 tên miền và thiết lập thêm bản ghi DNS (`DNS Record`) mới:

Type
: `A` _(khuyến nghị)_: bản ghi ánh xạ từ tên miền sang địa chỉ IPv4
: `AAAA`: bản ghi ánh xạ từ tên miền sang địa chỉ IPv6 _(Nếu có dùng thì cũng nên đi kèm 1 bản ghi `A` vì IPv6 vẫn là câu chuyện tương lai - 10 năm nay nó vẫn là chuyện tương lai)
: `CNAME`: bản ghi chuyển hướng tên miền, ví dụ: `www.example.com` về `example.com`

Name
: `@` hoặc/và `www` đối với tên miền gốc (còn gọi là `apex domain`, `root domain`,... ví dụ `example.com`)
: `<subdomain>` nếu sử dụng các tên miền con (ví dụ `subdomain.example.com`)

Value
: Địa chỉ IP công khai của home-server, diễn Nôm thì là cái IP mà nhà mạng cấp cho cục modem của mình _Vào trang gateway <192.168.1.1> của modem xem là chắc nhất_ vì các trang web kiểu `whatismyip` có thể dính VPN
: Nếu dùng bản ghi `Type CNAME` thì đặt là tên miền đích muốn chuyển đến

TTL
: Bao nhiêu cũng được, tùy thương gia bán tên miền thôi

![](assets/img/homeserver-casaos-bookworm/godaddy-dns.png)
_Ví dụ về bản ghi DNS của GoDaddy: `@` cho tên miền gốc, `subdomain` và `sub-của-sub-domain`. TTL được tùy chọn từ 1/2 tiếng đến 1 tuần thì mình chọn 1 tiếng cho đẹp!_

#### Port Fowarding 

> Thưở Internet sơ khai, trên các diễn đàn cổ xưa về Torrent thường được diễn Nôm là `mở port`. Nhưng giờ mình gọi là `chuyển tiếp cổng` cho nó sang mồm
{: .prompt-info}

![](assets/img/homeserver-casaos-bookworm/port-forwading-lazyadmin.png)
_Mô hình mạng đơn giản mượn từ LazyAdmin_

Đại khái là khi đi từ Internet vào home-server của mình sẽ có 1 con đường là `tên miền > modem > server`
: Thông qua DNS đã thiết lập thì từ `tên miền` đã đi được đến `modem` thông qua địa chỉ IP công khai do nhà mạng cấp
: Nhưng từ `modem` đến `server` thì cần có 1 thằng dẫn đường, và ở đây mình dùng thằng `port`
: Lúc này `modem` sẽ chuyển yêu cầu kết nói qua `port` xác định đến địa chỉ một địa chỉ IP xác định

Và ở đây mình cần làm 2 việc

1. Đặt địa chỉ IP tĩnh cho server CasaOS
2. Port forwarding thằng 2 cổng `80` và `443` tới địa chỉ IP của CasaOS

##### 1. Đặt địa chỉ IP tĩnh cho server CasaOS

**_Cách 1: Đặt địa chỉ trên system_**

Tùy Desktop Environment sẽ có giao diện khác nhau, nhưng nhìn chung là có dạng kiểu này

![](assets/img/homeserver-casaos-bookworm/desktop-environment-static-ip.png)
_Giao diện Ubuntu_

Tuy nhiên là **không nên** dùng cách này, vì đây là kiểu xin `Ê router, cho tao địa chỉ IP này đi`. Chẳng may không xin được là khỏi vào mạng!

**_Cách 2: Config DHCP của router_** _(Khuyến nghị)_

Đại khái là đặt gạch trước địa chỉ IP dành riêng cho card mạng của server (phân biệt bằng địa chỉ MAC): Đảm bảo là lúc nào cũng server cũng sẽ đúng địa chỉ nội bộ. Cũng tùy router và firmware mà có giao diện config khác nhau, lọ mọ quanh mấy từ khóa `DHCP Reservation`, `Reserve IP`,...

![](assets/img/homeserver-casaos-bookworm/openwrt-dhcp-reservation.png)
_Giao diện OpenWRT_

##### 2. Port Forwading 2 cổng `80` và `443` tới CasaOS

Mỗi Router, firmware lại có thao tác khác nhau. Nhưng nhìn chung sẽ quanh quẩn mấy từ khóa `NAT`, `Virtual Server`, `Port Forwarding`, `Applications and Gaming`...

![](assets/img/homeserver-casaos-bookworm/vnpt-igate-port-forwarding.png)
_Giao diện modem iGate của VNPT_

#### Đổi port của WebUI CasaOS (Vì thằng Nginx Proxy Manager cần port 80)

![](assets/img/homeserver-casaos-bookworm/casaos-dashboard-change-port.png)

#### Dựng Nginx Proxy Manager lên chạy thôi

Import `docker compose` chạy agent vào CasaOS > :heavy_plus_sign: > Customized App

```yaml
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - /DATA/AppData/nginx-proxy-manager/data:/data
      - /DATA/AppData/nginx-proxy-manager/letsencrypt:/etc/letsencrypt
```

Kiểm tra lại đường dẫn Web UI
: | http:// | | :81 | / |

Mở WebUI của Nginx Proxy Manager, đăng nhập theo tài khoản mặc định, xong rồi kiểu gì cũng phải đổi

Username
: admin@example.com

Password
: changeme

**Host > Proxy Host > Add Proxy Host**

**_Tab `Details`_**

Domain Names
: ví dụ `example.com`

Scheme | Forward Hostname/IP   | Port |
|-|-|-|
`http`   | IP LAN của CasaOS | Port WebUI của App

[] Cache Assets
[] Block Common Exploits
[] Websockets Support

**_Tab `SSL`_**: Chọn `Request Lets Encrypt SSL` và Nhập Email

## Nguồn/Tham khảo:
[^minimal_bookworm_xfce]: <https://github.com/coonrad/Debian-Xfce4-Minimal-Install>
[^minimal_bookworm_debloat]: <https://github.com/LostByteSoft/Debian-10>