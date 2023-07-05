## Ikhtisar Konfigurasi

CDN Tencent Cloud mendukung konfigurasi aturan daftar blokir/daftar izin User-Agent (UA) untuk kontrol akses.
CDN memeriksa bidang `User-Agent` di header permintaan HTTP berdasarkan aturan untuk mengizinkan atau menolak permintaan akses pengguna.

## Panduan Konfigurasi

### Batasan konfigurasi

- Daftar blokir dan daftar izin tidak dapat diatur secara bersamaan. Silakan tetapkan aturan daftar blokir atau aturan daftar izin.
- Jumlah maksimum aturan daftar blokir/daftar izin: 10
- Aturan mendukung kartubebas `*`. Silakan pisahkan beberapa nilai dengan `|`.
- Jenis efek yang didukung: semua konten, ekstensi file, direktori file, dan file tertentu. Pencocokan reguler saat ini tidak didukung.

### Petunjuk konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, lalu klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Pilih tab **Access Control** (Kontrol Akses) untuk menemukan konfigurasi daftar blokir/daftar izin UA, yang dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/07914bd30b3d422fb4bddf3a323d92f2.png)
Saat switch dinonaktifkan, klik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan daftar blokir/daftar izin satu per satu:
![](https://main.qcloudimg.com/raw/66d3fc72f575efaa4ae42382d8fde179.png)

>!
>1. Hanya kartubebas `*` yang didukung; karakter reguler lainnya tidak didukung.
>2. Jika tidak ada `*`, semua karakter akan digunakan untuk pencocokan persis.

Konfigurasi keseluruhan akan dinonaktifkan setelah aturan ditambahkan sehingga layanan yang sedang berjalan tidak akan terpengaruh:
![](https://main.qcloudimg.com/raw/679129885ec36329178e87af671d6743.png)
Anda dapat mengaktifkan switch untuk men-deploy secara resmi daftar blokir/daftar izin UA yang dikonfigurasi.
![](https://main.qcloudimg.com/raw/fd85de8e702b24e7d2eaaf8b34667c95.png)

## Sampel Konfigurasi

Konfigurasi daftar blokir/daftar izin dari `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/c7e06060bc627aab2e4939b53460951d.png)
Jika `User-Agent` di header permintaan HTTP adalah sebagai berikut:

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.61 Safari/537.36
```

Daftar blokir akan di-hit dan kesalahan 403 akan langsung dikembalikan.

