Dokumen ini menjelaskan cara menghubungkan Kingdee K/3 WISE 15.0/15.1 ke TencentDB for SQL Server agar dapat menjalankan transaksi terdistribusi antara instans TencentDB for SQL Server dan Windows CVM.

Solusi ini terdiri dari tiga langkah berikut:
1. Migrasikan data ke TencentDB for SQL Server, yaitu memulihkan cadangan data lengkap dari database kumpulan akun di instans Kingdee K/3 WISE lokal ke TencentDB for SQL Server.
2. Aktifkan eksekusi transaksi terdistribusi, yaitu menyesuaikan pengaturan akses instans TencentDB for SQL Server dan Windows CVM untuk memastikan bahwa port yang relevan terbuka untuk eksekusi transaksi terdistribusi.
3. Ganti alat manajemen kumpulan akun agar kompatibel dengan TencentDB for SQL Server.

>?
>- Untuk mendukung transaksi terdistribusi, sumber daya tambahan diperlukan untuk konfigurasi; dengan demikian, Anda dapat mengonfigurasi instans Edisi Ketersediaan Tinggi hanya dalam spesifikasi yang lebih tinggi dari "1-core 8 GB MEM". Harap tingkatkan versi instans yang tidak memenuhi persyaratan minimum sebelum melakukan koneksi.
>- Sesuaikan pengaturan akses TencentDB for SQL Server untuk memastikan bahwa transaksi terdistribusi dapat dijalankan. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan. Untuk meningkatkan efisiensi pemrosesan tiket, pastikan Anda telah membaca dokumen ini dan menyelesaikan proses migrasi data ke TencentDB for SQL Server sebelum mengirimkan tiket.


## Langkah 1. Migrasikan data ke TencentDB for SQL Server
Prasyarat: Anda telah mencadangkan data lengkap dari file database kumpulan akun di instans Kingdee K/3 WISE lokal Anda.

1. [Login ke instans Windows CVM](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) dan instal Kingdee K/3 WISE.
>?Instans CVM tempat Kingdee diinstal dan instans TencentDB for SQL Server harus berada di VPC yang sama di wilayah yang sama.
2. - [Buat instans TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238/31571).
3. Unggah file cadangan lengkap dan pulihkan datanya. Untuk petunjuk terperinci, silakan lihat [Mengunggah File Cadangan ke COS](https://intl.cloud.tencent.com/document/product/238/32558) dan [Memigrasikan Data Melalui File Sumber di COS](https://intl.cloud.tencent.com/document/product/238/32558).
4. Buat akun TencentDB for SQL Server dan berikan otorisasi. Untuk informasi selengkapnya, silakan lihat [Membuat Akun](https://intl.cloud.tencent.com/document/product/238/7521).

## Langkah 2. Aktifkan eksekusi transaksi terdistribusi
### Mengatur TencentDB for SQL Server
Sesuaikan pengaturan akses TencentDB for SQL Server untuk memastikan bahwa transaksi terdistribusi dapat dijalankan. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.

### Mengatur instans CVM
#### Mengatur grup keamanan
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/instance), pilih wilayah keberadaan instans, dan klik ID instans untuk masuk ke halaman manajemen.
2. Pilih tab **Security Group** (Grup Keamanan) dan ubah aturan sebagai berikut:
 - Informasi IP "Sumber", yang dapat diperoleh dengan [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category).
 - "Port protokol" aturan masuk dan keluar. Anda perlu membuka port 1433, 135, dan 1024–65535.


#### Mengatur OS Windows
1. [Login ke instans CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
2. Buka file `hosts` yang berlokasi di `C:\Windows\System32\drivers\etc\hosts`.
3. Tambahkan informasi VIP dan host (yang dapat diperoleh dengan [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category)) yang disediakan oleh TencentDB for SQL Server hingga akhir file `hosts` dan simpan perubahannya.

4. Buka "Component Services" (Layanan Komponen) di "Control Panel" (Panel Kontrol) > "System and Security" (Sistem dan Keamanan) > "Administrative Tools" (Alat Administratif).
5. Pilih "Component Services" (Layanan Komponen) > "Computers" (Komputer) > "My Computer" (Komputer Saya) > "Distributed Transaction Coordinator" (Koordinator Transaksi Terdistribusi).
6. Klik kanan DTC lokal di sebelah kanan dan pilih "Properties" (Properti).

7. Pilih tab "Security" (Keamanan), atur sebagai berikut, dan klik **OK**.

8. Di kotak dialog layanan MSDTC pop-up, klik **Yes** (Ya) dan tunggu hingga layanan MSDTC dimulai ulang.
 

## Langkah 3. Inisialisasi manajmenen kumpulan akun
1. Unduh alat manajemen kumpulan akun: Kingdee K/3 WISE 15.1 atau 15.0.
>?Alat manajemen kumpulan akun yang diperlukan berbeda-beda, tergantung versi Kingdee K/3 WISE.
2. Lakukan dekompresi paket dan ganti file di direktori instalasi Kingdee `K3ERP\KDSYSTEM\KDCOM` dengan file yang diekstrak.
3. Buka Kingdee K/3 WISE.
4. Pada halaman pengaturan database manajemen kumpulan akun pop-up, atur informasi verifikasi identitas dan server data yang relevan.
>?Masukkan alamat jaringan pribadi instans TencentDB for SQL Server sebagai server data, yang dapat dilihat di [konsol](https://console.cloud.tencent.com/sqlserver).
>

5. Dalam daftar drop-down "System" (Sistem), klik **Preset Connection** (Koneksi Prasetel) dan atur koneksi prasetel agar lebih mudah digunakan.

6. Dalam daftar drop-down database, klik **Register Account Set** (Daftarkan Kumpulan Akun).

7. Pilih database yang sesuai dan klik **All** (Semua).

 
## Langkah 4. Login ke dan gunakan Kingdee K/3 WISE
Setelah menyelesaikan semua pengaturan di atas, transaksi terdistribusi dapat didukung antara CVM dan instans TencentDB for SQL Server, dan Anda dapat login dan menggunakan Kingdee K/3 WISE secara normal.

Jika pesan kesalahan berikut ditampilkan saat login:
`Gagal membuat transaksi di lapisan perantara. Silakan hubungi administrator sistem. Tampilan lanjutan: kode kesalahan: 5(5H)`
Harap pecahkan masalah kesalahan seperti yang diinstruksikan dalam [dokumentasi resmi Kingdee](https://club.kingdee.com/club/newclub/helpDetail?product_id=3&id=366259). 


