TDSQL-C MySQL 版提供数据存储安全高保障。TDSQL-C MySQL 管理系统能够保证数据在存储过程中的机密性和完整性。

## 自动备份
TDSQL-C MySQL 版支持自动备份和手动备份来保障数据可恢复性，进而保证数据的完整性和可靠性。TDSQL-C MySQL 版默认提供数据备份和 binlog 备份功能，其中自动备份按照每日备份一次（默认在每日2:00至6:00间）的频率，您也可以根据业务需求，在控制台对备份开始的时间周期以及备份保留时间进行设置。若有其他备份需求，可通过控制台或 API 随时发起手动备份。

功能使用请参见 [自动备份数据](https://intl.cloud.tencent.com/document/product/1098/48399)。

## 定期备份保留
TDSQL-C MySQL 版支持设置备份开始的时间周期以及备份保留时间，可灵活配置备份文件的保留时间，保障您的数据安全，您可根据业务需求，缩短或延长备份保留的时间，默认保留时长为7天且最大可设置为1830天，超过备份保留时间的备份文件过期自动删除。

功能使用请参见 [设置备份保留时间](https://intl.cloud.tencent.com/document/product/1098/48396)。


## 数据安全
**敏感数据发现**功能可通过识别规则自动发现实例敏感数据，并对所发现的敏感数据实现自动化分类分级保护。支持多达20种内置的敏感数据识别规则，在满足合规性的基础上，能够对数据集的所有字段进行敏感属性识别，确保隐藏在大段文本中的敏感信息能够得到妥善处理。同时，产品还支持自定义敏感数据类型的自动发现，满足用户个性化的数据保护需求。

**数据脱敏**功能内置多种高级脱敏算法，可智能化执行与管理脱敏任务，针对不同业务场景实现数据脱敏，进而达到企业核心数据保密的效果。数据脱敏在确保安全性的同时，处理过的数据依然保持原始数据的分布特征、数据格式，使统计分析、测试、研发、培训等用途不受影响。
- 在合规性方面，数据脱敏能够通过匿名化技术，确保脱敏后数据无法被还原。保障企业个人信息使用时严格遵守相关法律法规，满足企业客户合规性需求。
- 在系统性能方面，数据脱敏在任务开始时拉取的是用户最新的实时备份数据，不需要源数据库停服，更不会给数据库性能带来额外的影响和开销，在用户无感知的情况下即可动态在线实时完成脱敏任务。

功能使用请参见 [数据脱敏](https://www.tencentcloud.com/document/product/1035/48605)。
