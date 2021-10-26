## Ikhtisar Konfigurasi
Untuk mengontrol sumber akses ke sumber daya bisnis Anda, Anda dapat menggunakan fitur perlindungan hotlink referer di CDN Tencent Cloud.

Dengan mengonfigurasi kebijakan kontrol akses pada nilai bidang referer di header permintaan HTTP, Anda dapat mengontrol sumber akses untuk mencegah terjadinya hotlink oleh pengguna yang berniat buruk.


## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Access Control** (Kontrol Akses) untuk melihat bagian **Hotlink Protection Configuration** (Konfigurasi Perlindungan Hotlink). Ini dinonaktifkan secara default.
![](https://main.qcloudimg.com/raw/53cfa056e5574aae9c912db36fcbf67b.png)

### Mengaktifkan konfigurasi

Alihkan switch, pilih jenis perlindungan hotlink, beri centang pada **Allow blank referer** (Izinkan referer kosong) sesuai kebutuhan, masukkan IP atau nama domain di kotak input, dan klik **OK**.
![](https://main.qcloudimg.com/raw/951eb25d77110a01fcd91ab9bfcd1cad.png)
**Referer blocklist** (Daftar blokir referer):

- Jika bidang referer permintaan cocok dengan string yang dikonfigurasi dalam daftar blokir, simpul CDN tidak akan mengembalikan informasi yang diminta dan kode status 403 akan dikembalikan.
- Jika bidang referer permintaan tidak cocok dengan string yang dikonfigurasi dalam daftar blokir, simpul CDN akan mengembalikan informasi yang diminta.
- Jika **Allow blank referer** (Izinkan referer kosong) dicentang, simpul CDN tidak akan mengembalikan informasi yang diminta dan kode status 403 akan dikembalikan jika bidang referer kosong atau tidak ada dalam permintaan (seperti permintaan peramban).

**Referer allowlist** (Daftar izin referer):
- Jika bidang referer permintaan cocok dengan string yang dikonfigurasi dalam daftar izin, simpul CDN akan mengembalikan informasi yang diminta.
- Jika bidang referer permintaan tidak cocok dengan string yang dikonfigurasi dalam daftar izin, simpul CDN tidak akan mengembalikan informasi yang diminta dan kode status 403 akan dikembalikan.
- Setelah daftar izin dikonfigurasi, simpul CDN hanya dapat mengembalikan permintaan yang cocok dengan string yang dikonfigurasi dalam daftar izin.
- Jika **Allow blank referer** (Izinkan referer kosong) dicentang, simpul CDN akan mengembalikan informasi yang diminta jika bidang referer kosong atau tidak ada dalam permintaan (seperti permintaan peramban).

**Batasan konfigurasi**:
+ Perlindungan hotlink mendukung aturan nama domain/IP (jika aturan IP digunakan, pencocokan awalan tersedia; jika aturan nama domain digunakan, pencocokan awalan tidak didukung). Misalnya, jika `www.abc.com` dikonfigurasi, `www.abc.com/123` akan dicocokkan, tetapi `www.abc.com.cn` tidak; jika `127.0.0.1` dikonfigurasi, `127.0.0.1/123` akan dicocokkan.
+ Perlindungan hotlink mendukung pencocokan kartubebas, misalnya, jika `*.qq.com` dikonfigurasi, `www.qq.com` dan `a.qq.com` akan dicocokkan.

### Menonaktifkan konfigurasi
Anda dapat menonaktifkan switch untuk menonaktifkan fitur ini. Saat switch dinonaktifkan, fitur ini tidak diterapkan di lingkungan produksi meskipun ada konfigurasi yang sudah ada. Jika Anda mengaktifkan switch, konfigurasi akan diterapkan di seluruh jaringan setelah tindakan dikonfirmasi.
![](https://main.qcloudimg.com/raw/0eff7fac96363892b1b95f53fbadf47d.png)

### Konfigurasi khusus wilayah
Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global dan Anda ingin mengonfigurasi akselerasi di dalam dan di luar Tiongkok Daratan dengan pengaturan perlindungan hotlink referer yang berbeda, Anda dapat mengeklik **Add Special Configuration** (Tambahkan Konfigurasi Khusus).
![](https://main.qcloudimg.com/raw/31d414d5adf37f8a2deadce688962645.png)

> !Saat ini, item konfigurasi khusus wilayah tidak dapat dihapus setelah ditambahkan, tetapi item tersebut dapat dinonaktifkan.

## Sampel Konfigurasi

Jika konfigurasi perlindungan hotlink dari nama domain akselerasi `www.test.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/027832bf7f5df50370257cce662105d8.png)
Maka akses aktualnya adalah sebagai berikut:

1. Jika pengguna di Tiongkok Daratan memulai permintaan dengan bidang referer yang memuat `1.1.1.1`, yang cocok dengan daftar izin yang dikonfigurasi untuk Tiongkok Daratan, konten yang diminta akan langsung dikembalikan.
2. Jika pengguna di luar Tiongkok Daratan memulai permintaan dengan referer kosong, yang cocok dengan daftar blokir yang dikonfigurasi untuk wilayah di luar Tiongkok Daratan, kode status 403 akan dikembalikan.

