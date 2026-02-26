# 主要機能

1. [LED設定](#ledsettings)
   1. [カラーモード](#color_modes)
   2. [ライトモード](#light_modes)
   3. [その他の設定](#other_settings)
2. [ソング機能](#songs)
   1. [録音](#recording)
   2. [再生](#playing)
   3. [学習（練習）](#learning)
   4. [Synthesiaでの学習](#learning_with_synthesia)
   5. [ソングの管理](#managing_songs)
3. [シーケンス](#sequences)
4. [LEDアニメーション](#led_animations)

# LED設定 <a name="ledsettings"></a>

各設定はWebインターフェース、またはRaspberry Piの画面から変更できます。

## カラーモード <a name="color_modes"></a>

- ### **Single (単色)**

  ![learnmidi_pic](https://i.imgur.com/1CmdUSC.png)

- ### **Multicolor (マルチカラー)**

  色と範囲を定義できます。範囲が定義されていないキーは、周囲の色からグラデーションが作成されます。
  ![learnmidi_pic](https://i.imgur.com/NOgFYoD.png)
  ![learnmidi_pic](https://i.imgur.com/fd0OVlf.png)

- ### **Rainbow (レインボー)**

  虹色のエフェクトを作成します。虹のスケールを編集したり、時間とともに変化（左右に移動）させたりできます。
  ![learnmidi_pic](https://i.imgur.com/JBthTuW.png)

- ### **Velocity Rainbow (ベロシティ・レインボー)**

  キーを押す速さ（強さ）に基づいて色が変わります。
  ![learnmidi_pic](https://imgur.com/b65QO45.jpg)

- ### **Speed (スピード)**

  キーを押す頻度（演奏の速さ）に応じてLEDの色が変化します。
  ![learnmidi_pic](https://i.imgur.com/QRHHuwI.png)

- ### **Gradient (グラデーション)**

  ![learnmidi_pic](https://i.imgur.com/hJeAqK6.png)

- ### **Scale (音階)**
  音階に応じて色が変わります。下の例では、黒鍵を赤色で光らせています。
  ![learnmidi_pic](https://i.imgur.com/hQxsUvP.png)

## ライトモード <a name="light_modes"></a>

3つのモードがあります。

- ### Normal (ノーマル)
- ### Fading (フェーディング)
  キーを離すと、LEDがゆっくりと消灯します。
- ### Velocity (ベロシティ)
  キーを速く（強く）弾くほど、LEDが明るく光ります。サスティンペダルが踏まれている場合は、キーを離してもゆっくりと消えていきます。ペダルがない場合は即座に消えます。

## その他の設定 <a name="other_settings"></a>

- **Brightness (明るさ)**
- **Backlight (バックライト)**: 弾いていないときもすべてのキーを薄く光らせます。
- **Sides colors (サイドカラー)**: 1つのキーに対して3つのLEDを光らせます。隣接するLEDを別の色に設定することも可能です。
- **Skipped notes (スキップノート)**: 左右の手の情報をフィルタリングします。Synthesiaで入力が重複する場合に便利です。
- **Led count (LED数)**: 88鍵未満のキーボードを使用する場合に設定します。
- **Shift (シフト)**: LEDテープの配置調整に使用します。
- **Reverse (反転)**: LEDテープが右から左に向かって取り付けられている場合に使用します。
- **LED notes offset (LEDノートオフセット)**: キーとLEDの位置がずれている場合に調整します。

# 録音と再生 <a name="songs"></a>

## 録音 <a name="recording"></a>

演奏を録音できます。マルチカラーモード選択時は、各色を別々のMIDIトラックとして記録します。録音された曲は「Songs」フォルダに保存され、Webインターフェースからダウンロード可能です。
![learnmidi_pic](https://i.imgur.com/jAcR3kT.png)

## 再生 <a name="playing"></a>

Webインターフェースまたはピアノを通じて直接再生できます。ブラウザでの再生時は、シンプルな「降ってくるノート」のビジュアライゼーションも表示されます。
![learnmidi_pic](https://i.imgur.com/izbDAYb.png)

## 学習（練習） <a name="learning"></a>

ビジュアライザーには学習ツールが組み込まれています。MIDIファイルを読み込むと、次に弾くべきキーが光ります。Webインターフェースでは楽譜も表示されます。

練習には以下の3つのモードが使用できます：

- **Melody (メロディ)**: 正しいノートを弾くまで曲が待機します。
- **Rhythm (リズム)**: 指定したテンポで進みます。ミスをせずに弾けるまでテンポを落として練習できます。
- **Listen (鑑賞)**: 指定したテンポで自動演奏されます。

間違ったキーを弾いたときに赤く光らせるオプションや、未来のノートを薄く光らせるオプションもあります。
![learnmidi_pic](https://i.imgur.com/2BDSkS8.jpg)

## Synthesiaでの学習 <a name="learning_with_synthesia"></a>

PC/Mac/Androidと接続する方法は主に3つあります（詳細は [接続図](https://github.com/mono0926/Piano-LED-Visualizer/blob/ja/Docs/external_devices.md) 参照）：

1. **Sevilla's Soft MIDI USB-USB デバイス**: 最も推奨される方法。低遅延でパケットロスがなく、安定しています。
2. **RTP MIDI**: Ethernet経由のMIDI。同じローカルネットワークに接続されている必要があります。
3. **Bluetooth**: Windows 10以外では接続が不安定な場合があるため、あまり推奨されません。

# シーケンス <a name="sequences"></a>

演奏中にLEDのプロパティを切り替える機能です。Waveshareハットのボタン、ピアノのペダル、またはWebインターフェースの「next step」から制御できます。
カスタムプリセットを名前付きで保存する手段としても利用できます。
![learnmidi_pic](https://i.imgur.com/iDedXym.png)

# LEDアニメーション <a name="led_animations"></a>

LEDテープのシンプルなアニメーションを実行できます。アイドル時に自動実行するように設定することも可能です。
![learnmidi_pic](https://i.imgur.com/gybF01Y.png)
