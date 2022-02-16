## Ikhtisar
Perintah ini digunakan untuk mempelajari penggunaan perintah.

## Sintaksis
```
## Mendapatkan Semua Perintah dan Penggunaannya
bantuan;
 
## Memperoleh Petunjuk Mendetail dari Perintah Tertentu
bantuan [perintah];
```

## Sampel
```
tcaplus>help;
--------------------------------------------------------------------------------
      help: tampilkan penggunaan perintah, contoh: "help select;".
      show: mendapatkan informasi terkait status server. menjalankan "help show;" untuk detailnya.
      exit/quit: keluar dari klien.
     count: mencetak nomor catatan dalam database.
 
      desc: cetak nama dan jenis bidang tabel.
    select: catatan kueri dari database.
    insert: menyisipkan catatan baru ke dalam database.
   replace: mengganti catatan ke dalam database.
    update: memperbarui catatan dalam database.
    delete: menghapus catatan dari database.
 
      dump: membuang catatan dari database.
      load: memuat catatan ke dalam database.
 
    setttl: atur ttl untuk catatan
    getttl: dapatkan ttl untuk catatan
 
--------------------------------------------------------------------------------
 
tcaplus> help select;
--------------------------------------------------------------------------------
contoh: pilih key1, key2, key3, value1, value2 [into result.csv] dari tabel dengan key1 = 1 dan key2 = "abc" [and -index = 1] [\P] [\G];
         catatan kueri dari database, Anda dapat menentukan bagian dari bidang atau seluruh bidang (pilih *), dan Anda dapat menulis hasilnya ke file, yang dapat digunakan dengan "insert" dan "load"
         untuk tabel generik, jika kunci dengan klausul tidak lengkap, kunci tersebut akan mengirim "GetByPartkey"
         untuk tabel daftar, jika "-index" tidak ditentukan dalam klausul where, kunci akan mengirim "ListGetAll", jika tidak akan mengirim "ListGet"
         \P: penggunaan waktu cetak secara detail
         \G: mencetak bidang di kolom
         Catatan: "-index" hanya digunakan untuk tabel daftar
 
contoh: pilih * [into result.xml] dari tabel dengan key1 = 1 dan key2 = "abc" [and -index = 1] menggunakan tdr [\P];
         jika Anda menentukan "menggunakan tdr", catatan akan diuraikan oleh file tdr dan dicetak dalam format xml. Anda dapat menulis hasilnya ke dalam file, yang dapat digunakan dengan "load"
         catatan hanya mendukung "pilih *" sebagai ganti bagian dari bidang tertentu saat menentukan "menggunakan tdr"
         Catatan: "-index" hanya digunakan untuk tabel daftar
 
kueri indeks global:
   contoh: pilih * dari tabel dengan key1 > 1 dan value1 > 100;
   contoh: pilih * dari tabel dengan value1 seperti "test";
   contoh: pilih field1, field2 dari tabel dengan key1 > 1 atau value1 > 100;
   contoh: pilih * dari tabel dengan value1 antara 100 dan 200;
   contoh: pilih * dari tabel dengan value1 > 100 limit 100 offset 0;
   contoh: pilih sum(value2), max(value2), min(value2), avg(value2), count(*) dari tabel dengan value1 > 100;
   Catatan: kueri indeks global hanya mendukung tabel generik;
   Catatan: dukungan saat ini: =,!=,>,>=,<,<=, like, not like, between, in, not in, and, or, limit offset;
   Catatan: agregasi dukungan saat ini: count, sum, max, min, avg;
   Catatan: untuk tabel protobuf mendukung: "select field1.field2 from test where value1 > 100";
   Catatan: limit harus digunakan dengan offset, kekurangan offset akan membuat kueri gagal;
   Catatan: bidang dengan kondisi dan agregasi harus sudah membuat indeks;
   Catatan: tidak mendukung: menyimpan hasil ke file, seperti "pilih * ke file XXX" tidak mendukung;
   Catatan: tidak mendukung: "pilih * dari tabel"; yang berarti untuk melintasi tabel, Anda dapat menggunakan metode melintasi api untuk melintasi tabel;
   Catatan: tidak mendukung: diurutkan berdasarkan, dikelompokkan berdasarkan, memiliki, bergabung, gabungan, dan sebagainya;
   Catatan: tidak mendukung: pilih a+b XXX; pilih * dari tabel dengan a+b>0; pilih sum(XX),field1 dari XXX; pilih *,field1 dari XXX; ......;
--------------------------------------------------------------------------------
```
