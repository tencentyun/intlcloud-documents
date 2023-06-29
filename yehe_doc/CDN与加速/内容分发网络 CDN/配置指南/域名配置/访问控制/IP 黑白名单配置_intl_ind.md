## Ikhtisar Konfigurasi
Untuk mengontrol sumber akses ke sumber daya bisnis Anda, Anda dapat menggunakan fitur daftar blokir/daftar izin IP di CDN Tencent Cloud.

Dengan mengonfigurasi kebijakan kontrol akses pada IP permintaan pengguna, Anda dapat mengontrol sumber akses secara efektif, mencegah terjadinya hotlink oleh IP dan serangan berbahaya, dll.

## Panduan Konfigurasi

### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Access Control** (Kontrol Akses) untuk melihat bagian **IP Blocklist/Allowlist Configuration** (Konfigurasi Daftar Blokir/Daftar Izin IP). Ini dinonaktifkan secara default.
![](https://main.qcloudimg.com/raw/f151317bd14f053a125bf0c3841da033.png)

### Mengaktifkan konfigurasi

Alihkan switch, beri centang pada **Blocklist** (Daftar Blokir) atau **Allowlist** (Daftar Izin), masukkan daftar IP atau rentang IP, dan klik **OK**:
![](https://main.qcloudimg.com/raw/0b278589542a7022b3525f80ecadd2e3.png)
**IP blocklist** (Daftar blokir IP)
Jika IP klien cocok dengan IP atau rentang IP di daftar blokir, simpul CDN yang diakses akan langsung mengembalikan kode status 514.
**IP allowlist** (Daftar izin IP)
Jika IP klien tidak cocok dengan IP atau rentang IP di daftar izin, simpul CDN yang diakses akan langsung mengembalikan kode status 514.
**Batasan konfigurasi**

- Daftar blokir dan daftar izin IP saling eksklusif dan tidak dapat dikonfigurasi secara bersamaan.
- Masing-masing hingga 200 entri dapat ditambahkan ke daftar blokir dan daftar izin.
- Hanya rentang IP `/8`, `/16`, dan `/24` yang didukung.
- Format `IP: Port` tidak didukung di sini.

### Menonaktifkan konfigurasi
Anda dapat menonaktifkan switch untuk menonaktifkan fitur ini. Saat switch dinonaktifkan, fitur ini tidak diterapkan di lingkungan produksi meskipun ada konfigurasi yang sudah ada. Jika Anda mengaktifkan switch, konfigurasi akan diterapkan di seluruh jaringan setelah tindakan dikonfirmasi.
![](https://main.qcloudimg.com/raw/24a3de16131fd945c05307493eb768f0.png)

>!Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global, daftar blokir/daftar izin IP akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari wilayah di dalam dan di luar Tiongkok Daratan.

## Sampel Konfigurasi

Jika konfigurasi daftar blokir/daftar izin IP dari nama domain `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/29a9307902d03f686345eef2964c5ec2.png)
Maka akses aktualnya adalah sebagai berikut:
1. Pengguna dengan IP klien `1.1.1.1` mengakses sumber daya `http://www.test.com/test.txt`. Karena IP cocok dengan IP dalam daftar izin, konten yang diminta akan dikembalikan.
2. Pengguna dengan IP klien `2.1.1.1` mengakses sumber daya `http://www.test.com/test.txt`. Karena IP tidak cocok dengan IP mana pun dalam daftar izin, kode status 514 akan dikembalikan.

