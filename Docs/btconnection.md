# Bluetooth接続の設定

詳細な手順については、以下のページの「MIDI BLUETOOTH SETUP」セクションを参照してください。
[こちらのページ（アーカイブ）](https://web.archive.org/web/20221210063153/https://neuma.studio/rpi-midi-complete.html)

### PCとRaspberry Piの接続に問題がある場合

`/etc/bluetooth/main.conf` ファイルに以下の行を追加してみてください。変更を適用するには、Raspberry Piの再起動が必要です。

```ini
DisablePlugins = pnat
```

### Windowsタブレット/PCとの接続に依然として問題がある場合

グラフィカルなBluetoothマネージャーである「Blueman」のインストールを試してください。

```bash
sudo apt-get install blueman
```

※ Raspberry Pi OS Liteを使用している場合は、まずGUI環境をインストールする必要があります。

### SynthesiaでBluetooth（BT）サポートを有効にする

1.  Shiftキーを押しながらSynthesiaを起動し、設定ウィンドウを開きます。
2.  ドロップダウンボックスの設定項目から「Midi.UseWinRTMidi」を見つけます。
3.  「Value」ボックスにチェックを入れます。

### 各デバイスのBluetooth MIDI対応状況

- **macOS**: 完全に自動でサポートされています。
- **iOS**: 完全に自動でサポートされています。
- **Windows 10**: 上記の「Midi.UseWinRTMidi」詳細オプションを有効にして、MicrosoftのUWPドライバーを試すことができます。（※[かなり不安定](https://www.synthesiagame.com/forum/viewtopic.php?p=47530#p47530)なようです）
- **Android**: デバイスが「Android M MIDI」機能をサポートしている場合、[この手順](https://synthesiagame.com/forum/viewtopic.php?p=47541#p47541)に従って接続すれば動作するはずですが、Android特有のひどいレイテンシやパケットロスの問題が発生する可能性があります。
