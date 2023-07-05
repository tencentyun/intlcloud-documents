CVMインスタンスの一般的に使用されるポートリストは次のとおりです。
## Linuxの一般的なサービス
<table>
<tr>
<th><b>サービス</b></th>
<th><b>機能</b></th>
<th><b>サービスタイプ</b></th>
<th><b>サービス名</b></th>
<th><b>バックエンドサービスアクセスドメイン名</b></th>
<th><b>バックエンドサービスアクセスポート</b></th>
</tr>
<tr>
<td rowspan="5">インスタンス初期化サービス</td> 
<td rowspan="5">インスタンス初期化機能の提供</td> 
<td rowspan="5">非常駐サービス、<br>実行完了後に終了</td> 
<td rowspan="2">cloud-init</td> 
<td>mirrors.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>tlinux-mirrors.tencentyun.com</td>
<td>443</td>
</tr>
<tr>
<td rowspan="3">公共サービス</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67、68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan="3">CM</td> 
<td rowspan="2">CM機能の提供</td> 
<td rowspan="2">常駐サービス</td> 
<td rowspan="2">barad_agent</td> 
<td>receiver.barad.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>eventproxy.tencentyun.com</td>
<td>80</td>
</tr>
<tr>
<td>CMのインストールおよび<br>CMのアップグレード</td>    
<td>常駐サービス</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection（クラウドイメージ）</td> 
<td rowspan="4">クラウドセキュリティ機能の提供</td> 
<td rowspan="4">常駐サービス</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080、80</td> 
</tr>
</table>

## Windowsの一般的なサービス
<table>
<tr>
<th><b>サービス</b></th>
<th><b>機能</b></th>
<th><b>サービスタイプ</b></th>
<th><b>サービス名</b></th>
<th><b>バックエンドサービスアクセスドメイン名</b></th>
<th><b>バックエンドサービスアクセスポート</b></th>
</tr>
<tr>
<td rowspan="5">インスタンス初期化サービス</td> 
<td rowspan="5">インスタンス初期化機能の提供</td> 
<td rowspan="5">非常駐サービス、<br>実行完了後に終了</td> 
<td rowspan="2">cloudbase-init</td> 
<td>kms.tencentyun.com</td> 
<td>1688</td> 
</tr>
<tr>
<td>kms1.tencentyun.com</td>
<td>1688</td>
</tr>
<tr>
<td rowspan="3">公共サービス</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67、68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan="3">CM</td> 
<td rowspan="2">CM機能の提供</td> 
<td rowspan="2">常駐サービス</td> 
<td rowspan="2">BaradAgentSvc</td> 
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>custom.message.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>CMのインストールおよび<br>CMのアップグレード</td>    
<td>常駐サービス</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection<br>（クラウドイメージ）</td> 
<td rowspan="4">クラウドセキュリティ機能の提供</td> 
<td rowspan="4">常駐サービス</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080、80</td> 
</tr>
</table>



