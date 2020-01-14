## SDK準備
関連[Demo及びSDK](https://main.qcloudimg.com/raw/5ef28eba111891591f576dbbbaed601c.zip)をダウンロードします。本文は主に Android、iOS 及び Windowsという3つのバージョンのアクセスガイドを含みます。

## Androidアクセス
### 準備作業
- SDKにアクセスするには、次の手順を完了する必要があります。
 1. オペレーティングプラットフォームに応じて対応するsoファイルを選択し、soファイルとjarファイルをプロジェクトディレクトリにコピーし、依存関係を追加します。
 2. SDKインターフェイス関数を呼び出して透かし情報を生成します。
 3. メッセージを送信するときは、20バイトの透かし情報をメッセージ本文の前に置きます。
- SDKファイルにはsoファイルとjarファイルが含まれ、ディレクトリ構造は次のとおりです。
![](https://main.qcloudimg.com/raw/917fa4204160a4def749d5c71a98f810.png)
- SDK APIの説明：
 - プログラムパッケージ：com.gamesec
 - クラス：Mark
- インターフェイスの説明：
<table>
<tbody>
<tr>
<th>インターフェイスの名称</th>
<th>説明</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>透かし生成</td></tr></tbody></table>

### アクセス手順（Android Studio）
1. sdk/androidフォルダの内容をプロジェクトディレクトリのlibs フォルダにコピーします。
 ![](https://main.qcloudimg.com/raw/10957eeaba136e56d53528d4cedc4001.png)
2. アイテムのbuild.gradleファイルを変更し、jniファイルディレクトリを設定し、jar依存関係を追加します。
```
android {
		sourceSets {
				main {
						jniLibs.srcDirs =['libs/jni'] // jni ディレクトリ設定
					 }
				   }
			}
		dependencies {
						implementation files('libs/gamesec.jar') // 依存関係追加
				     }
```
3. Eclipseのアクセス方法が類似し、build.gradleファイルを設定する必要がありません。

### インターフェイスの呼び出し
1. プログラムパッケージをインポートします。
```
import com.gamesec.*;
```
2. Markオブジェクトをインスタンス化します。
```
Mark mark = new Mark();
```
3. CreateSDKBuffFromStrを呼び出して透かしを生成します。
```
byte [ ] CreateSDKBuffFromStr (String pSDKinfo, String buffer, String uDesIp, int uDesPort)
```
 - **パラメータの説明：**
<table>
<tr>
<th>パラメータ</th>
<th>タイプ</th>
<th>意味</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>String</td>
<td>透かし保護キー</td>
</tr>
<tr>
<td>buffer</td>
<td>String</td>
<td>プレースホルダパラメータであり、空の文字列に送信すればいいです</td>
</tr>
<tr>
<td>uDeslp</td>
<td>String</td>
<td>サーバーIP、例えば 「1.2.3.4」</td>
</tr>
<tr>
<td>uDesPort</td>
<td>int</td>
<td>サーバーポート</td>
</tr>
</table>
 - **戻り値：**
<table>
<tr>
<th>タイプ</th>
<th>意味</th>
</tr>
<tr>
<td>byte[]</td>
<td>計算された透かし情報であり、20バイトをとります</td>
</tr>
</table>
 - **呼び出しの例：**
```
String pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
String uDesIp = "115.159.147.198";
int uDesPort = 8899 ;
byte[] bytes = mark.CreateSDKBuffFromStr(pSDKinfo, "", uDesIp, uDesPort);
```

4. メッセージ本文に透かし情報を追加します。コードの例は次のとおりです。
```
Socket s = new Socket(uDesIp, uDesPort);
OutputStream out = s.getOutputStream();
PrintWriter output = new PrintWriter(out, true);
// まず、透かし情報を送信します
output.print(bytes); 
output.println("msg msg msg");
BufferedReader input = new BufferedReader(new InputStreamReader(s.getInputStream()));
String msg = input.readLine();
s.close();
```

## iOSアクセス

### 準備作業
- SDKにアクセスするには、次の手順を完了する必要があります。
	1. SDKファイルをプロジェクトディレクトリにコピーし、Swift プロジェクトはブリッジファイルを追加する必要があります。
	2. SDKインターフェイス関数を呼び出して透かし情報を生成します。
	3. メッセージを送信するときは、20バイトの透かし情報をメッセージ本文の前に置きます。
- SDKファイルにはaファイルとhファイルが含まれ、ディレクトリ構造は次のとおりです。
 ![](https://main.qcloudimg.com/raw/64126dc978ed27a9c4c5d02ad906a250.png)
- インターフェイスの説明：
<table>
<tbody>
<tr>
<th>インターフェイスの名称</th>
<th>説明</th></tr>
<tr>
<td>CreateSDKBuffFromStr</td>
<td>透かし生成</td></tr></tbody></table>

### アクセス手順（Xcode）
1. sdk/iosフォルダの内容をプロジェクトディレクトリにコピーします。
![](https://main.qcloudimg.com/raw/1e6284a08a2d17c9138e4442cb7204b1.png)
2. SDKファイルをXcodeに追加します。プロジェクト名を右クリックして、「Add Files to」をクリックします。
![](https://main.qcloudimg.com/raw/d2dc416312ca9c2b244c7a0ba75ce841.png)
3. ダイアログで 「Create folder references」を選択し、SDK の二つのファイルを選択し、Addをクリックします。
![](https://main.qcloudimg.com/raw/2a7bf9fb066bd7c4ab584eb4287a5f1b.png)
4. プロジェクト名を左クリックして、Generalを選択し、a ファイルを 「Linked Framews and Libraries」に追加します。
![](https://main.qcloudimg.com/raw/b509d322e2cb7485c848f4226ed9ccfd.png)
5. Swiftアイテムであれば、ブリッジファイルを作成する必要があり、Object-Cアイテムはこのステップをスキップできます。Header Fileを作成し、bridge.hに命名します。次のコードをファイルに追加します。
			# import "gamesec.h";
6. プロジェクト名を左クリックして、Build Settingsを選択し、 bridge.h を Object-C Bridging Headerに追加します。
![](https://main.qcloudimg.com/raw/2a7bf9fb066bd7c4ab584eb4287a5f1b.png)

### インターフェイスの呼び出し

1. Swiftアイテムは、生成された透かし関数を直接呼び出すことができ、Object-Cアイテムは、使用されるファイルにヘッダーファイルを追加する必要があります。
```
# import "gamesec.h";
```
2. CreateSDKBuffFromStrを呼び出して透かしを生成します。
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_tuDstPort);
```
**パラメータの説明：**
<table>
<tr>
<th>パラメータ</th>
<th>タイプ</th>
<th>意味</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>透かし保護キー</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>透かしポインタは、透かし結果を出力します</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>サーバーIP、例えば、「1.2.3.4」</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>サーバーポート</td>
</tr>
</table>
 
 >**注意：**
 >透かし結果はパラメータbufferに保存され、20バイトを取ります。
3. 呼び出しの例。
**Swiftの呼び出し：**
```
	let pSDKinfo = UnsafeMutablePointer<Int8>(mutating: (
			"566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c" 
			as NSString).utf8String);
					var buffer = UnsafeMutablePointer<UInt8>.allocate(capacity: 20);
			let uDstIp = UnsafeMutablePointer<Int8>(mutating: (
			"115.159.147.198" as NSString).utf8String);
					let uDstport = UInt16.init("8899")!;

			CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstport);

					for i in 0 ..< 20 {
							let b = (buffer+i).pointee;
							// 透かし情報は前の20バイトにあり、ここで出力されたのはuint8
							print(" \(b)")であることに注意してください;
					}
**Object-Cの呼び出し：** 

			char *pSDKinfo = "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
					uint8_t buffer[20];
					char *uDstIp = "115.159.147.198";
					uint16_t uDstPort = 8899;

					CreateSDKBuffFromStr(pSDKinfo, buffer, uDstIp, uDstPort);

					for(int i=0;i<20;i++)
			{
					// 透かし情報は前の20バイトにある
							NSLog(@"%d", (int8_t)buffer[i]); 
			}
```
4. メッセージを送信する前に、20バイトの透かし情報をメッセージ本文の前に置きます。

## Windowsアクセス
### 準備作業
SDK はgamesec.dllファイルであり、透かしを生成する関数を持っています。
```
uint32_t CreateSDKBuffFromStr(char *pSDKinfo, uint8_t *buffer, char* uDstIp, uint16_t uDstPort);
```
**パラメータ説明：**
<table>
<tr>
<th>パラメータ</th>
<th>タイプ</th>
<th>意味</th>
</tr>
<tr>
<td>pSDKinfo</td>
<td>char *</td>
<td>透かし保護キー</td>
</tr>
<tr>
<td>buffer</td>
<td>uint8_t *</td>
<td>透かしポインタは、透かし結果を出力します</td>
</tr>
<tr>
<td>uDeslp</td>
<td>char *</td>
<td>サーバーIP、例えば、「1.2.3.4」</td>
</tr>
<tr>
<td>uDesPort</td>
<td>uint16_t</td>
<td>サーバーポート</td>
</tr>
</table>

 >**注意：**
>透かし結果はパラメータbufferに保存され、20バイトを取ります。


### インターフェイスの呼び出し

かし関数を使用する場合は、まず、dllファイルをインポートする必要があり、LoadLibrary関数を使用できます（Windows.hを追加する必要があります ）。
```
 // 関数ポインタの定義
    typedef int(*FUNC)(char *, uint8_t *, char* , uint16_t );
    //dll経路設定
    HINSTANCE Hint = ::LoadLibrary(L"E:\\sdk\\gamesec.dll");
    FUNC CreateSDKBuffFromStr = (FUNC)GetProcAddress(Hint, "CreateSDKBuffFromStr");
```
完全な呼び出しの例：
```
 // 透かしを保存します
    uint8_t buffer[BUFFER_SIZE];
    memset(buffer, 0, BUFFER_SIZE);
    
    int UDP_TEST_PORT = 8899;
    
    const char * CONST_UDP_SERVER_IP  = "115.159.147.198";
    char * UDP_SERVER_IP = new char[strlen(CONST_UDP_SERVER_IP)];
    strcpy(UDP_SERVER_IP, CONST_UDP_SERVER_IP);
    
    const char * CONST_pSDKinfo = 
    "566c2dea9420eb37-b6c8-566c2dea9420eb3710525135e8485e80806a2f9c";
    char * pSDKinfo = new char[strlen(CONST_pSDKinfo)];
    strcpy(pSDKinfo, CONST_pSDKinfo);
    
    // 10回呼び出します
    for (int i = 0; i < 5; i++) {
    CreateSDKBuffFromStr(pSDKinfo, buffer, (char *)UDP_SERVER_IP, UDP_TEST_PORT);
    
    for (int i = 0; i <= 20; i++)
    {
    // 透かし情報は前の20バイトにあります
    printf("%d ", (int8_t)buffer[i]);
    }
    printf("\n\n");
    }
```
