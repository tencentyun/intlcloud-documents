## Ikhtisar
Peran Cloud Access Management (CAM) adalah identitas virtual dengan kumpulan izin. Ini digunakan untuk memberikan izin kepada entitas peran untuk mengakses layanan dan sumber daya dan melakukan operasi di Tencent Cloud. Anda dapat mengaitkan peran CAM dengan instans CVM untuk memanggil Tencent Cloud API lainnya dari instans menggunakan kunci Security Token Service (STS) sementara yang diperbarui secara berkala. Hal ini memastikan keamanan SecretKey Anda dan membantu Anda menerapkan kontrol izin yang disempurnakan, menghindari risiko keamanan dari penggunaan kunci persisten.

Dokumen ini menjelaskan cara mengikat, mengubah, dan menghapus peran.

## Keuntungan
Mengikat peran CAM ke instans dilengkapi dengan fitur dan keuntungan berikut.
- Anda dapat mengakses layanan Tencent Cloud lainnya menggunakan kunci sementara STS. Untuk informasi selengkapnya, lihat [STS API](https://intl.cloud.tencent.com/document/product/598/35840).
- Anda dapat memberikan peran yang terkait dengan kebijakan akses yang berbeda ke instans sehingga instans tersebut diberikan izin akses yang berbeda ke sumber daya Tencent Cloud, yang membantu Anda menerapkan kontrol izin yang disempurnakan.
- Anda tidak perlu menyimpan SecretKey dalam instans. Sebagai gantinya, Anda dapat mengontrol izin akses instans secara mudah dengan mengubah otorisasi peran.




## Menggunakan Petunjuk
- Instans hanya mengizinkan entitas peran yang berisi `cvm.qcloud.com` untuk mengambil peran. Untuk informasi selengkapnya, lihat [Konsep](https://intl.cloud.tencent.com/document/product/598/19421).
- Instans harus berada di VPC.
- Instans hanya dapat mengikat satu peran CAM dalam satu waktu.
- Anda dapat mengikat, mengubah, atau menghapus peran tanpa membayar biaya tambahan.


## Petunjuk

### Mengikat/memodifikasi peran
#### Mengikat/memodifikasi peran satu CVM
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm), lalu klik **Instances** (Instans) di bilah sisi kiri.
2. Pada halaman **Instances** (Instans), pilih instans CVM yang ingin Anda ikat atau ubah perannya, lalu klik **More** (Lainnya) > **Instance Settings** (Pengaturan Instans) > **Bind/Modify a Role** (Ikat/Modifikasi Peran) di bawah kolom **Operation** (Operasi), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/34d5a9866aa28fdb8a3363884918e3bb.png)
3. Di jendela pop-up, pilih peran yang ingin Anda ikat, lalu klik **OK** (OKE).
#### Mengikat/memodifikasi peran secara massal
1. Pada halaman **Instances** (Instans), pilih instans CVM yang ingin Anda ikat atau ubah perannya, klik **More Actions** (Tindakan Lainnya) > **Instance Settings** (Pengaturan Instans) > **Bind/Modify a Role** (Ikat/Modifikasi Peran) di daftar teratas, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/4093443ee4f5b484860f8c8eae3b3b3e.png)
2. Di jendela pop-up, pilih peran yang ingin Anda ikat, lalu klik **OK** (OKE).
>?CVM yang dimodifikasi dengan menggunakan metode ini akan memiliki nama peran yang sama.



### Menghapus peran
#### Menghapus peran satu CVM
1. Pada halaman **Instances** (Instans), cari instans CVM yang ingin Anda hapus perannya, klik **More** (Lainnya) > **Instance Settings** (Pengaturan Instans) > **Delete a Role** (Hapus Peran) di bawah kolom **Operation** (Operasi), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/8b44772763ab60fa69c404360db1ebbf.png)
2. Klik **OK** (OKE) di jendela pop-up.
#### Menghapus peran secara massal
1. Pada halaman **Instances** (Instans), pilih instans CVM yang ingin Anda hapus perannya, klik **More Actions** (Tindakan Lainnya) > **Instance Settings** (Pengaturan Instans) > **Delete a Role** (Hapus Peran) di atas daftar, seperti yang ditunjukkan di bawah.
![](https://main.qcloudimg.com/raw/72669a0d3bbdde1491c24b5acc0eadbf.png)
2. Klik **OK** (OKE) di jendela pop-up.



