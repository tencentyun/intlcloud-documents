TencentDB for Redis mendukung akses yang diaktifkan oleh kata sandi dan bebas kata sandi.

>?
>- Demi keamanan data, Anda tidak disarankan mengaktifkan akses bebas kata sandi.
>- Setelah akses bebas kata sandi diaktifkan, sebaiknya batasi jumlah server yang mengakses menggunakan grup keamanan.

## Mengatur Akses Bebas Kata Sandi
#### Pilih akses bebas kata sandi saat membuat instans
1. Login ke [konsol Redis](https://console.cloud.tencent.com/redis), lalu klik **Create Instances** (Buat Instans) untuk melihat daftar instans.
2. Pilih **Password Exemption Authentication** (Autentikasi Pembebasan Kata Sandi) di opsi **Set Password** (Atur Kata Sandi) pada halaman pembelian instans. Setelah instans berhasil dibuat, instans dapat diakses tanpa kata sandi.
![](https://main.qcloudimg.com/raw/03a688ea981ccaf28124b74ebb8d9223.png)

#### Aktifkan akses bebas kata sandi untuk instans yang ada
Dalam daftar instans, klik ID instans untuk masuk ke halaman detail instans, dan klik **Password Exemption Access** (Akses Pembebasan Kata Sandi) di "Configuration Info" (Info Konfigurasi) > "Connection Password" (Kata Sandi Koneksi).

## Melihat Status Akses Bebas Kata Sandi
Dalam daftar instans, klik ID instans untuk masuk ke halaman detail instans, dan Anda dapat melihat apakah instans telah mengaktifkan akses pembebasan kata sandi di "Configuration Info" (Info Konfigurasi) > "Connection Password” (Kata Sandi Koneksi).
![](https://main.qcloudimg.com/raw/ddd227bf61e70cb72e3971ea58c9d773.png)

## Menonaktifkan Akses Bebas Kata Sandi
Pada bagian "Configuration Info" (Info Konfigurasi) > "Connection Password” (Kata Sandi Koneksi), klik **Reset Password** (Atur Ulang Kata Sandi) untuk menonaktifkan akses pengecualian kata sandi.

