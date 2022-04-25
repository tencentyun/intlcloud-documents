ここで紹介するPC版TUIRoomコンポーネントは、柔軟なレイアウトで、適用性の高いオーディオビデオコミュニケーションツールです。コラボレーションオフィス、リモート採用、リモート問診、保険金査定、オンラインカスタマーサービス、ビデオ面接、デジタル行政、金融のデジタル化、オンラインミーティング、eラーニングなどのシーンで使用することができます。 各業界のシナリオと深く結びつき、企業のコスト削減と効率アップを助け、デジタルトランスフォーメーションを加速し、競争力を向上させます。
[Windows](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Win_Demo.exe)または[Mac](https://liteav.sdk.qcloud.com/app/install/TXLiteAVSDK_Mac_Demo.tar.bz2)プラットフォームのAppをダウンロード、インストールして体験できます。

## デモンストレーション
<table>
<tr><td><img src="https://qcloudimg.tencent-cloud.cn/raw/71f2649be2c654e1c5f217dc10e88efc.png" width="600" height="300"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9d927c98a595667d9f3f16d597abc77e.png" width="600" height="340"></td>
</tr></table>



## ソリューションの優位性
- 超低遅延のオーディオビデオ通話、チャットルーム、画面共有、美顔、デバイス検出、データ統計などの機能を統合し、多人数オーディオビデオルームの一般的な機能をカバーします。
- 二次開発の需要に応じて、カスタムUIやレイアウトを迅速に実装し、ビジネスの迅速な立ち上げに役立ちます。
- TRTCとIMの基本SDKをカプセル化し、基本的なロジックコントロールを実装し、呼び出しを容易にするインターフェースを提供します。

## アクセスガイド
多人数オーディオビデオルーム機能をスピーディーに統合するため、ここでは2種類の統合方法をお勧めしています。ご自身に合った方法を選択して二次開発にお役立てください。
- [外部プロセス起動](#start)
- [カスタムUIの実装](#ui)

### 環境の準備
- **Windows環境** ：
	- Visual Studio 2015およびそれ以上の統合開発環境。
	- QT5.9.1およびそれ以上のバージョンのQT開発データベース。
	- VS下のQT開発プラグインQt Visual Studio Tools 2.2.0およびそれ以上。
	- サポートする最低システム要件：Windows 8。
	- 正常な開発が行える統合開発環境であることを確実にしてください。
- **Mac環境**：
	- QT5.9.1およびそれ以上のバージョンのQT開発データベース。
	- QtCreatorは開発環境を統合します。 QTのインストール時に、QtCreatorの同時インストールを選択すればよく、バージョンはQTの公式インストールパッケージに従います。
	- 統合開発環境QtCreatorで正常な開発が行えることを確実にしてください。

### 外部プロセス起動[](id:start)
1. **RoomAppプログラムのコンパイル**
	- 外部プロセスによるRoomApp起動方式を使用する場合は、元のRoomAppの実行プログラムに依存するため、事前のコンパイルが必要です。
	クリックして[RoomApp](https://github.com/tencentyun/TUIRoom)に進み、ソースコードをCloneし、プロジェクトを設定し、RoomAppをコンパイルして生成できます。
2. **TestAppプロジェクトの新規作成**
<dx-tabs>
::: Windowsプラットフォーム
1. VSを開き、Qt Widgets Applicationプロジェクトタイプを選択し、TestAppプロジェクトを作成します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/45b191db25ad1a36eb2c10440f1790ce.png" width="600">
2. プロセスを起動するプログラムを作成し、適切な位置にLoadRoomApp関数を呼び出します。
```C++
#include <QProcess>
#include <QApplication>
void LoadRoomApp() {
    QString executable_file_path = QApplication::applicationDirPath();
    QString app_path = executable_file_path + "/RoomApp.exe";
    QProcess::startDetached(app_path);
}
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/0943ef183039229ff92cb54b2bdc4b2a.png" width="600">

3. プロジェクトをコンパイルし、RoomAppをコンパイルした成果物を現在実行可能なプログラムディレクトリにコピーします。release x86プログラムを例にとると、次のようになります。
`TUIRoom\Windows-Mac\RoomApp\bin\Win32\Release`ディレクトリ下のすべてのファイルを現在のプログラムディレクトリ下にコピーします。
4. プログラムを実行します。TestAppの起動と同時にRoomAppを起動します。
:::
::: Macプラットフォーム
1. QtCreatorを開き、Qt Widgets Applicationプロジェクトを選択して新規作成し、TestAppプロジェクトを作成します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6c90f6f6916843a3360bbc7c3ea3fc67.png" width="600">
2. プロセスを起動するプログラムを作成し、適切な位置にLoadRoomApp関数を呼び出します。
```C++
#include <QProcess>
#include <QApplication>
void LoadRoomApp() {
    QString executable_file_path = QApplication::applicationDirPath();
    QString app_path = executable_file_path + "/../../../RoomApp.app/Contents/MacOS/RoomApp";
    QProcess::startDetached(app_path);
}
```
<img src="https://qcloudimg.tencent-cloud.cn/raw/0fd090fbeef17d75a9b119b1a7e4fc9b.png" width="600">
3. プロジェクトをコンパイルし、RoomAppをコンパイルした生成物`RoomApp.app`を現在のプロジェクトの生成物と同一階層のディレクトリ下にコピーします。上の図で作成したプロジェクトのパスを例にとると、次のようになります。
`RoomApp.app`を`/Users/mac/Desktop/TestApp/build-TestApp-Desktop_Qt_5_9_1_clang_64bit-Release`ディレクトリ下にコピーします。
4. プログラムを実行します。TestAppの起動と同時にRoomAppを起動します。
:::
</dx-tabs>


### カスタムUIの実装[](id:ui)
- 当社が提供するAppを直接変更して適用するか、あるいはAppのソースコードのModuleを使用してカスタムUIを実装することができます
- ソースコードのModuleには、TRTC SDKおよびIM SDKのカプセル化が含まれています。`TUIRoomCore.h`、`TUIRoomCoreCallback.h`、`TUIRoomDef.h` などのファイルでこのモジュールが提供するインターフェース関数およびその他定義を確認し、対応するインターフェースを使用してカスタムUIを実装できます
- AppディレクトリにはUIに関連する設計とロジックが含まれており、必要に応じてRoomAppソースコードを変更し、二次開発を行うことができます。主な機能ポイントは次のとおりです。
<table>
<thead>
<tr>
<th>機能ポイント</th>
<th>ファイルディレクトリ</th>
</tr>
</thead>
<tbody><tr>
<td>トップページログイン</td>
<td>Windows-Mac\RoomApp\App\LoginViewController.cpp</td>
</tr>
<tr>
<td>デバイス検査</td>
<td>Windows-Mac\RoomApp\App\PresetDeviceController.cpp</td>
</tr>
<tr>
<td>ホームページ</td>
<td>Windows-Mac\RoomApp\App\MainWindow.cpp</td>
</tr>
<tr>
<td>配信側リスト</td>
<td>Windows-Mac\RoomApp\App\StageListController.cpp</td>
</tr>
<tr>
<td>メンバーリスト</td>
<td>Windows-Mac\RoomApp\App\MemberListViewController.cpp</td>
</tr>
<tr>
<td>設定ページ</td>
<td>Windows-Mac\RoomApp\App\SettingViewController.cpp</td>
</tr>
<tr>
<td>チャットルーム</td>
<td>Windows-Mac\RoomApp\App\ChatRoomViewController.cpp</td>
</tr>
<tr>
<td>画面共有</td>
<td>Windows-Mac\RoomApp\App\ScreenShareWindow.cpp</td>
</tr>
<tr>
<td>下部ツールバー</td>
<td>Windows-Mac\RoomApp\App\BottomBarController.cpp</td>
</tr>
</tbody></table>

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
