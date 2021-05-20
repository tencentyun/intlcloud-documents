ここでは、各リージョンの遅延測定アドレスとサンプルについて説明します。スピードテストドメイン名は、HTTPSおよびUDPをサポートします。

### 各リージョンのスピードテストのHTTPSおよびUDPアドレスは下表のとおりです。 

|   地域   |                 HTTPSスピードテストアドレス                 |   UDPスピードテストアドレス   |
| :------: | :-------------------------------------------: | :-------------: |
|   北京   |    https://ap-beijing.speed.tencentgse.com    | ap-beijing.speed.tencentgse.com |
|   上海   |   https://ap-shanghai.speed.tencentgse.com    | ap-shanghai.speed.tencentgse.com  |
|   中国香港   |   https://ap-hongkong.speed.tencentgse.com    | ap-hongkong.speed.tencentgse.com  |
|   広州   |   https://ap-guangzhou.speed.tencentgse.com   |  ap-guangzhou.speed.tencentgse.com |
|   成都   |   https://ap-chengdu.speed.tencentgse.com   |   ap-chengdu.speed.tencentgse.com | 
|  シンガポール  |   https://ap-singapore.speed.tencentgse.com   |  ap-singapore.speed.tencentgse.com  |
|   ムンバイ   |    https://ap-mumbai.speed.tencentgse.com     | ap-mumbai.speed.tencentgse.com  |
|   シリコンバレー   | https://na-siliconvalley.speed.tencentgse.com |  na-siliconvalley.speed.tencentgse.com   |
| バージニア |    https://na-ashburn.speed.tencentgse.com    |  na-ashburn.speed.tencentgse.com   |
| フランクフルト |   https://eu-frankfurt.speed.tencentgse.com   | eu-frankfurt.speed.tencentgse.com  |
|   ソウル   |     https://ap-seoul.speed.tencentgse.com     | ap-seoul.speed.tencentgse.com  |
|   東京   |     https://ap-tokyo.speed.tencentgse.com     | ap-tokyo.speed.tencentgse.com  |



### デモの説明  
以下、広州リージョンを例に説明します。
- **HTTPS**
```plaintext
ping ap-guangzhou.speed.tencentgse.com
curl https://ap-guangzhou.speed.tencentgse.com/v1/ping
```
- **UDP**
```
ドメイン名 + PORT（8888）
ap-guangzhou.speed.tencentgse.com + PORT(8888)
```
