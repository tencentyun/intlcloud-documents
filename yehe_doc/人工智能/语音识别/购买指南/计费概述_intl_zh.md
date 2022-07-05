腾讯云语音识别 ASR 提供后付费计费模式，开通服务后默认使用后付费的计费模式。

## 产品价格
### 后付费
所有语音识别服务开通后即默认采用后付费的方式。
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
## 计费与结算方式

### 后付费
每月接口调用总量达到某个阶梯后，所有调用量按该阶梯的单价进行计费，阶梯越高，单价越低。使用实时语音识别，每日会对上一日用量输出账单并扣费。

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
      <td align="center"> 实时语音识别</td> 
     </tr>
  <tr>
      <td align="center">适用场景</td>   
      <td align="center">适用于使用量有较大波动性，或无法预估的业务</td> 
      </tr>   
</table>




## 费用计算示例
### 后付费

#### 示例一
用户**当日**识别实时语音文件时长到达315小时，所需支付的费用计算如下：
315 × 1.2 = 378（美元）



