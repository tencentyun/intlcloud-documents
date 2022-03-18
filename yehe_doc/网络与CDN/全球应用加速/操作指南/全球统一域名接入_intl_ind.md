## Membuat Nama Domain Terpadu
1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Unified Domain Name** (Nama Domain Terpadu) dan klik **Create** (Buat).
2. Konfigurasikan nama domain terpadu yang dibuat.
 ![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)
- **Project** (Proyek): proyek tempat nama domain terpadu berada, yang dapat diubah kemudian.
- **Domain Name** (Nama Domain): terdiri dari maksimum 30 karakter.
- **Default Entry** (Entri Default): alamat akses untuk wilayah yang tidak diakselerasi, dan biasanya merupakan alamat IP dari server asal.

> ! Secara default, jumlah nama domain terpadu adalah 5. Jika Anda membutuhkan lebih banyak nama domain terpadu, hubungi perwakilan Tencent Cloud.

## Mengonfigurasi Wilayah Akselerator
1. Masuk ke halaman [Nama Domain Terpadu](https://console.cloud.tencent.com/gaap/domain), lalu klik nama domain tersebut atau **Set** (Atur) nama domain.

	- **Domain Name** (Nama Domain): nama domain yang diakses oleh klien.
	- **Default Entry** (Entri Default): alamat akses untuk wilayah yang tidak diakselerasi, dan biasanya merupakan alamat IP dari server asal.
	- **Number of Connections** (Jumlah Koneksi): jumlah koneksi yang dimiliki nama domain terpadu.
	- **Status**: nama domain terpadu hanya dapat berfungsi dengan baik dalam status **Enabled** (Diaktifkan).
2. Klik **Add Setting Item** (Tambahkan Item Pengaturan). Di jendela pop-up, pilih wilayah dan koneksi akselerator terdekat, lalu klik **OK** (Oke).
 ![](https://main.qcloudimg.com/raw/9ebb9dbdffbe57a7438b8ce169b9dd1e.png)

## Mengonfigurasi Entri Default
Setelah layanan akses nama domain terpadu global diaktifkan, untuk menghindari latensi jaringan yang tidak perlu akibat detour dan biaya lalu lintas tambahan, Anda perlu mengonfigurasi jalur akses untuk jenis pengguna berikut:
1. Pengguna yang berada di atau di dekat wilayah server asal: pengguna ini umumnya dapat mengakses langsung server asal melalui jaringan publik alih-alih menggunakan koneksi akselerasi.
2. Pengguna yang berada jauh dari wilayah entri koneksi akselerasi: pengguna ini umumnya mengakses langsung server asal melalui jaringan publik. Akses melalui koneksi akselerasi tidak memiliki efek akselerasi yang ideal.

Di halaman **Unified Domain Name** (Nama Domain Terpadu), klik nama domain tersebut atau **Set** (Atur) nama domain. Kemudian, klik ikon **Edit** di sebelah kanan **Default Entry** (Entri Default) untuk mengonfigurasi entri default.
Setelah alamat IP entri dikonfigurasi, pengguna di wilayah yang tercakup oleh koneksi akselerasi dan di wilayah lain dapat mengakses langsung server asal Anda menggunakan alamat IP ini melalui jaringan publik.
![](https://main.qcloudimg.com/raw/9f2f9980950bdb8b0273c0015b5a777d.png)


