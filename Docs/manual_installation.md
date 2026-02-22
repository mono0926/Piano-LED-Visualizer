# 手動インストール手順

## インストール前の準備

Raspberry Pi OS Liteをインストールする際、以下の設定を推奨します：

- **ユーザー名**: `plv`
- **パスワード**: `visualizer`
- **ローカルホスト名**: `pianoledvisualizer.local`

これらの設定は、**Raspberry Pi Imager** ツールを使用して簡単に行えます：

1. Raspberry Pi Imagerを開く
2. OSとして「Raspberry Pi OS Lite」(RPi Zero用)を選択する
3. 歯車アイコンをクリックして詳細設定を開く
4. ホスト名を `pianoledvisualizer.local` に設定
5. SSHを有効にする
6. ユーザー名を `plv`、パスワードを `visualizer` に設定
7. 必要に応じてWi-Fi設定を行う
8. 設定を保存してSDカードに書き込む

この設定を行っておくと、`ssh plv@pianoledvisualizer.local` コマンドで簡単にSSH接続できるようになります。

---

[Raspberry Pi OS Lite](https://www.raspberrypi.org/software/) をSDカードにインストールします。

モニター、マウス、キーボードを直接接続できない場合は、[Wi-Fi経由のSSH(英語)](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/wifi_setup.md) で接続してください。

### インストールスクリプトの実行

以下のコマンドを実行することで、自動インストールが可能です：

`sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/onlaj/Piano-LED-Visualizer/master/autoinstall.sh)"`

---

## ステップバイステップの手順（手動設定）

自動スクリプトを使用しない場合は、以下の手順に従ってください：

### 1. OSのアップデート

起動後、すべてを最新の状態にします。

- `sudo apt-get update`
- `sudo apt-get upgrade` （※時間がかかるので、コーヒーでも飲んでお待ちください）

### 2. SPIインターフェースの有効化

- [公式手順（英語）](https://www.raspberrypi-spy.co.uk/2014/08/enabling-the-spi-interface-on-the-raspberry-pi/)
- または、以下のコマンドを実行します：
  ```bash
  sudo raspi-config nonint do_spi 0
  ```

### 3. パッケージのインストール

（※もう一杯コーヒーが必要かもしれません）

```bash
sudo apt-get install -y ruby git python3-pip autotools-dev libtool autoconf libasound2 libavahi-client3 libavahi-common3 libc6 libgcc-s1 libstdc++6 python3 libopenblas-dev libavahi-client-dev libasound2-dev libusb-dev libdbus-1-dev libglib2.0-dev libudev-dev libical-dev libreadline-dev libopenjp2-7 libtiff6 libjack0 libjack-dev fonts-freefont-ttf gcc make build-essential scons swig abcmidi
```

### 4. オーディオ出力の無効化

LEDテープの制御と競合を避けるためにオーディオを無効にします。

```bash
sudo nano /etc/modprobe.d/snd-blacklist.conf
```

- 以下を貼り付けて保存：
  `blacklist snd_bcm2835`

別のファイルも編集します：

```bash
sudo nano /boot/config.txt
```

- `dtparam=audio=on` を `#dtparam=audio=on` に変更

完了後、再起動します：

```bash
sudo reboot
```

### 5. RTP-midi サーバーのインストール（オプション）

_Raspberry PiをPCに接続しない場合は不要です。_

[RTP MIDI User Space Driver Daemon](https://github.com/davidmoreno/rtpmidid/releases) を使用します。

1. `/home` フォルダへ移動：
   `cd /home/`
2. 依存パッケージ `libfmt9` のダウンロードとインストール：
   ```bash
   sudo wget http://ftp.de.debian.org/debian/pool/main/f/fmtlib/libfmt9_9.1.0+ds1-2_arm64.deb
   sudo dpkg -i libfmt9_9.1.0+ds1-2_arm64.deb
   sudo apt -f install
   ```
3. `rtpmidid` パッケージのダウンロードとインストール：
   ```bash
   sudo wget https://github.com/davidmoreno/rtpmidid/releases/download/v24.12/rtpmidid_24.12.2_armhf.deb
   sudo dpkg -i rtpmidid_24.12.2_armhf.deb
   sudo apt -f install
   ```

### 6. Piano-LED-Visualizer のインストール

1. `/home` フォルダへ移動：
   `cd /home/`
2. リポジトリをクローン：
   `sudo git clone https://github.com/onlaj/Piano-LED-Visualizer`
   `cd Piano-LED-Visualizer`
3. 必要なライブラリをインストール：

   ```bash
   sudo apt-get install -y python3-rpi.gpio python3-webcolors python3-psutil python3-mido python3-pillow python3-rtmidi python3-spidev python3-numpy python3-flask python3-waitress python3-websockets python3-werkzeug
   sudo pip3 install rpi-ws281x --break-system-packages
   ```

4. 起動時の自動ログインを有効化：
   `sudo raspi-config` を実行し、`System options` > `Boot / Auto Login` > `Console Autologin` を選択。

5. 自動起動サービスの設定：
   `sudo nano /lib/systemd/system/visualizer.service`
   以下を貼り付けて保存：

   ```ini
   [Unit]
   Description=Piano LED Visualizer
   After=network-online.target
   Wants=network-online.target

   [Install]
   WantedBy=multi-user.target

   [Service]
   ExecStart=sudo python3 /home/Piano-LED-Visualizer/visualizer.py
   Restart=always
   Type=simple
   User=plv
   Group=plv
   ```

   ※ WaveShare 1.3インチ 240x240 LED Hatを使用している場合は、`ExecStart` に `--display 1in3` を追加してください。
   ※ 画面を上下反転させたい場合は `--rotatescreen true` を追加してください。

6. サービスの有効化と開始：

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable visualizer.service
   sudo systemctl start visualizer.service
   ```

7. 権限の変更：
   `sudo chmod a+rwxX -R /home/Piano-LED-Visualizer/`

以上で完了です。`sudo reboot` で再起動してテストしてください。1〜3分後にビジュアライザーのメニューが表示されるはずです。
