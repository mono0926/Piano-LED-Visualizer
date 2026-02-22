# <a href="url"><img src="https://raw.githubusercontent.com/onlaj/Piano-LED-Visualizer/master/Docs/logo.svg" align="left" height="40" width="40" ></a> Piano LED Visualizer (日本語訳)

### <a style="color:inherit;margin-left:10px;" href="https://discord.gg/kQyABw8GCD"><img src="https://raw.githubusercontent.com/onlaj/Piano-LED-Visualizer/master/Docs/discord-logo.svg" align="left" height="25" width="25">Discordに参加する</a>

## [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/onlaj)

[![Everything Is AWESOME](https://i.imgur.com/AEGVXs2.png)](https://www.youtube.com/watch?v=t6PyMeW4dmw 'Piano LED Visualizer')

Piano LED Visualizerは、Raspberry PiにLEDテープを接続し、ピアノ演奏を魅力的な視覚エフェクトで彩るプロジェクトです。このリポジトリでは、LEDテープのセットアップ、電子ピアノへの接続、演奏との同期方法について詳しく解説しています。また、Synthesiaなどの外部ソフトウェアと連携して、学習体験を向上させることも可能です。

# 主な機能

- **視覚エフェクト**: サウンドビジュアライザーとして機能し、音楽に反応して光るエフェクトで演奏を彩ります。
- **学習支援**: 鍵盤の上のLEDが次に弾くべきキーを示し、ピアノの練習をサポートします。
- **MIDI統合**: Synthesiaなどの外部ソフトウェアに対応し、次に弾くべきキーをガイドします。
- **カスタマイズ**: スタイルに合わせて色や明るさを自由に変更できます。
- **録音・再生**: 演奏を録音して保存したり、ビジュアライザーから直接再生したりできます。
- **MIDIファイル対応**: MIDIファイルを読み込んで、どのキーを弾くかを確認しながら練習できます。
- **ライトシーケンス**: 演奏中に異なるライト設定を切り替えるシーケンスを作成できます。
- **Webコントロール**: シンプルなWebインターフェースからライトのセットアップや操作が可能です。
- **拡張ハット（オプション）**: ボタンとスクリーンを備えた追加ハットを使用して、スタンドアロンデバイスとして操作しやすくできます。
- **アニメーション**: 音楽に合わせたアニメーションで、演奏の雰囲気を高めます。

## [画像付きの機能詳細はこちら (英語)](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/features.md)

# 必要なもの

- **MIDIまたはUSB出力付きのピアノ**
- **MIDI-USBインターフェース**（ピアノにUSB出力がない場合） [Amazon US](https://amzn.to/2nhsYBl) | [Amazon FR](https://amzn.to/3Ul5wAi) | [Aliexpress](https://s.click.aliexpress.com/e/_DBobxwH)
  - 安価なMIDIインターフェースは意図通りに動作しない場合があるため、有名ブランドの製品を推奨します。作者は iConnectivity mio を使用しています。
- **Raspberry Pi Zero WH** [Amazon US](https://amzn.to/3D9hMdc) | [Amazon FR](https://amzn.to/3SDyxWA) | [Aliexpress](https://s.click.aliexpress.com/e/_dXc8jGl)
- **MicroSDカード**（16GBで十分です。高速読み込みのためClass 10推奨） [Amazon US](https://amzn.to/2oR93cC) | [Amazon FR](https://amzn.to/480tZxM)
- **USB OTGハブ**（ピアノとPC/タブレット接続のため、少なくとも2ポート必要） [Amazon US](https://amzn.to/3yVpdmV) | [Amazon FR](https://amzn.to/3HBY6kv) | [Aliexpress](https://s.click.aliexpress.com/e/_DBrYA2p)
- **WS2812B LEDテープ**（少なくとも1.5m、144個/mの密度を推奨） [Amazon US](https://amzn.to/2JTFpuh) | [Amazon FR](https://amzn.to/3SBT0eh) | [Aliexpress](https://s.click.aliexpress.com/e/_DEEkJyR)
- **電源**（5V 6Aあれば、172個のLEDを50%のパワーで光らせるのに十分です） [Amazon US](https://amzn.to/3O5zAJc) | [Amazon FR](https://amzn.to/42loc4x) | [Aliexpress](https://s.click.aliexpress.com/e/_Dn5Mt0n)

> [!CAUTION]
> **必ず5V（5ボルト）の電源を使用してください。それ以上の電圧を使用すると、LEDテープとRaspberry Piの両方を破損させる恐れがあります。**

- **DC 5.5x2.5mm メスジャック（クイック接続対応）** [Amazon US](https://amzn.to/3NJcTfP) | [Aliexpress](http://s.click.aliexpress.com/e/T8YSkbq)
  - Amazonで電源を購入した場合、既に含まれていることがあります。
- **配線用のワイヤー**（22–18 AWG、少なくとも1メートル。RPiをピアノから離して設置する場合はより長く） [Amazon US](https://amzn.to/3ky6k2G) | [Aliexpress](https://s.click.aliexpress.com/e/_AKKvPu)

**必須ではありませんが、見た目を整えるためにあると良いもの:**

- **カスタム3Dプリントケース**（作者が改造した [STLファイル](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/RPICaseModel.stl) があります。電源ソケットや配線用の穴が追加されています。[オリジナルモデル](https://www.thingiverse.com/thing:3393553)）
- **ナイロンスペーサー M2.5 10mm** [Amazon US](https://amzn.to/3Ku1Lma)
- **ネジ M2.5 10mm** [Amazon US](https://amzn.to/47iQv5P)
- **Waveshare LCD TFT 1.44'' 128x128px** [Amazon US](https://amzn.to/2YkW5nC)
- **ケーブル用ブレード（スリーブ）** [Amazon US](https://amzn.to/3rmCrYF)
- **熱収縮チューブ**（ワイヤーの絶縁と固定に使用） [Amazon US](https://amzn.to/3NPO3uy)
- **アルミニウムLEDプロファイル（ディフューザー付き）**: 地元のハードウェアショップで探すことを強くお勧めします。[参考1](https://i.imgur.com/MF7dd1R.png) [参考2](https://i.imgur.com/fFWOs3v.png)
  - シリカゲル製等の代替品: [Aliexpress](https://s.click.aliexpress.com/e/_A0HNfF) (12mm 2mのT0515を選択)
- **両面テープ**: ピアノに固定するために使用します。
- **Windows 10搭載のノートPC/タブレット**: Synthesiaを実行するために必要。
- **カバー検知用スイッチ**: 鍵盤カバーの開閉を検知する場合（[説明書(英語)](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/cover_detection.md)参照）。

_ネジ、スペーサー、ワイヤーなどの小物は、まとめ買いを避けるために地元のショップで探すのが賢明です。_

**総額（ピアノとタブレットを除く）は約75-100 USD程度になるはずです。**

# ソフトウェアの準備

設定済みのシステムイメージを使用する方法と、手動でインストールする方法の2つがあります。

### 1. システムイメージを使用する

- リリースページから最新のzipファイルをダウンロードします。
- ファイルを解凍します。
- [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) や [Etcher](https://www.balena.io/etcher/) などのプログラムを使用して、システムイメージをSDカード（最小4GB）に書き込みます。

Wi-Fi接続が不要な場合は、そのままSDカードをRaspberry Piに差し込めば、3〜8分後（SDカードの速度によります）に画面にメニューが表示されます。

バージョン1.5以降の場合:
RPiは「PianoLEDVisualizer」（パスワード: visualizer）という名前のWi-Fiホットスポットをセットアップします。接続後、ブラウザで `pianoledvisualizer.local` にアクセスしてWebインターフェースを開いてください。「Network」タブから通常のネットワークに接続できます。

[手動でのWi-Fi設定方法(英語)](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/wifi_setup.md) もあります。

### 2. 手動インストール

[手動インストールの手順(英語)](https://github.com/onlaj/Piano-LED-Visualizer/blob/master/Docs/manual_installation.md)

# LEDテープとRaspberry Piの接続

[こちらの配線図](https://web.archive.org/web/20230319222537/https://tutorials-raspberrypi.com/wp-content/uploads/2017/03/Raspberry-Pi-WS2812-Steckplatine.png) が参考になります。

LEDテープのワイヤーは以下のように接続します：

- **DIN (data)**: Piの18番ピンに接続
- **GND**: PiのGNDと電源のマイナス（-）に共通接続
- **+5V**: 電源のプラス（+）に接続（**Piには接続しないでください**）

> [!IMPORTANT]
> LEDテープの配線を再確認してください。多くのテープはG-D-V（GND, Data, Voltage）の順ですが、図面とは電圧とデータのラインが入れ替わっている場合があります。電圧をデータピンに直接接続すると、Raspberry Piを深刻に損傷させる可能性があります。

# Webインターフェース

Webインターフェースを使用して、LEDの色変更、ポート設定、アニメーションの実行、シーケンスの制御、MIDIファイルの管理（アップロード、ダウンロード、名前変更、削除、再生）が行えます。

接続するには、ブラウザでRaspberry PiのローカルIPアドレス（例: `http://192.168.1.10`）を入力します。同じネットワークに接続されている必要があります。

デフォルトではポート80で動作しますが、必要に応じて `config/settings.xml` で変更可能です：

```xml
<web_listen_ip>192.168.1.10</web_listen_ip>
<web_listen_port>80</web_listen_port>
```

起動時の引数 `--port` でも指定できます：
`sudo python3 /home/Piano-LED-Visualizer/visualizer.py --port 5000`

# FAQ

**Q - Raspberry Pi Zero以外のモデル（1/2/3/4など）は使えますか？**
A - 理論上は可能ですが、多くのユーザーからZero以外のモデルではキー入力に対するライトの反応に大きな遅延が発生すると報告されています。

**Q - Wi-Fi/BluetoothなしのRaspberry Pi Zeroは使えますか？**
A - 視覚効果のみが目的でSynthesiaを使わないのであれば可能です。ただし、Webインターフェイスは使えません。

**Q - 他のスクリーンやスクリーンなしでも使えますか？**
A - 現在、他にサポートされているのは Waveshare LCD TFT 1.3" のみです。スクリーンなしの場合は、Webインターフェースを代わりに使用できます。

**Q - LEDテープの基板（PCB）の色は関係ありますか？**
A - いいえ、見た目の違いだけです。

**Q - 他の種類のLEDテープは使えますか？**
A - WS281Xシリーズのみサポートされています。

**Q - LEDテープ用の電源は必須ですか？**
A - RPi本体からの給電でも10個程度のLEDなら点灯可能かもしれませんが、お勧めしません。

**Q - はんだ付けのスキルは必要ですか？**
A - Amazonなどで購入するLEDテープは1メートル単位で届くことがあり、その場合は連結のために必要です。Aliexpressなどで1本の長いテープとして購入すれば、はんだ付けなしでも構成可能です。

**Q - 録音したファイルにアクセスするには？**
A - Wi-Fi経由でSFTPまたはWebインターフェースから転送できます。Webの場合は `pianoledvisualizer.local` のメニューから「songs management」タブを選択します。SFTPの場合は Filezilla などで `/home/Piano-LED-Visualizer/Songs` にアクセスしてください。

**Q - ビジュアライザーをアップデートする方法は？**
A - メニューの `Other Settings > Update visualizer > Confirm` から行えます。完了後は再起動が必要です。

![Image](https://i.imgur.com/9MgNUl5.jpg?1)
![Image](https://i.imgur.com/WGxGdNM.jpg?2)
![Image](https://i.imgur.com/J1wA1rU.jpg)

![sidebar](https://i.imgur.com/ZVLsu0K.png)
![homepage](https://i.imgur.com/LiSszwF.png)
![changing led colors](https://i.imgur.com/iBEIM3x.png)
![ports settings](https://i.imgur.com/k6stIXg.png)
![songs_management](https://i.imgur.com/uoD2Gxz.png)
