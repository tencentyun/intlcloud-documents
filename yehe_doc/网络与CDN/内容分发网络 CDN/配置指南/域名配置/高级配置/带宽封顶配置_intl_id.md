
## Ikhtisar Konfigurasi

CDN Tencent Cloud adalah layanan yang dibayar sesuai pemakaian. Jika Anda khawatir tentang penggunaan bandwidth yang berlebihan dan lonjakan biaya karena serangan hotlink oleh pengguna yang berniat buruk, Anda dapat mengatur batas pemakaian bandwidth untuk mengontrol penggunaan. Fitur ini hanya berlaku untuk pengguna ditagih per bandwidth.

Konfigurasi batas pemakaian bandwidth dapat mendeteksi bandwidth yang dihasilkan dalam periode statistik (pada perincian 5 menit) dan melakukan tarik-asal paksa sesuai dengan konfigurasi atau menonaktifkan layanan CDN (kesalahan 404 akan dikembalikan untuk semua permintaan) jika melebihi batas pemakaian tersebut. Ini akan menghindari timbulnya biaya akselerasi CDN tambahan.

>! Konfigurasi batas pemakaian bandwidth membutuhkan waktu sekitar 10 menit untuk diterapkan, selama konsumsi yang dihasilkan dikenakan biaya.

## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Buka tab **Advanced Configuration** (Konfigurasi Lanjutan) untuk melihat bagian **Bandwidth Cap Configuration** (Konfigurasi Batas Pemakaian Bandwidth). Ini dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/2dc4d64a3c1f4054471a31681c19765e.png)
### Memodifikasi konfigurasi
#### 1. Memodifikasi konfigurasi
Anda dapat mengaktifkan switch untuk mengonfigurasi batas pemakaian bandwidth:
- Untuk nama domain dengan asal COS, mengembalikan kesalahan 404 adalah satu-satunya pilihan saat batas pemakaian tercapai.
- Jika bandwidth nama domain yang terdeteksi melebihi batas pemakaian, tarik-asal atau kembalinya kesalahan 404 untuk akses perlu diimplementasikan di seluruh jaringan simpul demi simpul; oleh sebab itu, penundaan tertentu mungkin terjadi agar konfigurasi dapat diterapkan.

![](https://main.qcloudimg.com/raw/7520963775f790d2adaf588b9418bd7c.png)

#### 2. Menonaktifkan konfigurasi
Anda dapat menonaktifkan fitur ini secara langsung. Saat dinonaktifkan, konfigurasi ini tidak diterapkan di lingkungan produksi. Jika Anda mengaktifkan switch, konfigurasi akan diterapkan di seluruh jaringan setelah tindakan dikonfirmasi.
![](https://main.qcloudimg.com/raw/1a18d747e269347c90aa17f116601509.png)

#### 3. Menambahkan konfigurasi khusus wilayah
Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global dan Anda ingin mengonfigurasi akselerasi di dalam dan di luar Tiongkok Daratan dengan pengaturan batas pemakaian bandwidth yang berbeda, Anda dapat mengeklik **Add Special Configuration** (Tambahkan Konfigurasi Khusus).
![](https://main.qcloudimg.com/raw/ee63c14e4bcbd38899e8d9c063499db9.png)

>!
>
>- Saat ini, item konfigurasi khusus wilayah tidak dapat dihapus setelah ditambahkan, tetapi item tersebut dapat dinonaktifkan.


## Sampel Konfigurasi
Jika konfigurasi batas pemakaian bandwidth dari nama domain akselerasi `cloud.tencent.com` adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/772256e11f3c1c9a85ae9cc57315c4f6.png)
Maka akses aktualnya adalah sebagai berikut:
Jika bandwidth mencapai 11 Gbps di Tiongkok Daratan dan 4 Gbps di luar Tiongkok Daratan, kesalahan 404 akan dikembalikan untuk permintaan akses dari semua pengguna di Tiongkok Daratan, sedangkan pengguna di luar Tiongkok Daratan tetap dapat menikmati layanan akselerasi.

