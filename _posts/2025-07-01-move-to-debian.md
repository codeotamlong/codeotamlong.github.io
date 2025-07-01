---
title: "Chuyển nhà sang Debian"
date: 2025-07-01 16:00:00 +0700
categories: [work, daily, debian, bookworm]
tags: [work, daily, debian, bookworm]
---

## Debian là gì

Debian là một distro linux

## Phần cứng

```
λ › fastfetch                                                                                                    ~
        _,met$$$$$gg.          ducminh3112@debiplex
     ,g$$$$$$$$$$$$$$$P.       --------------------
   ,g$$P""       """Y$$.".     OS: Debian GNU/Linux 12 (bookworm) x86_64
  ,$$P'              `$$$.     Host: OptiPlex 5080
',$$P       ,ggs.     `$$b:    Kernel: Linux 6.1.0-37-amd64
`d$$'     ,$P"'   .    $$$     Uptime: 15 mins
 $$P      d$'     ,    $$P     Packages: 2728 (dpkg), 12 (flatpak)
 $$:      $$.   -    ,d$$'     Shell: zsh 5.9
 $$;      Y$b._   _,d$P'       Display (DELL E2214H): 1080x1920 @ 60 Hz in 22" [External]
 Y$$.    `.`"Y$$$$P"'          Display (DELL U2720Q): 3840x2160 @ 60 Hz (as 2194x1234) in 27" [External] *
 `$$b      "-.__               DE: KDE Plasma 5.27.5
  `Y$$b                        WM: KWin (Wayland)
   `Y$$.                       WM Theme: Breeze
     `$$b.                     Theme: Breeze (Light) [Qt], Breeze [GTK2/3]
       `Y$$b.                  Icons: breeze [Qt], breeze [GTK2/3/4]
         `"Y$b._               Font: Noto Sans (10pt) [Qt], Noto Sans (10pt) [GTK2/3/4]
             `""""             Cursor: breeze (24px)
                               Terminal: konsole 22.12.3
                               CPU: Intel(R) Core(TM) i7-10700 (16) @ 4.80 GHz
                               GPU: Intel UHD Graphics 630 @ 1.20 GHz [Integrated]
                               Memory: 6.28 GiB / 15.33 GiB (41%)
                               Swap: 0 B / 977.00 MiB (0%)
                               Disk (/): 18.91 GiB / 232.24 GiB (8%) - ext4
                               Disk (/media/ducminh3112/Internal): 19.35 GiB / 223.58 GiB (9%) - fuseblk
                               Local IP (eno1): 10.0.5.9/24
                               Locale: en_US.UTF-8
```

## Cài Debian 12 "Bookworm"

Desktop Environment thì chọn `XFCE` cho nhẹ, hoặc `KDE` cho nhiều tính năng. Máy cùi Celeron thì chọn `XFCE` thôi

Nên cài = file ISO `netinstall`, chứ cài bằng file full lại phải vào `/etc/apt/sources.list` tắt cái source DVD đi. Không tắt thì `apt update` nó lại báo lỗi thiếu source, lằng nhằng lắm

> Cài Debian 12 đến bước chọn Desktop Environment có thể chọn luôn`XFCE`, `ssh server` và `standard system utilities` cho nhanh
{: .prompt-info }

> Chạy với quyền `su`
> ```bash
> su -
> ```
{: .prompt-warning}

## Mấy thứ khác

### Thêm user vào sudo

```bash
su -
usermod -aG sudo <username>
```

### Flatpak + Flathub

```
# Install Flatpak
sudo apt install flatpak

# Install the Software Flatpak plugin
sudo apt install plasma-discover-backend-flatpak

# Add the Flathub repository
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

# Restart
```

### Trình duyệt Zen Browser

``` bash
# Manual Install
flatpak install flathub app.zen_browser.zen

# Run
flatpak run app.zen_browser.zen
```

### Docker

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install the latest Docker packages.
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Verify
sudo docker run hello-world
```

### WakeMeOps + lazydocker

```bash
# Add WakeMeOps repository
curl -sSL https://raw.githubusercontent.com/upciti/wakemeops/main/assets/install_repository | sudo bash

# Install lazydocker
sudo apt install lazydocker
```

### zsh + zimfw

```bash
# Install
sudo apt install zsh

# Make zsh default
chsh -s /bin/zsh

# Installing Zim
curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh

# zsh theme
sudo nano ~/.zimrc
# Add 'zmodule <theme>' to ~/.zimrc
zimfw install
```

### LocalSend

```bash
# Install
flatpak install flathub org.localsend.localsend_app

# Run
flatpak run org.localsend.localsend_app
```

### Tự động mount ổ cứng Data

![](assets/img/homeserver-casaos-bookworm/kde-partition-manager.png)
_KDE Partition Manager > Edit Mount Point_

## Nguồn/Tham khảo: