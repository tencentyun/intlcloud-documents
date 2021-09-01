## 現象の説明
Linux CVMインスタンスには、メモリの問題に起因する障害が発生します。例えば、システム内部サービスの応答速度が遅くなったり、サーバーがログインに失敗したり、システムがOOM(Out Of Memory)をトリガーしたりするなどです。

## 考えられる原因
インスタンスのメモリ使用率が高すぎることなどが原因と考えられます。通常、インスタンスのメモリ使用率が持続的に90%を超える場合は、インスタンスのメモリ使用率が高すぎると判断できます。


## トラブルシューティングの考え方
1. [処理手順](#ProcessingSteps)を参照して、メモリ使用率が高すぎることが原因で問題が発生しているのかどうか判断してください。
2. [その他のメモリ問題による典型的ケースの分析](#OtherProcessingSteps)を参照して、問題の原因を特定します。

## 処理手順[](id:ProcessingSteps)
1. [関連操作](#RelatedOperations)を参照して、メモリ使用率が高すぎないか確認してください。
 - メモリ使用率が高すぎる場合は、次の手順に進んでください。
 - メモリ使用率が正常な場合、[その他のメモリ問題による典型的ケースの分析](#OtherProcessingSteps)を参照して、問題の原因をさらに特定してください。
2. システム内部で`top`コマンドを実行した後、**M**を押して、「RES」列と「SHR」列のプロセスがメモリを占有しすぎていないか確認します。
  - 「いいえ」の場合は、次の手順に進んでください。
  - 「はい」の場合は、プロセスタイプに応じて操作してください。詳細については、[分析プロセス](https://intl.cloud.tencent.com/document/product/213/32387)をご参照ください。
3. 以下のコマンドを実行して、共有メモリを占用しすぎているかどうか確認します。
```
cat /proc/meminfo | grep -i shmem
```
返された結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/269ca888f6f0232a63705b6f9fd578a8.png)
4. 以下のコマンドを実行して、回収不能なslabのメモリの占有が多すぎるかどうかを確認します。
```
cat /proc/meminfo | grep -i SUnreclaim
```
返された結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/9e6c84eb5bfb0be315fc39d1b768d168.png)
5. 以下のコマンドを実行して、メモリラージページがあるかどうか確認します。
```
cat /proc/meminfo | grep -iE "HugePages_Total|Hugepagesize"
```
返された結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/aae7ce06f7034c123c26ef92265b82ea.png)
 - `HugePages_Total`の出力は0です。[その他のメモリ問題による典型的ケースの分析](#OtherProcessingSteps)を参照して、問題の原因をさらに特定してください。
 - `HugePages_Total`の出力が0でない場合は、メモリラージページが設定されていることを意味します。 メモリラージページのサイズは、`HugePages_Total*Hugepagesize`です。hugepageが他の悪意のあるプログラム用に設定されているかどうか確認する必要があります。メモリラージページが不要になったことを確認した場合、`/etc/sysctl.conf`ファイルの`vm.nr_hugepage`設定項目にコメントを付けてから、`sysctl -p`コマンドを再実行してメモリラージページをキャンセルします。

## 関連操作[](id:RelatedOperations)
### メモリ使用率の確認
異なるLinuxディストリビューションでは、`free`コマンドの出力の意味が異なる可能性があるため、単純に`free`コマンドの出力情報からメモリ使用率を算出することはできません。以下の手順に従い、Tencent Cloudのメモリ監視を介してメモリ使用率を取得してください。
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインして、インスタンス管理ページに進みます。
2. インスタンスIDを選択し、インスタンス詳細ページに進み、【監視】タブを選択します。
3. 「メモリ監視」では、インスタンスのメモリ使用率を表示できます。下図のとおりです。
![](https://main.qcloudimg.com/raw/4f9f423e6d9d460d1413ff0ead6c7e96.png)

### メモリ使用率の計算
メモリ監視でのメモリ使用率は、バッファとシステムキャッシュによって占有されているコンテンツを除いた、メモリの合計量に対するユーザーが使用したメモリ量の比率として計算します。計算プロセスは次のとおりです。
= `(Total - available)100% / Total`
= `(Total - (Free + Buffers + Cached + SReclaimable - Shmem))100% /Total`
= `(Total - Free - Buffers - Cached - SReclaimable + Shmem）* 100% / Total`

計算プロセスで使用される`Total`、`Free`、`Buffer`、`Cached`、`SReclaimable`および`Shmem`のパラメータは、`/proc/meminfo`から取得できます。`/proc/meminfo`の例は次のとおりです。
```plaintext
1. [root@VM_0_113_centos test]# cat /proc/meminfo 
2. MemTotal: 16265592 kB
3. MemFree: 1880084 kB
4. ......
5. Buffers: 194384 kB
6. Cached: 13647556 kB
7. ......
8. Shmem: 7727752 kB
9. Slab: 328864 kB
10. SReclaimable: 306500 kB
11. SUnreclaim: 22364 kB
12. ......
13. HugePages_Total: 0
14. Hugepagesize: 2048 kB
```
パラメータの説明は次のとおりです。
<table>
<tr>
<th>パラメータ</th>
<th>説明</th>
</tr>
<tr>
<td><code>MemTotal</code></td>
<td>システムのメモリ合計。</td>
</tr>
<tr>
<td><code>MemFree</code></td>
<td>システムの余剰メモリ。</td>
</tr>
<tr>
<td><code>Buffers</code></td>
<td>ブロックデバイス(block device)が占有するキャッシュページを意味します。直接読み取り/書き込みと、SuperBlockが使用するキャッシュページなどのような、ファイルシステムのメタデータ(metadata)を含みます。</td>
</tr>
<tr>
<td><code>Cached</code></td>
<td>page cache、tmpfsのファイル<code>POSIX/SysV shared memory</code>および<code>shared anonymous mmap</code>を含みます。
</td>
</tr>
<tr>
<td><code>Shmem</code></td>
<td>共有メモリ、tmpfsなどを含みます。
</td>
</tr>
<tr>
<td><code>Slab</code></td>
<td>カーネルslabアロケータによって割り当てられたメモリは、 <code>slabtop</code>で確認できます。
</td>
</tr>
<tr>
<td><code>SReclaimable</code></td>
<td>回収可能なslabです。</td>
</tr>
<tr>
<td><code>SUnreclaim</code></td>
<td>回収不可能なslabです。</td>
</tr>
<tr>
<td><code>HugePages_Total</code></td>
<td>メモリラージページの合計ページ数です。</td>
</tr>
<tr>
<td><code>Hugepagesize</code></td>
<td>メモリラージページ1ページ分のサイズです。</td>
</tr>
</table>

### その他のメモリ問題による典型的ケースの分析[](id:OtherProcessingSteps)
上記の手順で問題を処理できない場合、またはCVMの使用時に以下のタイプのエラー情報が表示される場合は、以下のソリューションをご参照ください。
- [ログエラーfork：Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)
- [VNCログインエラーCannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40503)
- [インスタンスメモリが使い果たされていない場合、Out Of Memoryがトリガーされます](https://intl.cloud.tencent.com/document/product/213/40504) 
