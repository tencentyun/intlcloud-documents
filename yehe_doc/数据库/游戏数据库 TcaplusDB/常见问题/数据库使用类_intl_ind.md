
- [Bagaimana cara mendapatkan definisi kode kesalahan dalam paket respons?](#42)
- [Bagaimana cara kerja penguncian optimis TcaplusDB dan bagaimana menggunakannya?](#44)
- [Apa kasus penggunaan dan tindakan pencegahan untuk tabel LIST (DAFTAR)?](#45)
- [Apa perbedaan antara INSERT (SISIPKAN), UPDATE (PERBARUI), dan REPLACE (GANTI)?](#46)
- [Bagaimana cara mendapatkan jumlah catatan dalam tabel?](#47)
- [Apakah TcaplusDB mendukung operasi penjelajahan?](#48)
- [Apakah TcaplusDB mendukung pembaruan dan pengambilan sebagian bidang?](#49)
- [Apakah TcaplusDB mempertahankan pesanan untuk operasi berkelanjutan dari satu kunci primer?](#50)
- [Apakah TcaplusDB mendukung perubahan definisi tabel?](#51)
- [Bagaimana cara mengetahui apakah pengemasan paket respons telah berakhir?](#54)
- [Apa perbedaan antara GetRecordCount dan GetRecordMatchCount?](#55)
- [Apakah TcaplusDB memiliki bidang pass-through?](#56)
- [Apa peran SetResultFlag?](#57)
- [Dapatkah saya melakukan operasi peningkatan pada beberapa bidang kunci non-primer sekaligus? Bagaimana jika kunci primer tidak ada?](#58)
- [Bagaimana cara mengurangi biaya lalu lintas ketika TcaplusDB membaca catatan?](#60)
- [Apakah TcaplusDB mendukung pemutaran kembali? Apa yang dimaksud dengan granularitas pemutaran kembali yang didukung?](#64)
- [Seberapa efisien kueri dengan kunci parsial (indeks) dengan TcaplusDB?](#70)
- [Apa yang dimaksud dengan mekanisme waktu habis untuk TcaplusDB API? Apa yang dimaksud dengan kesalahan "waktu habis"?](#75)
- [Apa peran fungsi SendRequest, OnUpdate, dan ReceiveResponse dari TcaplusDB API?](#76)
- [Bagaimana TcaplusDB mencapai peningkatan bidang otomatis global?](#77)
- [Aturan apa yang ditentukan untuk kueri dengan kunci parsial (indeks)?](#78)
- [Bagaimana cara mencapai kueri dua arah dari ID dan nama tabel tunggal?](#79)
- [Apakah tcaplus_client mendukung tampilan bidang pada tingkat berlapis kedua atau yang lebih tinggi?](#83)
- [Apa yang harus diperhatikan saat mengubah tabel di TcaplusDB?](#86)
- [Apa yang harus diperhatikan saat mendefinisikan tabel di TcaplusDB?](#87)

<span id="42"></span>
### Bagaimana cara mendapatkan definisi kode kesalahan dalam paket respons?
Sebaiknya panggil fungsi `TcapErrCode::TcapErrCodeInit` dan `TcapErrCode::GetErrStr` di server game untuk mendapatkan kode kesalahan, atau mencari file header TcaplusDB API secara lokal.

<span id="44"></span>
### Bagaimana cara kerja penguncian optimis TcaplusDB dan bagaimana cara menggunakannya?
Mari gunakan pembelian tiket kereta api sebagai contoh:
1. 100 orang ingin mengambil tiket kereta api yang sama. Nomor versi yang dicatat untuk tiket kereta api adalah 10, dan 100 orang menggunakan nomor versi yang dicatat yang sama untuk mengambil tiket kereta api.
2. 100 orang melakukan operasi penulisan pada tiket ini. Setelah operasi tulis selesai, nomor versi yang dicatat akan bertambah. Dengan demikian, untuk operasi kunci tunggal, utas pekerja tcapsvr akan dimasukkan dalam antrean. Ketika orang pertama berhasil membeli tiket, nomor versi tiket kereta api yang tercatat berubah menjadi 11, dan nomor versi yang dicatat dari 99 orang yang tersisa masih 10.
3. Ketika tcapsvr menangani permintaan penulisan dari 99 orang, kesalahan akan terjadi karena nomor versi yang dicatat di akhir tcapsvr tidak konsisten dengan nomor versi dalam permintaan. Prinsip-prinsip serentak adalah sebagai berikut:
 - Permintaan N. Jika hanya permintaan pertama yang berhasil dan permintaan N-1 lainnya gagal, aturan perlindungan versi akan digunakan.
 - Permintaan N. Jika semua permintaan N harus dijalankan, tidak ada aturan perlindungan versi yang diperlukan. TcaplusDB beroperasi pada kunci yang sama.
 
Masukkan dalam antrean dan panggil fungsi `SetCheckDataVersionPolicy`, yang nilainya meliputi:
 - `CHECKDATAVERSION_AUTOINCREASE`: nomor versi yang dicatat terdeteksi, yang hanya akan bertambah secara otomatis jika sama dengan nomor versi sisi server.
 - `NOCHECKDATAVERSION_OVERWRITE`: nomor versi yang dicatat tidak terdeteksi, dan nomor versi klien yang dicatat secara paksa ditulis ke server.
 - `NOCHECKDATAVERSION_AUTOINCREASE`: nomor versi yang dicatat tidak terdeteksi, dan nomor versi yang dicatat dari server akan meningkat secara otomatis.
 - Sebaiknya gunakan jenis default `CHECKDATAVERSION_AUTOINCREASE`.

<span id="45"></span>
### Apa kasus penggunaan dan tindakan pencegahan untuk tabel LIST?
Saat ada kasus penggunaan 1:N, ketika N < 1024, tabel LIST diprioritaskan, seperti menyimpan 100 email terbaru pemain, 100 catatan pertempuran terbaru, dan sebagainya. Tabel LIST mendukung penyisipan di ujung antrean dan penghapusan di akhir antrean, penyisipan di akhir antrean dan penghapusan di ujung antrean, serta operasi N Top diurutkan berdasarkan waktu penyisipan. Jumlah unit di bawah satu kunci dapat ditingkatkan dengan memodifikasi tabel, karena data lama harus kompatibel dan tidak dapat diubah menjadi lebih kecil. Anda dapat memperoleh jumlah total catatan di bawah kunci tunggal menggunakan `listgetall`. Sebaiknya peroleh data sesuai dengan offset dan batas ambang tertentu yang Anda tetapkan. Untuk `listreplace`, `listdelete`, dan `listdeletebatch`, Anda perlu menentukan indeks yang benar. Untuk `listaddafter`, Anda perlu menentukan aturan eliminasi saat jumlah unit elemen di bawah kunci tunggal mencapai batas atas. Jika fungsi `SetListShiftFlag` dipanggil, tabel LIST memiliki dua arah peningkatan dan dua arah perolehan. Ada 4 kemungkinan:
1. Kueri A, B, C, D, E sebagai offset = bilangan positif dan batas = 2, dan hasilnya adalah A, B; C, D; E.
2. Kueri A, B, C, D, E sebagai offset = bilangan negatif dan batas = 2, dan hasilnya adalah D, E; B, C; A.
3. Kueri E, D, C, B, A sebagai offset = bilangan positif dan batas = 2, dan hasilnya adalah E, D; C, B; A.
4. Kueri E, D, C, B, A sebagai offset = bilangan negatif dan batas = 2, dan hasilnya adalah B, A; D, C; E.

Selain itu, memanggil `GetRecordMatchCount` bisa mendapatkan jumlah total catatan.

<span id="46"></span>
### Apa perbedaan antara INSERT (SISIPKAN), UPDATE (PERBARUI), dan REPLACE (GANTI)?
Untuk operasi INSERT, ketika kunci tidak ada, operasi INSERT akan dijalankan; ketika kunci ada, kode kesalahan akan dikembalikan: `TcapErrCode::SVR_ERR_FAIL_RECORD_EXIST`.
Untuk operasi REPLACE, ketika kunci tidak ada, operasi INSERT akan dijalankan; ketika kunci ada, jika kunci optimis digunakan, operasi yang berbeda akan dijalankan berdasarkan hasil kunci optimis. Jika operasi berhasil, operasi REPLACE akan dijalankan, dan jika gagal, kode kesalahan akan dikembalikan: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION;`. Jika penguncian optimis tidak digunakan, operasi REPLACE akan dijalankan.
Untuk operasi UPDATE, ketika kunci ada, jika kunci optimis digunakan, operasi yang berbeda akan dijalankan berdasarkan hasil dari kunci optimis. Jika operasi berhasil, operasi UPDATE akan dijalankan, dan jika gagal, kode kesalahan akan dikembalikan: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION`. Jika penguncian optimis tidak digunakan, operasi UPDATE akan dijalankan. Ketika kunci tidak ada, kode kesalahan akan dikembalikan: `TcapErrCode::TXHDB_ERR_RECORD_NOT_EXIST`.

<span id="47"></span>
### Bagaimana cara mendapatkan jumlah catatan dalam tabel?
Ada kata perintah jumlah di TcaplusDB API. Jika `tcaplus_client` digunakan, Anda dapat menggunakan perintah nama tabel `count` untuk mendapatkan jumlah catatan dalam tabel.

<span id="48"></span>
### Apakah TcaplusDB mendukung operasi penjelajahan?
TcaplusDB mendukung operasi penjelajahan, termasuk operasi penjelajahan untuk tabel GENERIC dan LIST. Anda dapat menggunakan API `SetOnlyReadFromSlave(bool flag)` untuk melintasi data dari tcapsvr sekunder, yang tidak akan memengaruhi layanan yang disediakan oleh tcapsvr primer.

<span id="49"></span>
### Apakah TcaplusDB mendukung pembaruan dan pengambilan bidang parsial?
Dukungan TcaplusDB memperbarui bidang parsial. Saat memperbarui dan memperoleh catatan, sebaiknya panggil API `SetFieldNames(IN const char* field_name[], IN const unsigned field_count)` secara eksplisit untuk menentukan bidang operasi baca dan tulis ini, dan mengurangi overhead lalu lintas jaringan yang disebabkan oleh bidang yang tidak valid.

<span id="50"></span>
### Apakah TcaplusDB mempertahankan pesanan untuk operasi berkelanjutan dari satu kunci primer?
Untuk server game yang sama, operasi dari kunci primer yang sama adalah mempertahankan pesanan, sedangkan operasi dari kunci primer yang berbeda tidak mempertahankan pesanan. Untuk server game yang berbeda, urutannya tidak dipertahankan.

<span id="51"></span>
### Apakah TcaplusDB mendukung perubahan definisi tabel?
TcaplusDB mendukung perubahan definisi tabel. Untuk menambahkan bidang kunci non-primer dan mengubah makro, cukup ubah tabelnya. Untuk perubahan yang lebih kompleks, Anda dapat mengubah struktur tabel secara dinamis menggunakan migrasi data dan log. Untuk menggunakan fitur ini, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) dan pilih **More** (Lainnya) di halaman **Select the related product** (Pilih produk terkait).

<span id="54"></span>
### Bagaimana cara mengetahui apakah pengemasan paket respons telah berakhir?
Untuk penjelajahan, periksa apakah penjelajahan berakhir sesuai dengan status, yaitu API `GetState`. Untuk skenario pengemasan lainnya, periksa apakah pengemasan berakhir sesuai dengan fungsi `HaveMoreResPkgs`.

<span id="55"></span>
### Apa perbedaan antara GetRecordCount dan GetRecordMatchCount?
Sebuah permintaan mungkin memiliki paket respons N. Jika ada beberapa paket, `GetRecordCount` mengacu pada jumlah catatan dalam paket respons, dan `GetRecordMatchCount` mengacu pada catatan data yang disimpan di tcapsvr (lapisan penyimpanan) (jumlah total catatan untuk kunci tunggal).

<span id="56"></span>
### Apakah TcaplusDB memiliki bidang pass-through?
Protokol CS dari TcaplusDB dibagi menjadi dua bagian: judul dan isi. `UserBuff` (ukuran maksimum adalah 1 KB), `AsyncID` dan `Sequence` di judul semuanya adalah bidang pass-through. Anda dapat menggunakannya dengan semestinya.

<span id="57"></span>
### Apa peran SetResultFlag?
Saat melakukan operasi tulis, paket respons mendukung catatan yang dikembalikan. Saat melakukan operasi baca, pemanggilan fungsi ini tidak valid. Nilai spesifik dari `result_flag` adalah sebagai berikut:
0: hanya mengembalikan apakah operasi berhasil atau tidak tanpa mengembalikan bidang nilai.
1: mengembalikan data yang sesuai dengan bidang permintaan.
2: kembalikan data terbaru untuk semua bidang catatan yang diubah.
3: kembalikan data lama untuk semua bidang catatan yang diubah.

API `SetResultFlagForSuccess` dapat digunakan untuk mengembalikan data jika operasi berhasil; API `SetResultFlagForFail` dapat digunakan untuk mengembalikan data jika operasi gagal.

<span id="58"></span>
### Dapatkah saya melakukan operasi peningkatan pada beberapa bidang kunci non-primer sekaligus? Bagaimana jika kunci primer tidak ada?
Untuk menambah beberapa bidang kunci non-primer, bidang ini perlu diberi nilai oleh permintaan dari server game. Jika salah satu kunci tidak ada, Anda dapat menggunakan fungsi `SetAddableIncreaseFlag` untuk melakukan operasi peningkatan. Jika tidak ada kunci, masukkan kunci lalu lakukan operasi peningkatan, tempat bidang kunci yang tidak bertambah tidak akan disimpan dan akan mengambil nilai default saat catatan dibaca. Jika kuncinya ada, operasi peningkatan dapat segera dilakukan.

<span id="60"></span>
### Bagaimana cara mengurangi biaya lalu lintas ketika TcaplusDB membaca catatan?
Ketika TcaplusDB membaca catatan, hal ini dapat diatur sehingga tidak mengembalikan bidang nilai jika catatan tidak berubah dalam jangka waktu tertentu, juga tidak mengembalikan bidang nilai jika nomor versi catatan tidak berubah. Untuk informasi selengkapnya, lihat fungsi `SetFlags`.

<span id="64"></span>
### Apakah TcaplusDB mendukung pemutaran kembali? Apa granularitas pemutaran kembali yang didukung?
TcaplusDB mendukung pemutaran kembali, termasuk pemutaran kembali semua server/semua wilayah, pemutaran kembali tabel tunggal, dan dapat memutar kembali catatan N dari 100 miliar catatan. Ini juga mendukung pemutaran kembali waktu cold standby (paling baru pukul 01.05.00), pemutaran kembali waktu yang tepat (ke detik), dan pemutaran kembali fuzzy (Anda dapat menentukan aturan pemutaran kembali). Untuk referensi kecepatan, waktu pemutaran kembali yang tepat membutuhkan waktu sekitar 2 jam untuk pemutaran kembali data 300 GB dan Ulog sebesar 200 GB. Prinsip pemutaran kembali waktu cold standby adalah mengganti file mesin. Prinsip pemutaran kembali waktu yang tepat adalah memutar kembali file mesin cold standby + Ulog ke titik waktu yang diperlukan. Pemutaran kembali berbasis kunci mengharuskan Anda untuk memblokir kunci ini terlebih dahulu dan kemudian membuka blokirnya setelah TcaplusDB menyelesaikan pemutaran kembali.

<span id="70"></span>
### Seberapa efisien kueri dengan kunci parsial (indeks) dengan TcaplusDB?
Sebaiknya gunakan kueri dengan kunci parsial (indeks) dalam skenario aplikasi 1:N (N > 1024). Jumlah kunci primer di bawah kunci indeks tunggal sama dengan 10 GB/ukuran kunci primer dari catatan tunggal. Satu operasi indeks baca-tulis membutuhkan waktu sekitar 100 mdtk (ada lebih dari 100.000 bagian catatan data di bawah kunci indeks tunggal).

<span id="75"></span>
### Apa mekanisme waktu habis untuk TcaplusDB API? Apa yang dimaksud dengan kesalahan "waktu habis"?
TcaplusDB API memberikan ID untuk setiap permintaan. Setelah berhasil dikirim, ID didorong ke dalam struktur penilaian waktu habis. Jika paket respons untuk permintaan kembali, ID dihapus dari struktur. Jika paket respons permintaan belum diproses oleh lapisan aplikasi dalam waktu 3 detik, log kesalahan dengan kata kunci "waktu habis" akan dicetak. Anda kemudian perlu memeriksa apakah server game diblokir. Mungkin tcaproxy (lapisan akses) menjatuhkan paket saat mengembalikan paket ke server game, atau paket respons telah tiba di server game, tetapi server game tidak memprosesnya tepat waktu.
TcaplusDB merekomendasikan Anda untuk mengimplementasikan mekanisme waktu habis sendiri, yang memungkinkan Anda melakukan percobaan ulang dan proses lain untuk permintaan waktu habis.

<span id="76"></span>
### Apa peran fungsi SendRequest, OnUpdate, dan ReceiveResponse dari TcaplusDB API?
Peran `SendRequest` adalah untuk mengirim permintaan. Permintaan ini mungkin telah dikirim ke jaringan, atau mungkin diblokir di saluran pengiriman server game dan tcaproxy (lapisan akses). Peran `ReceiveResponse` adalah untuk mendapatkan paket respons dari antrean penerimaan lokal. `OnUpdate` bertanggung jawab untuk mengirim permintaan antrean kirim ke jaringan dan menerima paket respons dari jaringan ke antrean terima. Dalam mode pemrograman berbasis pesan, `OnUpdate` direkomendasikan untuk dipanggil sekali setiap milidetik.

<span id="77"></span>
### Bagaimana TcaplusDB mencapai peningkatan bidang otomatis global?
Anda perlu menentukan tabel tunggal, dan mengatur jenis bidang dari kunci dan nilai tunggal ke int64_t (beberapa bidang nilai dapat mengimplementasikan berbagai penghitung). Beberapa server game dapat meningkatkan satu kunci secara bersamaan (tanpa menetapkan aturan perlindungan versi), dan mengembalikan hasil peningkatan untuk operasi ini, artinya hasil peningkatan akan menjadi peningkatan otomatis global.

<span id="78"></span>
### Aturan apa yang ditentukan untuk kueri dengan kunci parsial (indeks)?
Kunci indeks harus menjadi bagian dari kunci primer, kunci indeks harus berisi shardkey, dan kunci indeks tidak boleh menjadi kunci primer.

<span id="79"></span>
### Bagaimana cara mencapai kueri dua arah dari ID dan nama tabel tunggal?
Bidang kunci ketiga x digunakan sebagai shardkey, dan indeks dibuat pada ID dan x, nama serta x untuk mencapai fitur ini. Misalnya, saat menyimpan informasi pemain, distrik pemain dapat ditambahkan, yaitu, kunci primer adalah uin, nama, distrik, dan kunci indeks adalah uin dan distrik, dan nama dan distrik.

<span id="83"></span>
### Apakah tcaplus_client mendukung tampilan bidang pada tingkat berlapis kedua atau yang lebih tinggi?
Ya. Anda dapat menjalankan `help select` untuk melihat bagaimana `select * into a.xml` digunakan.

<span id="86"></span>
### Apa yang harus diperhatikan saat mengubah tabel di TcaplusDB?
1. Anda hanya dapat menambahkan bidang baru. Anda tidak dapat mengubah jenis dan nama bidang yang sudah ada, atau menghapus bidang yang sudah ada. Untuk memodifikasinya, Anda perlu memodifikasi struktur tabel secara dinamis.
2. Panjang array atau string dalam bidang kunci non-primer dapat ditingkatkan tetapi tidak dapat dikurangi. Untuk memodifikasinya, Anda perlu memodifikasi struktur tabel secara dinamis.
3. Nomor versi harus bertambah 1 untuk setiap bidang baru, dan nomor versi yang ditentukan di bagian atas file XML juga harus bertambah 1 (yaitu, nomor versi file XML harus sama dengan nomor versi bidang baru). Tabel di TcaplusDB perlu diubah sebelum tabel di server game diubah. TcaplusDB mendukung modifikasi struktur tabel dinamis, dan untuk menggunakan fitur ini, harap [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) dan pilih **Other** (Lainnya) pada halaman **Select the related product** (Pilih produk terkait).

<span id="87"></span>
### Apa yang harus diperhatikan saat mendefinisikan tabel di TcaplusDB?
1. Bidang `refer` perlu ditambahkan ke bidang `count`.
2. shardkey tabel harus sangat diskrit.
3. Kunci indeks tidak boleh sama dengan kunci primer.


