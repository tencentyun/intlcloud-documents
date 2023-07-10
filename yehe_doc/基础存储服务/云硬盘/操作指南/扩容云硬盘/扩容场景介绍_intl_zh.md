
## 扩容类型为系统盘的云硬盘
当扩容类型为系统盘的云硬盘时，您可 [通过云服务器控制台扩容](https://intl.cloud.tencent.com/document/product/362/5747)。


## 扩容类型为数据盘的云硬盘

当扩容类型为数据盘的云硬盘时，您可通过以下3种方式进行扩容。
- [通过云服务器控制台扩容](https://intl.cloud.tencent.com/document/product/362/5747)
- [通过云硬盘控制台扩容](https://intl.cloud.tencent.com/document/product/362/5747)
- [通过 API 扩容](https://intl.cloud.tencent.com/document/product/362/5747)




根据 CBS 数据盘“可卸载”属性的不同，您可选择不同的操作入口对数据盘进行扩容。
- 若当前硬盘为“可卸载”的 CBS 数据盘，您可经由云硬盘控制台或使用 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/16310) 进行扩容操作。
- 若当前硬盘为“不可卸载”的 CBS 数据盘，您可经由云服务器实例控制台或使用 [扩容云硬盘](https://intl.cloud.tencent.com/document/product/362/16310) 进行扩容操作。



<dx-alert infotype="notice" title="">
如果云硬盘的最大容量仍无法满足您的业务需求，您可以使用 [多块弹性云硬盘构建 RAID 组](https://intl.cloud.tencent.com/document/product/362/2932) 或 [多块弹性云硬盘构建 LVM 逻辑卷](https://intl.cloud.tencent.com/document/product/362/2933)。
</dx-alert>


数据盘扩容完成后，需要进行相关后续操作才能为实例识别并使用：
<table>
     <tr>
         <th nowrap="nowrap">扩容前</th>  
         <th nowrap="nowrap">扩容后</th>  
		 <th>后续操作</th>  
     </tr>
	 <tr>
         <td   rowspan="2" nowrap="nowrap">未创建文件系统</td>
         <td>磁盘容量小于2TB</td>
		 <td><a href="https://intl.cloud.tencent.com/document/product/362/31597">初始化云硬盘（小于2TB）</a></td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">磁盘容量大于等于2TB</td>
         <td><a href="https://intl.cloud.tencent.com/document/product/362/31598">初始化云硬盘（大于等于2TB）</a></td>
     </tr>
	 <tr>
         <td   rowspan="2">已创建文件系统</td>
         <td>磁盘容量小于2TB</td>
    		 <td><ul><li>扩容的是 Windows 云服务器的云硬盘：<a href="https://intl.cloud.tencent.com/document/product/362/31601">扩展分区及文件系统（Windows）</a></li>
			 <li>扩容的是 Linux 云服务器的云硬盘：<a href="https://intl.cloud.tencent.com/document/product/362/39995">扩展分区及文件系统（Linux）</a></li></ul>
				 </td>
     </tr>
	 <tr>
         <td>磁盘容量大于等于2TB</td>
         <td>
				 <ul><li>采用 GPT 分区格式： <a href="https://intl.cloud.tencent.com/document/product/362/31601">扩展分区及文件系统（Windows）</a>或 <a href="https://intl.cloud.tencent.com/document/product/362/39995">扩展分区及文件系统（Linux）</a>。</li>
				 <li>采用 MBR 分区格式：不支持。</li>MBR 格式分区支持的磁盘最大容量为2TB。如果您的硬盘分区为 MBR 格式，且需要扩容到超过2TB时，建议您重新创建并挂载一块新的数据盘，然后使用 GPT 分区方式后将数据拷贝至新盘中。</ul>
				 </td>
     </tr>
</table>

## 费用说明
扩容云硬盘将会收取扩容容量的费用，针对不同计费方式的云硬盘：
- **包年包月云硬盘**：扩容容量按照生命周期的剩余时间补齐新配置与旧配置的差价。具体情况以实际情况为准，您可以在付款页面查看。
- **按量计费云硬盘**：立即生效，并开始按新配置的价格进行计费。
- 包年包月云硬盘具体费用规则：
 - 遵循按天补差价，升配费用 = 按月升配差价 × 升配月数 × 适用折扣。
 - 按月升配差价：新老配置原价按月的单价。
 - 升配月数：升配的费用按天折算到月
 - 升配天数 = 资源到期时间 - 当前时间
 - 升配月数 = 升配天数 /（365/12）
 - 适用折扣：根据升配月数匹配官网适用折扣，其中折扣为官网生效的折扣。
<dx-alert infotype="explain" title="">
- 本操作不影响资源到期时间。
- 本操作可以使用代金券和平台赠送余额（赠送金）抵扣费用。
</dx-alert>

