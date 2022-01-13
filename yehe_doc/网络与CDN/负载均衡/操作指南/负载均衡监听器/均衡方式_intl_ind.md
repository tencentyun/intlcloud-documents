Metode penyeimbangan beban adalah algoritme yang mengalokasikan lalu lintas ke [server asli](https://intl.cloud.tencent.com/document/product/214/32388).Setiap metode menghasilkan efek penyeimbangan beban yang berbeda.

## Penjadwalan Round-Robin Tertimbang
Algoritme penjadwalan round-robin tertimbang adalah untuk menjadwalkan permintaan ke server berbeda berdasarkan polling.Algoritme ini bisa menyelesaikan masalah performa tidak seimbang di server berbeda.Algoritme ini memakai bobot untuk mewakili performa pemrosesan server dan menjadwalkan permintaan ke server berbeda berdasarkan bobot dengan cara polling.Algoritme ini menjadwalkan server berdasarkan jumlah koneksi baru, tempat server dengan bobot lebih tinggi menerima koneksi lebih awal dan berpeluang lebih tinggi untuk dipilih.Server dengan bobot yang sama akan memproses jumlah koneksi yang sama.
- **Advantage** (Keunggulan): algoritme ini memberikan kemudahan dan kepraktisan tinggi.Algoritme ini tidak perlu mencatat status semua koneksi dan oleh karena itu merupakan algoritme penjadwalan stateless.
- **Disadvantage** (Kekurangan): algoritme ini cukup sederhana sehingga tidak cocok untuk situasi saat waktu layanan permintaan berubah secara signifikan, atau setiap permintaan membutuhkan jumlah waktu yang berbeda.Dalam kasus-kasus ini, algoritme itu akan menyebabkan distribusi beban yang tidak seimbang di antara server.
- **Applicable scenario** (Skenario yang berlaku): Algoritme ini cocok untuk skenario saat setiap permintaan pada dasarnya membutuhkan jumlah waktu yang sama di backend dengan performa pemuatan terbaik.Algoritme ini biasanya digunakan di layanan koneksi non-persisten seperti layanan HTTP.
- **Recommendation** (Rekomendasi): jika Anda tahu bahwa setiap permintaan pada dasarnya membutuhkan jumlah waktu yang sama di backend (contohnya, permintaan yang diproses server asli berjenis sama atau mirip), Anda sebaiknya menggunakan penjadwalan round-robin.Jika perbedaan waktu antara setiap permintaan kecil, sebaiknya menggunakan algoritme ini juga, karena tingkat konsumsi rendah dan efisiensi tinggi, tanpa membutuhkan traversal.

## Penjadwalan Koneksi Terkecil Tertimbang
Pada situasi sebenarnya, waktu yang dihabiskan permintaan-permintaan klien di server bisa sangat bervariasi.Makin panjang waktu pengerjaannya, jika round-robin sederhana atau algoritme penyeimbangan beban acak digunakan, jumlah proses koneksi di setiap server bisa sangat bervariasi sehingga tidak bisa mencapai efek penyeimbangan beban.
Berbeda dengan penjadwalan round-robin, penjadwalan koneksi terkecil adalah algoritme penjadwalan dinamis yang memperkirakan beban server berdasarkan kuantitas koneksi aktifnya.Penjadwal harus merekam jumlah koneksi di setiap server yang saat ini tersambung.Jika ada permintaan yang dijadwalkan ke satu server, jumlah koneksinya akan bertambah 1.Jika koneksi terhenti atau habis waktu, jumlah koneksinya akan berkurang 1.
Pada algoritme penjadwalan koneksi terkecil tertimbang yang didasarkan pada penjadwalan koneksi terkecil, bobot berbeda dialokasikan ke server-server sesuai kemampuan pemrosesannya.Dengan cara ini, satu server bisa mencapai jumlah permintaan terkait yang sesuai dengan bobotnya, yang merupakan peningkatan di penjadwalan koneksi terkecil.
> Misalkan bobot satu server asli adalah wi, dan jumlah koneksi saat ini adalah ci.Nilai ci/wi setiap server dihitung secara berurutan.Server asli dengan nilai ci/wi terkecil akan menjadi server yang menerima permintaan baru berikutnya.Jika ada server asli dengan nilai ci/wi yang sama, mereka akan dijadwalkan sesuai penjadwalan round-robin tertimbang.

- **Advantage** (Keunggulan): algoritme ini cocok untuk permintaan yang pemrosesannya butuh waktu lama, seperti FTP.
- **Disadvantage** (Kekurangan): karena batasan API, koneksi terkecil dan persistensi sesi tidak bisa diaktifkan di waktu yang sama.
- **Applicable scenario** (Skenario yang berlaku): algoritme ini cocok untuk skenario saat waktu yang dihabiskan setiap permintaan di backend sangat bervariasi.Algoritme ini biasanya digunakan pada layanan koneksi persisten.
- **Recommendation** (Rekomendasi): jika Anda harus memproses permintaan-permintaan berbeda dan waktu layanan yang dibutuhkan di backend sangat bervariasi (seperti 3 milidetik dan 3 detik), Anda sebaiknya menggunakan penjadwalan koneksi terkecil tertimbang untuk mencapai penyeimbangan beban.

## Penjadwalan Hashing Sumber
Algoritme penjadwalan hashing sumber (ip_hash) menggunakan alamat IP sumber dari permintaan sebagai kunci hash dan mencari server yang sesuai dari tabel hash yang ditetapkan secara statis.Permintaan akan dikirimkan ke server ini jika tersedia dan tidak kelebihan beban; jika tidak, nol akan dikembalikan.
- **Advantage** (Keunggulan): ip_hash bisa memetakan permintaan dari satu klien ke server asli yang sama melalui tabel hash.Oleh karena itu, dalam skenario saat persistensi sesi tidak didukung, algoritme ini bisa digunakan untuk mencapai efek persistensi sesi sederhana.
- **Recommendation** (Rekomendasi): Algoritme menghitung nilai hash dari alamat sumber satu permintaan dan mendistribusikan permintaan itu ke server asli berdasarkan bobotnya.Dengan cara ini, semua permintaan dari IP klien yang sama bisa didistribusikan ke server yang sama.Algoritme ini cocok untuk protokol yang tidak mendukung cookie.

## Memilih Algoritme Penyeimbangan Beban dan Mengonfigurasi Bobot
Agar kluster server asli bisa menjalankan bisnis dengan stabil dalam berbagai skenario, beberapa kasus mengenai cara memilih algoritme penyeimbangan beban dan mengonfigurasi bobot tersedia di bawah ini untuk referensi Anda.
- Skenario 1:
1.Misalkan ada 3 server asli dengan konfigurasi yang sama (CPU dan memori) dan Anda mengatur semua bobotnya ke 10 karena performanya sama.
2.100 koneksi TCP telah dibuat antara setiap server asli dan klien, dan satu server asli baru ditambahkan.
3.Dalam skenario ini, Anda sebaiknya menggunakan algoritme penjadwalan koneksi terkecil, yang bisa dengan cepat menambah beban server asli ke-4 dan mengurangi tekanan pada 3 server lainnya.
- Skenario 2:
1.Misalkan Anda menggunakan layanan Tencent Cloud untuk pertama kalinya dan situs web Anda baru saja dibuat dengan beban rendah.Anda sebaiknya membeli server asli dengan konfigurasi yang sama, karena semuanya merupakan server layer akses setara.
2.Di skenario ini, Anda bisa mengatur bobot semua server asli ke nilai default 10 dan menggunakan algoritme penjadwalan round-robin tertimbang untuk mendistribusikan lalu lintas.
- Skenario 3:
1.Misalkan kamu memiliki 5 server asli yang menjalankan permintaan akses ke halaman statis sederhana, dan rasio daya komputasi (dihitung berdasarkan CPU dan memori) server-server ini adalah 9:3:3:3:1.
2.Pada skenario ini, Anda bisa mengatur bobot server asli itu masing-masing ke 90, 30, 30, 30, dan 10.Karena kebanyakan permintaan akses ke halaman statis adalah jenis koneksi non-persisten, Anda bisa menggunakan algoritme penjadwalan round-robin, agar instance CLB bisa mengalokasikan permintaan sesuai rasio performa servernya.
- Skenario 4:
1.Misalkan Anda memiliki 10 server asli untuk menjalankan sejumlah besar permintaan akses web dan tidak ingin membeli server lagi, karena bisa menambah pengeluaran, dan salah satu server itu sering mulai ulang karena kelebihan beban.
2.Dalam skenario ini, Anda sebaiknya mengatur bobot server itu sesuai performanya dan mengatur bobot yang cukup kecil untuk server dengan beban tinggi.Selain itu, Anda bisa menggunakan algoritme penjadwalan koneksi terkecil untuk mengalokasikan permintaan ke server asli dengan koneksi aktif yang lebih sedikit agar server tidak kelebihan beban
- Skenario 5:
1.Misalkan Anda memiliki 3 server asli untuk memproses beberapa koneksi persisten, rasio daya komputasi (dihitung dari CPU dan memori) server-server ini adalah 3:1:1.
2.Server dengan performa terbaik memproses lebih banyak permintaan, tetapi Anda tidak ingin sampai kelebihan beban dan ingin mengalokasikan permintaan baru ke server diam,.
3.Dalam skenario ini, Anda bisa menggunakan algoritme penjadwalan koneksi terkecil dan dengan tepat mengurangi bobot server yang sibuk, agar instance CLB bisa mengalokasikan permintaan ke server asli dengan koneksi aktif yang lebih sedikit sehingga mencapai penyeimbangan beban.
- Skenario 6:
1.Misalkan Anda ingin permintaan dari klien berikutnya dialokasikan ke server yang sama.Karena penjadwalan round-robin tertimbang atau koneksi terkecil tertimbang tidak bisa memastikan bahwa permintaan dari klien yang sama dialokasikan ke server yang sama,
2.Untuk memenuhi persyaratan server aplikasi tertentu Anda dan mempertahankan "kelengketan" (atau "kelanjutan") sesi klien tersebut, Anda bisa menggunakan ip_hash untuk mendistribusikan lalu lintasnya.Algoritme ini bisa memastikan semua permintaan dari klien yang sama akan didistribusikan ke server asli yang sama, kecuali jika jumlah server berubah atau server menjadi tidak tersedia.
