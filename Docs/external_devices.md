# 外部デバイスとの接続構成

## 構成 1

### バージョン A

![configuration 1A](https://i.imgur.com/1vFlqLs.png)

この構成では、電子ピアノをRaspberry Piに接続します（間にUSB OTGハブを介します）。
PC/Mac/タブレット（以下「PC」と呼びます）もUSB OTGハブに接続しますが、その間に **Sevilla's USB-USBデバイス** を介在させます。このセットアップにより、PCが接続されていない状態でもLEDを光らせることが可能です。

### バージョン B

![configuration 1B](https://i.imgur.com/f5xmQGt.png)

第2の構成では、電子ピアノをPCに直接接続します。
PCとRaspberry Piの間の接続は、Sevilla's USB-USBを使用します。この構成は、演奏の録音や学習において、ピアノとPCの間の遅延を最小限に抑えたい場合に有用です。ただし、有線接続であれば遅延の差は無視できるレベルであるため、この構成はあまり推奨されません。また、PCの電源が常に入っている必要があります。

### なぜ Sevilla's USB-USB が必要なのか？

USB経由でMIDI信号を送受信するには、少なくとも一方のデバイスが「MIDIデバイス」として認識される必要があります。Raspberry Pi自体をMIDIデバイスとして振る舞わせるオプションもありますが、その場合は1つのデバイスしか接続できません。代わりに、MIDI信号をシミュレートするデバイス（Sevilla's USB-USB）を使用することで、非MIDIデバイス同士の橋渡し（ブリッジ）が可能になります。

---

## 構成 2

### バージョン A

![configuration 2A](https://i.imgur.com/d61eT1Y.png)

Sevilla USB-USBを持っていない場合は、代わりにワイヤレス接続を使用できます。
これには **RTP MIDI** プロトコルを利用します。ピアノはケーブルでRaspberry Piに接続します。
PC側でRTP MIDIソフトウェアを設定し、PCとRaspberry Piの間に接続を確立します。

### バージョン B

![configuration 2B](https://i.imgur.com/DI3Cd7h.png)

別の構成として、ピアノをPCに接続する方法があります。
Raspberry PiとPCの間の接続は、RTP MIDIプロトコルを介して行います。構成1Bと同様に、ピアノとPCの間の遅延を最小限に抑えることが目的です。ワイヤレス接続の場合、遅延の差が顕著になる可能性があります。この構成では、PCの電源が入っていることと、Synthesiaなどの適切なソフトウェア設定が必要になりますが、学習中の遅延をなくしたい場合に有用です。

---

## 構成 3

![configuration 3](https://i.imgur.com/OxzG7cv.png)

この構成は、Androidシステムを搭載したタブレットやスマートフォンに特化したものです。
Androidの設定で「MIDI」オプションを選択すると、Androidデバイス自体がMIDIデバイスとして機能します。これにより、Sevilla's USB-USBを介さずにMIDIメッセージの送信が可能になります。
