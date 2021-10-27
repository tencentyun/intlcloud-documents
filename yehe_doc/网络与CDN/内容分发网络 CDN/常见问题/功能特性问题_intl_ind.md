[](id:q1)
### Apakah Tencent Cloud CDN mendukung akselerasi global?
Ya.Tencent telah membuat banyak simpul selama sepuluh tahun lebih.Tencent Cloud CDN menyediakan lebih dari 800 simpul luar negeri di lebih dari 70 negara dan wilayah untuk membantu agar bisnis Anda mendunia dengan lancar.

[](id:q2)
### Setelah terhubung ke CDN, apakah harus dilakukan perubahan pada server asal agar layanan akselerasi terlaksana?
Tidak. Namun, untuk mencapai hasil akselerasi yang lebih baik, Anda disarankan untuk menetapkan file statis dan dinamis ke nama domain yang berbeda dan hanya mempercepat sumber daya statis.

[](id:q3)
### Apakah Tencent Cloud CDN mendukung akses lintas-wilayah?
Ya.Jika akses lintas-wilayah diperlukan untuk situs web Anda, konfigurasikan saja bidang `Kontrol-Akses-Izinkan-Asal` pada situs web Anda atau konfigurasikan header lintas-wilayah untuk nama domain Anda pada Konsol CDN.Untuk informasi selengkapnya, silakan lihat [Header Respons HTTP](https://intl.cloud.tencent.com/document/product/228/35320).

[](id:q4)
### Di mana saya dapat mengunduh log akses CDN?
Anda dapat mengunduh log akses CDN di Konsol CDN.Untuk mendapatkan petunjuk terperinci, silakan lihat [Unduh Log](https://intl.cloud.tencent.com/document/product/228/6316).

[](id:q5)
### Bagaimana saya menggunakan alat diagnosis mandiri CDN?
Alat diagnosis mandiri menyediakan berbagai fitur diagnosis seperti pengujian resolusi DNS, kualitas tautan, ketersediaan situs, dan konsistensi akses data untuk nama domain yang diakses.Untuk informasi selengkapnya, silakan lihat [Alat Diagnosis Mandiri](https://intl.cloud.tencent.com/document/product/228/6304).Alat ini tergantung pada konfigurasi lingkungan jaringan lokal dan tidak dapat sepenuhnya menampilkan hasil pengujian seluruh jaringan.

[](id:q6)
### Apa perbedaan antara diagnosis akses lokal dan diagnosis akses pengguna?
Diagnosis akses lokal: jika Anda menemukan kelainan pada salah satu akses sumber daya Anda, Anda dapat memulai pengujian dengan "diagnosis akses lokal".
Diagnosis akses pengguna: jika pengguna Anda melaporkan kelainan pada akses sumber daya mereka, Anda dapat mengetahui masalahnya melalui "diagnosis akses pengguna" dan mengatasi masalah tersebut sesuai dengan saran Tencent Cloud.

[](id:q7)
### Apakah CDN mendukung permintaan POST?
Ya.

[](id:q8)
### Apakah CDN mendukung konfigurasi Kontrol-Cache server asal?
Ya.Menurut pengaturan default-nya, CDN mendukung konfigurasi Kontrol-Cache server asal.

[](id:q9)
### Apakah CDN mendukung kompresi gzip?
Ya.Untuk membantu Anda mengamankan lalu lintas data, CDN mengompres file antara 256 byte dan 2.048 KB dengan ekstensi nama file .js, .html, .css, .xml, .json, .shtml, dan .htm menjadi file gzip.

[](id:q10)
### Apakah akselerasi CDN mendukung port selain 80?
Ya.Akselerasi CDN mendukung port 80, 443, dan 8080.

[](id:q11)
### Apa itu server perantara CDN?
Server perantara CDN adalah server tarik-asal lapis-tengah yang terletak antara server bisnis dan simpul CDN.Server perantara ini menyatukan semua permintaan tarik-asal simpul untuk mengurangi tekanan tarik-asal pada server asal Anda.

[](id:q12)
### Bagaimana saya mendapatkan IP klien yang sebenarnya?
Setelah suatu permintaan melalui server tepi, header `x-forward-for` yang berisi informasi IP klien yang sebenarnya akan ditambahkan ke permintaan tersebut.

[](id:q13)
### Bagaimana saya mengonfigurasi subpengguna CDN?
Subpengguna tidak perlu didaftarkan di Tencent Cloud atau mengaktifkan layanan CDN.Mereka ditambahkan ke daftar subpengguna oleh pembuatnya.Ada dua jenis subpengguna:
1.Penerima pesan.
2.Pengguna konsol.Untuk informasi selengkapnya mengenai cara membuat dan mengonfigurasi subpengguna, silakan lihat [Izin Konsol](https://intl.cloud.tencent.com/document/product/228/35229).

[](id:q14)
### Bagaimana saya mengonfigurasi daftar blokir/daftar izin IP di CDN?
CDN mendukung konfigurasi daftar blokir/daftar izin IP.Anda dapat membuat kebijakan pemfilteran untuk IP sumber permintaan pengguna berdasarkan kebutuhan bisnis Anda sehingga membantu mencegah hotlinking dan serangan dari IP yang berbahaya.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Daftar Blokir/Daftar Izin IP](https://intl.cloud.tencent.com/document/product/228/6298).

Untuk informasi selengkapnya mengenai konfigurasi ini, silakan lihat [Konfigurasi Batas Akses IP](https://intl.cloud.tencent.com/document/product/228/6420) dan [Konfigurasi Perlindungan Hotlink](https://intl.cloud.tencent.com/document/product/228/6292).

[](id:q15)
### Bagaimana saya mengonfigurasi Range GETs di CDN?
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah sisi kiri, dan klik **Kelola** di kanan nama domain yang ingin Anda edit.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Range GETs](https://intl.cloud.tencent.com/document/product/228/7184).
![](https://main.qcloudimg.com/raw/af642b65bed86a97fadaf229e26aceac.png)
Klik **Origin Configuration** (Konfigurasi Asal) dan Anda akan melihat modul "Konfigurasi Range GETs". ![](https://main.qcloudimg.com/raw/79d08718f1399b735b9b2dc804bf383e.png)

[](id:q16)
### Mengapa CDN tidak dapat menyembunyikan IP sepenuhnya?
1.IP sudah terbuka sebelum CDN digunakan.
2.Bahkan IP masih dapat dilihat melalui perangkat teknis setelah CDN digunakan.
3.Ada beberapa situs web pada server, dan jika nama domain lain tidak terhubung ke CDN, IP tersebut bisa terbuka.

[](id:q17)
### Apa yang dilakukan server asal cadangan dinamis?
Jika server asal primer Anda adalah server eksternal, Anda dapat menambahkan server asal cadangan dinamis.Semua permintaan tarik-asal akan diteruskan ke server asal primer terlebih dahulu.Jika kode kesalahan 4XX atau 5XX dikembalikan atau suatu kelainan seperti waktu koneksi habis atau ketidakcocokan protokol terjadi, permintaan akan diteruskan ke server asal cadangan dinamis untuk menarik sumber daya sehingga menjamin ketersediaan tarik-asal yang tinggi.

[](id:q18)
### Apakah CDN mendukung nama domain .top?
Ya.CDN telah mendukung nama domain yang berakhiran .pw atau .top.

[](id:q19)
### Apakah ada batas ukuran untuk file yang diunggah ke CDN?
Ya.Ukuran maksimal file yang dapat diunggah ke CDN adalah 32 MB menurut pengaturan default.

[](id:q20)
### Apakah CDN mendukung nama domain bahasa Mandarin?
Tidak. Saat ini, CDN tidak mendukung nama domain bahasa Mandarin (bahkan setelah pentranskodean).

[](id:q21)
### Dapatkah CDN meneruskan permintaan ke server asal melalui jaringan pribadi?
Tidak. Saat ini, CDN hanya dapat meneruskan permintaan ke server asal melalui jaringan publik.

[](id:q22)
### Apakah CDN mendukung skrip tepi untuk mengimplementasikan konfigurasi yang dapat diprogram?
Ya.CDN saat ini menggunakan skrip Lua untuk mengimplementasikan konfigurasi yang dapat diprogram, yang umumnya digunakan untuk penyesuaian serta ditulis dan dirilis oleh tim dukungan teknis CDN.

[](id:q23)
### Apakah CDN mendukung konfigurasi server asal yang berbeda untuk permintaan klien yang berbeda?
Ya.Tarik-asal IP klien berbasis-wilayah masih dalam tahap beta.Silakan tunggu peluncuran resminya.

[](id:q24)
### Apakah CDN mendukung konfigurasi tarik-asal dinamis dan antrean tarik-asal?
Jika server asal primer merespons secara luar biasa, server tersebut dapat mengalihkan permintaan ke server asal cadangan yang dikonfigurasikan sesuai urutan untuk permintaan kembali.
