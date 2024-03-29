<div class="tab_list">
<ul>
    <li><a href="#A-E">A-E</a></li>
    <li><a href="#F-J">F-J</a></li>
    <li><a href="#K-O">K-O</a></li>
    <li><a href="#P-T">P-T</a></li>
    <li><a href="#U-Z">U-Z</a></li>
</ul>
</div>

<span id="A-E"></span>
## A-E 
### 备份保留期
自动备份的保留时间，超过保留期的备份将被自动删除。

### 备份存储
用于持久化保存数据库数据或日志等备份的底层存储资源。

<span id="F-J"></span>
## F-J 
### 高可用性
指系统无中断地执行其功能的能力，代表系统的可用性程度。

### 关系型数据库
按照关系型数据结构来联系和组织的数据库。关系型数据库模型是把复杂的数据结构归结为简单的二元关系（即二维表格形式）。在关系型数据库中，对数据的操作几乎全部建立在一个或多个关系表格上，通过对这些关联的表格分类、合并、连接或选取等运算来实现数据的管理。常用关系型数据库有：Oracle、MySQL、MariaDB、Microsoft SQL Server、Access、DB2、PostgreSQL、Informix、Sybase等。


### 故障切换
数据库实例在发生计划外的中断时，会自动切换到备实例，从而尽快恢复数据库操作而无需管理干预。完成故障转移所用的时间取决于在主数据库实例变为不可用时的数据库活动和其他条件。故障转移时间从秒级到分钟级不等。

<span id="K-O"></span>
## K-O 
### 每秒进行读写操作的次数
每秒完成的 I/O 操作数。该指标以给定时间间隔内 IOPS 平均值的形式进行报告。总 IOPS 是读取和写入 IOPS 的总和。IOPS 典型值在每秒零至数万之间。

<span id="P-T"></span>
## P-T 
### 热备份
系统处于正常运转状态下的备份。这种情况下，由于系统中的数据可能随时在更新，备份的数据相对于系统的真实数据可能有一定滞后。

### 实例 ID
每个数据库实例都有一个数据库实例 ID。在与控制台和 API 交互时，客户提供的名称可唯一标识数据库实例。对于某个地区中的客户而言，数据库实例 ID 必须具有唯一性。

### 实例规格
数据库实例的计算和内存容量由数据库实例规格决定。通过更改数据库实例规格，可以更改数据库实例的可用 CPU 和内存。

### 手动备份
是由用户启动的数据库实例的全量备份，备份文件会一直保存，直到用户手动删除。

### 数据复制
在主备高可用架构下，数据在主实例被提交后会从主实例复制到备实例，这个过程叫数据复制。数据复制方式通常分为强同步复制、半同步复制和异步复制。

### 数据库管理员
数据库管理员（DBA）是负责管理数据库的人，使用专门的软件存储和数据组织。该角色职责包括但不限于数据库的容量规划、安装、配置、数据库设计、迁移、性能监测、安全性、故障排除以及备份和数据恢复。

### 数据库连接数
连接到数据库实例的客户端会话数。

### 数据库迁移
随着业务的变化，数据库也需要随着应用业务从一个环境迁移到另一个环境，例如从本地数据中心迁移到云上，或者从某个云迁移到另一个云上。

### 数据库实例
数据库实例是在云中运行的独立数据库环境。一个数据库实例可以包含多个由数据库用户创建的数据库，并且可以使用与独立数据库实例相同的客户端工具和应用程序进行访问。

### 数据库实例生命周期
数据库实例生命周期是从数据库实例创建开始到最后释放。在数据库实例生命周期内，可以对数据库执行备份、还原、规格变更、存储扩容、重启、删除等操作。

### 数据库用户帐户
数据库用户帐户与客户云帐户不同，它仅在指定云数据库实例环境内使用，用来控制对客户的数据库实例的访问。数据库主用户帐户是本机数据库用户帐户，可用来连接数据库实例。创建数据库实例后，客户可以使用数据库用户帐户连接到数据库。之后，客户也可以创建其他数据库用户帐户，以满足帐户需求。

### 事务速率/数据库吞吐量
在特定时间间隔内完成的事务数量，通常用 TPM（每分钟事务数）或 TPS（每秒钟事务数）表示。事务速率的另一个常用术语是数据库吞吐量。数据库具有高事务速率，因此存在极少或根本没有磁盘吞吐量。

### 吞吐量/磁盘吞吐量
每秒传入或传出磁盘的字节数。该指标以给定时间间隔内吞吐量平均值的形式进行报告。每分钟分别报告一次读取和写入吞吐量，所用单位为每秒兆字节（MB/s）。吞吐量的典型值在零到 I/O 通道的最大带宽之间。

<span id="U-Z"></span>
## U-Z
### 网络流量
网络传输吞吐量，即每秒出入数据库实例的网络流量速率（以 MB 为单位）。

### 性能指标
反映数据库实例性能状况的指标，例如 CPU 使用率、内存使用率、存储空间使用率、网络流量、数据库连接数、事务速率/数据库吞吐量、提交延迟、存储延迟、存储 IOPS、存储吞吐量、存储队列深度等。

### 主数据库实例
在对外提供数据库服务的各节点中，提供读写服务的数据库实例。

### 自动备份
由系统自动创建数据库实例的全量备份。用户可以配置自动备份开始时间段和自动备份保留期。



