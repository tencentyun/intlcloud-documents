Persistensi sesi bisa meneruskan permintaan dari IP yang sama ke server asli yang sama.Secara default, instance CLB akan mengarahkan permintaan ke server asli berbeda untuk penyeimbangan beban; tetapi Anda bisa menggunakan persistensi sesi untuk mengarahkan permintaan dari pengguna tertentu ke server asli yang sama sehingga beberapa aplikasi yang harus menyimpan sesinya (seperti keranjang belanja) bisa berjalan lancar.

## Persistensi Sesi Lapisan 4
Protokol lapisan 4 (TCP/UDP) mendukung persistensi sesi berbasis IP sumber.Durasi persistensi sesi bisa diatur ke integer berapa pun antara 30 dan 3600 detik.Jika ambang batas waktu terlampaui dan tidak ada permintaan baru di sesi, persistensi sesi akan berakhir.Persistensi sesi bergantung pada mode penyeimbangan beban:
- Dalam mode "round-robin tertimbang" tempat permintaan didistribusikan sesuai bobot server asli, persistensi sesi berdasarkan IP source didukung.
- Dalam mode "koneksi terkecil tertimbang" tempat penjadwalan keseluruhan bergantung pada beban dan bobot server, persistensi sesi tidak didukung.

## Persistensi Sesi Lapisan 7
Protokol lapisan 7 (HTTP/HTTPS) mendukung persistensi sesi berdasarkan penyisipan cookies (CLB menyisipkan cookie ke klien).Durasi persistensi sesi bisa diatur ke nilai berapa pun antara 30 dan 3600 detik.Persistensi sesi bergantung pada mode penyeimbangan beban:
- Dalam mode "round-robin tertimbang" tempat permintaan didistribusikan sesuai bobot server asli, persistensi sesi berdasarkan penyisipan cookies didukung.
- Dalam mode "koneksi terkecil tertimbang" tempat penjadwalan keseluruhan bergantung pada beban dan bobot server, persistensi sesi tidak didukung.
- Mode "IP Hash" mendukung persistensi sesi berdasarkan pada IP sumber, tetapi tidak pada penyisipan cookie.

## Periode Waktu Habis Koneksi
Saat ini, periode waktu habis koneksi HTTP (`keepalive_timeout`) adalah 75s secara default.Jika Anda ingin mengubahnya, silakan aktifkan [konfigurasi khusus](https://intl.cloud.tencent.com/document/product/214/32427).Jika ambang batas terlampaui dan tidak ada transmisi data di sesi, koneksi akan diputus.
Saat ini, periode waktu habis koneksi TCP adalah 900s secara default dan tidak bisa diubah.Jika ambang batas terlampaui dan tidak ada transmisi data di sesi, koneksi akan diputus.

## Mengonfigurasi Persistensi Sesi
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance) dan klik ID instance CLB yang akan dikonfigurasikan dengan persistensi sesi untuk masuk ke halaman detailnya.
2.Pilih tab **Listener Management** (Manajemen Pendengar).
3.Klik **Modify** (Modifikasi) setelah pendengar CLB untuk dikonfigurasikan dengan persistensi sesi.
4.Pilih apakah akan mengaktifkan fitur persistensi sesi.Klik tombol untuk mengaktifkannya, masukkan durasi persistensinya, dan klik **OK**.

## Hubungan Antara Koneksi Persisten dan Persistensi Sesi

### Skenario 1.Bisnis lapisan 7 HTTP

**Dengan asumsi klien mengakses protokol HTTP/1.1 dan `Connection:keep-alive` dikonfigurasi di informasi header.Klien mengakses CVM melalui instance CLB tanpa mengaktifkan persistensi sesi.Apakah klien bisa mengakses CVM yang sama kali berikutnya?**

**J:** tidak.

Pertama, keep-alive HTTP menandakan koneksi TCP tetap tersambung setelah permintaan dikirimkan sehingga peramban bisa mengirimkan permintaan melalui koneksi yang sama.Koneksi persisten mengurangi waktu yang dibutuhkan untuk membuat koneksi baru untuk setiap permintaan dan mengurangi konsumsi bandwidth.Periode waktu habis default kluster CLB adalah 75s (jika tidak ada permintaan baru dalam 75s, sambungan TCP akan diputuskan secara default).

Keep-alive HTTP dibuat antara klien dan instance CLB.Jika persistensi sesi cookie dinonaktifkan, instance CLB akan memilih acak instance CVM sesuai kebijakan polling.Koneksi persisten sebelumnya sudah tidak berlaku.

Oleh karena itu, kami menyarankan Anda untuk mengaktifkan persistensi sesi.

Jika periode persistensi sesi cookie dikonfigurasi pada 1000s, klien akan memulai permintaan lagi.Karena periode antara dua permintaan melebihi 75s, koneksi TCP harus dibuat lagi.Layer aplikasi mengidentifikasi cookie dan menemukan instance yang diakses klien terakhir kali, jadi akan diakses lagi kali ini.

### Skenario 2.Bisnis lapisan 4 TCP
**Dengan asumsi klien memulai akses, TCP adalah protokol layar transportasi, koneksi persisten diaktifkan, tetapi persistensi sesi berdasarkan IP sumber dinonaktifkan.Apakah klien yang sama bisa mengakses server yang sama dengan permintaan akses berikutnya?**

**J:** belum tentu.

Pertama, menurut mekanisme implementasi lapisan 4, saat koneksi persisten diaktifkan untuk TCP dan tidak ditutup, dan koneksi yang sama diakses dalam dua permintaan, maka klien yang sama bisa mengakses server yang sama.Jika koneksi ditutup karena suatu alasan (seperti mulai ulang jaringan atau waktu koneksi habis) dalam permintaan akses kedua, permintaan itu bisa dijadwalkan ke server asli lainnya.Periode waktu habis global default untuk koneksi persisten adalah 900s, artinya, koneksi persisten akan dilepaskan jika tidak ada permintaan baru dalam 900s.
