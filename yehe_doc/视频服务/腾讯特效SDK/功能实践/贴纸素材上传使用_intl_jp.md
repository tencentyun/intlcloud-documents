このドキュメントではDemoを例に、購入または自作した素材をプロジェクトに組み入れ、使用する方法についてご紹介します。

## iOS
iOS端末のDemoの、リソースパック初期化に関連するコードは`BeautyViewModel.m`にあり、ステッカー素材リストの初期化メソッドは**setupData**です。

1. ステッカー素材名（ディレクトリ名）を**_motion2DMenuIDS** リストに入れます。
2. 素材パッケージをDemoプロジェクトの**resources/2dMotionRes.bundle**にコピーし、再コンパイルしてDemoを実行します。

> ?ステッカーのあるbundleは表示位置にのみ関係しており、ステッカーのタイプとは関係ありません。

## Android

Android端末のDemoの、リソースパック初期化に関連するコードは**XmagicResParser.java**にあり、ステッカー素材リストの初期化メソッドは**parseMotion**です。

1. ステッカー素材名（ディレクトリ名）を文字列**motionResStr**の任意の位置にスプライシングします（コンマに注意してください）。
2. 素材パッケージをDemoプロジェクトの**src/main/asstes/MotionRes/2dMotionRes**ディレクトリ下にコピーし、再コンパイルしてDemoを実行します。

#### 事例：
ステッカー素材フォルダを**video_mymotion**と命名したとします。その場合、次のようにする必要があります。
```java
final String MotionResStr = "video_lianliancaomei:恋恋草苺," +
......
```
を下記のように変更すれば、
```java
final String MotionResStr = "video_mymotion:マイステッカー," +
                            "video_lianliancaomei:恋恋草苺," +
......
```
> !素材パッケージは他の**xxxMotionRes**ディレクトリにコピーすることもできます。これが影響するのはDemo内の表示位置のみであり、ステッカー自体のタイプとは関係ありません。

