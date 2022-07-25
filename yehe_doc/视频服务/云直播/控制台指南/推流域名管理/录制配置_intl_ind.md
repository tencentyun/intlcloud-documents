Fitur perekaman dinonaktifkan secara default untuk push CSS. Dokumen ini menjelaskan cara mengikat templat perekaman ke nama domain push yang ditentukan guna mengaktifkan fitur perekaman dan cara melepaskan ikatan templat setelah pengikatan berhasil dilakukan guna menonaktifkan fitur tersebut.

[](id:limit)
## Batasan Penggunaan
- File video yang direkam disimpan di [konsol VOD](https://console.cloud.tencent.com/vod/overview) secara default. Anda sebaiknya mengaktifkan layanan VOD terlebih dahulu dan membeli paket sumber daya yang sesuai untuk mencegah penangguhan layanan karena keterlambatan pembayaran. Informasi selengkapnya dapat dilihat di [Getting Started with VOD (Langkah Awal Memulai Penggunaan VOD)](https://intl.cloud.tencent.com/document/product/266/8757).
- Setelah fitur perekaman diaktifkan, pastikan layanan VOD Anda dalam status normal. Jika fitur perekaman tidak diaktifkan atau ditangguhkan karena keterlambatan pembayaran, perekaman CSS tidak akan tersedia, file rekaman tidak akan dibuat, dan biaya perekaman tidak akan dikenakan.
-  Konfigurasi templat akan diterapkan dalam waktu sekitar 5–10 menit. 
- Setelah templat berhasil diikat, fitur perekaman akan diaktifkan untuk alamat push di nama domain push yang ditentukan.
- Satu nama domain hanya dapat diikatkan ke satu templat perekaman. Setelah terikat, semua streaming di nama domain tersebut akan direkam sesuai dengan templat ini.
- Perekaman streaming campuran tidak mendukung pencampuran streaming di dalam dan di luar Tiongkok Daratan karena kesalahan file rekaman akan terjadi dan memengaruhi pemutaran ulang normal.

## Prasyarat
- Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live) dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Anda telah [membuat templat perekaman](https://intl.cloud.tencent.com/document/product/267/34223).


[](id:conect)
## Mengikat Templat Perekaman
1. 	Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain** (domain push) yang akan dikonfigurasi atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. 	Pilih tab **Template Configuration** (Konfigurasi Templat), lalu klik **Edit** di sudut kanan atas bagian **Recording Configuration** (Konfigurasi Perekaman).
![](https://qcloudimg.tencent-cloud.cn/raw/a56ed2f940b60babab0e2bbbe4eebaab.png)
3. Pilih templat konfigurasi perekaman dan klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/b4e5b04ee6e79636e52ae907556cd5d1.png)


[](id:unite)
## Melepaskan Ikatan Templat Perekaman
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **push domain** (domain push) yang akan dikonfigurasi atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Pilih tab **Template Configuration** (Konfigurasi Templat), lalu klik **Edit** di sudut kanan atas bagian **Recording Configuration** (Konfigurasi Perekaman).
3. Hapus templat target dan klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/ae44efc51b581100735c7faafe2414e8.png)

>? 
>- Melepaskan ikatan templat perekaman tidak akan memengaruhi streaming langsung yang sedang berjalan.
>- Agar pelepasan ikatan diterapkan, hentikan sementara streaming langsung yang sedang berjalan dan lakukan push lagi pada streaming. Streaming langsung baru tidak akan menghasilkan file rekaman.


[](id:get_record)
## Mendapatkan File Rekaman
File rekaman yang dibuat secara otomatis disimpan di sistem VOD dan dapat diperoleh dengan cara berikut:

### Konsol VOD
Masuk ke konsol VOD, pilih dan masukkan subaplikasi target, lalu klik **[Media Assets](https://console.cloud.tencent.com/vod/media)** (Aset Media) di sebelah kiri untuk menelusuri semua file rekaman.
![](https://main.qcloudimg.com/raw/b41dc459807ac1986d1db04032ea7942.png)
 
### Pemberitahuan peristiwa perekaman
URL panggilan balik perekaman dapat diatur di konsol atau melalui panggilan API. Pemberitahuan akan dikirim ke alamat panggilan balik setelah file rekaman dibuat. Setelah itu, Anda dapat mempelajari [konten protokol panggilan balik](https://intl.cloud.tencent.com/document/product/267/31566) untuk perekaman untuk mengetahui langkah selanjutnya yang harus diambil.
>?Mekanisme pemberitahuan peristiwa efisien, andal, dan real-time. Oleh karena itu, kami menyarankan Anda menggunakan metode panggilan balik untuk mendapatkan file rekaman.

### Kueri API VOD
Informasi lebih lanjut tentang cara melakukan kueri dan memfilter file rekaman dapat dilihat di [SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179).
