# Wi-Fi設定 (オプション)

1. OSを書き込んだSDカードの `boot` パーティションに、`wpa_supplicant.conf` という名前のファイルを作成し、以下の内容をコピーします。`ssid` と `psk` はご自身の環境に合わせて書き換えてください。

```ini
country=JP
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
    scan_ssid=1
    ssid="Wi-Fiネットワーク名"        # ここを書き換える
    psk="Wi-Fiパスワード"           # ここを書き換える
    key_mgmt=WPA-PSK
}
```

2. 同じフォルダに `ssh` という名前の空ファイルを作成します（拡張子は不要です）。これにより、初回起動時からSSH接続が可能になります。

3. SDカードをRaspberry Piに差し込んで電源を入れます。起動には数分かかる場合があります。接続されたRaspberry PiのIPアドレスを確認するには、以下の方法があります：
   - **液晶ディスプレイがある場合**: _`Other Settings`_ > _`Screensaver`_ > _`Content`_ で `Local IP` を有効にします。その後、_`Other Settings`_ > _`System Info`_ を開くとIPアドレスが表示されます。
   - **pingコマンド**: `ping pianoledvisualizer.local` を実行します。応答があればIPアドレスが表示されます。
   - **nmapコマンド**: `nmap 192.168.0.1/24 -p 80` などを実行してスキャンします（サブネットは環境に合わせて変更してください）。
   - **Fingアプリ**: スマートフォンの [Fing](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=en_IN) などのアプリを使用してネットワーク上のデバイスを探します。

4. SSHで接続するには、`ssh plv@[確認したIPアドレス]` を実行します。パスワードは `visualizer` です。
