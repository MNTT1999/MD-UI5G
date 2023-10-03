# MD-UI5G

![](https://img.shields.io/github/v/release/alireza0/x-ui.svg)
![](https://img.shields.io/docker/pulls/alireza7/x-ui.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/alireza0/x-ui)](https://goreportcard.com/report/github.com/alireza0/x-ui)
[![Downloads](https://img.shields.io/github/downloads/alireza0/x-ui/total.svg)](https://img.shields.io/github/downloads/alireza0/x-ui/total.svg)
[![License](https://img.shields.io/badge/license-GPL%20V3-blue.svg?longCache=true)](https://www.gnu.org/licenses/gpl-3.0.en.html)

> **Tuyên bố miễn trừ trách nhiệm: Dự án này chỉ dành cho mục đích học tập và giao tiếp cá nhân, vui lòng không sử dụng nó cho mục đích bất hợp pháp, vui lòng không sử dụng nó trong môi trường sản xuất**

bảng điều khiển xray hỗ trợ đa giao thức, **Đa ngôn ngữ (tiếng Anh, tiếng Farsi, tiếng Trung, tiếng Nga)**

| Tính năng | Cho phép? |
| ------------------------------------ | :----------------: |
| Đa ngôn ngữ | :heavy_check_mark: |
| Chủ đề tối/sáng | :heavy_check_mark: |
| Tìm kiếm sâu | :heavy_check_mark: |
| Nhiều người dùng trong nước | :heavy_check_mark: |
| Lưu lượng truy cập nhiều người dùng và thời gian hết hạn | :heavy_check_mark: |
| API REST | :heavy_check_mark: |
| Telegram BOT (quản trị viên + khách hàng) | :heavy_check_mark: |
| Sao lưu cơ sở dữ liệu bằng Telegram BOT | :heavy_check_mark: |
| Liên kết đăng ký + userInfo | :heavy_check_mark: |
| Tính ngày hết hạn trong lần sử dụng đầu tiên | :heavy_check_mark: |

**Nếu bạn cho rằng dự án này hữu ích với bạn, bạn có thể cho ý kiến** :star2:

# Cài đặt & Nâng cấp lên phiên bản mới nhất

```sh
bash <(curl -Ls https://raw.githubusercontent.com/MNTT1999/MD-UI5G/main/install.sh)
```

## Cài đặt phiên bản tùy chỉnh

Để cài đặt phiên bản mong muốn, bạn có thể thêm phiên bản đó vào cuối lệnh cài đặt. Ví dụ cho phiên bản `0.5.2`:

```sh
bash <(curl -Ls https://raw.githubusercontent.com/MNTT1999/MD-UI5G/main/install.sh) 0.5.2
```

## Cài đặt và nâng cấp thủ công

1. Trước tiên hãy tải xuống gói nén mới nhất từ ​​https://github.com/alireza0/x-ui/releases, thường chọn Architecture `amd64`
2. Sau đó tải gói nén lên thư mục `/root/` của máy chủ và rootlog `root` vào máy chủ với người dùng

> Nếu kiến ​​trúc cpu máy chủ của bạn không phải là `amd64`, hãy thay thế kiến ​​trúc khác

```sh
ARCH=$(uname -m)
[[ "${ARCH}" == "s390x" ]] && XUI_ARCH="s390x" || [[ "${ARCH}" == "aarch64" || "${ARCH}" == "arm64" ]] && XUI_ARCH="arm64" || XUI_ARCH="amd64"
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-${XUI_ARCH}.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```


## Cài đặt bằng docker

1. cài đặt docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. cài đặt x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd \
    -p 54321:54321 -p 443:443 -p 80:80 \
    -e XRAY_VMESS_AEAD_FORCED=false \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    alireza7/x-ui:latest
```

> Xây dựng hình ảnh của riêng bạn

```shell
docker build -t x-ui .
```

 Đặc trưng

- Giám sát trạng thái hệ thống
- Tìm kiếm trong tất cả các khách hàng và khách hàng
- Hỗ trợ giao diện người dùng chủ đề Tối/Sáng
- Hỗ trợ nhiều người dùng, đa giao thức, thao tác trực quan hóa trang web
- Hỗ trợ cấu hình đa miền và gửi đến nhiều chứng chỉ
- Các giao thức được hỗ trợ: vmess, vless, trojan, Shadowocks, dokodemo-door, vớ, http
- Hỗ trợ cấu hình nhiều cấu hình vận chuyển hơn
- Thống kê lưu lượng, giới hạn lưu lượng, giới hạn thời gian hết hạn
- Mẫu cấu hình xray có thể tùy chỉnh
- Hỗ trợ liên kết đăng ký (đa)
- Phát hiện sớm người dùng sắp hết hạn hoặc vượt quá giới hạn lưu lượng
- Hỗ trợ truy cập https (tên miền tự cung cấp + chứng chỉ ssl)
- Hỗ trợ ứng dụng chứng chỉ SSL bằng một cú nhấp chuột và tự động gia hạn
- Để biết thêm các mục cấu hình nâng cao, vui lòng tham khảo bảng
- Hỗ trợ xuất/nhập cơ sở dữ liệu từ bảng điều khiển

## Hỗ trợ hệ điều hành

- CentOS 8+
- Ubuntu 20+
- Debian 10+
- Fedora 36+

## API routes

- `/login` với `PUSH` dữ liệu người dùng: `{username: '', password: ''}` cho đăng nhập
- `/xui/API/inbounds` với bảng hành động sau:

| Method | Path                            | Action                                    |
| :----: | ------------------------------- | ----------------------------------------- |
| `GET`  | `"/"`                           | Get all inbounds                          |
| `GET`  | `"/get/:id"`                    | Get inbound with inbound.id               |
| `GET`  | `"/createbackup"`               | Telegram bot sends backup to admins       |
| `POST` | `"/add"`                        | Add inbound                               |
| `POST` | `"/del/:id"`                    | Delete Inbound                            |
| `POST` | `"/update/:id"`                 | Update Inbound                            |
| `POST` | `"/addClient/"`                 | Add Client to inbound                     |
| `POST` | `"/:id/delClient/:clientId"`    | Delete Client by clientId\*               |
| `POST` | `"/updateClient/:clientId"`     | Update Client by clientId\*               |
| `POST` | `"/getClientTraffics/:email"`   | Get Client's Traffic                      |
| `POST` | `"/resetAllTraffics"`           | Reset traffics of all inbounds            |
| `POST` | `"/resetAllClientTraffics/:id"` | Reset inbound clients traffics (-1: all)  |
| `POST` | `"/delDepletedClients/:id"`     | Delete inbound depleted clients (-1: all) |

\*- The field `clientId` should be filled by:

- `client.id` for VMESS and VLESS
- `client.password` for TROJAN
- `client.email` for Shadowsocks

# Environment Variables

| Variable       |                      Type                      | Default       |
| -------------- | :--------------------------------------------: | :------------ |
| XUI_LOG_LEVEL  | `"debug"` \| `"info"` \| `"warn"` \| `"error"` | `"info"`      |
| XUI_DEBUG      |                   `boolean`                    | `false`       |
| XUI_BIN_FOLDER |                    `string`                    | `"bin"`       |
| XUI_DB_FOLDER  |                    `string`                    | `"/etc/x-ui"` |

# Screenshot from Inbouds page

![inbounds](./media/inbounds.png)
![Dark inbounds](./media/inbounds-dark.png)

## SSL certificate application

<details>
  <summary>Click for details</summary>

### Certbot

```bash
snap install core; snap refresh core
snap install --classic certbot
ln -s /snap/bin/certbot /usr/bin/certbot

certbot certonly --standalone --register-unsafely-without-email --non-interactive --agree-tos -d <Your Domain Name>
```

</details>

## Tg robot use

<details>
  <summary>Click for details</summary>

X-UI supports daily traffic notification, panel login reminder and other functions through the Tg robot. To use the Tg robot, you need to apply for the specific application tutorial. You can refer to the [blog](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Set the robot-related parameters in the panel background, including:

- Tg robot Token
- Tg robot ChatId
- Tg robot cycle runtime, in crontab syntax
- Tg robot Expiration threshold
- Tg robot Traffic threshold
- Tg robot Enable send backup in cycle runtime
- Tg robot Enable CPU usage alarm threshold

Reference syntax:

- 30 \* \* \* \* \* //Notify at the 30s of each point
- 0 \*/10 \* \* \* \* //Notify at the first second of each 10 minutes
- @hourly // hourly notification
- @daily // Daily notification (00:00 in the morning)
- @every 8h // notify every 8 hours

### Tính năng của Telegram Bot

- Báo cáo định kỳ
- Thông báo đăng nhập
- Thông báo ngưỡng CPU
- Ngưỡng thời gian hết hạn và lưu lượng truy cập để báo cáo trước
- Hỗ trợ menu báo cáo khách hàng nếu tên người dùng telegram của khách hàng được thêm vào cấu hình của người dùng
- Hỗ trợ báo cáo lưu lượng điện tín được tìm kiếm bằng UUID (VMESS/VLESS) hoặc Mật khẩu (TROJAN) - ẩn danh
- Bot dựa trên menu
- Tìm kiếm khách hàng qua email (chỉ quản trị viên)
- Kiểm tra tất cả các đường vào
- Kiểm tra trạng thái máy chủ
- Kiểm tra người dùng đã cạn kiệt
- Nhận backup theo yêu cầu và theo báo cáo định kỳ
- Bot đa ngôn ngữ
</ chi tiết>

#T-Shoot:

**Nếu bạn nâng cấp từ phiên bản cũ hoặc các fork khác, để kích hoạt lưu lượng truy cập cho người dùng bạn nên làm :**

tìm cái này trong cấu hình:

```json
 "policy": {
    "system": {
```

**và thêm phần này ngay sau ` "policy": {` :**

```json
    "levels": {
      "0": {
        "statsUserUplink": true,
        "statsUserDownlink": true
      }
    },
```

**đầu ra cuối cùng giống như :*

```json
  "policy": {
    "levels": {
      "0": {
        "statsUserUplink": true,
        "statsUserDownlink": true
      }
    },

    "system": {
      "statsInboundDownlink": true,
      "statsInboundUplink": true
    }
  },
  "routing": {
```

restart panel

</details>

# lời cảm ơn đặc biệt tới

- [HexaSoftwareTech](https://github.com/HexaSoftwareTech/)
- [MHSanaei](https://github.com/MHSanaei)

# Nhìn nhận

- [Miền được lưu trữ tại Iran](https://github.com/bootmortis/iran-hosted-domains) (Giấy phép: **MIT**): _Danh sách đầy đủ các miền và dịch vụ của Iran được lưu trữ trong nước._
- [PersianBlocker](https://github.com/MasterKia/PersianBlocker) (Giấy phép: **AGPLv3**): _Danh sách mở rộng và tối ưu để chặn quảng cáo và trình theo dõi trên các trang web của Ba Tư._

## Nhà chiêm tinh theo thời gian

[![Người ngắm sao theo thời gian](https://starchart.cc/alireza0/x-ui.svg)](https://starchart.cc/alireza0/x-ui)
