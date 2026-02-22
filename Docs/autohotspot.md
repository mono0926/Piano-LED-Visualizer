# オートホットスポット設定 (ドラフト)

参考: https://github.com/schollz/raspberry-pi-turnkey

### ホットスポット用のデフォルト wpa.conf:

```
country=JP
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
```

### 通常のWi-Fi接続用:

```
country=JP
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    ssid="wifi名"
    psk="パスワード"
}
```

### Wi-Fi接続に切り替えた後のスクリプト:

```bash
#!/bin/bash

sleep 3

# アクセスポイント (AP) を無効にする
sudo cp config/hostapd.disabled /etc/default/hostapd
sudo cp config/dhcpcd.conf.disabled /etc/dhcpcd.conf
sudo cp config/dnsmasq.conf.disabled /etc/dnsmasq.conf

# wlan設定を読み込む
sudo cp disable_wpa.conf /etc/wpa_supplicant/wpa_supplicant.conf

sleep 5
sudo wpa_cli -i wlan0 reconfigure
sudo wpa_cli -i p2p-dev-wlan0
sleep 5
sudo ifconfig wlan0 down
sleep 10
sudo ifconfig wlan0 up
```

### ホットスポットに切り替えた後のスクリプト:

```bash
#!/bin/bash

sleep 3

# アクセスポイント (AP) を有効にする
sudo cp config/hostapd /etc/default/hostapd
sudo cp config/dhcpcd.conf /etc/dhcpcd.conf
sudo cp config/dnsmasq.conf /etc/dnsmasq.conf

# wan設定を読み込む
sudo cp wpa.conf /etc/wpa_supplicant/wpa_supplicant.conf

sleep 5
sudo wpa_cli -i wlan0 reconfigure
sudo wpa_cli -i p2p-dev-wlan0 reconfigure
sleep 5
sudo ifconfig wlan0 down
sleep 10
sudo ifconfig wlan0 up
sleep 20
sudo systemctl restart hostapd
```
