Izin tingkat sumber daya dapat digunakan untuk menentukan sumber daya mana yang dapat dimanipulasi oleh pengguna. TencentDB for SQL Server mendukung izin tingkat sumber daya tertentu. Artinya, untuk operasi TencentDB for SQL Server yang mendukung izin tingkat sumber daya, Anda dapat mengontrol waktu ketika pengguna diizinkan untuk melakukan operasi atau menggunakan sumber daya yang ditentukan. Tabel berikut menjelaskan jenis sumber daya yang dapat diotorisasi di CAM.

| Jenis Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :--------------- | :----------------------------------------------------------- |
| Sumber daya terkait instans TencentDB | `qcs::sqlserver:$region:$account:instance/*`<br>`qcs::sqlserver:$region:$account:instance/$instanceId` |

TencentDB for SQL Server mendukung otorisasi tingkat sumber daya. Anda dapat mengizinkan sub-akun memiliki izin API untuk sumber daya tertentu. Tabel di bawah mencantumkan operasi API TencentDB yang saat ini mendukung kontrol izin tingkat sumber daya serta sumber daya dan kunci kondisi yang didukung oleh setiap operasi. Saat menentukan jalur sumber daya, Anda dapat menggunakan karakter pengganti "*" di jalur tersebut.

>?Setiap API TencentDB yang tidak tercantum dalam tabel tidak mendukung izin tingkat sumber daya. Untuk melakukan operasi ini, Anda masih dapat mengotorisasi pengguna untuk melakukannya, tetapi Anda harus menetapkan `*` sebagai elemen sumber daya dalam pernyataan kebijakan.

| Nama API | Deskripsi | Contoh Sumber Daya Enam Segmen |
| :---------------------------- | :--------------- |  :----------------------------------------------------------- |
| CreateAccount                 | Membuat akun         | ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| CreateBackup                  | Membuat pencadangan         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| CreateDB                      | Membuat database       |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DeleteAccount                 | Menghapus akun         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DeleteDB                      | Meletakkan database       |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeAccounts              | Mengkueri daftar akun     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeBackups               | Mengkueri daftar pencadangan     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDatabaseNames         | Mengkueri nama database   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDBInstances           | Mengkueri daftar instans     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDBs                   | Mengkueri daftar database   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeInstanceTasks         | Mengkueri tugas instans     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeRollbackTime          | Mengkueri rentang waktu yang tersedia untuk pengembalian   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeSlowlogs              | Mengkueri daftar log lambat   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| InquiryPriceRenewDBInstance   | Mengkueri harga perpanjangan instans |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| InquiryPriceUpgradeDBInstance | Mengkueri harga peningkatan instans |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyAccountPrivilege        | Memodifikasi izin akun     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyAccountRemark           | Memodifikasi keterangan akun     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyBackupStrategy          | Memodifikasi waktu untuk pencadangan dingin     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDatabasePrivilege       | Memodifikasi izin database  |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBInstanceName          | Mengganti nama instans     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBInstanceProject       | Memodifikasi proyek instans     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBName                  | Mengganti nama database   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBRemark                | Memodifikasi keterangan database   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RenewDBInstance               | Memperpanjang instans        |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ResetAccountPassword          | Mengatur ulang kata sandi akun     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RestartDBInstance             | Memulai ulang instans         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RestoreInstance               | Memulihkan instans pencadangan dingin     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RollbackInstance              | Mengembalikan instans         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| TerminateDBInstance           | Menghentikan instans         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| UpgradeDBInstance             | Meningkatkan instans         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
