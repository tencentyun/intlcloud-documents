## Ikhtisar Pendengar UDP
Anda bisa membuat pendengar UDP ke instance CLB untuk meneruskan permintaan UDP dari klien.UDP cocok untuk skenario yang sangat membutuhkan kecepatan transfer tetapi tidak terlalu membutuhkan akurasi, seperti pesan singkat dan video online.Untuk pendengar UDP, server asli bisa memperoleh IP klien asli secara langsung.
## Prasyarat
Anda harus [membuat instance CLB](http://intl.cloud.tencent.com/document/product/214/6149) dahulu.

## Mengonfigurasi Pendengar UDP
### Langkah 1.Buka halaman "Manajemen Pendengar"
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Pilih **Instance Management** (Manajemen Instance) di bilah sisi kiri.
3.Di daftar instance, klik ID instance yang akan dikonfigurasi untuk masuk ke halaman detail instance.
4.Klik tab **Listener Management** (Manajemen Pendengar) atau klik **Configure Listener** (Konfigurasi Pendengar) di kolom "Operation" (Operasi).
![](https://main.qcloudimg.com/raw/2c2762f61caf469f88f43f260c3238ea.png)
5.Halaman "Listener Management" (Manajemen Pendengar) adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/053f8a784f0d960866dc59888181960f.png)

### Langkah 2.Konfigurasikan pendengar
Klik **Create** (Buat) di **TCP/UDP/TCP SSL Listener** (Pendengar TCP/UDP/TCP SSL) dan konfigurasikan pendengar UDP di jendela pop-up.
#### 1.Konfigurasi dasar
<table>
<thead>
<tr>
<th width="15%">Item Konfigurasi</th>
<th width="70%">Deskripsi</th>
<th width="15%">Contoh</th>
</tr>
</thead>
<tbody><tr>
<td>Nama</td>
<td>Nama pendengar</td>
<td><span>test-udp-8000 &nbsp; &nbsp; &nbsp;</span></td>
</tr>
<tr>
<td>Protokol pendengar dan port pendengaran</td>
<td>Protokol pendengar dan port pendengaran. <br><li>Protokol pendengar:CLB mendukung berbagai protokol, termasuk TCP, UDP, HTTP, dan HTTPS.UDP digunakan dalam contoh ini.</li><li>Port pendengaran:Port digunakan untuk menerima permintaan dan meneruskannya ke server asli.Rentang port: 1-65535.</li><li>Port pendengar harus unik di instance CLB yang sama.</li></td>
<td>UDP:8000</td>
</tr>
<tr>
<td>Metode penyeimbangan</td>
<td>Untuk pendengar UDP, CLB mendukung dua algoritme penjadwalan: round robin tertimbang (WRR) dan koneksi terkecil tertimbang (WLC). <br><li>WRR:Permintaan dikirimkan secara berurutan ke server-server asli berbeda sesuai bobotnya.Penjadwalan dilakukan berdasarkan <strong>jumlah koneksi baru</strong>, tempat server dengan bobot lebih tinggi akan melalui lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi), sementara server dengan bobot yang sama memproses jumlah koneksi yang sama.</li><li>WLC:Beban server dinilai sesuai dengan jumlah koneksi aktif ke server-server.Penjadwalan dilakukan berdasarkan beban dan bobot server.Jika bobotnya sama, server dengan koneksi aktif yang lebih sedikit akan menjalani lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi).</li></td>
<td>WRR</td>
</tr>
</tbody></table>

Konfigurasi tertentu pendengar UDP yang dibuat adalah seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ac649d8397dc27f29e5c01e1859613ac.png)

#### 2.Pemeriksaan kesehatan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status pemeriksaan kesehatan | Pemeriksaan kesehatan bisa diaktifkan atau dinonaktifkan.Di pendengar UDP, instance CLB mengirimkan perintah ping ke server untuk melakukan pemeriksaan kesehatan.| Diaktifkan |
| Periode waktu habis respons | <li> Periode waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika satu server asli gagal merespons dengan tepat dalam periode waktu habis, pemeriksaan kesehatan dianggap abnormal.</li><li>Rentang nilai: 2-60s.Nilai default: 2s.</li> | 2s |
| Interval pemeriksaan | <li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300s.Nilai default: 5s.</li> | 5s |
| Ambang batas tidak sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) gagal berturut-turut, instance akan dianggap tidak sehat, dan status yang ditampilkan di konsol akan menjadi **Abnormal**.</li><li>Rentang nilai:2-10.Nilai default: 3. | 3 kali |
| Ambang batas sehat | <li>Jika hasil pemeriksaan kesehatan menerima n kali (n adalah jumlah yang dimasukkan) berhasil berturut-turut, instance akan dianggap sehat, dan status yang ditampilkan di konsol akan menjadi **Healthy** (Sehat).</li><li>Rentang nilai:2-10.Nilai default: 3.</li> | 3 kali |

Konfigurasi khusus pemeriksaan kesehatannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1b44a861227794f91ba77b4a8039258b.png)

#### 3.Persistensi sesi
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Status persistensi sesi | Persistensi sesi bisa diaktifkan atau dinonaktifkan. <br><li>Jika persistensi sesi diaktifkan, pendengar CLB akan mengirimkan permintaan akses dari klien yang sama ke server asli yang sama.</li><li>Persistensi sesi UDP diimplementasikan berdasarkan alamat IP klien, misalnya, permintaan akses dari alamat IP yang sama diteruskan ke server asli yang sama.</li><li>Persistensi sesi bisa diaktifkan untuk penjadwalan WRR, tetapi tidak untuk penjadwalan WLC.</li> | Diaktifkan |
| Waktu persistensi sesi | Waktu persistensi sesi. <br> <li>Jika tidak ada permintaan baru di koneksi dalam waktu persistensi sesi, persistensi sesi akan diputus secara otomatis.</li><li>Rentang nilai: 30-3,600s.</li> | 30s |

Konfigurasi khusus persistensi sesi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d63d71c974299c968e08f4a113303ab3.png)

### Langkah 3.Mengikat server asli
1.Di halaman "Manajemen Pendengar", klik pendengar `UDP:8000` yang dibuat untuk melihat server asli yang diikat di sebelah kanan pendengar.
![](https://main.qcloudimg.com/raw/c1169f8489ab530722677ed78e27aa6e.png)
2.Klik **Bind** (Ikat), pilih server asli yang akan diikat dan konfigurasikan port server dan bobot di jendela pop-up.
1.Tambahkan Port:Di kotak "Terpilih" di sebelah kanan, klik **Add Port** (Tambahkan Port) untuk menambahkan beberapa port untuk instance CVM yang sama, seperti port 80, 81, dan 82.
2.Port Default:Masukkan “Port Default” dahulu, kemudian pilih instance CVM.Port dari setiap instance CVM adalah port default.
![](https://main.qcloudimg.com/raw/a39ed8adb8e16928835342fcd8524bba.png)

Setelah tiga langkah ini selesai, aturan pendengar UDP sudah dikonfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3ffbe2442ba826e4d1d395e3f2a99f61.png)

### Langkah 4.Grup keamanan (opsional)
Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Langkah 5.Modifikasi/hapus satu pendengar (opsional)
Jika Anda perlu memodifikasi atau menghapus pendengar yang dibuat, klik pendengar di halaman "Manajemen Pendengar" dan pilih **Modify** (Modifikasi) atau **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/505c464643460e5d0c7008167f0edd77.png)
