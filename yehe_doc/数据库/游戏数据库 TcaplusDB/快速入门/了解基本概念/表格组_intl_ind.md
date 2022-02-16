## Ikhtisar Grup Tabel
Sebagai metode isolasi logika di TcaplusDB, grup tabel merepresentasikan partisi data yang dapat memisahkan tabel yang berbeda satu sama lain. Sebuah kluster dapat berisi beberapa grup tabel, dan grup tabel dapat berisi beberapa tabel. Grup tabel yang berbeda tidak dapat mengakses data satu sama lain.

Dari perspektif bisnis gaming, jika bisnis gaming mendukung server terpadu di semua zona dan dapat membaca/menulis grup tabel yang sama dalam kluster, maka tidak perlu dibagi menjadi zona yang berbeda. Ini juga bisa spesifik server/khusus zona, yaitu kluster dapat berisi beberapa grup tabel.

## Membuat Grup Tabel
Untuk petunjuk terperinci, silakan lihat [Membuat Tabel Grup](https://intl.cloud.tencent.com/document/product/1016/32716).

## Detail Grup Tabel
Anda dapat melihat konfigurasi dan atribut grup tabel pada halaman daftar kluster untuk memahami penggunaan kluster secara keseluruhan.
Anda dapat masuk ke [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) dan masuk ke daftar kluster untuk melihat informasi grup tabel dari kluster target.

Informasi grup tabel berisi empat bidang berikut:
- ID: ID grup tabel di kluster saat ini yang diperlukan selama koneksi database. Harap dicatat bahwa ID grup tabel dapat berulang dalam kluster berbeda.
- Nama Grup Tabel: Anda dapat menyesuaikan nama grup tabel berdasarkan tujuan sebenarnya.
- Jumlah Tabel: menunjukkan jumlah tabel dalam grup tabel saat ini.
- Kapasitas Total: ini menunjukkan kapasitas disk yang digunakan oleh tabel dalam grup tabel saat ini.
