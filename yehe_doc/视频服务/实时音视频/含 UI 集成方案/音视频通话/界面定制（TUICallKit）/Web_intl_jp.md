ここではTUICallKitのユーザーインターフェースをカスタマイズする方法についてご説明します。インターフェース微調整と自身でのUI実装という2つのソリューションをご用意しています。

## 方法1：インターフェース微調整ソリューション

ご提供するUIソースコードを直接変更することで、TUICallKitのユーザーインターフェースを調整します。TUICallKitのインターフェースソースコードは[Github](https://github.com/tencentyun/TUICallKit)の`Web/`フォルダにあります。

### アイコンの置き換え

`src/icons`フォルダ内のアイコンコンポーネントを直接変更し、app全体のアイコンの色やスタイルに統一性を持たせることができます。置き換える際にアイコンファイルの名前を変更しないようにしてください。アイコンのプレビューは`src/assets`で参照できます。
![img](https://qcloudimg.tencent-cloud.cn/image/document/63512402ae3cee72786afcc919a988ce.png)

### UIレイアウトの調整

src/components/ファイルのそれぞれのページを変更することで、オーディオビデオ通話インターフェースを変更できます

```bash
- components/
    - Calling-C2CVideo.vue          2人ビデオ通話
    - Calling-Group.Vue             多人数オーディオ・ビデオ通話
    - ControlPanel.vue              コントロールパネル
    - ControlPanelItem.vue          コントロールパネルサブ項目
    - Dialing.vue                   電話発信ページ、着信ページ、2人オーディオ通話
    - MicrophoneIcon.vue            音量の変化を表示できるマイクIcon
    - TUICallKit.vue                TUICallKit全体コンポーネント
```

### スタイルの変更

スタイルファイルは`src/style.css`にあります。UIのスタイルに合わせてご自身で調整できます。

## 方法2：自身でのUI実装ソリューション

TUICallKitの通話機能全体はTUICallEngineというUIレスSDKをベースにして実装されており、TUICallEngineを完全にベースにしてご自身のUIを実装することが可能です。詳細については、[APIインターフェースアドレス](https://www.tencentcloud.com/document/product/647/51016)をご参照ください。