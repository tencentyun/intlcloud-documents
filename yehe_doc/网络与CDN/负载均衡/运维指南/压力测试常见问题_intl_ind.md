Berdasarkan pengalaman pelanggan dalam pengujian tekanan, dokumen ini merangkum permasalahan umum kinerja dalam pengujian tekanan serta memberikan solusi dan saran penanggulangan masalah.

## Pertanyaan Umum Seputar Pengujian Tekanan

### 1.Akses jaringan publik tidak diaktifkan di server asli
Jika akses jaringan publik tidak diaktifkan ketika Anda membeli CVM, penerusan bisa gagal ketika CLB jaringan publik dipasang di instance CVM.
### 2.Bandwidth dari server asli tidak cukup
Jika bandwidth-nya rendah, server asli tidak dapat mengembalikan paket ke CLB ketika ambang batas terlampaui.CLB akan mengembalikan kesalahan 504 atau 502 kepada klien.
### 3.Port klien tidak cukup
Jika jumlah klien terlalu kecil atau rentang port klien terlalu sempit, port klien menjadi tidak cukup dan koneksi akan gagal dibuat.Selain itu, jika nilai `keep_alive` lebih besar daripada 0 ketika koneksi persisten sudah jadi, koneksi akan menggunakan port secara permanen sehingga mengurangi jumlah port klien yang tersedia.
### 4.Aplikasi yang menjadi andalan server asli mengalami masalah kinerja
Setelah permintaan sampai di server asli melalui CLB, muatan di server asli menjadi normal.Meskipun demikian, karena aplikasi di server asli juga mengandalkan aplikasi lain seperti database, masalah kinerja di dalam database juga dapat memengaruhi kinerja pengujian tekanan.
### 5.Server asli tidak sehat
Status kesehatan server asli bisa diabaikan dalam pengujian tekanan.Jika server asli mengalami kegagalan pemeriksaan kesehatan atau status pemeriksaan kesehatan tidak stabil (kadang-kadang bagus, kadang-kadang buruk dengan perubahan cepat), kinerja pengujian tekanan bisa buruk.
### 6.Persistensi sesi yang diaktifkan untuk CLB mengakibatkan distribusi lalu lintas yang tidak merata di antara server asli
Setelah persistensi sesi diaktifkan untuk CLB, permintaan bisa didistribusikan kepada server asli tetap.Distribusi lalu lintas menjadi tidak merata sehingga memengaruhi kinerja pengujian tekanan.Anda sebaiknya menonaktifkan persistensi sesi selama pengujian tekanan.

## Saran untuk pengujian tekanan
>Konfigurasi berikut hanya digunakan untuk pengujian tekanan CLB.Anda tidak harus memilikinya di lingkungan produksi Anda.

- Anda sebaiknya menggunakan koneksi tidak persisten ketika tekanan menguji kemampuan meneruskan dari CLB.
Selain verifikasi terhadap fitur persistensi sesi, pengujian tekanan biasanya didesain untuk memverifikasi kemampuan meneruskan dari CLB.Oleh karena itu, koneksi tidak persisten dapat digunakan untuk menguji kemampuan pemrosesan CLB dan server asli.
- Anda sebaiknya menggunakan koneksi persisten untuk melakukan pengujian tekanan terhadap throughput CLB, seperti batas atas bandwidth dan layanan koneksi persisten.
Anda sebaiknya menyesuaikan periode waktu habis alat pengujian tekanan ke nilai yang kecil.Jika tidak, rata-rata waktu respons akan meningkat ketika periode waktu habis juga meningkat sehingga membuat Anda tidak dapat dengan cepat menilai tercapai tidaknya level tekanan.
- Anda sebaiknya menggunakan situs web statis yang disediakan oleh server asli untuk pengujian tekanan guna menghindari kerugian akibat logika aplikasi, seperti I/O dan DB.
- Nonaktifkan persistensi sesi untuk pendengar.Jika tidak, tekanan akan terkonsentrasi pada server asli tertentu.Jika kinerja tekanan tidak memuaskan, Anda dapat menetapkan merata tidaknya distribusi lalu lintas dengan memeriksa data pemantauan server asli di CLB.
- Nonaktifkan pemeriksaan kesehatan untuk pendengar agar dapat mengurangi permintaan akses ke server asli yang muncul selama pemeriksaan kesehatan.
- Gunakan beberapa klien (> 5) untuk pengujian tekanan.IP sumber yang tersebar dapat meniru kondisi online aktual dengan lebih baik.
