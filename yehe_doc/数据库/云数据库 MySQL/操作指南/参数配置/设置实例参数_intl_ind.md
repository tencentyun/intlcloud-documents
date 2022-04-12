
Anda dapat melihat dan mengubah parameter tertentu dan mengkueri log modifikasi parameter di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb).

## Catatan
- Untuk memastikan stabilitas instans, hanya beberapa parameter yang dapat dimodifikasi di konsol. Parameter ini ditampilkan di halaman **Parameter Settings** (Pengaturan Parameter).
- Jika parameter yang dimodifikasi memerlukan instans mulai ulang untuk diterapkan, sistem akan menanyakan apakah Anda ingin memulai ulang. Sebaiknya Anda melakukannya selama jam tidak sibuk dan memastikan bahwa aplikasi Anda memiliki mekanisme koneksi ulang.
- Jika Anda ingin kembali ke rumus default, hapus parameter yang dimasukkan dan terapkan.

## Memodifikasi Parameter dalam Daftar Parameter
### [Memodifikasi parameter dalam batch](id:plxgcs)
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Batch Modify Parameters** (Modifikasi Parameter Secara Massal).
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. Temukan parameter yang diinginkan, dan modifikasi nilainya di kolom **Current Value** (Nilai Saat Ini). Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Confirm Modification** (Konfirmasi Modifikasi).
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. Di jendela pop-up, pilih **execution mode** (mode eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
>

### [Memodifikasi satu parameter](id:xgdgcs)
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter), cari parameter yang diinginkan di daftar parameter dan klik <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> di kolom **Current Value** (Nilai Saat Ini).
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. Modifikasi nilai dalam batasan yang dinyatakan di kolom **Acceptable Values** (Nilai yang Dapat Diterima) dan klik <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> untuk menyimpan modifikasi. Anda dapat mengeklik <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> untuk membatalkan operasi.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. Di jendela pop-up, pilih **execution mode** (mode eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Memodifikasi Parameter dengan Mengimpor Templat Parameter
### Opsi 1. Mengimpor templat parameter di halaman "Pengaturan Parameter"
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman pengelolaan instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Custom Template** (Templat Kustom). (Jika Anda belum mengonfigurasi templat kustom yang umum digunakan, Anda dapat memilih **Custom Template** (Templat Kustom) di bilah sisi kiri di konsol TencentDB for MySQL, klik **Create Template** (Buat Templat) untuk mengonfigurasi templat parameter, lalu impor dari templat kustom seperti yang dijelaskan pada langkah 2.)
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. Di jendela pop-up, pilih templat parameter dan klik **Import and Overwrite Original Parameters** (Impor dan Timpa Parameter Asli).
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Confirm Modification** (Konfirmasi Modifikasi).
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. Di jendela pop-up, pilih **execution mode** (mode eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
>

### Opsi 2. Memodifikasi parameter dengan mengimpor file konfigurasi parameter
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Import Parameters** (Impor Parameter).
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. Klik **Select File** (Pilih File) untuk mencari file parameter yang diinginkan dan klik **Import and Overwrite Original Parameters** (Impor dan Timpa Parameter Asli).
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. Setelah mengonfirmasi bahwa semuanya sudah benar, klik **Confirm Modification** (Konfirmasi Modifikasi).
5. Di jendela pop-up, pilih **execution mode** (mode eksekusi) dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).


### Opsi 3. Mengimpor templat parameter pada halaman "Templat Parameter"
Untuk informasi selengkapnya, lihat [Mengelola Templat Parameter > Menerapkan Templat Parameter ke Database](https://intl.cloud.tencent.com/document/product/236/31906).

## Memulihkan ke Templat Default
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter), klik **Default Template** (Templat Default), pilih **High-Stability Template** (Templat Stabilitas Tinggi) atau **High-Performance Template** (Templat Performa Tinggi), dan klik **Import and Overwrite Original Parameter** (Impor dan Timpa Parameter Asli).
![](https://qcloudimg.tencent-cloud.cn/raw/030f986ea488796d5c084cb97aec5d6b.png)
3. Klik **Confirm Modification** (Konfirmasi Modifikasi) untuk mengalihkan ke periode konfirmasi modifikasi parameter.
![](https://qcloudimg.tencent-cloud.cn/raw/5ba2e9ba71f33211db43637e0aed8f37.png)
4. Di jendela pop-up, pilih **execution mode** (mode eksekusi), baca dan tunjukkan izin Anda terhadap **restart rules** (aturan mulai ulang), dan klik **OK** (OKE).
>?
>- Jika Anda memilih **Immediate execution** (Eksekusi langsung), tugas modifikasi parameter akan dijalankan dan segera berlaku.
>- Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
>

## Rumus Parameter
Anda dapat menggunakan rumus untuk mengatur parameter instans. Untuk melakukannya, atur parameter yang terkait dengan spesifikasi instans sebagai rumus, dan ketika spesifikasi instans diubah, nilai parameter dalam rumus akan berubah secara dinamis dan tetap berlaku setelah perubahan spesifikasi. Dengan cara ini, instans selalu dalam kondisi optimal untuk menjalankan bisnis dengan lancar.

Mengambil nilai `{DBinitMemory\*786432}` dari parameter `innodb_buffer_pool_size` sebagai contoh, ketika `DBinitMemory` dalam spesifikasi instans diubah, konfigurasi parameter di sini tidak perlu diubah, dan nilai `innodb_buffer_pool_size` akan diubah secara otomatis.
![](https://qcloudimg.tencent-cloud.cn/raw/696a0d3be52c058124f7c678a18e6b27.png)

Sintaksis ekspresi didukung sebagai berikut:

| Jenis yang Didukung | Deskripsi | Contoh |
| -------- | ------------------------------------------------------------ | --------------------- |
| Variabel   | <li>DBinitMemory: ukuran memori dari spesifikasi instans, yang merupakan bilangan bulat. Misalnya, jika ukuran memori spesifikasi instans adalah 4.000 MB, nilai `DBinitMemory` akan menjadi 4000.<li>DBInitCpu: jumlah inti CPU spesifikasi instans, yang merupakan bilangan bulat. Nilai parameter `innodb_buffer_pool_size` di TencentDB for MySQL harus antara 50% dan 90% dari ukuran memori. Jika nilai yang dikonfigurasi di atas 90% atau di bawah 50%, itu akan secara otomatis dikonversi menjadi 90% atau 50% masing-masing. | {DBinitMemory*786432} |
| Operator | Sintaksis rumus: harus diapit dalam kurung kurawal (`{}`).  <li>Operator pembagian (/): ini membagi dividen dengan pembagi dan mengembalikan hasil bagi bilangan bulat. Jika hasil perhitungan adalah angka desimal, hanya bagian bilangan bulat yang akan dipertahankan. Angka desimal tidak didukung; misalnya, `{MIN(DBInitMemory/4+500,1000000)}` bukan `{MIN(DBInitMemory\*0.25+500,1000000)}` didukung.<li>Operator perkalian (*): operator ini mengalikan dua angka dan menampilkan produk bilangan bulat. Jika hasil perhitungan adalah angka desimal, hanya bagian bilangan bulat yang akan dipertahankan. Perhitungan angka desimal tidak didukung. |  -                     |
| Fungsi | <li>MAX(): mengembalikan nilai terbesar dalam bilangan bulat atau daftar rumus parameter. <li>MIN(): mengembalikan nilai terkecil dalam bilangan bulat atau daftar rumus parameter.</li> | {MAX(DBInitCpu/2,4)}  |


## Mengekspor Konfigurasi Parameter sebagai File
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Export Parameters** (Ekspor Parameter) untuk mengekspor file konfigurasi parameter.
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## Mengekspor Konfigurasi Parameter sebagai Templat
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter) dan klik **Save as Template** (Simpan sebagai Templat) untuk menyimpan konfigurasi parameter yang ada sebagai templat parameter.
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## Menyesuaikan Periode Waktu untuk Menerapkan Modifikasi Parameter
Sebelum Anda mengonfirmasi modifikasi parameter, kotak dialog "Modify Parameters" (Ubah Parameter) akan muncul agar Anda dapat memilih periode waktu khusus agar modifikasi diterapkan.
>?Jika Anda memilih **During maintenance time** (Selama waktu pemeliharaan), tugas modifikasi parameter akan dijalankan dan berlaku selama [waktu pemeliharaan instans](https://intl.cloud.tencent.com/document/product/236/10929).
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)

## Membatalkan Tugas Modifikasi Parameter
Jika tugas modifikasi parameter atau modifikasi batch telah dikirimkan tetapi Anda ingin membatalkannya, Anda dapat memilih **[Task List](https://console.cloud.tencent.com/mysql/task)** ([Daftar Tugas]) di bilah sisi kiri di konsol, menemukan tugas, dan mengklik **Cancel** (Batal) di kolom **Operation** (Operasi). Anda dapat membatalkan tugas hanya sebelum dijalankan. Status tugas harus **Waiting for execution** (Menunggu dijalankan).
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)

## Melihat Log Modifikasi Parameter
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb), klik ID instans di daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Database Management** (Manajemen Database) > **Parameter Settings** (Pengaturan Parameter), klik **Recent Modifications** (Modifikasi Saat Ini) di sebelah kanan.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. Anda dapat melihat catatan modifikasi parameter terbaru di sini.

## Operasi Selanjutnya
- Anda dapat menggunakan templat untuk mengelola parameter database dalam batch. Untuk informasi selengkapnya, lihat [Mengelola Templat Parameter](https://intl.cloud.tencent.com/document/product/236/31906).
- Untuk saran konfigurasi parameter utama, lihat [Saran tentang Pengaturan Parameter](https://intl.cloud.tencent.com/document/product/236/38056).

