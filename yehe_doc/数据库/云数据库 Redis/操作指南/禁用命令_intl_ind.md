## Ikhtisar
TencentDB for Redis mendukung penonaktifan beberapa perintah yang dapat menyebabkan ketidakstabilan layanan atau menghapus data secara tidak sengaja.

Anda dapat mengonfigurasi parameter `disable-command-list` untuk menonaktifkan perintah tersebut. Jika parameter ini tidak ditampilkan di konsol Anda, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meningkatkan versi kernel minor. Pemutusan hubungan singkat akan terjadi selama pemutakhiran versi, dan Anda dapat menyambung kembali setelah pemutakhiran selesai.

## Petunjuk
### Menonaktifkan perintah
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pilih **Parameter Configuration** (Konfigurasi Parameter) > **Modifiable Parameters** (Parameter yang Bisa Dimodifikasi) dan konfigurasikan daftar perintah untuk dinonaktifkan di baris parameter `disable-command-list`.
>?
>- Perintah yang dapat dinonaktifkan termasuk `flushall`, `flushdb`, `keys`, `hgetall`, `eval`, `evalsha`, dan `script`, yang tidak dinonaktifkan secara default pada instans TencentDB for Redis baru yang dibeli setelah 1 Januari 2019.
>- Penonaktifan perintah akan berlaku dalam dua menit untuk koneksi yang ada tanpa memulai ulang layanan Redis.
>
![](https://main.qcloudimg.com/raw/3641b6811d698955f9564a34dfe73e36.png)

### Mengaktifkan perintah yang dinonaktifkan
Pada tab **Parameter Configuration** (Konfigurasi Parameter) > **Modifiable Parameters** (Parameter yang Dapat Dimodifikasi), hapus perintah dari daftar perintah yang dinonaktifkan di **Current Value** (Nilai Saat Ini) untuk mengaktifkannya.

### Riwayat modifikasi parameter
Lihat riwayat modifikasi parameter pada tab **Parameter Configuration** (Konfigurasi Parameter) > **Modification Log** (Log Modifikasi).

