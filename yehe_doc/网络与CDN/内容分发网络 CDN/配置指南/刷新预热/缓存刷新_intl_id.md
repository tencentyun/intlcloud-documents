## Ikhtisar Fitur

CDN mampu mengonfigurasi cache dasar.Validitas cache dapat dikonfigurasi berdasarkan aturan seperti jenis layanan, direktori, dan URL tertentu yang ditentukan untuk membersihkan sumber daya yang di-cache pada simpul secara teratur, menarik sumber daya terbaru dari server asal, dan sumber daya tersebut di-cache lagi.

Selain itu, CDN dapat membersihkan cache untuk URL atau direktori tertentu dalam batch:

- Purge URL (Bersihkan URL): opsi ini menghapus cache sumber daya yang sesuai di semua simpul CDN.
- Purge directory (Bersihkan direktori): jika Anda memilih **Purge updated resources** (Bersihkan sumber daya yang diperbarui), saat pengguna akhir mengakses sumber daya di bawah direktori yang sesuai, informasi `Last-Modify` (Modifikasi Terakhir) dari sumber daya tersebut akan diambil dari server asal.Jika sama dengan sumber daya yang di-cache, sumber daya yang di-cache akan langsung dikembalikan; jika tidak, sumber daya yang diperbarui akan ditarik dari server asal dan di-cache lagi.Jika Anda memilih **Purge all resources** (Bersihkan semua sumber daya), saat pengguna mengakses sumber daya di bawah direktori yang sesuai, versi terbaru dari sumber daya tersebut akan langsung diambil dari server asal dan di-cache lagi.

>? Setelah pembersihan berhasil dijalankan, sumber daya yang sesuai pada simpul tidak akan memiliki cache yang valid.Ketika pengguna memulai permintaan akses lagi, simpul akan menarik sumber daya yang diperlukan dari server asal dan di-cache di simpul.Jika Anda mengirimkan sejumlah besar tugas pembersihan, banyak cache akan dihapus, yang mengakibatkan lonjakan permintaan tarik-asal dan tekanan tinggi pada server asal.

## Kasus Penggunaan

### Rilis sumber daya baru

Saat sumber daya ditimpa oleh sumber daya baru dengan nama yang sama di server asal, Anda dapat mengirimkan permintaan untuk membersihkan URL/direktori dan menghapus semua cache sehingga pengguna dapat langsung mengakses versi sumber daya terbaru.Ini akan mencegah pengguna mengakses versi sumber daya lama yang di-cache di simpul.

### Pembersihan sumber daya ilegal

Saat sumber daya ilegal (seperti sumber daya yang terkait dengan pornografi, narkoba, atau perjudian) ditemukan di server asal Anda, sumber tersebut mungkin masih dapat diakses bahkan setelah Anda menghapusnya di server asal karena cache simpul.Untuk melindungi keamanan lingkungan jaringan Anda, Anda dapat menghapus sumber daya yang di-cache melalui pembersihan URL.

## Petunjuk

### Cara penggunaan

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Purge and Pramuat** (Bersihkan dan Pramuat) di bilah samping kiri, dan kirimkan tugas **Purge URL** (Bersihkan URL) atau **Purge Directory** (Bersihkan Direktori).Anda dapat membersihkan URL/direktori CDN dan ECDN secara bersamaan.
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)
>? Jika fitur penyandian URL diaktifkan, karakter bahasa Mandarin akan dikonversi ke format yang disandikan URL selama pembersihan URL dan direktori.

<span ID = "catatan"></span>
Di tab **History** (Riwayat), Anda dapat membuat kueri tugas berdasarkan periode, kata kunci, dan jenis tugas yang ditentukan.Kueri kata kunci hanya mendukung kueri dengan nama domain atau URL/direktori lengkap yang dibersihkan:
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)

>? Konsol dapat mengembalikan hingga 10.000 log sekaligus, yang dapat diekspor ke file Excel.Jika Anda memiliki lebih dari 10.000 tugas pembersihan, silakan lakukan kueri dan ekspor tugas tersebut dalam batch.

### Tindakan pencegahan

**Pembersihan URL:**

- Hingga 10.000 URL dapat dihapus per hari untuk setiap akun dengan layanan akselerasi di dalam atau di luar Tiongkok Daratan, dan hingga 1.000 URL dapat dihapus sekaligus.Untuk setiap akun yang menggunakan layanan CDN global, kuota pembersihan harian untuk layanan akselerasi di dalam dan di luar Tiongkok Daratan masing-masing adalah 10.000 URL.
>?	
>- Saat Anda kehabisan kuota pembersihan harian, Anda dapat meningkatkannya sendiri di konsol CDN Tencent Cloud.
>- Kuota baru akan langsung diterapkan.Halaman akan disegarkan secara otomatis.Anda tidak perlu sering mengeklik tombol refresh (segarkan).
>- Kuota hanya dapat ditingkatkan sekali dalam sehari.
>- Peningkatan kuota di berbagai wilayah tidak tergantung satu sama lain.
- Anda perlu menambahkan pengidentifikasi protokol "http://" atau "https://" saat mengirimkan tugas pembersihan.
- URL dalam format "http://*.test.com/" tidak didukung.Bahkan jika Anda menghubungkan nama domain kartubebas ke CDN, Anda harus mengirimkan nama subdomain yang sesuai untuk melakukan pembersihan.
- Saat Anda mengirimkan URL untuk pembersihan, nama domain seharusnya sudah terhubung ke CDN; jika tidak, pengiriman akan gagal.
- Secara default, URL akan dihapus oleh wilayah akselerasi nama domain di URL.

**Pembersihan direktori:**

- Batas atas untuk pembersihan direktori adalah 100 direktori per akun per hari.Batas tersebut ditetapkan untuk layanan akselerasi di dalam dan di luar Tiongkok Daratan secara terpisah.Hingga 20 direktori dapat dibersihkan sekaligus.
- Anda perlu menambahkan pengidentifikasi protokol "http://" atau "https://" saat mengirimkan tugas pembersihan.
- Direktori dalam format "http://*.test.com/" tidak dapat dibersihkan.Bahkan jika Anda menghubungkan nama domain kartubebas ke CDN, Anda harus mengirimkan nama subdomain yang sesuai untuk melakukan pembersihan.
- Saat Anda mengirimkan URL untuk pembersihan, nama domain seharusnya sudah terhubung ke CDN; jika tidak, pengiriman akan gagal.

**Konfigurasi izin subpengguna:**

- Pembersihan direktori, pembersihan URL, dan kueri riwayat pembersihan telah diintegrasikan ke sistem izin terbaru dan konfigurasi izin dukungan di tingkat sumber daya (nama domain).
- Untuk metode penetapan izin, lihat [Izin Konsol](https://intl.cloud.tencent.com/document/product/228/35229).

## Kasus Penggunaan

### Pembersihan direktori - bersihkan sumber daya yang diperbarui

Nama domain akselerasi adalah `purge-test-1251991073.file.myqcloud.com`, server asal adalah Tencent Cloud Object Storage (COS), dan sumber daya di server asal adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)

1.Mulai permintaan untuk mengakses sumber daya `1.txt` dan `2.txt` secara berurutan.Simpul yang akan di-hit dapat ditentukan berdasarkan `X-Cache-Lookup: (Pencarian X-Cache:)Hit From Disktank3 (Hit Dari Disktank3)` dan `Server:NWS_SPMid`, sumber daya akan langsung dikembalikan oleh simpul:
![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2.Di server asal, ganti `1.txt` dengan file yang memiliki nama yang sama, dan waktu modifikasi terakhir file akan berubah, sedangkan `2.txt` tetap sama:
![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3.Mulai permintaan lagi.Karena cache belum kedaluwarsa, konten lama dari sumber daya `1.txt` akan diakses:
![](https://main.qcloudimg.com/raw/b5769a3d7fddaeadfda229115ac59bb8.png)
4.Kirim tugas pembersihan direktori, pilih **Purge updated resources** (Bersihkan sumber daya yang diperbarui), dan tunggu hingga pembersihan selesai:
![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5.Setelah pembersihan selesai, karena `Last-Modified` (Modifikasi Terakhir) dari `1.txt` telah diubah, permintaan akan diteruskan ke server asal.Karena `2.txt` belum diubah, bahkan setelah tugas pembersihan direktori dikirimkan, tugas itu akan tetap di-hit dan dikembalikan:
![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
