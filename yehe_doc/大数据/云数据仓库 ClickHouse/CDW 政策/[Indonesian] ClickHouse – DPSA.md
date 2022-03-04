## 1.	LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan Cloud Data Warehouse (“**Fitur**”). Modul ini tergabung dalam Perjanjian Privasi dan Keamanan Data yang berada di https://intl.cloud.tencent.com/document/product/301/17347 (“**DPSA**”). Istilah-istilah yang digunakan, tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku meskipun terjadi inkonsistensi.

## 2.	PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Tujuan Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Konfigurasi:** informasi  konfigurasi klaster (termasuk mode penagihan, wilayah, zona ketersediaan,  nama klaster, deskripsi klaster, jumlah CPU CVM, virtual private cloud  (VPC), data penyimpanan (termasuk data untuk alokasi penyimpanan yang ditentukan oleh  Anda), perpanjangan otomatis, waktu pembelian  (kapan pesanan akan dihasilkan)) | Kami hanya memproses data ini untuk  tujuan menyediakan Fitur kepada Anda sesuai  konfigurasi spesifik Anda.  Harap perhatikan bahwa  data ini disimpan dalam fitur TencentDB for MySQL kami. |
| **Data Pemantauan:** Pemanfaatan CPU dan  memori, jumlah file terbuka per detik, penggunaan disk data, indikator utama  (termasuk jumlah kueri yang diproses per detik, waktu pemrosesan,  jumlah koneksi per detik, jumlah rekaman yang dihasilkan oleh klaster per  detik, total waktu perhitungan operator) | Kami menggunakan informasi ini untuk mendukung Anda memantau status operasi dan mengatur alarm ambang batas  untuk berbagai peristiwa di Fitur, seperti indikator kinerja atau  konsumsi.  Perlu diketahui bahwa  data ini dilakukan oleh dan disimpan dalam fitur Cloud Monitor (CM) kami, serta disimpan  dalam fitur TencentDB for MySQL kami. |
| **Data Bisnis:** file data biner  dari data bisnis dan konfigurasi Anda yang Anda impor/simpan di CBS dan/atau  Fitur ini | Kami hanya memproses data ini  untuk tujuan menyediakan Fitur kepada Anda, untuk mengeksekusi kueri Anda.  Harap diperhatikan bahwa data  ini terintegrasi dengan fitur CBS kami untuk tujuan ini. Jika Anda memilih untuk  menggunakan fungsi penyimpanan berjenjang, data ini juga disimpan di fitur COS. |



## 3.	WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4.	SUB-PROSESOR

Sebagaimana ditentukan dalam DPSA.

## 5.	RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi** | **Kebijakan Retensi**                                         |
| ------------------------ | ------------------------------------------------------------ |
| Data Konfigurasi       | Kami menyimpan data tersebut  selama Anda menggunakan Fitur. Apabila penggunaan Fitur Anda berakhir,  kami akan menghapus data ini setelah 7 hari. |
| Data Pemantauan          | Kami menyimpan data tersebut  selama Anda menggunakan Fitur. Apabila penggunaan Fitur Anda berakhir,  kami akan menghapus data ini setelah 7 hari. |
| Data Bisnis            | Kami menyimpan data tersebut  selama Anda menggunakan Fitur. Anda dapat menghapus data tersebut secara manual pada  Fitur. Setelah Anda memilih untuk menghapus data tersebut atau menghentikan penggunaan  Fitur, data tersebut akan segera dihapus setelah 7 hari. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6.	PERSYARATAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah yurisdiksi tempat pengguna akhir berada.