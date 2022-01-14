## Analisis Perbandingan Algoritme CLB

### Penjadwalan round-robin tertimbang
- **How it works** (Cara kerjanya)
Penjadwalan round-robin digunakan untuk menjadwalkan permintaan ke berbagai server berdasarkan polling, yaitu, sistem menjalankan `i = (i + 1) mod n` untuk memilih server i di setiap penjadwalan.Penjadwalan round-robin tertimbang dapat mengatasi ketidakseimbangan kinerja berbagai server.Algoritme ini memakai bobot untuk mewakili performa pemrosesan server dan menjadwalkan permintaan ke berbagai server berdasarkan bobot melalui polling.Server dengan bobot lebih tinggi akan lebih cepat mendapatkan koneksi, tetapi perlu memproses lebih banyak koneksi daripada server dengan bobot lebih rendah.Server dengan bobot yang sama memproses jumlah koneksi yang sama.
- **Advantages** (Keuntungan)
Algoritme ini memberikan kemudahan dan kepraktisan tinggi.Algoritme ini merupakan algoritme penjadwalan stateless yang tidak mencatat status semua koneksi.
- **Disadvantages** (Kekurangan)
Penjadwalan round-robin tertimbang ini cukup sederhana, tetapi tidak cocok untuk skenario dengan waktu layanan untuk suatu permintaan yang berubah secara signifikan, atau setiap permintaan membutuhkan jumlah waktu yang berbeda.Dalam skenario semacam ini, penjadwalan round-robin dapat menyebabkan ketidakseimbangan distribusi beban di antara server.
- **Use Cases** (Kasus Penggunaan)
Algoritme ini cocok untuk skenario saat setiap permintaan pada dasarnya membutuhkan jumlah waktu yang sama di backend dengan performa pemuatan terbaik.Algoritme ini biasanya digunakan di layanan koneksi non-persisten seperti layanan HTTP.
- **Recommendations** (Rekomendasi)
Jika Anda tahu bahwa setiap permintaan pada dasarnya membutuhkan jumlah waktu yang sama di backend (contohnya, permintaan yang diproses server asli berjenis sama atau mirip), sebaiknya Anda menggunakan penjadwalan round-robin tertimbang.Jika perbedaan waktu antara setiap permintaan kecil, sebaiknya Anda menggunakan algoritme ini karena memiliki tingkat konsumsi rendah, efisiensi tinggi, dan tidak membutuhkan traversal.

### Penjadwalan koneksi terkecil tertimbang
- **How it works** (Cara kerjanya)
Pada situasi sebenarnya, waktu yang dihabiskan setiap permintaan klien di server bisa sangat bervariasi.Jika round-robin sederhana atau algoritme penyeimbangan beban acak digunakan seiring bertambah panjangnya waktu pengerjaan, jumlah proses koneksi di setiap server bisa sangat bervariasi dan penyeimbangan beban bisa saja tidak tercapai.Berbeda dengan penjadwalan round-robin, penjadwalan koneksi terkecil adalah algoritme penjadwalan dinamis yang memperkirakan beban server berdasarkan jumlah koneksi aktifnya.Penjadwal mencatat jumlah koneksi yang saat ini tersambung di setiap server.Jika ada permintaan yang dijadwalkan ke satu server, jumlah koneksinya bertambah 1.Jika koneksi terhenti atau habis waktu, jumlah koneksinya berkurang 1.Algoritme penjadwalan koneksi terkecil tertimbang didasarkan pada dan menyempurnakan penjadwalan koneksi terkecil.Bobot yang beragam dialokasikan ke server berdasarkan performa pemrosesannya.Dengan demikian, server akan menerima jumlah permintaan yang sesuai dengan bobotnya.
1.Misalkan bobot satu server asli adalah wi (i=1…n) dan jumlah koneksinya saat ini adalah ci (i=1…n).Server asli dengan nilai ci/wi terkecil akan menjadi server berikutnya yang menerima permintaan baru.
2.Server asli dengan nilai ci/wi yang sama akan dijadwalkan berdasarkan round-robin tertimbang.
- **Advantages** (Keuntungan)
Algoritme ini cocok untuk permintaan yang membutuhkan waktu pemrosesan lama, seperti FTP.
- **Disadvantages** (Kekurangan)
Karena adanya pembatasan API, koneksi terkecil dan persistensi sesi tidak dapat diaktifkan secara bersamaan.
- **Use Cases** (Kasus Penggunaan)
Algoritme ini cocok untuk skenario ketika waktu yang digunakan oleh setiap permintaan di backend sangat bervariasi.Algoritme ini biasa digunakan di layanan koneksi persistensi.
- **Recommendations** (Rekomendasi)
Jika Anda perlu memproses beberapa permintaan dan waktu layanannya di backend sangat bervariasi (misalnya, 3 milidetik dan 3 detik), sebaiknya Anda menggunakan penjadwalan koneksi terkecil tertimbang untuk mencapai keseimbangan beban.

### Penjadwalan hashing sumber (ip_hash)
- **How it works** (Cara kerjanya)
Penjadwalan hashing sumber menggunakan alamat IP sumber permintaan sebagai kunci hash dan menemukan server yang sesuai dari tabel hash yang ditetapkan secara statis.Permintaan akan dikirimkan ke server ini jika tersedia dan tidak kelebihan beban; jika tidak, nol akan dikembalikan.
- **Advantages** (Keuntungan)
ip_hash dapat mencapai persistensi sesi tertentu dengan mengingat IP sumber dan memetakan permintaan dari klien ke server asli yang sama melalui tabel hash.Apabila persistensi sesi tidak didukung, ip_hash dapat digunakan untuk penjadwalan.
- **Recommendations** (Rekomendasi)
Algoritme ini menghitung nilai hash alamat sumber sebuah permintaan dan mendistribusikan permintaan tersebut ke server asli yang sesuai berdasarkan bobotnya.Ini memungkinkan pendistribusian permintaan dari IP klien yang sama ke server yang sama.Algoritme ini cocok untuk penyeimbangan beban melalui protokol TCP yang tidak mendukung cookie.

## Memilih Algoritme Penyeimbangan Beban dan Mengonfigurasi Bobot
Dalam fitur CLB yang akan datang, **penerusan lapisan 7 akan mendukung metode penyeimbangan koneksi terkecil.** Kami menyediakan beberapa contoh untuk referensi Anda tentang cara memilih algoritme penyeimbangan beban dan mengonfigurasi bobot agar Anda dapat memastikan bahwa kluster server asli dapat menjalankan bisnis dalam berbagai skenario dengan stabil.
- Skenario 1
Misalkan ada 3 server asli dengan konfigurasi yang sama (CPU dan memori) dan Anda mengonfigurasi semua bobotnya menjadi 10.Misalkan 100 koneksi TCP telah dibuat antara setiap server asli dan klien.Jika sebuah server asli baru ditambahkan, sebaiknya Anda menggunakan algoritme penjadwalan koneksi terkecil, yang bisa dengan cepat menambah beban server ke-4 dan mengurangi tekanan pada 3 server lainnya.
- Skenario 2
Misalkan Anda menggunakan layanan Tencent Cloud untuk pertama kalinya.Situs web Anda baru saja dibuat dan memiliki beban rendah.Sebaiknya Anda membeli server asli dengan konfigurasi yang sama, karena semuanya merupakan server layer akses.Dalam skenario ini, Anda bisa mengonfigurasi bobot semua server asli ke 10 dan menggunakan algoritme penjadwalan round-robin tertimbang untuk mendistribusikan lalu lintas.
- Skenario 3
Misalkan Anda memiliki 5 server asli untuk menjalankan permintaan akses sederhana ke situs web statis, dan rasio daya komputasinya (dihitung berdasarkan CPU dan memori) adalah 9:3:3:3:1.Dalam skenario ini, Anda dapat mengonfigurasi bobot tiap-tiap server itu menjadi 90, 30, 30, 30, dan 10.Karena sebagian besar permintaan akses ke situs web statis merupakan jenis koneksi non-persisten, Anda dapat menggunakan algoritme penjadwalan round-robin tertimbang agar CLB bisa mengalokasikan permintaan sesuai rasio performa server aslinya.
- Skenario 4
Misalkan Anda memiliki 10 server asli untuk menjalankan permintaan akses web dalam jumlah yang masif, dan Anda tidak ingin membeli server lagi.Salah satu server tersebut sering dimulai ulang karena kelebihan beban.Dalam skenario ini, sebaiknya Anda mengonfigurasi bobot server yang sudah ada tersebut sesuai dengan performanya.Server dengan beban lebih tinggi sebaiknya memiliki bobot lebih rendah.Selain itu, Anda dapat menggunakan algoritme penjadwalan koneksi terkecil untuk mengalokasikan permintaan ke server asli dengan koneksi aktif yang lebih sedikit agar server tidak kelebihan beban.
- Skenario 5
Misalkan Anda memiliki 3 server asli untuk memproses koneksi persisten, dan rasio daya komputasinya (dihitung dari CPU dan memori) adalah 3:1:1.Server dengan performa terbaik memproses lebih banyak permintaan, tetapi pastikan server itu tidak sampai kelebihan beban.Sebaiknya Anda mengalokasikan permintaan baru ke server yang sedang tidak digunakan.Dalam skenario ini, Anda dapat menggunakan algoritme penjadwalan koneksi terkecil dan mengurangi bobot server yang penuh dengan tepat. Ini dilakukan agar CLB dapat mengalokasikan permintaan ke server dengan jumlah koneksi aktif yang lebih sedikit sehingga tercipta keseimbangan beban.
- Skenario 6
Misalkan Anda ingin permintaan-permintaan berikutnya dari klien untuk dialokasikan ke server yang sama.Penjadwalan round-robin tertimbang atau koneksi terkecil tertimbang tidak menjamin bahwa permintaan dari klien yang sama akan dialokasikan ke server yang sama.Untuk memenuhi persyaratan server aplikasi pilihan Anda dan menjaga "kelekatan" (atau "kelanjutan") sesi klien, sebaiknya Anda menggunakan ip_hash untuk mendistribusikan lalu lintasnya.Algoritme ini memastikan bahwa semua permintaan dari klien yang sama akan didistribusikan ke server asli yang sama, kecuali jika jumlah servernya berubah atau server menjadi tidak tersedia.
