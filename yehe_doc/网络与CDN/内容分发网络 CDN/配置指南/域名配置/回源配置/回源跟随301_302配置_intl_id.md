## Konfigurasi
CDN Tencent Cloud tidak meng-cache kode status 301/302 secara default. Saat server asal mengembalikan permintaan 301/302, simpul CDN akan mengembalikan respons ke klien secara default, dan klien akan dialihkan ke sumber daya yang sesuai untuk akses.

Saat konfigurasi pengalihan ikuti 301/302 diaktifkan, simpul CDN akan dialihkan saat menerima permintaan pengalihan 301/302 selama tarik-asal hingga mendapatkan sumber daya yang diperlukan (mendukung hingga 3 pengikut). Konfigurasi ini kemudian akan mengembalikan sumber daya yang sebenarnya ke klien, yang tidak perlu dialihkan.
## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk mengakses halaman konfigurasinya. Di bawah tab **Origin Configuration** (Konfigurasi Asal), temukan **Follow 301/302 Configuration** (Konfigurasi Ikuti 301/302), yang dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/3d431956857ef20b21bb954e481c66e4.png)

### Memodifikasi konfigurasi
Anda dapat mengaktifkan switch konfigurasi pengalihan ikuti 301/302 berikut untuk mengaktifkan atau menonaktifkan fitur ini:
![](https://main.qcloudimg.com/raw/cbbd0f472a50287fd425cd093a2dacb9.png)

>Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global, konfigurasi pengalihan ikuti 301/302 berikut akan diterapkan secara global. Konfigurasi ini tidak membedakan antara permintaan dari dan di luar Tiongkok daratan.

## Sampel Konfigurasi
Misalkan konfigurasi pengalihan ikuti 301/302 untuk nama domain `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/cbbd0f472a50287fd425cd093a2dacb9.png)
Pengguna A meminta sumber daya `http://cloud.tencent.com/1.jpg`. Jika cache tidak mengenai hit pada simpul, simpul akan meminta sumber daya dari server asal. Jika kode status respons HTTP yang dikembalikan oleh server asal adalah 302 dan alamat pengalihannya adalah `http://cloud.tencent.com/1.jpg`,:

1. Setelah pengalihan ikuti 301/302 diaktifkan, simpul akan langsung memulai permintaan ke alamat pengalihan ketika menerima respons HTTP dengan kode status 301/302.
2. Sumber daya akan diperoleh, di-cache ke simpul, dan dikembalikan ke pengguna.
3. Saat ini, jika pengguna B juga mengirimkan permintaan untuk `http://cloud.tencent.com/1.jpg`, cache akan mengenai hit pada simpul dan sumber daya akan dikembalikan ke pengguna.
4. Setelah pengalihan ikuti 301/302 diaktifkan, hingga 3 pengikut diizinkan. Jika batas ini terlampaui, kode status 301/302 akan dikembalikan ke pengguna.

Misalkan konfigurasi pengalihan ikuti 301/302 untuk nama domain `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/3d431956857ef20b21bb954e481c66e4.png)
Pengguna A meminta sumber daya `http://cloud.tencent.com/1.jpg`. Jika cache tidak mengenai hit pada simpul, simpul akan meminta sumber daya dari server asal. Jika kode status respons HTTP yang dikembalikan oleh server asal adalah 301/302 dan alamat pengalihan adalah `http://xxx.tencent.com/1.jpg`,:
1. Simpul akan langsung mengembalikan respons HTTP ke pengguna.
2. Saat pengguna memulai permintaan untuk `http://xxx.tencent.com/1.jpg`, akselerasi tidak akan diterapkan jika nama domain tidak terhubung ke CDN.
3. Saat ini, jika pengguna B juga mengirimkan permintaan `http://cloud.tencent.com/1.jpg`, proses di atas akan diulang.

