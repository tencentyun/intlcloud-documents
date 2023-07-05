## 現象の説明
VNCまたはSSHログインを使用する際、エラーメッセージ“Permission denied”が表示される。
- VNCログインエラーは下図のように表示されます。
![](https://main.qcloudimg.com/raw/5f1aedd75b6d99cddab4d83fa82d964f.png)
- SSHログインエラーは下図のように表示されます。
![](https://main.qcloudimg.com/raw/7ab31fbb82391da2c8ae28e8ad3b961f.png)

## 考えられる原因
VNCまたはSSHを使用したログインでは`/etc/pam.d/login`というpamモジュールを呼び出して検証を行います。`/etc/pam.d/login`の設定において、デフォルトでは`system-auth`モジュールをインポートして認証を行い、`system-auth`モジュールはデフォルトで`pam_limits.so`モジュールをインポートして認証を行います。`system-auth`のデフォルト設定は下図のとおりです。
![](https://main.qcloudimg.com/raw/e32db00ec665388bc4c7cb0454fd6fab.png)
`pam_limits.so`モジュールの主な機能はユーザーのセッションの過程で各種システムリソースの使用状況を制限することです。デフォルトではこのモジュールの設定ファイルは`/etc/security/limits.conf`であり、この設定ファイルはユーザーが使用可能な最大ファイル数、最大スレッド数、最大メモリなどのリソース使用量を規定しています。パラメータの説明は下表のとおりです。
<table>
<tr>
<th style="width:20%">パラメータ</th><th>説明</th>
</tr>
<tr>
<td><code>soft nofile</code></td>
<td>開くことができるファイルディスクリプタの最大数（ソフトリミット）。</td>
</tr>
<tr>
<td><code> hard nofile</code></td>
<td>開くことができるファイルディスクリプタの最大数（ハードリミット）。この設定値を超えることはできません。</td>
</tr>
<tr>
<td><code>fs.file-max </code></td>
<td>システムクラスにおいて開くことができるファイルハンドラ（カーネル中のstruct file）の数量。システム全体に対する制限であり、ユーザーに対してのものではありません。</td>
</tr>
<tr>
<td><code>fs.nr_open</code></td>
<td>1つのプロセスで割り当て可能な最大ファイルディスクリプタ数（fd個数）。</td>
</tr>
</table> 

正常にログインできない原因は、設定ファイル`/etc/security/limits.conf`中のrootユーザーが開くことのできるファイルディスクリプタの最大数の設定にエラーがあることによる可能性があります。 正しい設定は`soft nofile ≤ hard nofile ≤ fs.nr_open`の関係を満たしていなければなりません。


## 解決方法
[処理手順](#ProcessingSteps)を参照し、`soft nofile`、`hard nofile`および`fs.nr_open`を正しい設定に修正します。

[](id:ProcessingSteps)

## 処理手順

1. SSHを使用したCVMインスタンスへのログインを試してください。詳細については[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501)をご参照ください。
	- ログインに成功した場合は次の手順に進みます。
	- ログインに失敗した場合は、単一ユーザーモードを使用する必要があります。
2. パラメータ`soft nofile`、`hard nofile`および`fs.nr_open`の値が`soft nofile ≤ hard nofile ≤ fs.nr_open`の関係を満たしているかどうかを確認します。
 - 次のコマンドを実行し、`soft nofile`および`hard nofile`の値を確認します。
```
/etc/security/limits.conf
```
ここでの取得結果は3000001と3000002です。下図のように表示されます。
![](https://main.qcloudimg.com/raw/3bc035efb6cf46f70b30017dbefe831a.png)
 - 次のコマンドを実行し、`fs.nr_open`の値を確認します。
```
sysctl -a 2>/dev/null | grep -Ei "file-max|nr_open"
```
ここでの取得結果は1048576です。下図のように表示されます。
![](https://main.qcloudimg.com/raw/0fee5e2cda62d6a558cf808652a6b9dd.png)
3. `/etc/security/limits.conf`ファイルを修正し、次の設定をファイルの末尾に追加または修正します。 
 - `root soft nofile`:100001
 - `root hard nofile`:100002
4. `/etc/sysctl.conf`ファイルを修正し、次の設定をファイルの末尾に追加または修正します。
>?`soft nofile ≤ hard nofile ≤ fs.nr_open`の関係を満たしている場合は、この手順は必須ではありません。システムの最大制限が不足している場合に再調整することができます。
>
 - `fs.file-max` = 2000000
 - `fs.nr_open` = 2000000
5. 次のコマンドを実行すると、設定は直ちに有効になります。設定を完了するとログインできるようになります。
```
sysctl -p
```

