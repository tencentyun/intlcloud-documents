Dokumen ini membantu Anda mulai menggunakan Tencent Cloud Content Delivery Network (CDN).

## 1.Pengetahuan CDN Dasar

- [Bagaimana cara kerja CDN?] (https://intl.cloud.tencent.com/document/product/228/2939)
- [Mengapa Tencent Cloud CDN?](https://intl.cloud.tencent.com/document/product/228/2941)
- [Kasus penggunaan CDN] (https://intl.cloud.tencent.com/document/product/228/32980)
- [Apa saja batas penggunaan CDN?] (https://intl.cloud.tencent.com/document/product/228/32981)
- [Konsep dasar](https://intl.cloud.tencent.com/document/product/228/36183)



## 2.Cara Penagihan CDN

Tencent Cloud CDN memiliki dua cara penagihan: **penagihan-berdasarkan-bandwidth** dan **penagihan-berdasarkan-lalu-lintas**.Anda perlu memahami kedua cara penagihan CDN ini agar dapat memilih cara yang cocok untuk Anda.Untuk informasi selengkapnya, silakan baca [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949).






## 3.Memulai

#### 3.1.Aktifkan layanan dan pilih cara penagihan

Sebelum menggunakan CDN, Anda perlu mendaftar akun Tencent Cloud dan mengaktifkan layanan CDN.Untuk informasi selengkapnya, silakan baca [Mengonfigurasi CDN dari Nol](https://intl.cloud.tencent.com/document/product/228/32978).

#### 3.2.Buat koneksi nama domain

Anda perlu menambahkan nama domain akselerasi untuk layanan akselerasi Anda.Melalui nama domain akselerasi, CDN meng-cache sumber daya dari server asal ke simpul cache CDN yang terdekat dengan klien untuk mempercepat akses sumber daya.Untuk informasi selengkapnya, silakan baca [Menambahkan Nama Domain](https://intl.cloud.tencent.com/document/product/228/5734).

#### 3.3 Mengonfigurasi CNAME

Ketika distribusi dibuat, CDN akan menetapkan alamat CNAME yang sesuai kepada Anda yang perlu dikonfigurasi sebelum aktif.Untuk mendapatkan petunjuk lengkap, silakan lihat [Konfigurasi CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

>? Anda juga dapat mengikuti praktik terbaik berikut untuk mulai menggunakan CDN dan mempercepat nama domain Anda:
>- [Mempercepat akses ke CVM dengan CDN](https://intl.cloud.tencent.com/document/product/228/34035)
>- [Mempercepat akses ke COS dengan CDN](https://intl.cloud.tencent.com/document/product/228/34036)




## 4.Konsol

Berikut adalah halaman ikhtisar konsol CDN:
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)




## 5.Ikhtisar Fitur Konsol

<table>
<thead>
<tr>
<th>Operasi yang Dikehendaki</th>
<th>Dokumen Referensi</th>
</tr>
</thead>
<tbody><tr>
<td>Lihat, aktifkan, atau nonaktifkan nama domain akselerasi terkoneksi.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">Operasi Nama Domain</a></td>
</tr>
<tr>
<td>Filter dan lihat sumber daya Tencent Cloud atau kelola berdasarkan tanda, proyek, dll.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">Pencarian Nama Domain</a></td>
</tr>
<tr>
<td>Optimalkan efek akselerasi CDN Anda.CDN mendukung beragam konfigurasi khusus.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">Ikhtisar Konfigurasi</a></td>
</tr>
<tr>
<td>Lihat pemetaan antara fitur konsol dan nilai `Tindakan`.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">Izin Konsol</a></td>
</tr>
<tr>
<td>Dapatkan izin di level nama domain melalui pernyataan kebijakan khusus.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">Penyusunan Kebijakan</a></td>
</tr>
<tr>
<td>Dapatkan izin level-proyek yang berbeda.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">Izin Level-Proyek</a></td>
</tr>
<tr>
<td>Gunakan data pemantauan real-time untuk menganalisis status yang sedang aktif.</td>
<td><a href="https://cloud.tencent.com/document/product/228/30794" target="_blank">Pemantauan real-time</a></td>
</tr>
<tr>
<td>Lakukan analisis terhadap sumber, distribusi, dan penggunaan dari pengguna Anda.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">Analisis Data</a></td>
</tr>
<tr>
<td>Sumber daya pembersihan di-cache di simpul CDN secara rutin sehingga simpul tersebut akan menarik sumber daya versi terbaru dari server asal dan meng-cache-nya lagi.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">Bersihkan Cache</a></td>
</tr>
<tr>
<td>Muat sumber daya tertentu ke simpul cache terlebih dahulu.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">Pramuat Cache</a></td>
</tr>
<tr>
<td>Unduh log akses dan lakukan analisis terhadap sumber daya populer dan pengguna aktif sesuai kebutuhan.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">Unduh Log</a></td>
</tr>
<tr>
<td>Cari dan analisis data log Anda dengan cepat.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">Log Real-time</a></td>
</tr>
<tr>
<td>Lihat ikhtisar status real-time dan detail seluruh jaringan.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">Pemantauan Status Seluruh Jaringan</a></td>
</tr>
<tr>
<td>Lihat laporan multidimensi yang menunjukkan status bisnis Anda untuk keperluan analisis.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">Laporan Operasional</a></td>
</tr>
<tr>
 
 
</tr>
<tr>
<td>Lakukan verifikasi apakah IP tertentu merupakan bagian dari simpul CDN.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">Verifikasi Tencent</a></td>
</tr>
<tr>
<td>Lakukan diagnosis terhadap URL dengan perkecualian akses untuk mencari masalahnya dengan cepat.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">Alat Diagnosis Mandiri</a></td>
</tr>
<tr>
<td>Pantau dan lindungi sumber daya Anda dari serangan DDoS dan CC.</td>
<td>Jaringan Penayangan Konten Keamanan</a></td>
</tr>
<tr>
<td>Gunakan CDN untuk menayangkan gambar dalam jumlah sangat besar.</td>
<td><a href="https://cloud.tencent.com/document/product/228/43121" target="_blank">Pengoptimalan Gambar</a></td>
</tr>
</tbody></table>


## 6.Pertanyaan Umum
#### Penagihan
- [Bagaimana cara menanyakan tagihan CDN?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [Apakah CDN dapat ditagih berdasarkan jumlah permintaan?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Jika server asal menggunakan COS, apakah saya akan ditagih untuk lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke COS?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Ketika dinonaktifkan atau dimatikan, apakah CDN akan dapat menghasilkan lalu lintas dan memakan biaya?](https://intl.cloud.tencent.com/document/product/228/31479)
- [Bagaimana cara mengubah cara penagihan CDN?](https://intl.cloud.tencent.com/document/product/228/31479)
 
- [Apakah hanya lalu lintas downstream yang dapat ditagih di CDN?](https://intl.cloud.tencent.com/document/product/228/31479)

#### Koneksi nama domain

- [Apakah CDN mendukung nama domain kartubebas?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Nama domain saya sudah memperoleh izin ICP dari MIIT.Mengapa prompt sistem yang tidak memiliki berkas ICP ketika saya mencoba menghubungkannya ke CDN?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Berapa lama mengonfigurasi CDN?] (https://intl.cloud.tencent.com/document/product/228/31476)
- [Apakah saya dapat mengonfigurasi beberapa IP server asal?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Bagaimana cara mengetahui bahwa CDN sudah aktif?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Mengapa nama domain dapat dinonaktifkan tetapi tidak dapat dihapus?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Bagaimana cara menonaktifkan layanan akselerasi?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Bagaimana cara menghapus nama domain akselerasi?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Apakah saya dapat mengonfigurasi port untuk nama domain akselerasi atau server asal?](https://intl.cloud.tencent.com/document/product/228/31476)
- [Apa yang harus saya lakukan jika file tidak dapat diunduh dari CDN?](https://intl.cloud.tencent.com/document/product/228/31476)



## 7.Masukan dan Saran
Jika ada keraguan atau saran ketika menggunakan Tencent Cloud CDN, Anda dapat mengirimkan masukan melalui saluran berikut.Karyawan yang bertugas akan menghubungi Anda untuk mengatasi masalah Anda.
- Jika ada pertanyaan menyangkut dokumentasi CDN, seperti tautan, konten, atau API, silakan klik **Send Feedback** (Kirim Masukan) di bagian bawah halaman.
- Jika ada pertanyaan tentang CDN, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

