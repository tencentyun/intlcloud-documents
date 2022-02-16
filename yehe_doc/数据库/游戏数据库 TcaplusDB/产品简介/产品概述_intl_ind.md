## Ikhtisar
Dengan pertumbuhan eksplosif data game, semakin sulit bagi database relasional tradisional untuk memenuhi kebutuhan seperti fungsi baca dan tulis bersamaan yang tinggi, penyimpanan dan akses yang efisien ke data besar, skalabilitas tinggi, dan ketersediaan tinggi. Sebaliknya, database NoSQL telah berkembang pesat karena keunggulannya seperti perluasan sederhana dan fungsi baca dan tulis yang cepat.
TencentDB for TcaplusDB dibuat khusus untuk penyimpanan data game berdasarkan konsep desain dan teknologi database non-relasional. Keunggulannya dapat menyeimbangkan performa dan biaya sesuai dengan karakteristik game. Sejauh ini, produk ini telah menyediakan layanan penyimpanan data yang stabil untuk beberapa game online dengan puluhan juta DAU, seperti Arena of Valor, CrossFire, dan NARUTO.

## Pengantar
TencentDB for TcaplusDB adalah layanan penyimpanan data terdistribusi NoSQL yang dirancang untuk game dan mendukung akses API [Protobuf](https://intl.cloud.tencent.com/document/product/1016/30295#P). Dengan menggabungkan cache dengan disk, TcaplusDB dapat memberikan performa tinggi sekaligus menghemat biaya untuk mendukung struktur semua-server/semua-wilayah dan multi-server/multi-wilayah. Selain itu, layanan ini memberikan solusi yang aman, andal, dan lengkap yang mencakup perluasan/pengurangan kapasitas dengan layanan non-stop, pencadangan untuk pemulihan bencana, dan pemutaran kembali cepat sebagai respons terhadap pertumbuhan data yang eksplosif dan OPS game jangka panjang. Kini sudah banyak digunakan di ratusan game populer seperti Arena of Valor, CrossFire, dan NARUTO.

## Fitur
#### Cache yang dikombinasikan dengan penyimpanan persisten
Deskripsi: Penyimpanan cache dan disk digabungkan, dan hot data dan cold data secara otomatis ditukar masuk/keluar.
Nilai pengguna: Tidak perlu menggunakan dua jenis database, sehingga arsitektur aplikasi disederhanakan.
#### Dukungan semua-server/semua-wilayah
Deskripsi: Ruang penyimpanan tidak dibatasi, dengan satu tabel dibatasi hingga 50 TB. Perluasan/pengurangan kapasitas dengan layanan non-stop, serta semua-server/semua-wilayah dan multi-server/multi-wilayah didukung.
Nilai pengguna: Tidak perlu khawatir tentang perluasan ruang penyimpanan.
#### Dukungan akses PB
Deskripsi: Akses data yang fleksibel diaktifkan dengan menggunakan Protobuf, dan akses ke dan ekstraksi bidang tertentu didukung.
Nilai pengguna: Bandwidth sangat dihemat dan biaya berkurang.
#### Pemutaran kembali cepat
Deskripsi: Cold backup ditarik dengan cepat, lalu didekompresi paralel. Proses pemutaran kembali sepenuhnya otomatis, dan pemutaran kembali ke titik waktu yang tepat didukung. Dengan cadangan cold data sebesar 300 GB di setiap node, semua node dapat dipulihkan dalam waktu 2 jam.
Nilai pengguna: Pemutaran kembali cepat dapat mengurangi kerugian kegagalan.
#### Cadangan untuk pemulihan bencana
Deskripsi: perlindungan yang berlebihan; hot backup primer/sekunder; cold backup harian untuk pemulihan bencana dengan data disimpan hingga 30 hari dan catatan binlog selama 15 hari.
Nilai pengguna: Keamanan data dipastikan dan kegagalan operasi ditangani dengan mudah.
