## Ikhtisar

Perangkat keras instans Tencent Cloud CVM dapat disesuaikan dengan cepat dan fleksibel. Dokumen ini menjelaskan metode operasi untuk peningkatan konfigurasi, penurunan versi, dan penyesuaian lintas model.

## Prasyarat

Anda dapat menyesuaikan konfigurasi instans saat dalam status nonaktif atau berjalan. Jika instans sedang berjalan, penyesuaian akan berlaku setelah instans dinonaktifkan dan dimulai ulang secara paksa.
> 
> - Jika instans telah **shut down** (dimatikan), Anda dapat menyesuaikan konfigurasinya secara langsung melalui konsol.
> - Jika instans **running** (berjalan), Anda dapat menyesuaikan konfigurasinya secara online dan mengonfirmasi untuk mematikan instans secara paksa. Penyesuaian berlaku setelah instans dimulai ulang.
> - Anda dapat menyesuaikan konfigurasi instans secara online **in batches** (dalam batch). Jika sebuah instans dalam operasi batch sedang **running** (berjalan), Anda perlu memaksa instans untuk dinonaktifkan. Penyesuaian berlaku setelah instans dimulai ulang.

## Batas dan Dampak

### Batas penyesuaian konfigurasi

Hanya instans **whose system and data disks are both CBS cloud disks** (yang sistem dan disk datanya merupakan disk cloud CBS) yang mendukung penyesuaian konfigurasi.
- Peningkatan konfigurasi:
Tidak ada batasan jumlah peningkatan konfigurasi. Peningkatan akan segera berlaku.
- Penurunan konfigurasi:
 - Instans bayar sesuai pemakaian dapat diturunkan beberapa kali kapan saja.
- Penyesuaian antar keluarga instans: konfigurasi dapat disesuaikan antar keluarga instans tanpa perlu migrasi data.
Selama penyesuaian konfigurasi, spesifikasi target bergantung pada jenis instans yang disediakan di zona ketersediaan saat ini. Perhatikan batasan berikut:
 - **Spot instances** (Instans spot) tidak mendukung penyesuaian konfigurasi lintas model.
 - **Dedicated instances** (Instans khusus) tidak mendukung penyesuaian konfigurasi lintas model. Cakupan penyesuaian tunduk pada sumber daya yang tersisa dari host khusus tempat instans berada.
 - **Heterogeneous instances such as GPU and FPGA instances** (Instans heterogen seperti instans GPU dan FPGA) tidak dapat digunakan sebagai jenis instans sumber atau target untuk penyesuaian konfigurasi di seluruh kelompok instans.
 - **Instances configured with a classic network** (Instans yang dikonfigurasi dengan jaringan klasik) tidak dapat disesuaikan dengan instans yang hanya mendukung VPC.
 - Jika jenis instans target tidak mendukung jenis disk CBS yang dikonfigurasi untuk jenis instans saat ini, konfigurasi tidak dapat disesuaikan.
 - Jika jenis instans target tidak mendukung jenis citra yang dikonfigurasi untuk jenis instans saat ini, konfigurasi tidak dapat disesuaikan.
 - Jika jenis instans target tidak mendukung ENI atau kuantitas ENI yang dikonfigurasi untuk jenis instans saat ini, konfigurasi tidak dapat disesuaikan. Untuk informasi selengkapnya, lihat [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/576/18527).
 - Jika jenis instans target tidak mendukung batas bandwidth jaringan publik yang dikonfigurasi untuk jenis instans saat ini, konfigurasi tidak dapat disesuaikan. Untuk informasi selengkapnya, lihat [Batas Bandwidth Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/12523).

### Dampak

IP pribadi instans dapat berubah setelah penyesuaian konfigurasi. Dalam hal ini, prompt akan muncul di halaman penyesuaian konfigurasi. Jika tidak, IP pribadi akan tetap sama.

## Petunjuk

>
> - Jika bisnis Anda berubah, Anda dapat menyesuaikan konfigurasi instans.
> - Selama peningkatan konfigurasi, tingkatkan instans CVM Anda sebagaimana mestinya dan bayar biaya yang mungkin dibebankan.
> - Selama penurunan versi konfigurasi, menonaktifkan paksa dan mulai ulang instans CVM Anda agar konfigurasi baru segera diterapkan.

### Penyesuaian konfigurasi melalui konsol

#### Menyesuaikan konfigurasi satu instans

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm), lalu klik **Instances** (Instans) untuk melihat daftar instans CVM.
2. Temukan instans yang akan disesuaikan dan pilih **More** (Lainnya) > **Resource Adjustment** (Penyesuaian Sumber Daya) > **Adjust Configuration** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi) di sebelah kanan, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/65541031befe2d0144227cf5a616e161.png)
3. Pada langkah "Pilih konfigurasi target", konfirmasikan status dan operasi instans, **select the required model and specifications, confirm the performance parameters** (pilih model dan spesifikasi yang diperlukan, konfirmasi parameter performa), lalu klik **Next** (Selanjutnya), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/818fbf0dfa791ad5d5a76186eefba019.png)
4. Berdasarkan metode penagihan instans, konfirmasi biaya dan klik **Next** (Selanjutnya).
	- Instans bayar sesuai pemakaian: konfirmasikan jumlah yang akan dibekukan untuk jenis instans baru. Setelah penyesuaian konfigurasi, instans bayar sesuai pemakaian dikenakan biaya mulai dari harga tingkat-1. Konfirmasi aturan penagihan, seperti yang ditunjukkan pada gambar berikut:
	![](https://main.qcloudimg.com/raw/25f8630836acdfe274357142d8609c5d.png)
5. Pada langkah "Matikan CVM", baca perintah dengan cermat berdasarkan status instans yang berjalan.
 - Jika instans saat ini sedang berjalan, baca prompt dengan hati-hati dan pilih "Agree to a forced shutdown"" (Setujui untuk mematikan dengan paksa), seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/e016f2cc674938acd0046115f007669b.png)
 - Jika instans saat ini dimatikan, prompt berikut akan muncul:
![](https://main.qcloudimg.com/raw/8385495393237523d0d71460a7b7009b.png)
6. Klik **Adjust Now** (Sesuaikan Sekarang) untuk membuka halaman pesanan dan menyelesaikan pembayaran. 

### Penyesuaian konfigurasi melalui API 

Anda dapat menggunakan ResetInstancesType API untuk menyesuaikan konfigurasi instans. Untuk informasi selengkapnya, lihat dokumentasi API [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239).





