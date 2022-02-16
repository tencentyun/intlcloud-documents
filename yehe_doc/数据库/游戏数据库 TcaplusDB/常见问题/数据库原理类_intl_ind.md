
- [Bagaimana server game mengeluarkan node tcaproxy (lapisan akses) yang tidak valid?](#52)
- [Bagaimana server game memilih node tcaproxy (lapisan akses)?](#53)
- [Apakah TcaplusDB memiliki fitur kompresi?](#59)
- [Apakah TcaplusDB API tidak memengaruhi utas?](#61)
- [Bagaimana tcapsvr (lapisan penyimpanan) mencapai pemulihan bencana?](#63)
- [Bagaimana tcaproxy (lapisan akses) mencapai pemulihan bencana?](#62)
- [Apakah TcaplusDB memiliki perlindungan beban berlebihan?](#66)
- [Apa prinsip pertukaran cold data dan hot data untuk TcaplusDB?](#71)
- [Bagaimana cara tcaproxy (lapisan akses) memilih tcapsvr (lapisan penyimpanan)?](#81)
- [Berapa tingkat penguncian di TcaplusDB?](#84)

<span id="52"></span>
### Bagaimana server game mengeluarkan node tcaproxy (lapisan akses) yang tidak valid?
TcaplusDB API mendukung pemulihan bencana jika ada pengecualian tcaproxy. Ada dua cara utama tempat API memulai proses tcaproxy yang tidak valid:

1. API secara fisik menganggap bahwa tcaproxy tidak tersedia. API mengirimkan paket deteksi detak jantung ke semua tcaproxy yang terhubung setiap detik. Jika server game tidak menerima paket pengembalian detak jantung yang sesuai dari tcaproxy dalam waktu 10 detik, API akan secara aktif memutuskan koneksi TCP ke tcaproxy dan secara aktif menghubungkan tcaproxy pada pembaruan berikutnya.
2. API secara logis menganggap bahwa tcaproxy tidak tersedia. API menghitung rasio permintaan dan respons dari tcaproxy setiap 10 detik sebagai dasar penilaian. Ambang waktu habis untuk paket permintaan adalah 3 detik. Jika waktu tcaproxy habis lebih dari 3 kali, tcaproxy dianggap tidak tersedia dan tidak ada permintaan yang akan dikirimkan. Permintaan `getmetdata` dikirim ke tcaproxy 60 detik kemudian. Jika tcaproxy dapat menangani permintaan `getmetadata` dengan benar, API menganggap tcaproxy tersedia dan permintaan akan dikirimkan lagi.

Jika server game menemukan bahwa tcaproxy tidak tersedia dalam 10 detik, server tersebut tidak akan mengirim data ke node tcaproxy.

<span id="53"></span>
### Bagaimana server game memilih node tcaproxy (lapisan akses)?
Server game mempertahankan cincin Hash yang konsisten secara lokal. Setelah node tcaproxy (lapisan akses) diverifikasi, node tersebut akan ditambahkan ke cincin Hash. Jika node tcaproxy (lapisan akses) mengurangi kapasitas atau tautan TCP antara server game dan tcaproxy (lapisan akses) telah terputus karena kelainan mesin, server game akan menghapus node tcaproxy (lapisan akses) dari cincin Hash. Server game menghitung nilai hash berdasarkan kunci primer dalam permintaan (jika itu adalah permintaan `batchget`, server secara acak memilih satu node tcaproxy (lapisan akses)), lalu memilih satu node tcaproxy (lapisan akses) dari cincin Hash yang konsisten.

<span id="59"></span>
### Apakah TcaplusDB memiliki fitur kompresi?
TcaplusDB memiliki fitur kompresi berdasarkan algoritme kompresi cepat Google, termasuk kompresi protokol (yaitu, kompresi paket permintaan/tanggapan antara server game dan tcaproxy (lapisan akses) dan kompresi data (yaitu, kompresi data yang perlu disimpan oleh tcapsvr (lapisan penyimpanan)). Jika Anda ingin mengurangi biaya lalu lintas jaringan antara server game dan tcaproxy (lapisan akses), sebaiknya aktifkan kompresi protokol. Anda juga dapat memanggil fungsi `SetCompressSwitch` dari TcaplusDB API untuk mengaktifkan kompresi tcapsvr (lapisan penyimpanan), yang dapat menghemat ruang disk, meningkatkan performa disk IO, dan mengurangi sumber daya CPU yang digunakan untuk kompresi dan dekompresi.

<span id="61"></span>
### Apakah TcaplusDB API tidak memengaruhi utas?
TcaplusDB API memengaruhi utas, terutama karena komponen seperti tlog dan tdr memengaruhi utas. Direkomendasikan bahwa satu utas menggunakan satu objek API dan satu wilayah game menggunakan satu objek API. Jika Anda perlu berinteraksi di seluruh wilayah game, sebaiknya pertahankan beberapa objek API dengan satu server game.

<span id="62"></span>
### Bagaimana tcaproxy (lapisan akses) mencapai pemulihan bencana?
Tcaproxy (lapisan akses) mengadopsi skema desain peer-to-peer, yaitu, semua node tcaproxy (lapisan akses) di bawah satu wilayah game berisi informasi perutean semua tabel di bawah satu wilayah game. Jika tcaproxy (lapisan akses) gagal, selama node tcaproxy (lapisan akses) yang tersisa tidak kelebihan beban, server game akan mengeluarkan node tcaproxy (lapisan akses) yang tidak normal, yang tidak akan memengaruhi penggunaan server game. Tidak ada satu titik pun risiko kegagalan untuk tcaproxy (lapisan akses).

<span id="63"></span>
### Bagaimana tcapsvr (lapisan penyimpanan) mencapai pemulihan bencana?
Tcapsvr (lapisan penyimpanan) berjalan dalam mode primer-sekunder (tcapsvr primer dan tcapsvr sekunder). tcapsvr primer dan sekunder menyinkronkan data secara real-time, dan di-deploy di IDC yang berbeda di kota yang sama, sehingga memastikan bahwa latensi sinkronisasi primer-sekunder kurang dari 10 ms. Jika tcapsvr sekunder tidak normal, hal ini tidak akan memengaruhi penggunaan server game (jika pengalihan permintaan baca tidak diaktifkan, permintaan server game diproses oleh tcapsvr primer. Jika pengalihan permintaan baca diaktifkan, tcapsvr sekunder akan membantu dalam memproses sebagian permintaan baca), dan DBA akan membangun kembali tcapsvr sekunder; jika tcapsvr primer tidak normal, tcapsvr sekunder akan melakukan pemulihan kegagalan dan DBA akan meminta mesin baru untuk membangun kembali tcapsvr sekunder. Tidak ada satu titik pun risiko kegagalan untuk tcapsvr (lapisan penyimpanan).

<span id="66"></span>
### Apakah TcaplusDB memiliki perlindungan beban berlebihan?
Lapisan akses dan lapisan penyimpanan memiliki langkah-langkah perlindungan beban berlebihan tingkat proses untuk memastikan bahwa layanan tetap berfungsi selama jam sibuk.

<span id="71"></span>
### Apa prinsip pertukaran cold data dan hot data untuk TcaplusDB?
TcaplusDB menggunakan memori + penyimpanan disk SSD. Data GB pertama dari satu file mesin dipetakan dalam memori. Hot data ditempatkan di memori dan cold data ditempatkan pada disk. Algoritme LRU digunakan untuk pertukaran hot data dan cold data. Operasi `get` dari server game memicu operasi swap-in LRU, dan utas LRU tcapsvr (lapisan penyimpanan) bertanggung jawab atas operasi penukaran LRU. Cobalah untuk memastikan bahwa hot data disimpan dalam memori, sehingga memastikan tingkat hit cache yang tinggi dan latensi baca dan tulis tunggal yang rendah.

<span id="81"></span>
### Bagaimana tcaproxy (lapisan akses) memilih tcapsvr (lapisan penyimpanan)?
Setiap tabel mendefinisikan shardkey. Jika tidak ada shardkey yang ditentukan, shardkey diatur secara default ke kunci primer. Tcaproxy (lapisan akses) memilih tcapsvr (lapisan penyimpanan) yang sesuai menurut `hash (shardkey) % 10000` (dengan % adalah operator sisanya), sehingga shardkey harus sangat diskrit.

<span id="84"></span>
### Berapa tingkat penguncian di TcaplusDB?
Granularitas kunci di TcaplusDB adalah level logging.
