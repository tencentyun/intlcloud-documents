## 数值函数
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>函数名称</b></td><td rowspan="1" colSpan="1" ><b>功能</b></td><td rowspan="1" colSpan="1" ><b>示例</b></td><td rowspan="1" colSpan="1" ><b>结果</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >abs</td><td rowspan="1" colSpan="1" >取绝对值</td><td rowspan="1" colSpan="1" >abs(-1024)</td><td rowspan="1" colSpan="1" >1024</td>
</tr><tr>
<td rowspan="1" colSpan="1" >ceil</td><td rowspan="1" colSpan="1" >向上取整</td><td rowspan="1" colSpan="1" >ceil(5.1)</td><td rowspan="1" colSpan="1" >6</td>
</tr><tr>
<td rowspan="1" colSpan="1" >floor</td><td rowspan="1" colSpan="1" >向下取整</td><td rowspan="1" colSpan="1" >floor(4.9)</td><td rowspan="1" colSpan="1" >4</td>
</tr><tr>
<td rowspan="1" colSpan="1" >log</td><td rowspan="1" colSpan="1" >计算对数</td><td rowspan="1" colSpan="1" >log(16, 2)</td><td rowspan="1" colSpan="1" >4</td>
</tr><tr>
<td rowspan="1" colSpan="1" >pow</td><td rowspan="1" colSpan="1" >计算指数幂</td><td rowspan="1" colSpan="1" >pow(3,2)</td><td rowspan="1" colSpan="1" >9</td>
</tr><tr>
<td rowspan="1" colSpan="1" >max</td><td rowspan="1" colSpan="1" >取最大值</td><td rowspan="1" colSpan="1" >max(12,54,3)</td><td rowspan="1" colSpan="1" >54</td>
</tr><tr>
<td rowspan="1" colSpan="1" >min</td><td rowspan="1" colSpan="1" >取最小值</td><td rowspan="1" colSpan="1" >min(12, 54, 3)</td><td rowspan="1" colSpan="1" >3</td>
</tr>
</table>


## 字符串函数
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>函数名称</b></td><td rowspan="1" colSpan="1" ><b>功能</b></td><td rowspan="1" colSpan="1" ><b>示例</b></td><td rowspan="1" colSpan="1" ><b>结果</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >chomp</td><td rowspan="1" colSpan="1" >删除字符串末尾换行符</td><td rowspan="1" colSpan="1" >chomp("hello\n")</td><td rowspan="1" colSpan="1" >"hello"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >format</td><td rowspan="1" colSpan="1" >格式化字符串</td><td rowspan="1" colSpan="1" >format("Hello, %s!", "Ander")</td><td rowspan="1" colSpan="1" >"Hello, Ander!"</td>
</tr><tr><td rowspan="1" colSpan="1" >lower</td><td rowspan="1" colSpan="1" >字符串转小写</td><td rowspan="1" colSpan="1" >lower("HELLO")</td><td rowspan="1" colSpan="1" >"hello"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >upper</td><td rowspan="1" colSpan="1" >字符串转大写</td><td rowspan="1" colSpan="1" >upper("hello")</td><td rowspan="1" colSpan="1" >"HELLO"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >join</td><td rowspan="1" colSpan="1" >将字符串列表使用指定分隔符拼接</td><td rowspan="1" colSpan="1" >join(", ", ["foo", "bar", "baz"])</td><td rowspan="1" colSpan="1" >"foo, bar, baz"</td>
</tr><tr>
<td rowspan="1" colSpan="1" >replace</td><td rowspan="1" colSpan="1" >替换字符串中的指定字符</td><td rowspan="1" colSpan="1" >replace("1 + 2 + 3", "+", "-")</td><td rowspan="1" colSpan="1" >"1 - 2 - 3"</td>
</tr>
</table>


更多函数信息请参见 [Terraform 官网](https://www.terraform.io/language/functions)。