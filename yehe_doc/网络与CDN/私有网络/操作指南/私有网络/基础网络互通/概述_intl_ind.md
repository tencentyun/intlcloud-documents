Fitur Classiclink memungkinkan CVM berbasis VPC untuk berkomunikasi dengan CVM berbasis jaringan klasik. Dokumen ini terutama menjelaskan cara membuat dan mengelola Classiclink.

## Latar belakang
Jaringan klasik dan VPC adalah ruang jaringan di cloud. Jaringan klasik adalah kumpulan sumber informasi jaringan publik untuk semua pengguna Tencent Cloud (seperti yang ditampilkan di sisi kanan gambar di bawah). IP pribadi dari semua CVM ditetapkan oleh Tencent Cloud. Anda tidak dapat menyesuaikan rentang IP atau alamat IP. Sebaliknya, VPC adalah ruang jaringan yang terisolasi secara logis di Tencent Cloud (seperti yang ditampilkan di sisi kiri gambar di bawah). Di VPC, Anda dapat menyesuaikan rentang IP, alamat IP, dan kebijakan perutean.
VPC lebih cocok untuk kasus penggunaan yang memerlukan konfigurasi kustom.
>?
>+ Karena sumber informasi jaringan klasik menjadi semakin langka dan tidak dapat diperluas, akun Tencent Cloud yang terdaftar setelah 13 Juni 2017 dapat membuat instans (termasuk CVM dan TencentDB) hanya di VPC, bukan di jaringan klasik. Jika Anda perlu menggunakan layanan jaringan klasik, kirimkan permohonan.
>+ Anda dapat menggunakan `DescribeAccountVpcAttributes` API untuk menanyakan atribut jaringan suatu akun. Jika nilai `supportedPlatforms` adalah `only-vpc`, akun tersebut adalah pengguna VPC default, yang memiliki semua sumber informasi cloud di bawah VPC. Jika nilai `supportedPlatforms` adalah `classic`, akun tersebut adalah pengguna jaringan klasik default, yang memiliki semua sumber informasi cloud di bawah jaringan klasik.
>+ Anda dapat memigrasikan instans Anda dari jaringan klasik ke VPC untuk memfasilitasi penggunaan VPC Anda. Untuk petunjuk dengan detail, lihat [Beralih dari Jaringan Klasik ke VPC](https://intl.cloud.tencent.com/document/product/215/38117).
>
![](https://main.qcloudimg.com/raw/5fe7730ac2f302d960cf20443f976b6f.png)

## Ikhtisar
Secara default, VPC adalah ruang jaringan yang sepenuhnya terisolasi yang tidak dapat diakses oleh VPC lain atau jaringan klasik melalui jaringan pribadi. CCN memastikan interkoneksi antar VPC, sementara solusi berikut menyediakan komunikasi antara VPC dan jaringan klasik.
+ **Classiclink**: memungkinkan CVM berbasis jaringan klasik untuk berkomunikasi dengan sumber informasi VPC seperti instans CVM, TencentDB, dan CLB. Namun, ini hanya menyediakan akses antara CVM berbasis VPC dan CVM berbasis jaringan klasik daripada sumber informasi cloud lainnya termasuk TencentDB dan CLB dalam jaringan klasik, seperti yang ditampilkan di bawah ini.
 <img src="https://main.qcloudimg.com/raw/5c4c66605c6ecd04591dfff5236231df.png" width="50%" />
+ **Terminal connection** (Koneksi terminal): membantu membangun komunikasi antara instans di VPC dan sumber informasi di jaringan klasik (kecuali CVM) melalui jaringan pribadi. Ini memetakan IP instans berbasis jaringan klasik ke IP VPC, memungkinkan Anda mengakses instans berbasis jaringan klasik melalui IP VPC. Fitur ini sekarang mendukung instans CLB, MySQL, Memcached, Redis, dan MongoDB berbasis jaringan klasik. Namun, komunikasi lintas wilayah atau lintas akun tidak didukung. Jika Anda ingin membuat koneksi terminal, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).


## Membuat Classiclink
Classiclink menghubungkan CVM berbasis jaringan klasik dengan VPC untuk mengaktifkan interkoneksi antara VPC dan jaringan klasik. Hal ini memungkinkan CVM berbasis jaringan klasik untuk berkomunikasi dengan sumber informasi VPC.

### Batasan penggunaan
+ Rentang IP VPC harus berada dalam `10.0.0.0/16-10.47.0.0/16` (termasuk subset), jika tidak, mungkin ada konflik IP, yang dapat menyebabkan kegagalan saat menghubungkan dan berkomunikasi dengan CVM berbasis jaringan klasik.
+ CVM berbasis jaringan klasik hanya dapat dihubungkan dengan satu VPC dalam satu waktu.
+ Satu VPC mendukung hubungan dengan hingga 100 CVM berbasis jaringan klasik.
+ Sumber informasi VPC dapat mengakses CVM berbasis jaringan klasik daripada sumber informasi termasuk TencentDB dan CLB.
+ Setelah CVM jaringan klasik dihubungkan dengan VPC, CVM berbasis jaringan klasik hanya dapat berkomunikasi dengan sumber informasi di blok CIDR primer daripada blok CIDR sekunder dari VPC.
- VPC hanya dapat terhubung dengan jaringan klasik di wilayah yang sama.

### Catatan
+ IP pribadi dari CVM berbasis jaringan klasik terkait akan secara otomatis ditambahkan ke kebijakan lokal tabel rute VPC. Hal ini memungkinkan interkoneksi antara CVM ini dan CVM berbasis VPC, tanpa perlu mengubah kebijakan perutean VPC secara manual.
+ Setelah CVM berbasis jaringan klasik dihubungkan dengan VPC, pengaturan firewall dan ACL jaringan mereka akan tetap efektif. Artinya, Anda dapat mengonfigurasi ACL jaringan untuk subnet VPC guna membatasi akses dari CVM berbasis jaringan klasik yang terhubung. Anda juga dapat mengonfigurasi aturan grup keamanan untuk CVM di jaringan klasik dan VPC untuk membatasi akses jaringan dua arah.
+ Instans CLB di VPC tidak dapat diikat ke CVM berbasis jaringan klasik yang saling terhubung dengan VPC yang sama.
- Mengubah IP pribadi CVM berbasis jaringan klasik akan membatalkan hubungannya dengan VPC, dan menyebabkan konfigurasi menjadi tidak valid. Untuk menghubungkannya, Anda perlu menambahkan Classiclink lagi di konsol VPC.
- Classiclink tidak akan terpengaruh oleh tindakan yang diambil terkait CVM seperti isolasi karena pembayaran yang jatuh tempo, isolasi keamanan, migrasi cold, failover, modifikasi konfigurasi, dan peralihan sistem operasi.
- CVM akan otomatis diputuskan koneksinya dari VPC jika CVM dikembalikan.
+ Dalam situasi Classiclink, lalu lintas CVM hanya dapat dirutekan ke alamat IP pribadi di dalam VPC daripada tujuan di luar VPC. Artinya, CVM berbasis jaringan klasik tidak dapat mengakses sumber informasi jaringan publik atau pribadi di luar VPC saat ini melalui perangkat jaringan seperti VPN gateway, direct connect gateway, public gateway, peering connection, dan NAT Gateway. Demikian juga, peer dari VPN gateway, direct connect gateway, dan peering connection tidak dapat mengakses CVM berbasis jaringan klasik.

### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah, dan klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3. Klik tab **Classiclink** lalu klik **+Associate with CVM** (+Hubungkan dengan CVM). 
![](https://main.qcloudimg.com/raw/ad9b76faac017dbc093b3710f0d5070b.png)
4. Pada jendela pop-up, pilih CVM di jaringan klasik untuk dihubungkan dengan VPC dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/b99329129fc8de27dddfbe7897d59218.png)

## Melihat Classiclink
Anda dapat melihat daftar CVM berbasis jaringan klasik yang terhubung dengan VPC.
### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah, dan klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3. Klik tab **Classiclink** untuk melihat daftar CVM berbasis jaringan klasik yang terkait dengan VPC.
![](https://main.qcloudimg.com/raw/3b4e1ad2a860c35f89b42315e709d11f.png)
4. Masukkan IP pribadi di kotak pencarian sudut kanan atas untuk menemukan CVM dengan cepat.

<span id="release" ></span>
## Menghapus Classiclink
Tindakan ini memutuskan koneksi CVM berbasis jaringan klasik dari VPC dan menghentikan interkoneksinya.

### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3. Klik tab **Classiclink**, pilih CVM yang tidak akan dihubungkan dari daftar CVM klasik berbasis jaringan, dan klik **Disassociate** (Putuskan koneksi) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/156dd9a80b6923a96bb52e2d76b55993.png)
4. Periksa kembali catatan dan klik **OK** (Oke).
5. Untuk membatalkan hubungan beberapa CVM, Anda dapat memilih CVM ini untuk tidak dihubungkan dan klik **Disassociate** (Putuskan koneksi) di atas daftar.
