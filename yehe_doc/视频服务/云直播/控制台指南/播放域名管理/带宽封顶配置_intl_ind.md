CSS memungkinkan Anda menetapkan batas pemakaian bandwidth untuk domain pemutaran ulang Anda. Di wilayah akselerasi domain Anda, jika bandwidth downstream puncak dalam periode referensi mencapai batas yang Anda tetapkan, kesalahan 403 akan ditampilkan untuk permintaan pemutaran ulang. Fitur ini dinonaktifkan secara default.


## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
Anda telah menambahkan [nama domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:limit)
## Batas
| Wilayah Akselerasi | Wilayah Pembatasan Pemakaian Bandwidth Default | Keterangan |
|---------|---------|---------|
| Tiongkok Daratan | Tiongkok Daratan | Anda hanya dapat menetapkan batas pemakaian untuk Tiongkok Daratan. |
| Di Luar Tiongkok Daratan | Di Luar Tiongkok Daratan | Anda hanya dapat menetapkan batas pemakaian untuk luar Tiongkok Daratan. |
| Akselerasi global | Akselerasi global | <ul style="margin-bottom:0px;"><li> Anda dapat menetapkan batas pemakaian yang berbeda untuk di dalam dan di luar Tiongkok Daratan.</li><li>Anda juga dapat menetapkan batas pemakaian global.</li></ul> |


## Mengonfigurasikan Batas Pemakaian Bandwidth
1. Buka [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage). Klik nama domain pemutaran ulang Anda atau **Manage** (Kelola) di sebelah kanan.
2. Pilih tab **Advanced Configuration** (Konfigurasi Lanjutan).
3. Di area **Bandwidth cap configuration** (Konfigurasi batas pemakaian bandwidth), klik **Edit**.
4. Aktifkan **Bandwidth Cap** (Batas Pemakaian Bandwidth) ![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png), dan selesaikan pengaturan berikut:
	- **Wilayah yang valid** ditentukan oleh wilayah akselerasi domain pemutaran ulang Anda. Informasi mendetail dapat dilihat di [Batasan](#limit).
	- Masukkan batas pemakaian bandwidth.
	- Pilih unit bandwidth (Mbps, Gbps, atau Tbps).
5. Aktifkan **Alert threshold** (Ambang batas peringatan) ![](https://main.qcloudimg.com/raw/96d86bb811611dbc89c4757fb64af536.png). 
     Tetapkan ambang batas peringatan sebagai persentase batas bandwidth. Ketika ambang batas tercapai, sistem akan mengirimkan peringatan kepada Anda melalui Pusat Pesan atau saluran lainnya. 
6. Klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/b0cb7574efca181f31062e272211f103.png)

>! 
>- Faktor konversi antara unit bandwidth adalah 1.000: 1 Tbps = 1.000 Gbps; 1 Gbps = 1.000 Mbps
>- Jika Anda mengubah wilayah akselerasi untuk domain Anda, Anda perlu mengonfigurasikan batas pemakaian bandwidth lagi.
>- Ambang batas peringatan default adalah 80% dari batas pemakaian bandwidth. Rentang nilai: 0‒100.


## Menonaktifkan Batas Pemakaian Bandwidth
1. Buka [Domain Management (Manajemen Domain)](https://console.cloud.tencent.com/live/domainmanage). Klik nama domain pemutaran ulang Anda atau **Manage** (Kelola) di sebelah kanan.
2. Pilih tab **Advanced Configuration** (Konfigurasi Lanjutan).
3. Di area **Bandwidth cap configuration** (Konfigurasi batas pemakaian bandwidth), klik **Edit**.
4. Nonaktifkan **Bandwidth Cap** (Batas Pemakaian Bandwidth) ![](https://main.qcloudimg.com/raw/a02cf62f7cf3e9c072047690a6818ac2.png).
5. Klik **Save** (Simpan).

![](https://qcloudimg.tencent-cloud.cn/raw/490bd4983649a535f888a91a11446521.png)
