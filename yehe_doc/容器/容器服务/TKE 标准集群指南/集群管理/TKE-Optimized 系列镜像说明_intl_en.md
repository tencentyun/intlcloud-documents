


[Tencent Linux](https://intl.cloud.tencent.com/document/product/457/38854), a public image of Tencent Cloud that contains [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel) (a customized kernel maintained by the Tencent Cloud team), is available in TKE as a default image.

TKE-Optimized series images is once used for improving the stability of the image and providing more features, but it is not available for the clusters in TKE console after the Tencent Linux public image is launched.


<dx-alert infotype="notice" title="Note:">
- The clusters that are still using TKE-Optimized image are not affected and can continue to use it. But it is recommended that you switch to Tencent Linux 2.4. The new nodes in the cluster will use Tencent Linux 2.4 while the existing nodes are not affected and can continue to TKE-Optimized image.
- Centos7.6 TKE Optimized image is fully compatible with Tencent Linux 2.4 image.
- The user space tools of Ubuntu 18.04 TKE Optimized image are not fully compatible with Tencent Linux. If you have used these tools in your script, you need to modify the script after switching to Tencent Linux.
</dx-alert>


<style>
ul{
margin-bottom:0px !important;
}
</style>
