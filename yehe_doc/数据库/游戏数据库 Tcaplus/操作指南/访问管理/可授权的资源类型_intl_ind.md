## Ringkasan Izin Tingkat Sumber Daya
Izin tingkat sumber daya dapat digunakan untuk menentukan sumber daya mana yang dapat dimanipulasi oleh pengguna. TcaplusDB mendukung izin tingkat sumber daya tertentu, yaitu, memungkinkan pengguna melakukan operasi atau menggunakan sumber daya tertentu.

Di Cloud Access Management (CAM), jenis sumber daya TcaplusDB yang dapat diizinkan adalah sebagai berikut:

| Jenis Sumber Daya                         | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi                                     |
| :------------------------------- | ------------------------------------------------------------ |
| [Cluster](#tcaplusdbCorrelation)    | ` qcs::tcaplusdb:$region:$account:cluster/$clusterId `       |
| [Table group](#tablegroupCorrelation) | `qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [Table](#tableCorrelation)        | `qcs::tcaplusdb:$region:$account:table/$tableId`             |

Bagian [TcaplusDB cluster API](#tcaplusdbCorrelation), [TcaplusDB table group API](#tablegroupCorrelation), dan [TcaplusDB table APIs](#tableCorrelation) di bawah menjelaskan operasi TcaplusDB API yang saat ini mendukung kontrol izin tingkat sumber daya serta sumber daya dan kunci kondisi yang didukung oleh setiap operasi. Saat mengatur jalur sumber daya, Anda perlu mengganti parameter variabel seperti `$region` dan `$account` dengan informasi parameter asli Anda. Anda juga dapat menggunakan karakter pengganti `\*` di jalur. Untuk contoh operasi terkait, silakan lihat [Contoh Kontrol Akses TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35752).

> Untuk operasi API TcaplusDB yang tidak mendukung otorisasi pada tingkat sumber daya, Anda masih dapat mengotorisasi pengguna untuk melakukannya, tetapi Anda harus menentukan `\*` sebagai elemen sumber daya dalam pernyataan kebijakan.

## Daftar API yang Tidak Mendukung Izin Tingkat Sumber Daya

| Operasi API               | Deskripsi API                  |
| :--------------------- | :----------------------- |
| CreateBackup           | Membuat cadangan                 |
| CompareIdlFiles        | Mengunggah dan memverifikasi file modifikasi tabel       |
| VerifyIdlFiles         | Mengunggah dan memverifikasi file pembuatan tabel   |
| DescribeUinInWhitelist | Membuat kueri terkait apakah pengguna saat ini ada dalam daftar yang diizinkan |
| DescribeRegions        | Membuat kueri terkait daftar wilayah             |
| DeleteIdlFiles         | Menghapus file deskripsi IDL          |
|DescribeIdlFileInfos   | Membuat kueri terkait detail file deskripsi tabel       |
| DescribeIdlFileInfos          | Membuat kueri terkait daftar tugas             |

## Daftar API yang Mendukung Izin Tingkat Sumber Daya

<span id="tcaplusdbCorrelation"></span>
### API kluster TcaplusDB

| Operasi API                                                     | Jalur Sumber Daya                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateCluster](https://intl.cloud.tencent.com/document/product/1016/35053) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterName](https://intl.cloud.tencent.com/document/product/1016/35049) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DeleteCluster](https://intl.cloud.tencent.com/document/product/1016/35052) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DescribeClusters](https://intl.cloud.tencent.com/document/product/1016/35050) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterPassword](https://intl.cloud.tencent.com/document/product/1016/35048) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |

<span id="tablegroupCorrelation"></span>
### API grup tabel TcaplusDB

| Operasi API                                                     | Jalur Sumber Daya                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTableGroup](https://intl.cloud.tencent.com/document/product/1016/35027) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DeleteTableGroup](https://intl.cloud.tencent.com/document/product/1016/35026) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DescribeTableGroups](https://intl.cloud.tencent.com/document/product/1016/35025) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [ModifyTableGroupName](https://intl.cloud.tencent.com/document/product/1016/35024) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |

<span id="tableCorrelation"></span>
### API tabel TcaplusDB

| Operasi API                                                     | Jalur Sumber Daya                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTables](https://intl.cloud.tencent.com/document/product/1016/35039) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ClearTables](https://intl.cloud.tencent.com/document/product/1016/35042) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DeleteTables](https://intl.cloud.tencent.com/document/product/1016/35038) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTables](https://intl.cloud.tencent.com/document/product/1016/35036) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTablesInRecycle](https://intl.cloud.tencent.com/document/product/1016/35035) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableMemos](https://intl.cloud.tencent.com/document/product/1016/35034) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableQuotas](https://intl.cloud.tencent.com/document/product/1016/35033) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTables](https://intl.cloud.tencent.com/document/product/1016/35032) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RecoverRecycleTables](https://intl.cloud.tencent.com/document/product/1016/35031) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RollbackTables](https://intl.cloud.tencent.com/document/product/1016/35030) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
