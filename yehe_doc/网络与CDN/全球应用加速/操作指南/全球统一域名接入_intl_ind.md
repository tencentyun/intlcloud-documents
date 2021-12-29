## Membuat Nama Domain Terpadu

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Unified Domain Name** (Nama Domain Terpadu), dan klik **Create (Buat).
2. Konfigurasi informasi **new unified domain name** (nama domain terpadu baru).
![](https://main.qcloudimg.com/raw/ef657658a3746491785734a4b9436efe.png)
- Proyek: proyek tempat nama domain terpadu (nantinya dapat diubah).
- Nama domain: dapat berisi hingga 30 karakter.
- Entri Default: alamat akses untuk wilayah yang tidak dipercepat yang biasanya merupakan alamat IP dari server asal.

> ! Jumlah default nama domain terpadu adalah 5. Jika Anda membutuhkan lebih banyak, hubungi perwakilan Tencent Cloud Anda.

## Mengonfigurasi Wilayah Akses

1. Masuk ke halaman **[Unified Domain Name](https://console.cloud.tencent.com/gaap/domain)** ([Nama Domain Terpadu]) dan klik nama domain yang ditentukan atau **Set** (Atur) untuk melanjutkan ke halaman selanjutnya.
    ![](https://qcloudimg.tencent-cloud.cn/raw/2be645caa6cbc7d1c0f6016e7ac70fec.png)
   - Nama Domain: nama domain yang digunakan untuk akses klien.
   - Entri Default: alamat akses untuk wilayah yang tidak dipercepat yang biasanya merupakan alamat IP dari server asal.
   - Jumlah Koneksi: jumlah koneksi dalam nama domain terpadu.
   - Status: nama domain terpadu hanya dapat berfungsi dengan baik dalam status **Enabled (Diaktifkan).
2. Klik **Add Settings** (Tambahkan Pengaturan) untuk menampilkan jendela **Adding Settings** (Tambahkan Pengaturan), pilih wilayah akselerasi dari daftar serta node akses, dan klik **OK** (Oke) agar berlaku seperti yang ditunjukkan di bawah ini:
![](https://qcloudimg.tencent-cloud.cn/raw/1d5e8a5fb087abcd21c2ce17a94c12ef.png)

## Mengonfigurasi Entri Default

Setelah layanan akses nama domain terpadu global diaktifkan, untuk menghindari latensi jaringan yang tidak perlu yang disebabkan oleh jalan memutar dan biaya lalu lintas tambahan, Anda perlu mengonfigurasi jalur akses untuk pengguna dalam jenis berikut:

1. Pengguna di atau dekat dengan wilayah server asal: mereka umumnya dapat mengakses server asal secara langsung melalui jaringan publik alih-alih menggunakan koneksi akselerasi.
2. Pengguna yang jauh dari wilayah entri koneksi akselerasi: mereka umumnya mengakses server asal langsung melalui jaringan publik. Mengakses melalui koneksi akselerasi tidak memiliki efek akselerasi yang ideal.

Pada halaman **[Unified Domain Name](https://console.cloud.tencent.com/gaap/domain)** ([Nama Domain Terpadu]), klik nama domain yang ditentukan atau **Set** (Atur) untuk melanjutkan ke halaman selanjutnya. Kemudian, klik ikon **Edit** di sebelah kanan **Default Entry** (Entri Default) di bagian atas untuk mengonfigurasi **Default Entry** (Entri Default).
Setelah mengonfigurasi alamat IP entri, kecuali pengguna di wilayah yang tercakup oleh koneksi akselerasi yang dipilih, pengguna di wilayah lain akan mengakses server asal Anda secara langsung di IP ini melalui jaringan publik.
![](https://qcloudimg.tencent-cloud.cn/raw/c549724b7ac191aa4b45ca7d97144ce0.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3aa59862dd00d759ee4933d8cf7b2a34.png)

