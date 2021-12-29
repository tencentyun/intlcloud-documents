## Membuat Pendengar TCP/UDP

1. Login ke [konsol GAAP](https://console.cloud.tencent.com/gaap), masuk ke halaman **Access Management** (Manajemen Akses), dan klik **ID/Connection Name** (ID/Nama Koneksi) dari koneksi yang ditentukan.
2. Pada halaman yang muncul, pilih **TCP/UDP Listener Management**(Manajemen Pendengar TCP/UDP) > **Create** (Buat). Konfigurasi spesifiknya adalah sebagai berikut:
   1. Konfigurasi informasi pendengar untuk mengatur pemetaan protocol-port.
		![](https://qcloudimg.tencent-cloud.cn/raw/84cfd2802fbed4a46323e9e543aabcb6.png)
      
      - Jenis Server Asal: ini dapat berupa alamat IP atau nama domain, tetapi hanya satu jenis yang dapat dipilih untuk satu pendengar. (Catatan: saat ini, jenis nama domain tidak didukung untuk koneksi IPv6).
      - Dapatkan IP Klien: Anda dapat memilih TOA atau Proxy Protocol untuk mendapatkan IP pengguna yang nyata. Untuk informasi selengkapnya, lihat [Prinsip Dasar](https://intl.cloud.tencent.com/document/product/608/14429).
      - Port Pendengaran: ini adalah port akses dari koneksi akselerasi VIP. Rentang port yang valid: 1–64999 (port 21 saat ini tidak tersedia). Port tunggal atau rentang port berurutan didukung. Port harus unik. Maksimal 20 port berurutan dapat ditambahkan sekaligus, seperti 8000–8019.
   2. Konfigurasi kebijakan pemrosesan server asal; yaitu, jika pendengar terikat ke beberapa server asal, Anda harus memilih kebijakan penjadwalan untuk server asal.
      ![](https://qcloudimg.tencent-cloud.cn/raw/6da057ddde07681f3056153ad2bd3096.png)
      
      - RR: beberapa server asal melakukan origin-pull sesuai dengan kebijakan RR.
      - RR Tertimbang: beberapa server asal melakukan origin-pull sesuai dengan rasio bobot (Anda dapat mengatur bobot setiap server asal saat mengikat pendengar).
      - Koneksi Terkecil: ini berarti menjadwalkan server asal dengan jumlah koneksi paling sedikit terlebih dahulu.
      - Latensi Terkecil: ini berarti menjadwalkan server asal dengan latensi terkecil terlebih dahulu.
      - Server Asal Sekunder: Anda dapat memilih apakah akan mengaktifkan switch server asal primer/sekunder (untuk mengaktifkan fitur ini, Anda harus mengaktifkan pemeriksaan kesehatan server asal).
      <blockquote class="d-mod-notice">
      					<div class="d-mod-title d-explain-title">
      						<i class="d-icon-notice"></i>Catatan:
      					</div>
             <p>Pendengar dengan server asal tipe nama domain hanya mendukung **RR** dan **Least Connections** (Koneksi Terkecil) sebagai kebijakan penjadwalan dan tidak mendukung server asal sekunder.</p>
      				</blockquote>
3. Jika pendengar TCP digunakan, Anda dapat memilih untuk mengonfigurasi mekanisme pemeriksaan kesehatan untuk secara otomatis mendeteksi dan menghapus server asal pengecualian. Jika server asal sekunder diaktifkan, Anda tidak akan dapat menonaktifkan pemeriksaan kesehatan.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b317846881f8cc41983077c44df92ff0.png)
   
      - Waktu Respons habis: periode waktu respons server asal habis.
      - Interval Pemeriksaan Kesehatan: interval antara dua pemeriksaan kesehatan berturut-turut.
      - Ambang Batas Tidak Sehat: ini menunjukkan jumlah pemeriksaan gagal berturut-turut yang dilakukan oleh monitor sebelum server asal dianggap tidak sehat. Jika server asal dianggap tidak sehat selama pemeriksaan kesehatan, tidak ada lagi paket data yang akan diteruskan ke server tersebut hingga kembali ke status normal. 
      - Ambang Batas Sehat: ini menunjukkan jumlah pemeriksaan sukses berturut-turut yang dilakukan oleh monitor sebelum server asal dianggap sehat. Jika server asal dianggap sehat selama pemeriksaan kesehatan, paket data akan diteruskan ke server lagi.
4. Pilih apakah akan mengaktifkan persistensi sesi.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e2ee5834fc04cb1ef2d5ebda205a4193.png)
   
      - Persistensi Sesi: permintaan pengguna dari IP yang sama akan mengakses server asal yang sama.
      - Waktu Tunggu: durasi persistensi sesi. Ketika pendengar tidak memiliki permintaan untuk jangka waktu yang lebih lama dari waktu tunggu, persistensi sesi akan terputus secara otomatis.
3. Klik **Complete** (Selesai).

## Mengonfigurasi Pendengar TCP/UDP

Klik tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP) dan klik **Settings** (Pengaturan) di kolom **Operation** (Operasi) pada pendengar untuk mengganti namanya atau mengubah kebijakan penjadwalan dan parameter pemeriksaan kesehatannya.

## Mengikat Server Asal

1. Pilih tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP) dan klik **Bind Origin Server** (Ikat Server Asal) di kolom **Operation** (Operasi) dari "Pendengar TCP/UDP" yang dibuat untuk mengikat atau melepas ikatan satu atau beberapa server asal. Jika tidak ada informasi server asal yang ditemukan seperti yang ditampilkan di konsol, mungkin jenis server asal tidak valid atau server asal tidak ditambahkan ke [Manajemen Server Asal](https://console.cloud.tencent.com/gaap/listrs).
![](https://qcloudimg.tencent-cloud.cn/raw/2db94f9d3b3aae697dcfbb719fc44f40.png)
2. Pilih server asal dan konfigurasikan port origin-pull.
   - Jika RR primer/sekunder diaktifkan untuk pendengar, Anda perlu mengatur **Primary Origin Server** (Server Asal Utama) dan **Secondary Origin Server** (Server Asal Sekunder) di halaman **Bind Origin Server** (Ikat Server Asal).
   - Jika ingin mengatur port beberapa server asal, Anda dapat menggunakan fitur **Cover Port/Complement Port** di sudut kanan atas. Terlepas dari port server asal yang diatur sebelumnya, fitur **Cover Port** akan mengatur server asal tujuan yang Anda pilih ke nomor port yang Anda masukkan. Jika tidak ada port yang diatur untuk server asal tujuan yang dipilih, Anda dapat menggunakan fitur **Complement Port** untuk pengaturan terpadu guna mengurangi beban kerja berulang.
   - Jika kebijakan pendengar adalah **Weighted RR** (RR Tertimbang), Anda dapat mengatur bobot (1–100) server asal saat mengikatnya. Server asal dijadwalkan berdasarkan rasio bobotnya terhadap bobot total. Misalnya, jika bobot server asal 1 adalah 60 dan bobot server asal 2 adalah 80, maka rasio penjadwalannya adalah 60/(60 + 80) = 42,8% untuk server asal 1 atau 57,2% untuk server asal 2.
     ![](https://qcloudimg.tencent-cloud.cn/raw/d278faea3ac7a20e8a41b0a6f4dedbb0.png)
   - Jika diaktifkan, pemeriksaan kesehatan akan dimulai saat server asal terikat. Anda dapat menentukan apakah server asal normal dengan memeriksa status pendengar. Koneksi akselerasi hanya akan meneruskan paket ke server asal dalam status normal. Paket tidak akan diteruskan ke server asal pengeculian sampai mereka kembali ke status normal selama pemeriksaan kesehatan.
   - Jika tidak mengaktifkan pemeriksaan kesehatan, atau jika menggunakan pendengar UDP, koneksi akselerasi akan selalu meneruskan paket terlepas dari status server asal.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ed13a74bd6a1187caeb2969f4f471ade.png)
3. Konfirmasi konfigurasi.
   Setelah menyelesaikan konfigurasi server asal, klik **Next** (Selanjutnya) untuk masuk ke halaman konfirmasi konfigurasi, tempat Anda dapat melihat informasi koneksi dan detail pendengar yang saat ini dikonfigurasi.
![](https://qcloudimg.tencent-cloud.cn/raw/04e81f74564fc1604ef7f154afb1b383.png)
4. Klik **Complete** (Selesai).

## Menghapus Pendengar TCP/UDP

Buka tab **TCP/UDP Listener Management** (Manajemen Pendengar TCP/UDP) dan klik **Delete** (Hapus) di kolom **Operation** (Operasi) dari pendengar yang ditentukan untuk dihapus. Jika pendengar terikat ke server asal, Anda harus memilih **Allow force deletion of listeners with bound origin servers** (Izinkan penghapusan paksa pendengar dengan server asal terikat) terlebih dahulu. Setelah penghapusan, layanan akselerasi untuk port pendengar akan berhenti.
 ![](https://qcloudimg.tencent-cloud.cn/raw/200902ee0a9b4533825cae99a5050c94.png)