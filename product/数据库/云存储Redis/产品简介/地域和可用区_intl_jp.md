TencentDB for Redis は国内、中国国外のさまざまなリージョンでサポートを行っています。CVM がサポートするリージョンであればどこでも TencentDB for Redis に対応しています。

## ネットワークの説明
-  同一リージョンにあるクラウドサービス製品間は、イントラネットを介して相互運用を行います。
-  異なるリージョンにあるクラウドサービス製品間は、基本ネットワークのイントラネットで相互運用できないため、ネットワーク間が Peering Connection（PC）に対応している必要があります。
 >?TencentDB for Redis は、アクセス遅延を低減させるために CVM で同じリージョンを選択することをお勧めします。

## リージョンとアベイラビリティゾーン
**中国大陸エリア**

<table class="table-striped">
<tbody>
    <tr>
        <th>リージョン</th>
        <th>アベイラビリティゾーン</th>
    </tr>
    <tr>
        <td rowspan="4">華南エリア（広州）<br> ap-guangzhou</td>
        <td>広州1区（完売）<br> ap-guangzhou-1</td>
    </tr>    
    <tr>
        <td>広州2区<br> ap-guangzhou-2</td>
    </tr>
    <tr>
        <td>広州3区<br> ap-guangzhou-3</td>
    </tr>
    <tr>
        <td>広州4区<br> ap-guangzhou-4</td>
    </tr>
    <tr>
        <td rowspan="2">華南エリア（深圳金融）<br>ap-shenzhen-fsi</td>
        <td>深圳金融1区<span style="background-color: rgb(249, 249, 249);">（金融機関と企業に限り作業指示書提出により使用を申請）<br>ap-shenzhen-fsi-1</span></td>
    </tr>
    <tr>
        <td>深圳金融2区<span style="background-color: rgb(249, 249, 249);">（金融機関と企業に限り作業指示書提出により使用を申請）<br>ap-shenzhen-fsi-2</span></td>
    </tr>
    <tr>
        <td rowspan="4">華東エリア（上海）<br>ap-shanghai</td>
        <td>上海1区<br>ap-shanghai-1</td>
    </tr>
    <tr>
        <td>上海2区<br>ap-shanghai-2</td>
    </tr>
    <tr>
        <td>上海3区<br>ap-shanghai-3</td>
    </tr>
        <tr>
        <td>上海4区<br>ap-shanghai-4</td>
    </tr>
    <tr>
            <td rowspan="3">華東エリア（上海金融）<br>ap-shanghai-fsi</td>
            <td>上海金融1区（金融機関と企業に限り作業指示書提出により使用を申請）<br>ap-shanghai-fsi-1</td>
    </tr>
    <tr>
            <td>上海金融2区（金融機関と企業に限り作業指示書提出により使用を申請）<br>ap-shanghai-fsi-2</td>
    </tr>
        <tr>
            <td>上海金融3区（金融機関と企業に限り作業指示書提出により使用を申請）<br>ap-shanghai-fsi-3</td>
    </tr>
    <tr>
            <td rowspan="4">華北エリア（北京）<br>ap-beijing</td>
            <td>北京1区<br>ap-beijing-1</td>
    </tr>
    <tr>
            <td>北京2区<br>ap-beijing-2</td>
    </tr>
    <tr>
            <td>北京3区<br>ap-beijing-3</td>
    </tr>
        <tr>
            <td>北京4区<br>ap-beijing-4</td>
    </tr>
    <tr>
        <td rowspan="2">西南エリア（成都）<br>ap-chengdu</td>
        <td>成都1区<br>ap-chengdu-1</td>
    </tr>
    <tr>
            <td>成都2区<br>ap-chengdu-2</td>
    </tr>    
    <tr>
            <td >西南エリア（重慶）<br>ap-chongqing</td>
            <td>重慶1区<br>ap-chongqing-1</td>
    </tr>
</tbody>
</table>    


**国際エリア**

<table class="table-striped">
    <tbody>
    <tr>
            <th>リージョン</th>
            <th>アベイラビリティゾーン</th>
        </tr>
        <tr>
            <td rowspan="2">東南アジアエリア（中国香港）<br>ap-hongkong</td>
            <td>中国香港1区（中国香港ノードは東南アジアエリアをカバー可）<br>ap-hongkong-1</td>
        </tr>
<tr>
            <td>中国香港2区（中国香港ノードは東南アジアエリアをカバー可）<br>ap-hongkong-2</td>
           </tr>
        <tr>
            <td>東南アジアエリア（シンガポール）<br>ap-singapore</td>
            <td>シンガポール1区（シンガポールノードは東南アジアエリアをカバー可）<br>ap-singapore-1</td>
        </tr>
        <tr>
            <td >アジア太平洋エリア（ソウル）<br>ap-seoul</td>
            <td>ソウル1区（ソウルノードは東北アジアエリアをカバー可）<br>ap-seoul-1</td>
        </tr>
        <tr>
            <td >アジア太平洋エリア（東京）<br>ap-tokyo</td>
            <td>東京1区（東京ノードは東北アジアエリアをカバー可）<br>ap-tokyo-1</td>
        </tr>
       <tr>
            <td >アジア太平洋エリア（ムンバイ）<br>ap-mumbai</td>
            <td>ムンバイ1区（ムンバイノードはアジア太平洋南部エリアをカバー可）<br>ap-mumbai-1</td>
        </tr>
        <tr>
              <td >アジア太平洋エリア（タイ）<br>ap-bangkok </td>
                 <td >バンコク1区  （バンコクノードはアジア太平洋南部エリアをカバー可）<br>ap-bangkok-1</td>
        <tr>
            <td>北米エリア（トロント）<br>na-toronto</td>
            <td>トロント1区（トロントノードは北米エリアをカバー可）<br>na-toronto-1</td>
        </tr>
        <tr>
            <td rowspan="1">米国西部（シリコンバレー）<br>na-siliconvalley</td>
            <td>シリコンバレー1区（シリコンバレーノードは米国西部エリアをカバー可）<br>na-siliconvalley-1</td>
        </tr>
        <tr>
        <tr>
            <td>米国東部（ヴァージニア）<br>na-ashburn</td>
            <td>ヴァージニア1区 （ヴァージニアノードは米国東部エリアをカバー可）<br>na-ashburn-1</td>
        </tr>
            <td>欧州エリア（フランクフルト）<br>eu-frankfurt</td>
            <td>フランクフルト1区（フランクフルトノードは欧州エリアをカバー可）<br>eu-frankfurt-1</td>
        </tr>
        <td >欧州エリア（モスクワ）<br>eu-moscow</td>
        <td>モスクワ1区（モスクワノードは欧州エリアをカバー可）<br>eu-moscow-1</td>
        </tr>
    </tbody>
</table>

## 特別エリアの説明
華南エリア（深圳金融）、華東エリア（上海金融）では [作業指示の送信](https://console.cloud.tencent.com/workorder/category/create?level1_id=10&level2_id=103&level1_name=%E6%95%B0%E6%8D%AE%E5%BA%93&level2_name=%E4%BA%91%E5%AD%98%E5%82%A8Redis%20CRS) による申請処理が必要です。
