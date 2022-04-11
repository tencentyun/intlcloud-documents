
Dokumen ini menjelaskan cara membuat instans TencentDB for MySQL di konsol.

## Prasyarat
Anda telah mendaftarkan akun Tencent Cloud dan menyelesaikan verifikasi identitas.
- Untuk mendaftarkan akun Tencent Cloud:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Klik di sini untuk mendaftar akun Tencent Cloud</a></div>
- Untuk memverifikasi identitas Anda:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Klik di sini untuk memverifikasi identitas Anda</a></div>

## Petunjuk
1. Login ke [halaman pembelian TencentDB for MySQL](https://buy.cloud.tencent.com/cdb), konfigurasikan informasi instans berikut, dan klik **Buy Now** (Beli Sekarang).
 - **Billing Mode** (Mode Penagihan): bayar sesuai pemakaian
    - Jika volume permintaan bisnis Anda sangat berfluktuasi dan seketika, sebaiknya pilih penagihan bayar sesuai pemakaian.
 - **Region** (Wilayah): pilih wilayah yang Anda inginkan untuk men-deploy instans TencentDB for MySQL Anda. Sebaiknya gunakan wilayah yang sama dengan instans CVM yang akan dihubungkan. Produk Tencent Cloud di wilayah yang berbeda tidak dapat berkomunikasi satu sama lain melalui jaringan pribadi. Wilayah tidak dapat diubah setelah pembelian.
 - **Database Version** (Versi Database): saat ini, TencentDB for MySQL mendukung MySQL versi 8.0, 5.7, 5.6, dan 5.5. Untuk informasi selengkapnya tentang fitur setiap versi, lihat [dokumentasi resmi](https://dev.mysql.com/doc/refman/5.7/en/).
  - **Architecture** (Arsitektur): node tunggal, dua node, atau tiga node. Untuk informasi selengkapnya, lihat [Arsitektur Database](https://intl.cloud.tencent.com/document/product/236/38328).
  - **Data Replication Mode** (Mode Replikasi Data): mode replikasi asinkron, semi-sinkron, dan sinkronisasi yang canggih didukung. Untuk informasi selengkapnya, lihat [Replikasi Instans Database](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Source AZ** (Sumber AZ) dan **Replica AZ** (Replika AZ): pilih sumber dan AZ replika yang berbeda (yaitu, [penyebaran multi-AZ](https://intl.cloud.tencent.com/document/product/236/8459)) untuk melindungi database Anda dari kegagalan dan gangguan AZ.
>?
>- Jika node sumber dan replika berada di AZ yang berbeda, mungkin ada penundaan sinkronisasi jaringan tambahan sebesar 2-3 md.
>- Saat Anda membeli layanan Tencent Cloud, sebaiknya pilih wilayah terdekat untuk meminimalkan latensi akses dan meningkatkan kecepatan unduhan.
>
 - **Instance Type** (Jenis Instans): umum atau khusus. Untuk informasi selengkapnya, lihat [Kebijakan Isolasi Sumber Daya](https://intl.cloud.tencent.com/document/product/236/39794).
 - **Instance Specification** (Spesifikasi Instans): pilih spesifikasi sesuai kebutuhan.
 - **Hard Disk** (Hard Disk): ruang disk digunakan untuk menyimpan file yang dibutuhkan oleh eksekusi MySQL.
 - **Network** (Jaringan): pilih jaringan tempat instans TencentDB for MySQL berada, yaitu "Default-VPC (default)" secara default. Sebaiknya pilih VPC yang sama di wilayah yang sama dengan instans CVM yang akan dihubungkan. Jika tidak, instans MySQL tidak dapat terhubung ke instans CVM melalui jaringan pribadi.
 - **Security Group** (Grup Keamanan): untuk informasi selengkapnya tentang pembuatan dan pengelolaan grup keamanan, lihat [Manajemen Grup Keamanan TencentDB](https://intl.cloud.tencent.com/document/product/236/14470).
>?Port 3306 harus dibuka untuk instans MySQL melalui aturan masuk grup keamanan. Instans MySQL menggunakan port jaringan pribadi 3306 secara default dan mendukung port kustom. Jika port default diubah, port baru harus dibuka di grup keamanan.
 - **Parameter Template** (Templat Parameter): selain templat parameter sistem yang disediakan oleh TencentDB, Anda dapat membuat templat parameter kustom. Untuk informasi selengkapnya, lihat [Mengelola Templat Parameter](https://intl.cloud.tencent.com/document/product/236/31906).
 - **Alarm Policy** (Kebijakan Alarm): Anda dapat membuat kebijakan alarm untuk memicu alarm dan mengirim pesan saat status sumber daya Tencent Cloud berubah. Untuk informasi selengkapnya, lihat [Kebijakan Alarm (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
 - **Project** (Proyek): pilih proyek tempat instans TencentDB berada. Proyek default digunakan.
 - **Tag** (Tag): mengkategorikan dan mengelola sumber daya dengan tag. Untuk informasi selengkapnya, lihat [Tag > Ikhtisar](https://intl.cloud.tencent.com/document/product/236/31917).
 - **Instance Name** (Nama Instans): beri nama instans sekarang atau nanti.
 - **Quantity** (Jumlah): Anda dapat membeli hingga 10 instans bayar sesuai pemakaian di setiap AZ.
 - **Terms of Service** (Ketentuan Layanan): untuk informasi selengkapnya, lihat [Ketentuan Layanan](https://intl.cloud.tencent.com/document/product/236/35543).
2. Anda akan dikembalikan ke daftar instans setelah membeli instans. Instans akan berada dalam status **Delivering** (Dikirim). Anda dapat menginisialisasi instans setelah sekitar 3-5 menit saat statusnya berubah menjadi **Uninitialized** (Belum Diinisialisasi).

## Operasi Selanjutnya
Setelah membuat instans TencentDB for MySQL, Anda perlu menginisialisasinya sebelum dapat mulai menggunakannya. Untuk informasi selengkapnya, lihat [Menginisialisasi Instans MySQL](https://intl.cloud.tencent.com/document/product/236/3128).

