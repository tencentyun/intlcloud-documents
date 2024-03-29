## 任务式建模简介

任务式建模提供通过向导式的训练任务提交方式进行模型构建，支持基于多种算法来源进行训练任务提交，可直接通过代码包绑定主流训练框架启动训练任务，快速使用主流高性能及分布式训练框架提交训练任务。下面将由一个简单的PyTorch MPIJob 演示如何使用任务式建模快速创建任务
## 数据准备
### 数据集
本案例使用 mnist 数据集，下载地址为[数据集](https://tencent-cloud-product-release-1258877907.cos.ap-guangzhou.myqcloud.com/TI-ONE-release/TIONE%E5%85%AC%E6%9C%89%E4%BA%91%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8-%E5%8B%BF%E5%88%A0/ti-images.zip)
### 代码包
本案例的训练脚本是使用 PyTorch 框架撰写的，代码包下载地址为[代码包](https://tencent-cloud-product-release-1258877907.cos.ap-guangzhou.myqcloud.com/TI-ONE-release/TIONE%E5%85%AC%E6%9C%89%E4%BA%91%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8-%E5%8B%BF%E5%88%A0/mnist.pytorch.zip)
## 操作步骤
### 新建任务第一步
1. 进入【训练工坊】-【任务式建模】，单击【新建】，开始进入向导式训练任务创建。

![](https://qcloudimg.tencent-cloud.cn/raw/194bb4af4e6b76d69bd090f4905d7298.png)

1. 在基本信息页，填写如下信息：

   - 任务名称：mnist_train
   - 训练框架选择：内置框架 / PyTorch / 1.9-py3.6-cuda11.1-gpu
   - 训练模式：MPI
   - 计费模式：后付费
   - 算力规格：8C40G V100*1
   - 节点数量：1个
   - 标签和描述：无需填写

   填写完毕后点击下一步，开始填写任务配置页

![](https://qcloudimg.tencent-cloud.cn/raw/f40bdb4a0dfeffd009b711fea19f1521.png)

### 新建任务第二步

在任务配置页，填写如下信息：

1. 算法来源：

   - 代码包：点击【选择文件】，在弹出的 COS 对话框中，选择需要使用的存储桶，点击左下方【上传文件夹】将准备好的代码包（需要先解压）文件夹mnist.pytorch上传至COS存储桶中，并选定代码包所在路径
   - 启动命令：填写 sh start.sh

![](https://qcloudimg.tencent-cloud.cn/raw/20d6f01ce319820ef8ac8fc27a0a909a.png)

2. 数据来源：选择 COS 数据

   - 映射路径：填写 train
   - 数据所在路径：点击【选择文件】，在弹出的COS对话框中，选择需要使用的存储桶，点击左下方【上传文件夹】，将数据集解压后的文件夹ti-images上传，上传完成后选中文件夹路径，如图所示

![](https://qcloudimg.tencent-cloud.cn/raw/bf2e6ae479fe3c05384418259965ffa2.png)

![](https://qcloudimg.tencent-cloud.cn/raw/b9cd316c7b34404b575134b79c37c5c9.png)

3. 调优参数：无

4. 训练输出：点击【选择文件】，在弹出的COS对话框中，选择需要使用的存储桶，选择训练输出数据需要保存的路径，如图所示

![](https://qcloudimg.tencent-cloud.cn/raw/9e372ceee98928936105a675b265ab4a.png)

1. CLS日志：选择不投递
2. VPC：选择不使用

配置完成后，可在页面底部查看本次训练任务的每小时收费价格，点击确定，即完成任务提交。

![](https://qcloudimg.tencent-cloud.cn/raw/4da928c725228a855418f3f20e9b8a49.png)