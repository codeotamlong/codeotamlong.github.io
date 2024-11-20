---
title: "[Raspberry Pi] Đồng hồ để bàn Bulleyes!"
date: 2024-11-20 16:16:00 +0700
categories: [raspberry, pi, rpi]
tags: [raspberry, pi, rpi]
---

## Tại sao lại về Bulleyes?
- Không cần virtualenv để chạy Python
- Có vẻ (?) PiTFT tương thích tốt hơn
- - Không cần xoay cảm ứng
- - Độ phân giải tốt hơn

> Mỗi tội là phải build driver cho USB Wifi TPLink WR725N
{: .prompt-info }


## Phần cứng
- Raspberry Pi 2
- Màn PiTFT 2.8in cảm ứng điện trở 4 nút GPIO
- Thẻ nhớ 8GB
- Vỏ, chân, nguồn....

## Phần mềm
### Cài Raspbian

![](assets/img/rpi-magicmirror-deskclock/raspbian-bookworm-with-de.png)
_Cài bản `Legacy, 32-bit` có kèm Desktop Environment_

![](assets/img/rpi-magicmirror-deskclock/raspbian-username-pw.png)
_Đặt username và password để dùng SSH_

![](assets/img/rpi-magicmirror-deskclock/raspbian-ssh.png)
_Bật SSH_

![](assets/img/rpi-magicmirror-deskclock/openwrt-dhcp-leases.png)
_Cắm mạng, cắm nguồn, tìm IP của Raspberry Pi trong trang config router_

![](assets/img/rpi-magicmirror-deskclock/ssh-raspberry-pi.png)
_SSH vào_

### Build driver USB Wifi TPLink WR725N[^build-tplink-wr725n]

> **KHÔNG** cắm WR725N vào Pi2
{: .prompt-info }

#### Cài các gói yêu cầu

```bash
sudo apt-get update && sudo apt-get install -f
sudo apt-get dist-upgrade
sudo apt-get install -y build-essential git
sudo apt-get install -y linux-headers
sudo apt-get install -y raspberrypi-kernel-headers
sudo reboot
```

#### Build và cài driver

```bash
cd ~
git clone https://github.com/lwfinger/rtl8188eu.git`
cd rtl8188eu
make
```

```bash
sudo make install
sudo reboot
```

#### Tắt đi để cắm TPLink wr725n

```bash
sudo shutdown -h now`
```

### Cài PiTFT[^pitft-easy-install]

#### Cài `python` và `virtualenv`

```bash
cd ~
sudo apt install python3-venv
python -m venv env --system-site-packages
source env/bin/activate
```

> Từ `Debian 12 Bookworm`, mọi thứ python đều phải chạy trong `virtualenv`_
{: .prompt-info }

#### Tải script cài PiTFT

```bash
cd ~
sudo apt-get update
sudo apt-get install -y git python3-pip
pip3 install --upgrade adafruit-python-shell click
git clone https://github.com/adafruit/Raspberry-Pi-Installer-Scripts.git
cd Raspberry-Pi-Installer-Scripts
```

#### Cài PiTFT

```bash
sudo -E env PATH=$PATH python3 adafruit-pitft.py --display=28r --rotation=90 --install-type=mirror
```

> Chú ý:
> - Màn sử dụng là PiTFT 2.8in cảm ứng **điện trở**: `--display=28r`
> - Góc hiển thị 90 độ: `--rotation=90`
> - Chế độ hoạt động HDMI Mirror: `--install-type=mirror`
{: .prompt-info }

> Đối với các loại màn khác, xem thêm ở <https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install-2>
{: .prompt-info }

#### Chỉnh lại cảm ứng[^pitft-calibrate-touch]

```bash
cd /usr/share/X11/xorg.conf.d/
ls
```

![](assets/img/rpi-magicmirror-deskclock/ssh-rotate-touch.png)
_Tìm file `calibration.conf`. Trong hình sẽ là file `20-calibration.conf`_

```bash
nano 20-calibration.conf
```

Lưu lại ở chế độ xoay 270 độ

```
Section "InputClass"
        Identifier "STMPE Touchscreen Calibration"
        MatchProduct "stmpe"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"
EndSection
```
{: file='20-calibration.conf'}

Các tham số khác:

> - 90° = Option "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"
> - 180° = Option "TransformationMatrix" "-1 0 1 0 -1 1 0 0 1"
> - 270° = Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"

Khởi động lại

### Cài `MagicMirror²`

#### Cài `NodeJS 22`

```bash
sudo apt-get install -y curl
curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh
sudo -E bash nodesource_setup.sh
sudo apt-get install -y nodejs
node -v
```

#### Cài `MagicMirror²`

```bash
cd ~
git clone https://github.com/MagicMirrorOrg/MagicMirror
cd MagicMirror/
npm run install-mm
cp config/config.js.sample config/config.js
```

#### Cài `pm2`

```bash
sudo npm install -g pm2
pm2 startup
```

![](assets/img/rpi-magicmirror-deskclock/ssh-pm2-startup.png)
_Chạy dòng lệnh `pm2` đưa ra để hoàn tất cài đặt_

#### Tạo script khởi động MagicMirror

```bash
cd ~
nano mm.sh
```

```
cd ./MagicMirror
DISPLAY=:0 npm start
```
{: file='mm.sh'}

```bash
chmod +x mm.sh
```

#### Khởi động MagicMirror cùng hệ thống với `pm2`

```bash
pm2 start mm.sh
pm2 save
```

#### Điều khiển MagicMirror với `pm2`

```bash
pm2 restart mm
pm2 stop mm
pm2 logs mm
pm2 show mm
```

### Thiết lập MagicMirror²

#### Cài `mmpm`

```bash
cd ~
source env/bin/activate
python3 -m pip install --upgrade mmpm
echo 'export PATH="$PATH:$HOME/.local/bin"' >> ~/.bashrc && source ~/.bashrc
mmpm ui install -y
mmpm ui --url
```

![](assets/img/rpi-magicmirror-deskclock/ssh-mmpm-ui-url.png)
_Địa chỉ WebUI `mmpm`_

```bash
pm2 restart mm
pm2 save
```

#### Cài module khác

```bash
cd ~
source env/bin/activate
mmpm install -y MMM-Remote-Control
```

#### Thiết lập 

```javascript
/* Config Sample
 *
 * For more information on how you can configure this file
 * see https://docs.magicmirror.builders/configuration/introduction.html
 * and https://docs.magicmirror.builders/modules/configuration.html
 *
 * You can use environment variables using a `config.js.template` file instead of `config.js`
 * which will be converted to `config.js` while starting. For more information
 * see https://docs.magicmirror.builders/configuration/introduction.html#enviromnent-variables
 */
let config = {
	address: "0.0.0.0",	// Address to listen on, can be:
							// - "localhost", "127.0.0.1", "::1" to listen on loopback interface
							// - another specific IPv4/6 to listen on a specific interface
							// - "0.0.0.0", "::" to listen on any interface
							// Default, when address config is left out or empty, is "localhost"
	port: 8080,
	basePath: "/",	// The URL path where MagicMirror² is hosted. If you are using a Reverse proxy
									// you must set the sub path here. basePath must end with a /
	ipWhitelist: ["127.0.0.1", "192.168.0.0/24", "::ffff:127.0.0.1", "::1"],	// Set [] to allow all IP addresses
									// or add a specific IPv4 of 192.168.1.5 :
									// ["127.0.0.1", "::ffff:127.0.0.1", "::1", "::ffff:192.168.1.5"],
									// or IPv4 range of 192.168.3.0 --> 192.168.3.15 use CIDR format :
									// ["127.0.0.1", "::ffff:127.0.0.1", "::1", "::ffff:192.168.3.0/28"],

	useHttps: false,			// Support HTTPS or not, default "false" will use HTTP
	httpsPrivateKey: "",	// HTTPS private key path, only require when useHttps is true
	httpsCertificate: "",	// HTTPS Certificate path, only require when useHttps is true

	language: "en",
	locale: "en-US",
	logLevel: ["INFO", "LOG", "WARN", "ERROR"], // Add "DEBUG" for even more logging
	timeFormat: 24,
	units: "metric",

	modules: [
		{ module: "MMM-mmpm" },
		{
			module: "clock",
			position: "top_left",
			config: {
				dateFormat: "ddd, D MMM YYYY",
				displaySeconds: false,
			},
		},
		{
			module: "weather",
			position: "top_right",
			config: {
				weatherProvider: "openmeteo",
				type: "current",
				lon: 105.841171,
            	lat: 21.0245
			}
		},
		{
			module: "weather",
			position: "top_right",
			header: "Weather Forecast",
			config: {
				weatherProvider: "openmeteo",
				type: "forecast",
				lon: 105.841171,
            	lat: 21.0245,
				maxNumberOfDays: 3
			}
		},
		{
			module: 'MMM-Remote-Control',
			// uncomment the following line to show the URL of the remote control on the mirror
			// position: 'bottom_left',
			// you can hide this module afterwards from the remote control itself
			config: {
				customCommand: {},  // Optional, See "Using Custom Commands" below
				showModuleApiMenu: true, // Optional, Enable the Module Controls menu
				secureEndpoints: true, // Optional, See API/README.md
				// uncomment any of the lines below if you're gonna use it
				// customMenu: "custom_menu.json", // Optional, See "Custom Menu Items" below
				// apiKey: "", // Optional, See API/README.md for details
				// classes: {} // Optional, See "Custom Classes" below
			}
		},
	]
};

/*************** DO NOT EDIT THE LINE BELOW ***************/
if (typeof module !== "undefined") { module.exports = config; }
```
{: file='config.js'}


```css
body {
    zoom: 66%;
    margin: 20px;
    position: absolute;
    height: calc(100% - 40px);
    width: calc(100% - 40px);
    background: #000;
    color: #aaa;
    font-family: "Roboto Condensed", sans-serif;
    font-weight: 400;
    font-size: 2em;
    line-height: 1.5em;
    -webkit-font-smoothing: antialiased;
}
```
{: file='custom.css'}

### Kết quả

![](assets/img/rpi-magicmirror-deskclock/rpi-deskclock-result.jpg)
_Kết quả_

## Nguồn tham khảo
[^pitft-easy-install]: <https://learn.adafruit.com/adafruit-pitft-28-inch-resistive-touchscreen-display-raspberry-pi/easy-install-2>
[^pitft-calibrate-touch]: <https://www.instructables.com/Rotate-Raspberry-Pi-Display-and-Touchscreen/>
[^build-tplink-wr725n]: <https://gist.github.com/MBing/de297a8ae5e8a191c55a67a568d20d31>
