Dokumen ini menjelaskan cara memigrasikan data di konsol atau dengan alat baris perintah.

## Migrasi Data Melalui Konsol
Ada dua mode untuk memigrasi data melalui konsol: pencadangan fisik dan pencadangan logis. Untuk informasi selengkapnya, lihat:
- [Memulihkan Database dari Cadangan Fisik](https://intl.cloud.tencent.com/document/product/236/31910)
- [Memulihkan Database dari Cadangan Logis](https://intl.cloud.tencent.com/document/product/236/31909)

<span id="AA"></span>
## Migrasi Data dengan Alat Baris Perintah
1. Hasilkan file SQL yang akan diimpor dengan alat baris perintah MySQL "mysqldump" dengan cara berikut:
>!
>- File data yang diekspor menggunakan mysqldump harus kompatibel dengan spesifikasi SQL versi TencentDB for MySQL yang Anda beli. Anda dapat Login ke database dan mendapatkan informasi versi MySQL dengan menjalankan perintah `select version();`. Nama file SQL yang dihasilkan dapat berisi huruf, angka, dan garis bawah tetapi bukan "test" (tes).
>- Pastikan bahwa versi database sumber dan target yang sama, kumpulan karakter database sumber dan target, dan versi alat mysqldump digunakan. Anda dapat menentukan kumpulan karakter menggunakan parameter --default-character-set .
>
```
shell > mysqldump [opsi] db_name [tbl_name ...] > bak_pathname
```
Di sini, `options` adalah opsi ekspor, `db_name` adalah nama database, `tbl_name` adalah nama tabel, dan `bak_pathname` adalah jalur ekspor.
Untuk informasi selengkapnya tentang cara mengekspor data dengan mysqldump, silakan lihat [dokumentasi resmi MySQL](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).
2. Impor data ke database target dengan alat baris perintah MySQL sebagai berikut:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Di sini, `hostname` adalah server target untuk pemulihan data, `port` adalah port server target, `username` adalah nama pengguna database di server target, dan `bak_pathname` adalah jalur lengkap ke file cadangan.

### Memigrasikan data (Windows)
1. Gunakan mysqldump versi Windows untuk menghasilkan file SQL yang akan diimpor. Untuk informasi selengkapnya, silakan lihat deskripsi di [Migrasi Data dengan Alat Baris Perintah](#AA).
2. Masukkan prompt perintah dan impor data ke database target dengan alat baris perintah MySQL.
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [Login ke database MySQL target](https://dev.mysql.com/doc/refman/5.7/en/connecting.html), jalankan perintah `show databases;`, dan Anda dapat melihat bahwa database cadangan telah diimpor ke database target.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### Memigrasikan data (Linux)
>- Dokumen ini menggunakan CVM dengan CentOS 7.8 yang diinstal sebagai contoh. Untuk informasi selengkapnya tentang cara mengakses database dari instans CVM, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/236/3130" target="_blank">Mengakses Database MySQL</a>.

1. [Login ke instans CVM](https://intl.cloud.tencent.com/document/product/213/2936) dan buat file SQL untuk diimpor dengan alat baris perintah MySQL "mysqldump". Ambil database `db_blog` di TencentDB sebagai contoh:
![](https://main.qcloudimg.com/raw/de40c98620c6fdd96bc7839645b70103.png)
2. Gunakan alat baris perintah MySQL untuk mengembalikan data ke database target.
3. Login ke database MySQL target, jalankan perintah `show databases;`, dan Anda dapat melihat bahwa database cadangan telah diimpor ke database target.
![](https://main.qcloudimg.com/raw/072f4b0c6f2353cdd1bab1ca9b87a783.png)

## Masalah dengan Kumpulan Karakter File Data yang Diimpor
1. Jika tidak ada kumpulan karakter yang ditentukan selama impor file data ke TencentDB, yang ditetapkan oleh database akan digunakan.
2. Jika tidak, kumpulan karakter yang ditentukan akan digunakan.
3. Jika kumpulan karakter yang ditentukan berbeda dari TencentDB, teks kacau akan ditampilkan.

Untuk informasi selengkapnya, silakan lihat deskripsi kumpulan karakter di <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">Batas Penggunaan</a>.


