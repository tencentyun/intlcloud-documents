## テストツール
sysbench 1.0.20は、データベースのベンチマーク性能をテストするツールです。

####ツールのインストール
このドキュメントのテストではSysbenchバージョン1.0.20を使用します。インストール方法は次のとおりです。
```
git clone https://github.com/akopytov/sysbench.git
git checkout 1.0.20
yum install gcc gcc-c++ autoconf automake make libtool bzr mysql-devel git mysql
cd sysbench
./autogen.sh
./configure
make -j
make install
```

>?上記は負荷テストCVM（CentOS システム）へのインストール方法です。他のOSにインストールする必要がある場合は、[Sysbench公式ドキュメント](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)をご参照ください。

## テスト環境
| タイプ               | 説明                                                         |
| :----------------- | :----------------------------------------------------------- |
| テストインスタンスの仕様       | このテストでは、通常使用される4コア8GBメモリ、8コア32GBメモリ、16コア128GBメモリという3種類の仕様を選択しています |
| クライアント構成         | 64コア128GBメモリ                                                |
| クライアントプライベートネットワーク帯域幅     | 23Gbps                                                       |
| テストデータ量         |データベースインスタンスメモリ * 1.2                                           |
| テストデータベースインスタンスバージョン | 5.6 20210630、5.7 20210630、8.0 20210330                       |

- クライアント仕様の説明：単一クライアントでのテストによってデータベースインスタンスの性能負荷を測定できるように、マシンにはハイスペックなクライアントマシンが使用されます。ロースペッククライアントの場合は、同時インスタンス負荷テストに複数のクライアントを使用して、データの合計を求めることをお勧めします。
- ネットワークレイテンシーの説明：テスト環境は、クライアントのマシンとデータベースインスタンスが同じアベイラビリティーゾーンにあるようにし、テスト結果がネットワーク環境の影響を受けないようにします。


## テスト方法
### テストデータ準備
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write prepare
```

### 性能負荷テスト
```
sysbench --db-driver=mysql --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxxx --mysql-password=xxxx --mysql-db=sbtest --table_size=xxxx --tables=xxxx --events=0 --time=600 --threads=xxxx --percentile=95 --report-interval=1 oltp_read_write run
```

性能負荷テストパラメータの説明：
- `oltp_read_write`は、oltpモードのテスト用に /usr/share/sysbench/oltp_read_write.luaスクリプトが呼び出されることを示しています。
- `--tables=xxxx`は、今回のテストで使用するテーブルの数を示しています。
- `--table_size=xxxx`は、今回のテストで使用するテーブルの行数を示しています。
- `--threads=xxxx`は、今回のテストのクライアント接続同時実行数であることを示しています。
- `--report-interval=1`は、テスト結果が1秒に1回出力されることを示しています。
- `--percentile=95`は、サンプリング比率の設定を示しており、デフォルトは95%です。
- `--time=600`は、今回のテストの実行時間を示し、600は600秒を示しています。

### シナリオモデル
ここでのユースケースはすべて、sysbenchのluaスクリプトを使用しています。
一般的な設定タイプについて、さまざまなパラメータテンプレートでパフォーマンステストを行います。そのテスト結果を以下に示します。

## テスト結果
#### 5.6 20210630バージョン
<table>
<thead><tr><th>CPU（コア）</th><th>メモリ(GB)</th><th>threads</th><th>テスト時間</th><th>テンプレート</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>34428.69</td><td>1721.43</td><td>18.59ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>35917.50</td><td>1795.87</td><td>17.82ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>34834.04</td><td>1741.70</td><td>18.37ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>61210.19</td><td>3060.51</td><td>20.91ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>67719.55</td><td>3385.98</td><td>18.90ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>64910.09</td><td>3245.50</td><td>19.72ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>106965.44</td><td>5348.27</td><td>23.93ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>127955.48</td><td>6397.77</td><td>20.00ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>119509.02</td><td>5975.45</td><td>21.41ms</td></tr>
</tbody></table>

#### 5.7 20210630バージョン
<table>
<thead><tr><th>CPU（コア）</th><th>メモリ(GB)</th><th>threads</th><th>テスト時間</th><th>テンプレート</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>34428.69</td><td>1721.43</td><td>18.59ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>35917.50</td><td>1795.87</td><td>17.82ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>34834.04</td><td>1741.70</td><td>18.37ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>61210.19</td><td>3060.51</td><td>20.91ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>67719.55</td><td>3385.98</td><td>18.90ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>64910.09</td><td>3245.50</td><td>19.72ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>106965.44</td><td>5348.27</td><td>23.93ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>127955.48</td><td>6397.77</td><td>20.00ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>119509.02</td><td>5975.45</td><td>21.41ms</td></tr>
</tbody></table>

#### 8.0 20210330バージョン
<table>
<thead><tr><th>CPU（コア）</th><th>メモリ(GB)</th><th>threads</th><th>テスト時間</th><th>テンプレート</th><th>SysBench QPS</th><th>SysBench TPS</th><th>avg_lat</th></tr></thead>
<tbody><tr>
<td rowspan=3>4</td>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>32594.79</td><td>1629.74</td><td>19.63ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>33383.77</td><td>1669.19</td><td>19.17ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>32071.90</td><td>1603.60</td><td>19.95ms</td></tr>
<tr>
<td rowspan=3>8</td>
<td rowspan=3>32</td>
<td rowspan=3>64</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>65718.22</td><td>3285.91</td><td>19.47ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>70195.37</td><td>3509.77</td><td>18.23ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>60704.69</td><td>3035.23</td><td>21.08ms</td></tr>
<tr>
<td rowspan=3>16</td>
<td rowspan=3>128</td>
<td rowspan=3>128</td>
<td rowspan=3>10分間</td>
<td>デフォルトテンプレート（廃棄）</td><td>132023.66</td><td>6601.18</td><td>19.38ms</td></tr>
<tr>
<td>高性能パラメータテンプレート</td><td>151021.67</td><td>7551.08</td><td>16.95ms</td></tr>
<tr>
<td>高安定性テンプレート</td><td>132391.01</td><td>6619.55</td><td>19.33ms</td></tr>
</tbody></table>

