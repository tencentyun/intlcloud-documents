## RAID 概要
RAID は複数のディスクを組み合わせて、ディスクアレイを構成することにより、データの読み書き性能と信頼性を向上させることができます。OS はディスクアレイを一つのハードディスクとしてのみ利用します。現在、RAID は様々なレベルがあります。選択のバージョンに応じて、ディスクアレイは、同等の容量の大きなハードディスクと比べて、データ統合の強化、フォールトトレランス機能の強化、スループットまたは容量の増加等のメリットがあります。
>!
>- 有効期限が迫っているElastic CBS に対して、タイムリーに [更新](https://cloud.tencent.com/document/product/362/6739) 手続きをすることにより、期限切れでElastic CBSがシステムに強制的に隔離されることがRAIDに対する影響を回避します。
>-  RAID 1、RAID 01、RAID 10 を作成する時に、同じサイズのパーティションを利用して、ディスク容量の無駄を減らすことをお勧めします。

 RAID 0、RAID 1、RAID 01 と RAID 10の共通点と相違点は次の表の通り：
<table>
     <tr>
         <th nowrap="nowrap">RAID レベル</th>  
         <th>概要</th>  
		 <th>メリット/デメリット</th>
		 <th>ユースケース（推奨）</th>
     </tr>
	 <tr>
         <td>RAID 0</td>
				 <td>ストレージモード：データは分割されて異なるのディスクに保存されます。<br /></br>仮想ディスクのサイズ：ディスクアレイ内すべてのディスク容量の合計です。</td>
		 <td>
		 <ul><li><b>メリット</b>：読み取りと書き込みは並行で行えます。</br>理論的には、読み取り速度は単一ディスクの N 倍（N はRAID 0 を構成するディスクの数）に達することが可能です。ただ、実際の速度はファイルサイズ、ファイルシステムのサイズ等、複数の要因によって制限されます。</li>
		 <li><b>デメリット</b>：データの冗長性がないと、一つのディスクが破損した場合でも、最悪の場合にはすべてのデータが失う可能性があります</li></ul></td>
		 <td>他の手段でデータをバックアップしたかまたはデータをバックアップする必要がないユースケースに対して、高いI/O 性能が要求されます</td>
     </tr> 
	 <tr>
         <td>RAID 1</td>
         <td>ストレージモード：データはイメージに複数のディスクに保存されます。<br /></br> 仮想ディスクのサイズ：ディスクアレイ中の一番小さいディスクの容量です。</td>
		 <td>
		 <ul><li><b>メリット</b>：<ul>
		 <li>読み取り速度が速いです。</li>
		 <li>データの信頼性が高く、単一ディスクが破損してもデータの修復不可になることはありません。</li>
		 </ul>
		 <li><b>デメリット</b>：<ul>
		 <li>ディスクの利用率が最も低いです。</li>
		 <li>書き込み速度は単一ディスクの書き込み速度によって制限されます。</li>
		 </ul></ul>
		 </td>
		 <td>書き込まれたデータをバックアップする必要があるユースケースに対して、高い読み取り性能が要求されます。</td>
     </tr>
	 <tr>
         <td>RAID 01</td>
         <td>先に複数のディスクを利用して RAID 0を構築します。その後、複数の RAID 0 を利用して、 RAID 1 を構築します。</td>
		 <td><ul><li><b>メリット</b>：RAID 0 と RAID 1 両方のメリットを同時に備えます。</li>
		 <li><b>デメリット</b>：<ul><li>コストは比較的高く、四つ以上のディスクが必要です。</li><li>単一ディスクが破損すると、同ディスクアレイのすべてのディスクが利用できなくなります。</li></td>
		 <td   rowspan="2"> RAID 10 が推奨されます。</td>
     </tr>
	 <tr>
         <td>RAID 10</td>
         <td>先に複数のディスクを利用してRAID 1を構築します。その後、複数の RAID 1を利用して、 RAID 0 を構築します。</td>
		 <td><ul><li><b>メリット</b>：RAID 0 と RAID 1 両方のメリットを同時に備えます。</li>
		 <li><b>デメリット</b>：コストは比較的高く、四つ以上のディスクが必要です。</li></td>
     </tr>
</table>



## RAID を構築する
>?このドキュメントは CentOS CVMで四つのElastic CBSを利用して、RAID 0を構築する方法を説明します。OS とRAID レベルによって、操作が異なる場合があります。このドキュメントは参考までであり、具体的な操作手順と差異は該当OSの製品ドキュメントまたは RAID 関連のドキュメントをご参照ください。

LinuxカーネルはRAIDデバイスを管理するmdモジュールを提供します。直接mdadmツールを利用し、 mdモジュールを呼び出してRAID 0を作成します。
![](https://main.qcloudimg.com/raw/a7e717737b22456319cde4ec4bc0c8e1.png)

1. rootユーザーで [CVMにログインする](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 以下のコマンドを実行して、mdadm をインストールします。
```
yum install mdadm -y
```
インストールが成功した結果は下図に示すように：
![](https://main.qcloudimg.com/raw/9ae334a316638ebc8e8b95a587c6e8b5.png)
3. 以下のコマンドを実行し、 mdadm を利用してRAID 0を作成します。
```
mdadm --create /dev/md0 --level=0 --raid-devices=4 /dev/vd[cdef]1
```
作成が成功した結果は下図に示すように：
![](https://main.qcloudimg.com/raw/7c2d92dc0cf8225d56c6696127e1a6ce.png)
4. 以下のコマンドを実行し、 mkfs を利用してファイルシステム（例えば、EXT3 ファイルシステム）を作成します。
```
mkfs.ext3 /dev/md0
```
作成が成功した結果は下図に示すように：
![](https://main.qcloudimg.com/raw/ed6291597a03923a46914ff39005c90e.png)
5. 以下のコマンドを順番に実行して、ファイルシステムをマウントします。
```
mkdir md0/
mount /dev/md0 md0/
tree md0
```
マウントが成功した結果は下図に示すように：
![](https://main.qcloudimg.com/raw/c77863517336227b6dc5dc0180935e46.png)
6. 以下のコマンドを実行し、ファイルシステムの詳細を確認して、ファイルシステムのUUID（例えば、`c5d8a204:c28853ba:3882e9f8:62d078de`）を記録します。下図に示すように：
```
mdadm --detail --scan
```
![](https://main.qcloudimg.com/raw/bd258e727fc5ca5ee67ffe7ffeddea2a.png)
7. 以下のコマンドを実行して、mdadmの設定ファイルを編集します。
```
vi /etc/mdadm.conf
```
8. 編集モードで、関連情報を入力します。
Elastic CBS に対して、以下の設定を入力することをお勧めします。
```
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 1ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 2ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 3ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 4ID-part1 
ARRAY 論理デバイスパス metadata= UUID=
```
以下は論理デバイスパスが「/dev/md0」、metadata が1.2の場合を例に説明します。以下のコマンドを入力する：
```
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 1ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 2ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 3ID-part1 
DEVICE /dev/disk/by-id/virtio-Elastic Cloud Disk 4ID-part1 
ARRAY /dev/md0 metadata=1.2 UUID=3c2adec2:14cf1fa7:999c29c5:7d739349
```
9.  Esc を押して、`:wq`を入力し、保存して終了します。
