Setelah membuat instance CLB klasik, Anda perlu mengonfigurasikan pendengar untuknya.Pendengar mendengar permintaan di instance dan mendistribusikan lalu lintas ke server-server asli sesuai kebijakan penyeimbangan beban.

## Prasyarat
Anda harus [membuat instance CLB](https://intl.cloud.tencent.com/document/product/214/6149) dahulu dan memilih "CLB Klasik" untuk **Instance type** (Tipe instance).
>!Saat ini, ada dua jenis akun Tencent Cloud: tagihan per EIP/CLB dan tagihan per CVM.Semua akun Tencent Cloud yang terdaftar setelah 17 Juni 2020 00.00.00 adalah akun tagihan per EIP/CLB.Untuk akun Tencent Cloud yang terdaftar sebelum 17 Juni 2020, [periksa tipe akun Anda](https://intl.cloud.tencent.com/document/product/684/15246) di konsol.Akun tagihan per EIP/CLB tidak lagi mendukung CLB klasik.Anda kini hanya bisa membeli instance CLB.

## Mengonfigurasi Pendengar
### Langkah 1.Buka halaman **Listener Management** (Manajemen Pendengar)
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb).
2.Pilih **CLB Instance List** (Daftar Instance CLB) di bilah sisi kiri.
3.Di halaman **Instance Management** (Manajemen Instance), klik ID/Nama instance yang akan dikonfigurasi untuk masuk ke halaman detail instance.
4.Pilih tab **Listener Management** (Manajemen Pendengar), atau klik **Configure listener** (Konfigurasikan pendengar) di bawah kolom **Operation** (Operasi) di halaman **Instance Management** (Manajemen Instance).
![](https://main.qcloudimg.com/raw/3c63dacadca27ea0bb84d015954d741a.png)
5.Halaman **Listener Management** (Manajemen Pendengar) adalah seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/61ff0540f4eccdc24cb5f06f76af5299.png)

### Langkah 2.Konfigurasikan pendengar
Klik **Create** (Buat) di bawah **Listener Management** (Manajemen Pendengar) dan konfigurasikan pendengar TCP pada jendela pop-up.
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
<td>Nama pendengar.</td>
<td><span>test-tcp-80&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
</tr>
<tr>
<td>Port Protokol Pendengar</td>
<td>Protokol pendengar dan port pendengaran<br><li>Protokol pendengar:CLB mendukung protokol seperti TCP, UDP, HTTP, dan HTTPS.Contoh ini menggunakan TCP.</li><li>Port pendengaran: digunakan untuk menerima dan meneruskan permintaan ke server asli.Rentang port adalah 1-65535.</li><li>Port pendengaran harus unik di instance CLB yang sama.</li></td>
<td>TCP:80</td>
</tr>
<tr>
<td>Port Backend</td>
<td>Port tempat instance CVM menyediakan layanan, menerima dan memproses lalu lintas dari instance CLB.</td>
<td>80</td>
</tr>
</tbody></table>

Untuk membuat pendengar TCP, selesaikan konfigurasi dasar seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3773d74e1c13df06f7d70e89e3820624.png)

#### 2.Konfigurasi lanjutan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Metode Keseimbangan | Untuk pendengar TCP, CLB mendukung dua algoritme penjadwalan: round robin tertimbang (WRR) dan koneksi terkecil tertimbang (WLC).<br><li>WRR: permintaan diteruskan ke server-server berbeda secara berurutan sesuai bobotnya.Penjadwalan disesuaikan dengan <strong>jumlah koneksi baru</strong>, tempat server dengan bobot lebih tinggi menerima lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi) dan server dengan bobot yang sama memproses jumlah koneksi yang sama.</li><li>WLC: beban pada server dihitung berdasarkan jumlah koneksi aktifnya.Penjadwalan disesuaikan beban dan bobot server.Jika bobotnya sama, server asli dengan koneksi aktif yang lebih sedikit akan menerima lebih banyak polling (dengan kata lain, kemungkinan yang lebih tinggi).</li> | WRR |
| Persistensi Sesi | Mengaktifkan atau menonaktifkan sesi.<br><li>Setelah persistensi sesi diaktifkan, pendengar CLB akan mendistribusikan permintaan akses dari klien yang sama ke server asli yang sama.</li><li>Persistensi sesi TCP diimplementasikan sesuai alamat IP klien.Permintaan akses dari alamat IP yang sama diteruskan ke server asli yang sama.</li><li>Persistensi sesi bisa diaktifkan untuk penjadwalan WRR tetapi tidak untuk penjadwalan WLC.</li> | Diaktifkan |
| Waktu Tunggu | Waktu persistensi sesi.<br><li>Jika tidak ada permintaan baru di koneksi dalam waktu persistensi sesi, persistensi sesi akan diputus secara otomatis.</li><li>Rentang nilai: 30-3600 detik.</li> | 30s |

Selesaikan konfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ddc22b9e0638eb8f2d8803ffee6335f8.png)

#### 3.Pemeriksaan kesehatan
| Item Konfigurasi | Deskripsi | Contoh |
| ------- | ------------------------ | ---------------------------------------- |
| Pemeriksaan Kesehatan | Mengaktifkan atau menonaktifkan pemeriksaan kesehatan.Di pendengar TCP, instance CLB mengirimkan paket SYN ke port server tertentu untuk melakukan pemeriksaan kesehatan.| Diaktifkan |
| Protokol Pemeriksaan | Yang akan ditambahkan.| Yang akan ditambahkan |
| Port Pemeriksaan | Yang akan ditambahkan.| Yang akan ditambahkan |
| Waktu Habis Respons | <li> Periode waktu habis respons maksimum untuk pemeriksaan kesehatan.</li><li>Jika satu server asli gagal merespons dalam periode waktu habis, server dianggap tidak sehat.</li><li>Rentang nilai: 2-60 detik.Nilai default: 2s.</li> | 2s |
| Interval Pemeriksaan | <li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300 detik.Nilai default: 5s.</li> | 5s |
| Ambang Batas Tidak Sehat | <li>Jika pemeriksaan kesehatan mengembalikan `gagal` n kali berturut-turut (n ditentukan pengguna), server asli itu tidak sehat dan status **unhealthy** (tidak sehat) ditampilkan di konsol.</li><li>Rentang nilai: 2-10 kali.Nilai default: 3 kali</li> | 3 kali |
| Ambang Batas Sehat | <li>Jika pemeriksaan kesehatan mengembalikan `berhasil` n kali berturut-turut (n ditentukan pengguna), server asli itu sehat dan status **healthy** (sehat) ditampilkan di konsol.</li><li>Rentang nilai: 2-10 kali.Nilai default: 3 kali.</li> | 3 kali |

Selesaikan konfigurasi pemeriksaan kesehatan seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/a05f5672d4999a60f6e01b74df38fc6b.png)

### Langkah 3.Mengikat server asli
Klik **Bind** (Ikat) di halaman **Listener Management** (Manajemen Pendengar) dan pilih server asli yang akan diikat di jendela pop-up, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7ad71ca47183798e8cb54dfd25b9cdb3.png)

Konfigurasi seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ef63b9817686f4743408cb6e7fba19f3.png)

>?Jika Anda mengonfigurasi beberapa pendengar ke instance CLB klasik dan mengikat beberapa server asli, setiap pendengar akan meneruskan permintaan ke semua server asli sesuai konfigurasinya.

### Langkah 4.Grup keamanan (opsional)
Anda dapat mengonfigurasi grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Untuk informasi selengkapnya, lihat [Mengonfigurasi Grup Keamanan CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Langkah 5.Modifikasi atau hapus satu pendengar (opsional)
Jika Anda perlu memodifikasi atau menghapus pendengar yang ada, pilih pendengar di halaman **Listener Management** (Manajemen Pendengar) dan klik **Modify** (Modifikasi) atau **Delete** (Hapus).
![](https://main.qcloudimg.com/raw/b4003107882decddea5828bf887dab40.png)
