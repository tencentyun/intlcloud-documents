TencentDB for MySQL has released a new database proxy version. In order to support all the capabilities of the new version, new APIs are provided for replacing, upgrading, and configuring the database proxy as detailed below.

## Change time
Starting from Thursday, November 17, 2022.

## Replaced APIs

| Old API | New API | Description |
|---------|---------|---------|
| UpgradeCDBProxy | [AdjustCdbProxy](https://intl.cloud.tencent.com/document/product/236/45187) | Upgrades the configuration of the database proxy |
| ModifyCDBProxy | [AdjustCdbProxyAddress](https://intl.cloud.tencent.com/document/product/236/45194) | Configures the read/write separation of the database proxy |
