CDN menyediakan alat diagnosis mandiri untuk membantu Anda menyelesaikan masalah kegagalan akses URL. Alat ini menemukan masalah dengan memeriksa resolusi DNS, kualitas tautan, status simpul, server asal, dan konsistensi akses data, dan menawarkan solusi yang relevan.

>! URL sumber daya yang akan didiagnosis harus berupa nama domain yang **activated** (diaktifkan) di bawah akun Anda. Karena bandwidth yang dihasilkan selama diagnosis dikenakan biaya, sebaiknya sumber daya yang didiagnosis tidak lebih dari 200 MB.



## Diagnosis Kesalahan
### Proses diagnosis

Jika URL sumber daya tidak dapat diakses, Anda dapat memulai diagnosis melalui **Fault Self-diagnosis** (Diagnosis Mandiri Kesalahan) dalam langkah-langkah berikut:
1. Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Inspect Tool** -> **Fault Self-diagnosis** (Alat Periksa -> Diagnosis Mandiri Kesalahan).
2. Di halaman **Fault Self-diagnosis** (Diagnosis Mandiri Kesalahan), masukkan URL yang akan didiagnosis. URL harus dimulai dengan `http://` atau `https://`.
 ![](https://main.qcloudimg.com/raw/0b5b89dee36676027aeb15a118b4584e.png)
3. Klik **Get a Diagnosis Link** (Dapatkan Tautan Diagnosis) dan alamat tautan akan muncul di halaman.
 ![](https://main.qcloudimg.com/raw/35e6dc6b335db10c63dc729cbe11ddbe.png)
4. Klik tautan tersebut untuk membuka halaman diagnosis tempat informasi diagnosis akan dikumpulkan. Jangan tutup halaman selama proses diagnosis berlangsung. Anda dapat menutupnya secara manual setelah diagnosis selesai.
    ![](https://main.qcloudimg.com/raw/1e41c147e1e0ae216efc6635a43b1298.png)
5. Anda juga dapat mengirim tautan diagnosis ke orang lain untuk diagnosis kesalahan lokal. Setelah diagnosis selesai, Anda harus menutup halaman web secara manual.

>!
- Tautan diagnosis valid selama 24 jam dan mendukung hingga 10 diagnosis kesalahan.
- Anda dapat menyalin tautan diagnosis yang tersedia di halaman "Diagnostic Report" (Laporan Diagnosis).

## Laporan Diagnosis
### Melihat laporan
1. Setelah diagnosis selesai, klik **Diagnostic Report** (Laporan Diagnosis) untuk melihat laporan, yang ditampilkan dalam tabel dalam urutan kronologis. Isi tabel tersebut antara lain:
	- URL tempat tautan diagnosis dibuat.
	- Area target diagnosis URL.
	- Tautan diagnosis yang sesuai dengan URL.
	- Waktu ketika tautan diagnosis dibuat.
	- Status tautan diagnosis.
	- Jumlah diagnosis yang tersedia dari tautan diagnosis.

![](https://main.qcloudimg.com/raw/47c48777ace8428bb065695e1475600e.png)

2. Klik **Expand** (Perluas) di kolom operasi untuk melihat laporan yang dihasilkan oleh setiap diagnosis dan hasil diagnosis.
![](https://main.qcloudimg.com/raw/a439f2dbcadcb6d2790e846416717cea.png)
3. Laporan diagnosis akan membuat penilaian keseluruhan berdasarkan diagnosis untuk setiap langkah seperti yang ditunjukkan di bawah ini:
 - Normal
 - Abnormal
 - Halaman yang ditutup secara tidak normal. Ini biasanya terjadi ketika halaman ditutup sebelum diagnosis selesai.
4. Klik **View Report** (Lihat Laporan) untuk melihat detail diagnosis dan saran.

### Penafsiran laporan
1. Bagian pertama dari laporan menampilkan informasi diagnosis, termasuk:
 - ID laporan diagnosis.
 - URL yang akan didiagnosis.
 - Waktu saat diagnosis dipicu.
![](https://main.qcloudimg.com/raw/a7b7c60533782c95927d4860491594fd.png)

2. Bagian kedua memberikan gambaran tentang proses diagnosis dan hasil dari setiap modul diagnosis. Modul luar biasa diidentifikasi dengan jelas. Modul diagnosis meliputi:
 - Hasil pemeriksaan informasi klien.
 - Hasil pemeriksaan DNS.
 - Hasil pemeriksaan CNAME.
 - Hasil pemeriksaan tautan jaringan.
 - Hasil pemeriksaan simpul akses.
 - Hasil pemeriksaan simpul tarik-asal.
 - Hasil pemeriksaan server asal.
![](https://main.qcloudimg.com/raw/1298a6d0b2e72b70ca202a03660b409f.png)

3. Bagian ketiga menguraikan hasil diagnosis.
 #### Bagian 1. Informasi klien
Informasi seperti IP klien, distrik/ISP, dan User-Agent, referer, dan metode permintaan dari permintaan HTTP/HTTPS yang dimulai diperoleh. Tanpa informasi klien, beberapa pemeriksaan berikutnya tidak dapat dilakukan.
![](https://main.qcloudimg.com/raw/8219224766176ed87ebb421330170f4a.png)

 #### Bagian 2. Pemeriksaan DNS
IP DNS klien dikumpulkan dan diperiksa terhadap IP klien, untuk menentukan apakah pengecualian dalam konfigurasi DNS lokal menyebabkan masalah dalam menjadwalkan permintaan ke simpul cache yang optimal.
![](https://main.qcloudimg.com/raw/4ab79b159c3e983cd6db7c1fefeae9ea.png)

 #### Bagian 3. Pemeriksaan CNAME
Konfigurasi CNAME dari nama domain diperoleh. Resolusi CNAME dari nama domain perlu dikonfigurasi dengan nama domain yang benar dengan akhiran `*.cdn.dnsv1.com` (default); jika tidak, permintaan tidak akan dapat mencapai simpul CDN.
![](https://main.qcloudimg.com/raw/c3bbbb52440985415d9433b838dbde42.png)
>! Jika pemeriksaan konfigurasi CNAME gagal, permintaan tidak akan mencapai simpul CDN dan diagnosis selanjutnya tidak akan dilakukan.

 #### Bagian 4. Pemeriksaan tautan jaringan
Beberapa situs web diperiksa secara lokal untuk mendapatkan status jaringan klien. Jika situs web tidak dapat diakses karena konfigurasi proxy lokal, pemeriksaan tautan jaringan akan gagal, dan diagnosis selanjutnya tidak akan dilakukan.
![](https://main.qcloudimg.com/raw/be249d3593b9956bf4e03393f02bb1d4.png)

 #### Bagian 5. Pemeriksaan simpul akses
Setelah permintaan klien mencapai simpul CDN, informasi simpul akan dikumpulkan, termasuk IP simpul, distrik/ISP simpul, kode status yang dikembalikan oleh simpul, status hit, dan MD5 sumber daya.
 - Jika sumber daya telah di-cache pada simpul CDN, sumber daya tersebut akan langsung terkena hit, dan pemeriksaan simpul tarik-asal tidak akan dilakukan.
 - Jika cache mengalami miss, pemeriksaan simpul tarik-asal akan dilakukan.
 - Jika kode status yang dikembalikan oleh URL adalah 301, 302, atau 504, informasi pemeriksaan simpul tidak akan diperoleh, dan pemeriksaan selanjutnya tidak akan dilakukan.
 - Jika ACL telah dikonfigurasi untuk nama domain, simpul akses akan langsung mengembalikan 403, dan status hit-nya adalah **hit**.
![](https://main.qcloudimg.com/raw/cce938713c83879c50899efb71b9ea2e.png)

 #### Bagian 6. Pemeriksaan simpul tarik-asal
 1. Jika sumber daya dikembalikan secara langsung oleh simpul CDN, status hit dari simpul akses dan simpul tarik-asal adalah **hit**, dan CDN akan melanjutkan untuk memeriksa server asal untuk membantu memeriksa apakah kode status dan konten dikembalikan dari server asal sama dengan kode status dan konten pada simpul.
![](https://main.qcloudimg.com/raw/88ec7bc47877ef3c96b468a2a9c19a00.png)
 2. Jika sumber daya tidak langsung dikembalikan oleh simpul CDN, status hit dari simpul akses dan simpul tarik-asal adalah **missed**, dan konten akan dikembalikan oleh server asal.
![](https://main.qcloudimg.com/raw/ce8f450c620a6ed2b13de186a04b677b.png)
 3. Jika kode status luar biasa dibuat saat ini, Anda dapat membandingkan kode status server asal dan nilai MD5 file dengan yang dikembalikan oleh modul akses untuk menentukan apakah pengecualian tersebut disebabkan oleh simpul CDN atau oleh server asal, lalu perbaiki masalah sebagaimana mestinya.

>?Jika laporan diagnosis tidak dapat membantu Anda memecahkan masalah, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) atau hubungi dukungan teknis Tencent Cloud.

