Izin tingkat sumber daya dapat digunakan untuk menentukan sumber daya mana yang dapat dimanipulasi oleh pengguna. TencentDB for Redis mendukung izin tingkat sumber daya tertentu. Artinya, untuk operasi TencentDB for Redis yang mendukung izin tingkat sumber daya, Anda dapat mengontrol waktu ketika pengguna diizinkan untuk melakukan operasi atau menggunakan sumber daya yang ditentukan. Tabel berikut menjelaskan jenis sumber daya yang dapat diotorisasi di CAM.

| Jenis Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| ---------------------------- | ------------------------------------------------------------ |
| [Instans TencentDB for Redis](#xiangguan) | `qcs::redis:$region::instance/*`<br>`qcs::redis:$region:$account:instance/$instance` |

Tabel di bawah mencantumkan operasi API TencentDB for Redis yang saat ini mendukung kontrol izin tingkat sumber daya, serta sumber daya yang didukung setiap operasi. Anda dapat menggunakan karakter pengganti `*` di jalur sumber daya saat mendefinisikannya.

<span id="xiangguan"></span>
### [Daftar API yang mendukung otorisasi tingkat sumber daya](id:xiangguan)

| Operasi API | Jalur Sumber Daya |
| ---------------------------------------- | ------------------------------------------------------------ |
| AssignProject                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| AssociateSecurityGroups                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| AutoRenew                                | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| BackupInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CleanInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CleanUpInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ClearInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ClearRedis                               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstanceHour                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateInstances                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| CreateRedis                              | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DeleteInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DeleteInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeAutoBackupConfig                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeBackupUrl                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeDBSecurityGroupsDetail           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceAccount                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceBackups                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceDealDetail               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceParamRecords             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceParams                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSecurityGroup            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSecurityGroupsAssociated | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceShards                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstanceSlowlog                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeInstances                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeProjectSecurityGroup             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedis                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisDealDetail                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisProduct                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisProductList                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisRegions                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeRedisZones                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeSlowLog                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTaskInfo                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTaskList                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeTasks                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DescribeVPCRedis                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DestroyPostpaidInstance                  | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DestroyPrepaidInstance                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| DisableReplicaReadonly                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| EnableReplicaReadonly                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ExportRedisBackup                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetBackupDownloadUrl                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisBackupList                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisPerformance                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisSlowLogList                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| GetRedisTaskList                         | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| InitRedisPassword                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| InquiryRedisPrice                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ManualBackupInstance                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModfiyInstancePassword                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModfiyRedisPassword                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyAutoBackupConfig                   | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyDBInstanceSecurityGroups           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstance                           | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceAccount                    | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceParams                     | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyInstanceSecurityGroup              | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyNetworkConfig                      | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisName                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisParams                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ModifyRedisProject                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RenewInstance                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RenewRedis                               | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ResetPassword                            | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| ResetRedisPassword                       | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| RestoreInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| SetRedisAutoRenew                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| StartupInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| SwitchInstanceVip                        | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UnAssociateSecurityGroups                | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeInstance                          | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeRedis                             | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |
| UpgradeRedisInquiryPrice                 | `qcs::redis:$region:$account:instance/*`    `qcs::redis:$region:$account:instance/$instance` |

### Daftar API yang tidak mendukung otorisasi tingkat sumber daya
Untuk operasi API TencentDB yang tidak mendukung otorisasi tingkat sumber daya, Anda masih dapat mengotorisasi pengguna untuk melakukannya, tetapi Anda harus menentukan `*` sebagai elemen sumber daya dalam pernyataan kebijakan.

| Operasi API | Deskripsi API |
| ----------------------------- | ---------------------------- |
| CreateInstances              | Membuat instans TencentDB for Redis |
| CreateParamTemplate           | Membuat templat parameter                 |
| DeleteParamTemplate           | Menghapus templat parameter           |
| DescribeInstanceDealDetail      | Informasi urutan kueri       |
| DescribeParamTemplateInfo                 | mendapatkan detail templat parameter     |
| DescribeParamTemplates         | Mendapatkan daftar templat parameter          |
| DescribeTaskInfo         | Mengkueri informasi tugas          |
| DescribeTasks         | Mengkueri daftar tugas          |
| ModifyParamTemplate           | Memodifikasi templat parameter                 |
| ListUsers             | Mengkueri nama sub-akun |
| ListCollaborators     |   Mengkueri nama akun kolaborator  |
| ListWeChatWorkSubAccounts  | Mengkueri nama pengguna WeChat   |
