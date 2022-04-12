Izin tingkat sumber daya dapat digunakan untuk menentukan sumber daya mana yang dapat dimanipulasi oleh pengguna. TencentDB mendukung izin tingkat sumber daya tertentu. Artinya, untuk operasi TencentDB yang mendukung izin tingkat sumber daya, Anda dapat mengontrol waktu ketika pengguna diizinkan untuk melakukan operasi atau menggunakan sumber daya yang ditentukan. Tabel berikut menjelaskan jenis sumber daya yang dapat diotorisasi di CAM.

| Jenis Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :-------- |:-------------- |
| Terkait instans TencentDB |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`

Tabel di bawah mencantumkan operasi API TencentDB yang saat ini mendukung kontrol izin tingkat sumber daya serta sumber daya dan kunci kondisi yang didukung oleh setiap operasi. Saat menentukan jalur sumber daya, Anda dapat menggunakan karakter pengganti "*" di jalur tersebut.

### Daftar API yang mendukung otorisasi di tingkat sumber daya
| Operasi API | Jalur Sumber Daya |
|:---------|:-------------|
|AddTimeWindow| `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|AssociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|CloseWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|CreateAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|CreateBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|CreateDBImportJob|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DeleteAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DeleteBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DeleteTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBackupDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBackupDownloadDbTableCode|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBackups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBackupTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeBinlogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBImportRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBInstanceCharset|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBInstanceConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBInstanceRebootTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBSwitchRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeDBSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeInstanceParamRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeInstanceParams|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeRoGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeRollbackRangeTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeSlowLogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeSupportedPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DescribeTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabasesForInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeMonitorData |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTableColumns |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DropDatabaseTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|InitDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|IsolateDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyAccountDescription|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyAccountPassword|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyAutoRenewFlag|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyBackupInfo|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyDBInstanceName|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyDBInstanceProject|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyDBInstanceSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyDBInstanceVipVport|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyInstanceParam|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyDBInstanceModes|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ModifyTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyProtectMode |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OfflineDBInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|OpenDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|OpenWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|ReleaseIsolatedDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|RestartDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|StartBatchRollback|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|SubmitBatchOperation|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|SwitchDrInstanceToMaster|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|SwitchForUpgrade|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|DisassociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|UpgradeDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
|UpgradeDBInstanceEngineVersion|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 

### Daftar API yang tidak mendukung otorisasi di tingkat sumber daya
 Untuk operasi API TencentDB yang tidak mendukung otorisasi pada tingkat sumber daya, Anda masih dapat mengotorisasi pengguna untuk melakukannya, tetapi Anda harus menentukan `*` sebagai elemen sumber daya dalam pernyataan kebijakan.

| Operasi API | Deskripsi API |
| ----------------------------- | ---------------------------- |
| CreateDBInstanceHour          | Membuat instans TencentDB bayar sesuai pemakaian |
| CreateParamTemplate           | Membuat templat parameter               |
| DeleteParamTemplate           | Menghapus item templat pemantauan           |
| DescribeProjectSecurityGroups | Mengkueri informasi grup keamanan proyek            |
| DescribeDefaultParams         | Mengkueri daftar parameter default yang dapat dikonfigurasi     |
| DescribeParamTemplateInfo     | Mengkueri detail templat parameter             |
| DescribeParamTemplates        | Mengkueri daftar templat parameter             |
| DescribeAsyncRequestInfo      | Mengkueri hasil eksekusi tugas asinkron       |
| DescribeTasks                 | Mengkueri daftar tugas untuk instans TencentDB     |
| DescribeUploadedFiles         | Mengkueri daftar file SQL yang diimpor          |
| ModifyParamTemplate           | Memodifikasi templat parameter                 |
| RenewDBInstance               | Memperpanjang instans TencentDB             |
| StopDBImportJob               | Menghentikan tugas impor data             |
| DescribleRoMinScale | Mengkueri spesifikasi minimum instans baca saja |
| DescribeRequestResult           | Mengkueri detail tugas       |
| DescribeRoMinScale           | Mengkueri spesifikasi minimum instans baca saja yang dapat dibeli atau ditingkatkan          |
