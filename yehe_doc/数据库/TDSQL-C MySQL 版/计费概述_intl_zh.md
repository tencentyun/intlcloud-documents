TDSQL-C MySQL 版提供如下三种计费模式：

| 计费模式                             | 支持引擎          | 付费模式                       | 适用场景                              |
| -------------------------------- | ----------------- | -------------------------------- | --------------------------------------------- |
| 包年包月                                                     | MySQL | [预付费模式](https://intl.cloud.tencent.com/document/product/555/42701)，即在新建实例时支付费用。 | 适合业务量较稳定的长期需求，费用较按量计费模式更为低廉，且购买时长越长，折扣越多。 |
| 按量计费                                                     | MySQL | [后付费模式](https://intl.cloud.tencent.com/document/product/555/30328)，即先按需申请资源使用，在结算时会按您的实际资源使用量收取费用。 | 适合业务量有瞬间大幅波动的业务场景，用完可立即释放实例，节省成本。 |
| [Serverless](https://intl.cloud.tencent.com/document/product/1098/40618) | MySQL             | [后付费模式](https://intl.cloud.tencent.com/document/product/555/30328)，即计算先按需设置最大和最小算力范围，在结算时会按您的实际计算和存储资源使用量收取费用。 | 适合开发测试等低频和不确定负载的业务场景，按使用计费，不用不计费。<dx-alert infotype="explain" title="说明">Serverless 在初始化时会按照最小 CPU 进行启动，启动十分钟之后，如果没有请求才会进行降级，因此购买之后即使不使用也会有一个最小十分钟的计算节点计费。</dx-alert> |

## 计费说明
**包年包月/按量计费总费用 = 计算节点费用 + 存储空间费用 = 计算节点价格 × 计算节点数量 + 存储空间价格 × 存储空间**

**Serverless 总费用 = 计算节点费用 + 存储空间费用 = Serverless 算力价格 × CCU 量 + 存储空间价格 × 存储空间**

TDSQL-C MySQL 版采用计算和存储分离的架构，最小购买单位为集群，每个集群的计算节点和存储空间单独计费：

- 计算节点费用：根据用户所购买的规格按计费模式计费，支持包年包月和按量计费。
- 存储空间费用：根据用户所选择的计费模式计费，支持包年包月（即预购存储空间）和按量计费（按每小时存储实际使用计费）。
>?仅 TDSQL-C MySQL 版支持选择**预购存储空间**，且仅在 TDSQL-C MySQL 版选择包年包月计费模式后，存储才能选择**预购存储空间**包年包月计费模式。
>


## [产品规格](id:cpgg)

<table>
<thead><tr>
<th rowspan=2 >计算节点规格<br>（CPU 和内存）</th>
<th colspan = "2" style="text-align:center" width="50%">支持最大存储空间（GB)</th>
<th rowspan=2 >最大 IOPS</th>
<th rowspan=2 >I/O 带宽</th></tr>
<tr>
<th>MySQL 5.7内核小版本 &lt; 2.0.15<br>MySQL 8.0内核小版本 &lt; 3.1.2</th><th>MySQL 5.7内核小版本 ≥ 2.0.15<br>MySQL 8.0内核小版本 ≥ 3.1.2</th></tr>
</thead><tbody>
<tr>
<td>1核1GB</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>1核2GB</td>
<td>1000</td><td>3000</td><td>8000</td><td>1 Gbps</td></tr>
<tr>
<td>2核4GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2核8GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>2核16GB</td>
<td>5000</td><td>10000</td><td>48000</td><td>6 Gbps</td></tr>
<tr>
<td>4核8GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4核16GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4核24GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>4核32GB</td>
<td>10000</td><td>30000</td><td>96000</td><td>12 Gbps</td></tr>
<tr>
<td>8核16GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8核32GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8核48GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>8核64GB</td>
<td>10000</td><td>50000</td><td>216000</td><td>27 Gbps</td></tr>
<tr>
<td>12核48GB</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>12核72GB</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>12核96GB</td>
<td>10000</td><td>80000</td><td>288000</td><td>36 Gbps</td></tr>
<tr>
<td>16核64GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16核96GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>16核128GB</td>
<td>20000</td><td>100000</td><td>384000</td><td>48 Gbps</td></tr>
<tr>
<td>24核96GB</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>24核144GB</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>24核192GB</td>
<td>20000</td><td>150000</td><td>480000</td><td>60 Gbps</td></tr>
<tr>
<td>32核128GB</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>32核192GB</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>32核256GB</td>
<td>50000</td><td>200000</td><td>576000</td><td>72 Gbps</td></tr>
<tr>
<td>48核192GB</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48核288GB</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48核384GB</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>48核488GB</td>
<td>50000</td><td>300000</td><td>648000</td><td>81 Gbps</td></tr>
<tr>
<td>64核256GB</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>64核384GB</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>64核512GB</td>
<td>50000</td><td>400000</td><td>720000</td><td>90 Gbps</td></tr>
<tr>
<td>88核710GB</td>
<td>50000</td><td>400000</td><td>780000</td><td>98 Gbps</td></tr>
</tbody></table>		

## 计算节点价格
<table>
<thead><tr>
<th rowspan=2 >计算节点规格</th>
<th colspan=2>广州、上海、北京、南京</th><th colspan=2>中国香港</th><th colspan=2>硅谷、法兰克福</th><th colspan=2>新加坡</th><th colspan=2>东京</th></tr>
<tr>
<th>按量计费价格（美元/小时）</th><th>包年包月价格（美元/月）</th>
<th>按量计费价格（美元/小时）</th><th>包年包月价格（美元/月）</th>
<th>按量计费价格（美元/小时）</th><th>包年包月价格（美元/月）</th>
<th>按量计费价格（美元/小时）</th><th>包年包月价格（美元/月）</th>
<th>按量计费价格（美元/小时）</th><th>包年包月价格（美元/月）</th>
</tr></thead>
<tbody><tr>
<td>1核1GB</td>
<td>0.04</td><td>8.82</td><td>0.07</td><td>31.32</td><td>0.07</td><td>32.74</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>1核2GB</td>
<td>0.05</td><td>13.24</td><td>0.08</td><td>40.15</td><td>0.09</td><td>42</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>2核4GB</td>
<td>0.1</td><td>48</td><td>0.17</td><td>80.29</td><td>0.17</td><td>84</td><td>0.17</td><td>83.21</td><td>0.13</td><td>62.4</td></tr>
<tr>
<td>2核8GB</td>
<td>0.14</td><td>69.18</td><td>0.24</td><td>115.59</td><td>0.25</td><td>121.06</td><td>0.25</td><td>120.26</td><td>0.19</td><td>89.93</td></tr>
<tr>
<td>2核16GB</td>
<td>0.23</td><td>111.53</td><td>0.39</td><td>186.18</td><td>0.41</td><td>195.18</td><td>0.4</td><td>194.38</td><td>0.3</td><td>144.99</td></tr>
<tr>
<td>4核8GB</td>
<td>0.2</td><td>96</td><td>0.33</td><td>160.59</td><td>0.35</td><td>168</td><td>0.35</td><td>166.41</td><td>0.26</td><td>124.8</td></tr>
<tr>
<td>4核16GB</td>
<td>0.29</td><td>138.35</td><td>0.48</td><td>231.18</td><td>0.5</td><td>242.12</td><td>0.5</td><td>240.53</td><td>0.37</td><td>179.86</td></tr>
<tr>
<td>4核24GB</td>
<td>0.38</td><td>180.71</td><td>0.63</td><td>301.76</td><td>0.66</td><td>316.24</td><td>0.66</td><td>314.65</td><td>0.49</td><td>234.92</td></tr>
<tr>
<td>4核32GB</td>
<td>0.46</td><td>223.06</td><td>0.78</td><td>372.35</td><td>0.81</td><td>390.35</td><td>0.81</td><td>388.76</td><td>0.6</td><td>289.98</td></tr>
<tr>
<td>8核16GB</td>
<td>0.4</td><td>192</td><td>0.67</td><td>321.18</td><td>0.7</td><td>336</td><td>0.69</td><td>332.82</td><td>0.52</td><td>249.6</td></tr>
<tr>
<td>8核32GB</td>
<td>0.58</td><td>276.71</td><td>0.96</td><td>462.35</td><td>1.01</td><td>484.24</td><td>1</td><td>481.06</td><td>0.75</td><td>359.72</td></tr>
<tr>
<td>8核48GB</td>
<td>0.75</td><td>361.41</td><td>1.26</td><td>603.53</td><td>1.32</td><td>632.47</td><td>1.31</td><td>629.29</td><td>0.98</td><td>469.84</td></tr>
<tr>
<td>8核64GB</td>
<td>0.93</td><td>446.12</td><td>1.55</td><td>744.71</td><td>1.63</td><td>780.71</td><td>1.62</td><td>777.53</td><td>1.21</td><td>579.95</td></tr>
<tr>
<td>12核48GB</td>
<td>0.86</td><td>415.06</td><td>1.45</td><td>693.53</td><td>1.51</td><td>726.35</td><td>1.5</td><td>721.59</td><td>1.12</td><td>539.58</td></tr>
<tr>
<td>12核72GB</td>
<td>1.13</td><td>542.12</td><td>1.89</td><td>905.29</td><td>1.98</td><td>948.71</td><td>1.97</td><td>943.94</td><td>1.47</td><td>704.75</td></tr>
<tr>
<td>12核96GB</td>
<td>1.39</td><td>669.18</td><td>2.33</td><td>1117.06</td><td>2.44</td><td>1171.06</td><td>2.43</td><td>1166.29</td><td>1.81</td><td>869.93</td></tr>
<tr>
<td>16核64GB</td>
<td>1.15</td><td>553.41</td><td>1.93</td><td>924.71</td><td>2.02</td><td>968.47</td><td>2</td><td>962.12</td><td>1.5</td><td>719.44</td></tr>
<tr>
<td>16核96GB</td>
<td>1.5</td><td>722.82</td><td>2.52</td><td>1207.06</td><td>2.63</td><td>1264.94</td><td>2.62</td><td>1258.59</td><td>1.96</td><td>939.67</td></tr>
<tr>
<td>16核128GB</td>
<td>1.86</td><td>892.24</td><td>3.1</td><td>1489.41</td><td>3.25</td><td>1561.41</td><td>3.24</td><td>1555.06</td><td>2.42</td><td>1159.91</td></tr>
<tr>
<td>24核96GB</td>
<td>1.73</td><td>830.12</td><td>2.89</td><td>1387.06</td><td>3.03</td><td>1452.71</td><td>3.01</td><td>1443.18</td><td>2.25</td><td>1079.15</td></tr>
<tr>
<td>24核144GB</td>
<td>2.26</td><td>1084.24</td><td>3.77</td><td>1810.59</td><td>3.95</td><td>1897.41</td><td>3.93</td><td>1887.88</td><td>2.94</td><td>1409.51</td></tr>
<tr>
<td>24核192GB</td>
<td>2.79</td><td>1338.35</td><td>4.66</td><td>2234.12</td><td>4.88</td><td>2342.12</td><td>4.86</td><td>2332.59</td><td>3.62</td><td>1739.86</td></tr>
<tr>
<td>32核128GB</td>
<td>2.3</td><td>1106.82</td><td>3.85</td><td>1849.41</td><td>4.03</td><td>1936.94</td><td>4.01</td><td>1924.24</td><td>3</td><td>1438.87</td></tr>
<tr>
<td>32核192GB</td>
<td>3.01</td><td>1445.65</td><td>5.03</td><td>2414.12</td><td>5.27</td><td>2529.88</td><td>5.24</td><td>2517.18</td><td>3.91</td><td>1879.34</td></tr>
<tr>
<td>32核256GB</td>
<td>3.71</td><td>1784.47</td><td>6.21</td><td>2978.82</td><td>-</td><td>-</td><td>6.48</td><td>3110.12</td><td>4.83</td><td>2319.81</td></tr>
<tr>
<td>48核192GB</td>
<td>3.46</td><td>1660.24</td><td>5.78</td><td>2774.12</td><td>6.05</td><td>2905.41</td><td>6.01</td><td>2886.35</td><td>4.49</td><td>2158.31</td></tr>
<tr>
<td>48核288GB</td>
<td>4.51</td><td>2168.47</td><td>7.55</td><td>3621.18</td><td>-</td><td>21235.20</td><td>7.86</td><td>3775.76</td><td>5.87</td><td>2819.01</td></tr>
<tr>
<td>48核384GB</td>
<td>5.57</td><td>2676.71</td><td>9.31</td><td>4468.24</td><td>-</td><td>-</td><td>9.72</td><td>4665.18</td><td>7.25</td><td>3479.72</td></tr>
<tr>
<td>48核488GB</td>
<td>6.72</td><td>3227.29</td><td>11.23</td><td>5385.88</td><td>-</td><td>-</td><td>11.72</td><td>5628.71</td><td>8.74</td><td>4195.48</td></tr>
<tr>
<td>64核256GB</td>
<td>4.61</td><td>2213.65</td><td>7.71</td><td>3698.82</td><td>-</td><td>-</td><td>8.02</td><td>3848.47</td><td>5.99</td><td>2877.74</td></tr>
<tr>
<td>64核384GB</td>
<td>6.02</td><td>2891.29</td><td>10.06</td><td>4828.24</td><td>-</td><td>-</td><td>10.49</td><td>5034.35</td><td>7.83</td><td>3758.68</td></tr>
<tr>
<td>88核710GB</td>
<td>10.28</td><td>4939.06</td><td>-</td><td>-</td><td>-</td><td>-</td><td>17.93</td><td>8608.41</td><td>-</td><td>-</td></tr>
</tbody></table>

## Serverless 算力价格
<table>
<thead><tr>
<th rowspan=2 >计费单元</th>
<th >广州、上海、北京、南京</th>
<tr>
<th>CCU 按使用计费价格（美元/个/秒）</th></tr></thead>
<tbody><tr>
<td>Serverless 实例</td>
<td>0.00001397</td></tr>
</tbody></table>

>?
>- CCU（CynosDB Compute Unit）为 Serverless 的计算计费单位，一个 CCU 近似等于1个 CPU 和 2GB 内存的计算资源，每个计费周期的 CCU 使用数量为：`数据库所使用的 CPU 核数` 与 `内存大小的1/2` 二者中取最大值。
>- 您可参考 [产品规格](#cpgg) 选择相应的 CCU 最大最小值，存储空间上限与最大值相对应的 [普通计算节点规格](#cpgg) 的最大存储空间一致。

## 存储空间价格
<table>
<thead><tr>
<th colspan=2>广州、上海、北京、南京</th><th colspan=2>中国香港、中国台北、新加坡、硅谷、法兰克福、东京、弗吉尼亚</th></tr>
<tr>
<th>按量计费价格（美元/GB/小时）</th><th>包年包月价格（美元/GB/月）</th>
<th>按量计费价格（美元/GB/小时）</th><th>包年包月价格（美元/GB/月）</th>
</tr></thead>
<tbody><tr>
<td>0.00072</td><td><li>0 - 3000GB（不含3000GB）：0.20541177<br><li>3000GB及以上：0.18829412</td>
<td>0.000792</td><td><li>0 - 3000GB（不含3000GB）：0.22447059<br><li>3000GB及以上：0.20576471</td></tr>
</tbody></table>

## 费用计算示例
>?示例中的节点以及存储价格仅作参考，具体价格请您以实际购买页对应配置为准。
#### 包年包月
用户在北京三区，购买一个规格为1核2GB、实例数为1的 TDSQL-C MySQL 版集群，期间一直使用了10GB的存储空间，购买时长为1个月。

当月的计算节点费用 = 13.24美元 
当月的存储空间费用 = 0.20541177美元/GB/月 × 10GB = 2.0541177美元
当月的总费用 = 计算节点费用 + 存储空间费用 = 13.24美元 + 2.0541177美元 = 15.2947117美元

#### 按量计费
用户在北京三区，购买一个规格为1核2GB、实例数为1的 TDSQL-C MySQL 版集群，期间一直使用了10GB的存储空间。

每天的计算节点费用 = 0.05美元/小时 × 24小时 = 1.2美元
每天的存储空间费用 = 0.00072美元/GB/小时 × 10GB × 24小时 = 0.1728美元
每天的总费用 = 计算节点费用 + 存储空间费用 = 1.2美元 + 0.1728美元 = 1.3728美元

#### Serverless 计费
用户在北京三区，购买一个计算规格为最小0.25CCU/s、最大2CCU/s的 Serverless 数据库，一天中一直使用了10GB的存储空间，及一天中使用了1个小时的 Serverless，该小时内 CCU 平均用量为1.5CCU/s。

每天的计算节点费用 = 1.5个 x 3600秒 x 0.00001397美元/个/秒 = 0.075438美元
每天的存储空间费用 = 0.00072美元/GB/小时 × 10GB × 24小时 = 0.1728美元
每天的总费用 = 计算节点费用 + 存储空间费用 = 0.075438美元 + 0.1728美元 =0.248238美元

