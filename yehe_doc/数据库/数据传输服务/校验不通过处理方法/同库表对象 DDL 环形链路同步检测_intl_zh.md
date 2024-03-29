## 检查详情 
在双向同步、多对一同步、多活等需要配置多个同步任务的场景中，DDL 的配置不能形成环形链路，否则可能造成 DDL 语句在系统中循环，进而引发错误。

示例：下图中蓝色线条1、3、5三个同步任务中，最多只能在两个同步任务中选择 DDL，如果选择三个就构成环形链路了。 

<img src="https://qcloudimg.tencent-cloud.cn/raw/f1e3638e92d99b6e51b61e0980e96a83.png" style="zoom:40%;" />

## 修复方法
修改同步任务配置，在**设置同步选项和同步对象** > **数据同步选项** > **同步操作类型**中，修改 DDL 参数配置，避免形成环形链路。

