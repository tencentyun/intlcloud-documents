Selain templat parameter sistem yang disediakan oleh TencentDB for Redis, Anda dapat membuat templat parameter kustom untuk mengonfigurasi parameter secara berkelompok sesuai kebutuhan.

Anda dapat menggunakan templat parameter untuk mengonfigurasi dan mengelola parameter mesin database. Templat seperti kontainer nilai parameter mesin database, yang dapat diterapkan ke satu atau beberapa instans TencentDB.

Templat parameter mendukung fitur berikut:
- Mendukung templat parameter default.
- Membuat templat kustom dengan memodifikasi parameter default.
- Menyimpan konfigurasi parameter sebagai templat.
- Mengimpor parameter dari templat untuk diterapkan ke satu atau beberapa instans.
>!
>- Instans yang sudah menggunakan templat parameter tidak akan memperbarui parameternya saat templat parameter diperbarui, jadi Anda perlu memperbarui parameter instans secara manual secara berkelompok.
>- Untuk menerapkan parameter baru ke sekelompok instans, Anda dapat mengimpor templat yang menyertakan parameter baru ini dan menerapkan templat ke beberapa instans.

## Membuat Templat Parameter Kustom
Anda dapat membuat templat parameter, mengubah nilai parameter, dan menerapkan templat ke instans.

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, dan klik **Create Template** (Buat Templat).
![](https://qcloudimg.tencent-cloud.cn/raw/4f5eabc8bba157d095e430ca8d2c5e28.png)
2. Di kotak dialog pop-up, tentukan konfigurasi berikut, dan klik **Create and Set Parameters** (Buat dan Atur Parameter).
 - **Template Name** (Nama Templat): masukkan nama templat yang unik.
 - **Database Version** (Versi Database): pilih versi database.
 - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/ce72179be683129ed8d0884e60ef5e0c.png)
3. Pada halaman konfigurasi parameter yang ditampilkan, pastikan semua nilai parameter sudah benar dan templat parameter berhasil dibuat.
![](https://qcloudimg.tencent-cloud.cn/raw/d55f34b4c0f297c6043f1fac730cb7d7.png)

## Templat Default
Halaman ini menampilkan templat default yang berlaku untuk arsitektur standar Redis 2.8, arsitektur standar Redis 4.0, arsitektur klaster Redis 4.0, arsitektur standar Redis 5.0, dan arsitektur klaster Redis 5.0.
![](https://qcloudimg.tencent-cloud.cn/raw/8886085e6cb3cb394f362804a16dad17.png)

>!Pada halaman **Default Template** (Templat Default), Anda dapat mengeklik **View Details** (Lihat Detail) untuk melihat templat, tetapi pada halaman detail yang ditampilkan, Anda tidak dapat melakukan operasi apa pun.

## Menerapkan Templat Parameter ke Instans
### Menerapkan ke instans yang ada
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri.
2. Dalam daftar templat parameter, cari templat yang diinginkan dan klik **Apply to Instance** (Terapkan ke Instans) di kolom **Operation** (Operasi). Atau, klik **View Details** (Lihat Detail), masuk ke halaman detail templat, dan klik **Apply to Instance** (Terapkan ke Instans).
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20211126165013163.png)
3. Pada halaman yang ditampilkan, tentukan mode eksekusi dan instans, pastikan semua nilai parameter sudah benar, lalu klik **Submit** (Kirim).
 - **Redis Instance** (Instans Redis): pilih satu atau beberapa instans yang perlu menerapkan templat parameter di wilayah yang ditentukan.
 - **Parameter Comparison** (Perbandingan Parameter): lihat nilai parameter yang diubah dari instans yang dipilih.
>!Sebelum menerapkan templat parameter ke beberapa instans, pastikan instans mendukung parameter tersebut.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5ba226d16856effb3a19b4dcc765a608.png)

### Menerapkan ke instans baru
Di [halaman pembelian instan](https://buy.intl.cloud.tencent.com/redis), pilih templat parameter default atau kustom untuk instans baru.
- Klik kotak pilihan di sebelah **Parameter Template** (Templat Parameter) dan daftar drop-down dengan kotak pencarian akan muncul. Daftar tersebut menunjukkan nama dan ID dari semua templat parameter yang ada.
- Masukkan nama atau ID templat parameter di kotak pencarian untuk mencari templat.

![](https://qcloudimg.tencent-cloud.cn/raw/44bdb23e6fcc01e1efdbb2d041d567ef.png)

## Menyalin Templat Parameter
Untuk menyertakan sebagian besar parameter dan nilai kustom dari templat parameter yang ada di templat baru, Anda dapat menyalin templat yang ada dan mengubahnya.

### Metode 1. Menyalin templat parameter yang ada
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di daftar templat, dan masuk ke halaman detail templat parameter.
2. Klik **Save as Template** (Simpan sebagai Templat).
3. Di kotak dialog pop-up, tentukan konfigurasi berikut: 
  - **Template Name** (Nama Templat): masukkan nama templat yang unik.
  - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Save** (Simpan).

### Metode 2. Menyimpan parameter instans sebagai templat parameter
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), pilih **Instance List** (Daftar Instans) di bilah sisi kiri, klik ID instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Parameter Settings** (Pengaturan Parameter), klik **Save as Template** (Simpan sebagai Templat).
3. Di kotak dialog pop-up, tentukan konfigurasi berikut: 
 - **Template Name** (Nama Templat): masukkan nama templat yang unik.
 - **Template Description** (Deskripsi Templat): masukkan deskripsi singkat tentang templat parameter.
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Create and Save** (Buat dan Simpan).
>!Templat default tidak mendukung fitur **Save as Template** (Simpan sebagai Templat).

## Memodifikasi Nilai Parameter dalam Templat Parameter
1. Login ke [konsol TencentDB for Redis(https://console.cloud.tencent.com/redis), pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri, klik nama templat parameter atau **View Details** (Lihat Detail) di kolom **Operation** (Operasi) di daftar templat, dan masuk ke halaman detail templat parameter.
2. Klik **Batch Modify Parameters** (Modifikasi Parameter Secara Massal) atau klik <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> di kolom **Current Value** (Nilai Saat Ini) untuk memodifikasi nilai parameter.
>!Templat default tidak mendukung fitur **Batch Modify Parameters**, (Modifikasi Parameter Secara Massal), dan kolom **Current Value** (Nilai Saat Ini) tidak dapat dimodifikasi.

## Menghapus Templat Parameter
Jika templat parameter dibuat secara berlebihan atau tidak lagi diperlukan, templat tersebut dapat dihapus dengan mudah.
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) and pilih **Parameter Templates** (Templat Parameter) di bilah sisi kiri.
2. Dalam daftar templat parameter, cari templat yang diinginkan dan klik **Delete** (Hapus) di kolom **Operation** (Operasi).
3. Klik **OK** (OKE) di kotak dialog pop-up.

