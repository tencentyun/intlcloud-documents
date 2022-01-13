## Ikhtisar Pendengar HTTPS
Anda bisa membuat pendengar HTTPS ke instance CLB untuk meneruskan permintaan HTTPS dari klien.HTTPS cocok untuk aplikasi HTTP, tempat transfer data perlu dienkripsi.

## Prasyarat
Anda harus [membuat instance CLB](https://intl.cloud.tencent.com/document/product/214/6149) dahulu.

## Mengonfigurasi Pendengar HTTPS
### Langkah 1.Buka tab **Listener Management** (Manajemen Pendengar)
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Pilih **CLB Instance List** (Daftar Instance CLB) di bilah sisi kiri.
3.Di daftar instance, klik ID instance untuk masuk ke halaman detail.
4.Buka tab **Listener Management** (Manajemen Pendengar).Anda juga bisa masuk ke halaman dengan mengeklik **Configure Listener** (Konfigurasikan Pendengar) di bawah kolom **Operation** (Operasi) instance.
![](https://main.qcloudimg.com/raw/6c45e7c57eab15635e6a39ab37bdf69b.png)
5.Halaman "Listener Management" (Manajemen Pendengar) adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/334e907f32a007a50d58a628b369425a.png)

### Langkah 2.Konfigurasikan pendengar
Klik **Create** (Buat) di **HTTP/HTTPS Listener** (Pendengar HTTP/HTTPS) dan konfigurasikan pendengar HTTPS di jendela pop-up.
#### 1.Buat pendengar
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Nama | Nama pendengar | test-https-443 |
| Protokol dan port pendengaran | Protokol dan port pendengaran dari satu pendengar:<ul style="margin-bottom:0px;"><li>Protokol pendengaran:CLB mendukung berbagai protokol, termasuk TCP, UDP, TCP SSL, HTTP, dan HTTPS.HTTPS digunakan dalam contoh ini.</li><li>Port pendengaran:Port digunakan untuk menerima permintaan dan meneruskannya ke server asli.Rentang port:1 - 65535.Port-port ini sudah dicadangkan dan saat ini tidak tersedia bagi pengguna: 843, 1020, 1433, 1434, 3306, 3389, 6006, 20000, 36000, 42222, 48369, 56000, dan 65010.</li><li>Port pendengaran dari setiap instance CLB harus unik.</li></ul>| HTTPS:443 |
| Aktifkan SNI | Jika SNI diaktifkan, beberapa nama domain dari satu pendengar bisa dikonfigurasikan dengan sertifikat berbeda; jika dinonaktifkan, beberapa nama domain dari satu pendengar hanya bisa dikonfigurasikan dengan satu sertifikat.| Dinonaktifkan |
| Metode parsing SSL | Mendukung autentikasi satu arah dan autentikasi bersama | Autentikasi satu arah |
| Sertifikat server | Anda bisa memilih sertifikat yang ada di [layanan sertifikat SSL](https://console.cloud.tencent.com/ssl) atau mengunggah sertifikat | Pilih sertifikat yang ada cc/UzxFoXsE |

Konfigurasi tertentu pendengar HTTPS yang dibuat adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/0aed0d551700632ec37636fd41d3f66c.png)

#### 2.Buat aturan penerusan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Nama domain | Nama domain penerusan: <ul style="margin-bottom:0px;"><li>Panjang: 1 - 80 karakter. </li><li>Garis bawah (_) tidak bisa menjadi karakter pertama. </li><li>Mendukung nama domain persis dan kartubebas. </li><li>Mendukung ekspresi reguler. </li><li>Untuk aturan konfigurasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/9032">Aturan Penerusan Nama Domain dan URL Lapisan 7</a>.</li></ul> | www.example.com |
| Nama domain default   | <li>Jika semua nama domain pendengar tidak cocok, sistem akan mengarahkan permintaan ke nama domain default sehingga akses default terkendali.</li><li>Setiap pendengar hanya bisa dikonfigurasikan dengan satu nama domain default.</li>| Diaktifkan |
| HTTP 2.0   | Setelah HTTP 2.0 diaktifkan, instance CLB bisa menerima permintaan HTTP 2.0.Instance CLB mengakses server asli melalui HTTP 1.1 apa pun versi HTTP yang digunakan klien untuk mengakses instance CLB.| Diaktifkan |
| Jalur URL | Jalur URL penerusan:<ul style="margin-bottom:0px;"><li>Panjang: 1 - 200 karakter.</li><li>Mendukung ekspresi reguler.</li><li>Untuk aturan konfigurasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/214/9032">Aturan Penerusan Nama Domain dan URL Lapisan 7</a>.</li></ul> | /index |
| Metode penyeimbangan | Untuk pendengar HTTPS, CLB mendukung tiga algoritme penjadwalan: round robin tertimbang (WRR), koneksi terkecil tertimbang (WLC), dan hash IP.<ul style="margin-bottom:0px;"><li>WRR:Permintaan dikirimkan secara berurutan ke server-server asli berbeda sesuai bobotnya.Penjadwalan dilakukan berdasarkan **number of new connections** (jumlah koneksi baru), tempat server dengan bobot lebih tinggi akan melalui lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi), sementara server dengan bobot yang sama memproses jumlah koneksi yang sama.</li><li>WLC:Beban server dinilai sesuai dengan jumlah koneksi aktif ke server-server.Penjadwalan dilakukan berdasarkan beban dan bobot server.Jika bobotnya sama, server dengan koneksi aktif yang lebih sedikit akan menjalani lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi).</li><li>Hash IP:Kunci hash digunakan untuk menemukan server terkait di tabel hash statis berdasarkan IP sumber permintaan-permintaan.Jika server tersedia dan tidak kelebihan beban, permintaan akan dikirimkan ke sana; jika tidak, nilai nol akan dikembalikan.</li></ul>| WRR |
| Protokol backend  | Protokol backend di-deploy antara instance CLB dan server asli: <ul style="margin-bottom:0px;"> <li>Jika HTTP dipilih sebagai protokol backend, layanan HTTP harus di-deploy di server asli.</li><li>Jika HTTPS dipilih sebagai protokol backend, layanan HTTPS harus di-deploy di server asli, dan enkripsi dan deskripsi layanan HTTPS akan mengonsumsi lebih banyak sumber daya di server asli.</li></ul> |HTTP |
| Mendapatkan IP klien | Diaktifkan secara default | Diaktifkan |
| Kompresi Gzip | Diaktifkan secara default | Diaktifkan |

Pilih pendengar HTTPS yang akan dibuatkan aturan penerusan dan klik **+** di sebelah kanan.Konfigurasi khususnya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c5c41aa58dc013581fcbdfd97d4d8ad4.png)

#### 3.Pemeriksaan kesehatan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status pemeriksaan kesehatan | Pemeriksaan kesehatan bisa diaktifkan atau dinonaktifkan.Di pendengar HTTPS, instance CLB mengirimkan permintaan HTTPS ke port server tertentu untuk melakukan pemeriksaan kesehatan.| Diaktifkan |
| Nama domain pemeriksaan | Nama domain pemeriksaan kesehatan: <ul style="margin-bottom:0px;"><li>Panjang: 1 - 80 karakter. </li><li>Ini diatur secara default ke nama domain penerusan.</li><li>Tidak mendukung ekspresi reguler.Jika nama domain penerusan Anda adalah kartubebas, Anda harus menentukan nama tetap (non-ekspresi reguler) sebagai nama domain pemeriksaan kesehatan.</li><li>Karakter yang didukung: `a-z` `0-9` `.` `-`.</li></ul> | www.example.com (nilai default) |
| Jalur pemeriksaan | Jalur pemeriksaan kesehatan: <ul style="margin-bottom:0px;"><li>Panjang: 1 - 200 karakter. </li><li>Ini diatur secara default ke `/` dan harus dimulai dengan `/`.</li><li>Tidak mendukung ekspresi reguler.Kami menyarankan untuk menentukan jalur URL tetap (halaman statis) untuk pemeriksaan kesehatan.</li><li>Karakter yang didukung: `a-z` `A-Z` `0-9` `.` `-` `_` `/` `=` `?`.</li></ul> | / (nilai default) |
| Waktu habis respons | <li> Waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika satu server asli gagal merespons dalam periode waktu habis, pemeriksaan kesehatan dianggap abnormal.</li><li>Rentang nilai: 2 - 60 detik.Nilai default: 2 detik.</li> | 2 detik |
| Interval pemeriksaan | <ul style="margin-bottom:0px;"><li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5 - 300 detik.Nilai default: 5 detik.</li></ul> | 5 detik |
| Ambang batas tidak sehat | <ul style="margin-bottom:0px;"><li>Jika hasil pemeriksaan kesehatan gagal n (nilai khusus) kali berturut-turut, server asli itu tidak sehat dan **Abnormal** ditampilkan di konsol.</li><li>Rentang nilai: 2 - 10 kali.Nilai default: 3 kali</li></ul> | 3 kali |
| Ambang batas sehat | <ul style="margin-bottom:0px;"><li>Jika hasil pemeriksaan kesehatan berhasil n (nilai khusus) kali berturut-turut, server asli itu sehat dan **Healthy** (Sehat) ditampilkan di konsol.</li><li>Rentang nilai: 2 - 10 kali.Nilai default: 3 kali</li></ul> | 3 kali |
| Metode permintaan HTTP | Metode permintaan HTTP untuk pemeriksaan kesehatan.Nilai yang valid:GET (nilai default) dan HEAD: <ul style="margin-bottom:0px;"><li>Jika HEAD digunakan, server hanya akan mengembalikan informasi header HTTP, yang bisa mengurangi overhead backend dan meningkatkan efisiensi permintaan.Server asli harus mendukung HEAD.</li><li>Jika GET digunakan, server asli harus mendukung GET.</li></ul> | GET |
| Pemeriksaan kode status HTTP | Jika kode status termasuk yang terpilih, server asli dianggap hidup (sehat).Rentang nilai: http_1xx, http_2xx, http_3xx, http_4xx, dan http_5xx.| Beberapa nilai dipilih: http_1xx, http_2xx, http_3xx, dan http_4xx. |

Konfigurasi khusus pemeriksaan kesehatannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c0ef80ba20998381bde6fff98d9310ff.png)

#### 4.Persistensi sesi
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
|Status persistensi sesi | Persistensi sesi bisa diaktifkan atau dinonaktifkan: <ul style="margin-bottom:0px;"><li>Jika persistensi sesi diaktifkan, pendengar CLB akan mengirimkan permintaan akses dari klien yang sama ke server asli yang sama.</li><li>Persistensi sesi HTTPS diimplementasikan berdasarkan cookies, yang ditanamkan pada klien dengan instance CLB.</li><li>Persistensi sesi bisa diaktifkan untuk penjadwalan WRR tetapi tidak untuk penjadwalan WLC atau hash IP.</li></ul> | Diaktifkan |
| Periode persistensi sesi | Periode persistensi sesi: <ul style="margin-bottom:0px;"><li>Jika tidak ada permintaan baru di koneksi dalam periode persistensi sesi, sesi akan terputus secara otomatis.</li><li>Rentang nilai: 30 - 3600 detik.</li></ul> | 30 detik |

Konfigurasi khusus persistensi sesi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/56f43a42cb15e9909c95122960b0ca75.png)

### Langkah 3.Mengikat server asli
1.Di halaman "Manajemen Pendengar", pilih pendengar `HTTPS:443` yang dibuat.Klik **+** di sebelah kiri untuk memperluas nama domain dan jalur URL, pilih jalur URL yang diinginkan, dan lihat server asli yang terikat pada jalur itu di sebelah kanan pendengar.
![](https://main.qcloudimg.com/raw/1e61d584d4c2ca05ded255a7652e3396.png)
2.Klik **Bind** (Ikat), pilih server asli target, konfigurasikan port server dan beban di jendela pop-up.
① Tambahkan port:Di kotak "Terpilih" di sebelah kanan, klik **Add Port** (Tambahkan Port) untuk menambahkan beberapa port untuk instance CVM yang sama, seperti port 80, 81, dan 82.
② Port default:Masukkan **Default Port** (Port Default) dahulu, kemudian pilih instance CVM.Port dari setiap instance CVM adalah port default.
![](https://main.qcloudimg.com/raw/26021bf7db700056e2cae6a5f3769f4c.png)

Setelah tiga langkah ini selesai, aturan pendengar HTTPS sudah dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/56de905b9c6fa1d1323c77de45790322.png)

### Langkah 4.Grup keamanan (opsional)
Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, lihat [Konfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Langkah 5.Modifikasi dan hapus satu pendengar (opsional)
Jika Anda perlu memodifikasi atau menghapus pendengar yang dibuat, klik pendengar/nama domain/jalur URL pada tab **Listener Management** (Manajemen Pendengar) dan pilih **Modify** (Modifikasi) atau **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/b1732ce6293a7b3382d6e8c8a9b18342.png)


