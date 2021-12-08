

<b> `grpc_unity_package.VERSION.zip` ファイルダウンロードしてUnity プロジェクトに解凍した後、Unity Editor エラーが出た （[issue 22251](https://github.com/grpc/grpc/issues/22251) などで説明）場合は、どのように対処すればいいのですか？</b>
**対処方法**：v2.26 バージョン [grpc_unity_package.2.26.0-dev.zip](https://packages.grpc.io/archive/2019/12/a02d6b9be81cbadb60eed88b3b44498ba27bcba9-edd81ac6-e3d1-461a-a263-2b06ae913c3f/index.xml)を再度ダウンロードして解凍してください。

### MacOSサーバープログラムのパッケージ化を実行中に、`error: grpc_csharp_ext` が出た場合は、どのように対処すればよいですか？
<img src="https://main.qcloudimg.com/raw/703dc0dd20342b4aff5d499f2ac1df85.png" style="width: 718px;"></img>
**対処方法**： `Assert/Plugins/Grpc.Core/runtimes/osx/x64 ` パスの  `grpc_csharp_ext.bundle` ファイルを `grpc_csharp_ext` にリネームし、パス `YourUnityApp.app/Contents/Frameworks/MonoEmbedRuntime/osx` にコピーし、パスに存在しないディレクトリを作成してください。

### Linux サーバープログラムのパッケージ化を実行中に `Unable to preload the following plugins: ScreenSelector.so` エラーが出た場合は、どのように対処すればよいですか？
<img src="https://main.qcloudimg.com/raw/f2926b2ac676f2e1e1ce85b8bae397f1.png" style="width: 718px;"></img>
**対処方法**：Unity Editor の **File**>**Build Settings**で**Server Build** にチェックマークを付け、パッケージし直してください。
<img src="https://main.qcloudimg.com/raw/3ffa6a320c4269669c411f32cf7597f0.png" style="width: 718px;"></img>

### GSEが提供する Windows Server 2012 R2 データセンターバージョン64ビット英語バージョンのミラーを使用してサーバーを作成し、Windows サーバープログラムのパッケージ化を実行中に、次の図に示す問題が出現した場合、どのように対処すればよいですか？
![](https://main.qcloudimg.com/raw/aeb980b1528b7796481f2e552a340c64.png)
**対処方法**：下図に示すとおり、アセット作成時に中国語バージョンのミラーを選択し、コードをアップロードして、中国語バージョンのミラーを確認してください。
![](https://main.qcloudimg.com/raw/507d4226c74aa9ce30868be3e107d06c.png)
