
## Deskripsi Kesalahan
- Gejala 1: penggunaan koneksi tinggi.
![](https://qcloudimg.tencent-cloud.cn/raw/69734df69d793cce934c05b89a6d83b4.png)
- Gejala 2: koneksi tidak dapat dibuat.

## Penyebab Umum
- Koneksi bocor.
- Jumlah koneksi maksimum yang dikonfigurasi terlalu rendah.

## Solusi
Periksa kebocoran koneksi Untuk koneksi jaringan pihak ketiga, harus ada blok terakhir untuk dieksekusi; jika tidak; kode non-standar cenderung menyebabkan masalah di mana koneksi tidak dilepaskan dengan benar.

## Prosedur Pemecahan Masalah
### [Memodifikasi logika kode](id:xgdmlj)
Periksa apakah koneksi bocor, dan jika memang bocor, Anda dapat melepaskan koneksi yang tidak valid dan memperbaiki kode non-standar yang membocorkan koneksi.

### [Memodifikasi konfigurasi koneksi](id:xgljpz)
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman detail instans.
2. Dalam parameter **Network Info** (Info Jaringan) > **Max Connections** (Koneksi Maks) pada halaman detail instans, klik **Adjust** (Sesuaikan) untuk menyesuaikan jumlah koneksi maksimum.
![](https://qcloudimg.tencent-cloud.cn/raw/ed736808880fdd4f3ad4f86b69e0a617.png)
3. Di jendela pop-up, sesuaikan jumlah koneksi maksimum dan klik **OK** (OKE).

>?Jika masalah ini berlanjut, [kirim tiket](https://console.intl.cloud.tencent.com/workorder/category).
