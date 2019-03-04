## 制限と説明
### 制限条件

- CFSの対応するファイルシステムプロトコル：NFS v3.0/v4.0、CIFS/SMB。
- 単一ファイルシステム容量上限：160 TB（そのうち金融専用領域の単一ファイルシステム容量上限は 40 TB）。
- 単一ファイルシステムは200個以下の計算ノードのマウントをサポートします。
- 各ユーザーの各地区でのファイルシステムの上限個数は10個。


### 関連説明
#### UIDとGIDの説明

- NFS v3.0プロトコルを使用するとき、ローカルアカウントにファイルのUIDまたはGIDが存在しない場合、そのままUIDとGIDを表示します。LinuxのローカルアカウントにファイルのUIDまたはGIDが存在している場合、ローカルのUIDとGIDのマッピング関係により対応するユーザー名とグループ名を表示します。
- NFS v4.0プロトコルを使用するとき、Linuxのカーネルバージョンが3.0以降の場合、UIDとGIDの規則はNFS v3.0プロトコルと同じです。ローカルのカーネルバージョンが3.0以前の場合、すべてのファイルのUIDとGIDにnobodyが表示されます。
- 注意：3.0以前のLinuxカーネルバージョンでNFS v4.0プロトコルを用いてファイルシステムをマウントするとき、ファイルまたはディレクトリに対しchange ownerまたはchange group操作を実行しないことをおすすめします。さもなければ、このファイルまたはディレクトリのUIDとGIDはnobodyになります。


#### CIFS/SMBプロトコルの対応状況
- プロトコルバージョンの対応：CIFS、SMB 1.0以降のSMBプロトコルバージョンに対応します。ただし、SMB 1.0プロトコルでのマウントをおすすめしません。原因としては、SMB 1.0とSMB 2.0以後のバージョンと比べて、プロトコル設計の大きな違いがあり、性能と機能に重大きな欠点があり、SMB1.0またはその以前のプロトコルバージョンに対応するWindows製品はMicrosoftのサポートライフサイクルが終了することがあります。
- ユーザーがNFSとSMBを用いて同一ファイルシステムにアクセスすること、広域ネットワークを通じてSMBファイルシステムに直接アクセスすることをサポートしません。
- ファイルシステムレベルの読み書き権限のコントロールを提供しますかが、ファイル/ディレクトリレベルのACL権限のコントロールを提供しません。
- Sparse files、ファイル圧縮、ENI状態の照合、再解析ポイント（Reparse Point）等のIOCTL/FSCTL操作をサポートしません。
- 代替データストリーム（Alternate Data Streams）をサポートしません。
- SMB Direct、SMB Multichannel、SMB Directory Leasing、Persistent File Handle等のSMB 3.0以降の一部のプロトコル機能をサポートしません。 

 <!--
 * NFS v4.0の対応しないAttributes：FATTR4_MIMETYPE、FATTR4_QUOTA_AVAIL_HARD、FATTR4_QUOTA_AVAIL_SOFT、FATTR4_QUOTA_USED、FATTR4_TIME_BACKUP、FATTR4_TIME_CREATE。クライアントにNFS4ERR_ATTRNOTSUPPエラーが表示されます。
 * NFS v4.0の対応しないOP：OP_DELEGPURGE、OP_DELEGRETURN、NFS4_OP_OPENATTR。クライアントにNFS4ERR_NOTSUPPエラーが表示されます。
 * NFSv4はLockとDelegation機能をサポートしません。
 -->

