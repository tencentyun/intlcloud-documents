
### 源/目标实例发生 HA（High Availability）切换时，同步服务是否会受影响？
- 源实例支持并开启 GTID（Global Transaction Identifier）时，在增量同步阶段，如果源实例发生 HA，那么服务会自动重连，同步数据流在 HA 完成后迅速恢复
- 目标实例在增量同步阶段发生目标实例 HA，服务也会自动重连，同步数据流在 HA 完成后迅速恢复。

### 支持将高版本实例的数据同步到低版本的实例吗？
不支持。同一个类型的数据库，目标实例的大版本必须不小于源实例。以 MySQL 实例为例，不支持 MySQL 5.7 的实例同步到 MySQL 5.6。

### 源/目标能否为云下实例？
可以。可以将云上的数据库同步到云下，接入方式支持公网、云联网等。

### 在双向同步拓扑中，是否可以对 DDL 进行双向同步？
不可以。创建同步实例时，只能允许其中一个实例进行 DDL 同步，否则检测算法检测到 DDL 循环，会禁止其中一个实例的创建。

### 是否支持非事务引擎？
当前技术方案采用在事务中打上路由信息来标记事务的来源，依赖于事务的原子性。基于非事务引擎的库表，会破坏了事务的原子性，无法保证数据一致，不建议用户使用。
