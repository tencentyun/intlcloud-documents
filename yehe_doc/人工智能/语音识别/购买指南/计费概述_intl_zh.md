腾讯云语音识别 ASR 提供后付费计费模式，开通服务后默认使用后付费的计费模式。如果您拥有免费资源包或者付费资源包，将优先使用免费资源包，资源包耗尽后自动转入后付费的方式。实时语音识别、一句话识别和录音文件识别均支持该计费模式。

## 产品价格
### 免费额度
只要您开通了语音识别服务，选择后付费的计费方式，每项服务都可以享受免费调用额度，免费调用额度将以免费资源包的形式配送，并在计费结算时优先扣减。
具体的免费额度如下：

<table width="100%">
     <tr>
         <th width="20%" align="center">服务名称</th>
	 <th width="20%" align="center">免费额度</th>
     </tr>
  <tr>      
      	  <td colspan="1" align="center">录音文件识别</td> 
	  <td  align="center">每月10小时</td>  
     </tr> 
		   <tr>
           <td align="center">实时语音识别</td>   
      <td align="center"> 每月5小时</td>
			</tr> 
  <tr>
            <td align="center"> 一句话识别</td>   
      <td align="center"> 每月5000次</td>
     </tr> 
		 <tr>
     </tr>   
</table>


>?
- 免费资源包耗尽后，将**自动转入后付费**方式结算。
- 当月首次开通服务的新客户，开通后立即发放免费资源包；老客户的免费资源包从每月1日开始发放。免费资源包在发放之后才正式生效，且仅当月有效。

### 后付费
所有语音识别服务开通后即默认采用后付费的方式，资源包耗尽后均会**自动转入后付费**。如果您未购买预付费资源包，则每月在免费资源包耗尽后会**自动转入后付费**；如果您已经购买了预付费资源包，则在免费资源包和预付费资源包均耗尽以后，会**自动转入后付费**。
- 录音文件识别按识别时长计费，计费标准如下：
<table width="510" >
     <tr>
         <th width="150" align="center">服务名称</th>  
         <th width="180" align="center">每天用量（小时）</th>  
         <th width="180" align="center">单价（美元/小时）</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">录音文件识别</td>   
      <td align="right"> 0 ~ 299</td>   
      <td align="right">1 </td>   
     </tr> 
  <tr>
      <td align="right">300 ~ 999</td>   
      <td align="right">0.95 </td>
     </tr> 
  <tr>
      <td align="right">1000 ~ 2999</td>   
      <td align="right">0.90 </td>
     </tr> 
<tr>
      <td align="right">3000 ~ 4999</td>   
      <td align="right">0.85 </td>
     </tr> 
  <tr>      
      <td align="right">≥5000</td>   
      <td align="right">0.60</td>
	  </tr>
</table>


- 实时语音识别按识别时长计费，计费标准如下：
<table width="510" >
     <tr>
         <th width="150" align="center">服务名称</th>  
         <th width="180" align="center">用量梯度（小时/日）</th>  
         <th width="180" align="center">单价（美元/小时）</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">实时语音识别</td>   
      <td align="right">0 ~ 299</td>   
      <td align="right">1.4</td>   
     </tr> 
  <tr>
      <td align="right">300 ~ 999</td>   
      <td align="right">1.2</td>
     </tr> 
  <tr>      
         <td align="right">1000 ~ 2999</td>   
      <td align="right">1</td>   
	</tr>		
	<tr>      
         <td align="right">3000 ~ 4999</td>   
      <td align="right">0.86</td>   
	</tr>	
	<tr>      
         <td align="right">≥ 5000</td>   
      <td align="right">0.7</td>   
	</tr>	
</table>

- 一句话识别按接口调用次数计费，计费标准如下：
<table width="510" >
     <tr>
         <th width="150" align="center">服务名称</th>  
         <th width="180" align="center">用量梯度（千次/日）</th>  
         <th width="180" align="center">单价（美元/千次）</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">一句话识别</td>   
      <td align="right">0 ~ 299</td>   
      <td align="right">1.40</td>   
     </tr> 
  <tr>
      <td align="right">300 ~ 999</td>   
      <td align="right">1.20</td>
     </tr> 
  <tr>      
         <td align="right">1000 ~ 2999</td>   
      <td align="right">1.00</td>   
	</tr>		
	<tr>      
         <td align="right">3000 ~ 4999</td>   
      <td align="right">0.86</td>   
	</tr>	
	<tr>      
         <td align="right">≥ 5000</td>   
      <td align="right">0.70</td>   
	</tr>	
</table>


## 计费与结算方式

### 后付费
每月接口调用总量达到某个阶梯后，所有调用量按该阶梯的单价进行计费，阶梯越高，单价越低。使用实时语音识别、一句话识别和录音文件识别，每日会对上一日用量输出账单并扣费。

<table width="100%">
  <tr>
         <th width="12%" align="center">计费模式</th>
	 <th width="44%" align="center">后付费</th>
     </tr>
  <tr>       
      <td align="center">付款方式</td>   
      <td align="center">结算后付费</td> 
     </tr> 
  <tr>
      <td align="center"> 计费周期</td>   
      <td align="center"> 日</td> 
     </tr> 
  <tr>
      <td align="center">支持范围</td>   
      <td align="center"> 实时语音识别、一句话识别和录音文件识别</td> 
     </tr>
  <tr>
      <td align="center">适用场景</td>   
      <td align="center">适用于使用量有较大波动性，或无法预估的业务</td> 
      </tr>   
</table>



## 费用计算示例
### 后付费

#### 示例一
用户**当日**累计识别录音文件的时长到达510小时，所需支付的费用计算如下：
（510-10）× 0.95= 475（美元）

#### 示例二
用户**当日**调用一句话识别服务215000次时，免费额度剩余5000次，所需支付的费用计算如下：
（215000 - 5000）/ 1000 × 1 = 672（美元）

#### 示例三
用户**当日**识别实时语音文件时长到达315小时，且免费额度剩余5小时，所需支付的费用计算如下：
（315 - 5）× 1.2 = 372（美元）


## 查看账单详情
登录 [腾讯云控制台-费用中心](https://console.cloud.tencent.com/expense/overview)，在左侧菜单栏选择【费用账单】>【账单详情】，进入账单详情页根据时间、产品以及计费模式等查看账单详情。
![](https://main.qcloudimg.com/raw/3335527afeef175d26087832f5bfdbd9.png)

