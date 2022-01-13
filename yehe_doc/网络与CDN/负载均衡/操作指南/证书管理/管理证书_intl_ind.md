Ketika mengonfigurasi listener HTTPS pada instance CLB, Anda dapat langsung menggunakan sertifikat di SSL Certificate Service atau mengunggah sertifikat server dan [sertifikat SSL](https://intl.cloud.tencent.com/document/product/1007/30152) yang diterbitkan oleh pihak ketiga CA untuk CLB.

## Persyaratan Sertifikat
CLB hanya mendukung sertifikat dalam format PEM.Sebelum mengunggah sertifikat, pastikan sertifikat, rantai sertifikat, dan kunci privat Anda memenuhi persyaratan format.Untuk persyaratan sertifikat, lihat [Format Sertifikat SSL](https://intl.cloud.tencent.com/document/product/214/5369).

### Mengonfigurasi Sertifikat
Konfigurasi sertifikat untuk listener HTTPS dibagi menjadi dua tipe berikut:
- Jika SNI tidak diaktifkan, sertifikat dapat dikonfigurasi pada tingkat listener, selama semua nama domain menggunakan sertifikat yang sama.Untuk informasi selengkapnya, lihat [Mengonfigurasi Listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).
- Jika SNI diaktifkan, sertifikat dapat dikonfigurasi pada tingkat nama domain, dan sertifikat lainnya dapat dikonfigurasi untuk nama domain lain dalam listener.Untuk informasi selengkapnya, lihat [Dukungan SNI untuk Mengikat Beberapa Sertifikat ke Satu Instance CLB](https://intl.cloud.tencent.com/document/product/214/19048).

## Memperbarui Sertifikat dalam Batch
Agar sertifikat yang kedaluwarsa tidak menghambat layanan Anda, silakan perbarui sertifikat sebelum sertifikat kedaluwarsa.
>?Setelah sertifikat diperbarui, sistem tidak akan menghapus sertifikat lama; tetapi akan membuat sertifikat baru.Sertifikat secara otomatis akan diperbarui untuk semua instance CLB yang menggunakannya.

1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Klik **Certificate Management** (Manajemen Sertifikat) di bilah sisi kiri.
3.Dalam daftar sertifikat di halaman **Certificate Management** (Manajemen Sertifikat), klik **Update** (Perbarui) pada kolom "Operation" (Operasi) di sebelah kanan sertifikat target.
4.Dalam kotak dialog "Create Certificate" (Buat Sertifikat) yang muncul, masukkan isi sertifikat dan isi kunci sertifikat baru, lalu klik **Submit** (Kirim).
![](https://main.qcloudimg.com/raw/d6534b57f4a33fab69b98fca4d1023f3.png)

## Menampilkan Instance CLB yang Terkait dengan Sertifikat
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Klik **Certificate Management** (Manajemen Sertifikat) di bilah sisi kiri.
3.Dalam daftar sertifikat pada halaman **Certificate Management** (Manajemen Sertifikat), klik ID sertifikat target.
4.Di halaman "Basic Info" (Info Dasar), tampilkan instance CLB yang terkait dengan sertifikat.
![](https://main.qcloudimg.com/raw/b3670e111ec8b9e1a43b9c7d2e870be3.png)
