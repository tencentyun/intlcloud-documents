
### Mengapa grup keamanan memiliki aturan penolakan secara default?

Aturan grup keamanan berlaku secara berurutan mulai dari atas ke bawah. Jika aturan izinkan yang ditetapkan sebelumnya sudah berlaku, aturan lain akan ditolak secara default. Jika aturan izinkan ini membuka semua port ke Internet, aturan penolakan terakhir tidak akan berlaku. Kami menyediakan pengaturan default ini karena masalah keamanan.

### Bagaimana cara menyesuaikan prioritas grup keamanan?

Untuk informasi selengkapnya, lihat [Menyesuaikan Prioritas Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/35375).

### Jika saya salah mengikat grup keamanan ke sebuah instans, apa saja dampaknya pada instans tersebut? Bagaimana cara memperbaiki masalah ini?

**Potential problems** (Potensi Masalah)

- Anda mungkin gagal terhubung dalam jarak jauh ke instans Linux melalui SSH atau instans Windows melalui desktop jarak jauh.
- Anda mungkin gagal melakukan ping ke IP publik dan alamat IP pribadi dari instans CVM dalam jarak jauh di grup keamanan ini.
- Anda mungkin gagal mengakses melalui HTTP layanan web yang diekspos oleh instans CVM dalam grup keamanan ini.
- Instans CVM dalam grup keamanan ini mungkin gagal mengakses layanan Internet.

**Solutions** (Solusi)

- Jika salah satu masalah yang disebutkan di atas terjadi, Anda bisa membuka **Security Groups** (Grup Keamanan) di Konsol dan mengubah aturan grup keamanan. Misalnya, Anda bisa mengubah aturan menjadi "bind only all-ports-open security groups by default" (hanya mengikat grup keamanan semua port yang terbuka secara default).
- Untuk informasi selengkapnya tentang cara menyetel aturan grup keamanan, lihat [Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

### Apa yang dimaksud dengan arah dan kebijakan grup keamanan?

Ada arah grup keamanan keluar dan masuk. Arah keluar memfilter lalu lintas keluar dari instans CVM, sedangkan arah masuk memfilter lalu lintas masuk dari instans CVM.
Kebijakan grup keamanan dibagi menjadi **allow** (izinkan) dan **refuse** (tolak) lalu lintas.

### Bagaimana urutan penerapan kebijakan grup keamanan?

Kebijakan grup keamanan berlaku secara berurutan mulai dari atas ke bawah saat lalu lintas masuk melalui grup keamanan. Setelah lalu lintas sesuai dengan kebijakan, maka kebijakan tersebut akan segera diterapkan.

### Mengapa alamat IP yang sudah ditolak oleh grup keamanan masih bisa mengakses instans CVM?

Kemungkinan penyebabnya adalah sebagai berikut:
- CVM terikat ke beberapa grup keamanan, dan alamat IP ini diizinkan oleh grup keamanan lain di antaranya.
- Alamat IP ini milik layanan publik Tencent Cloud yang disetujui.

### Bisakah iptable digunakan bersama dengan grup keamanan?

Ya. Grup keamanan dan iptable dapat digunakan secara bersamaan. Lalu lintas Anda akan difilter dua kali dengan arah berikut:
- Keluar: proses dalam instans Anda > iptable > grup keamanan.
- Masuk: grup keamanan > iptable > proses di instans Anda.

### Mengapa grup keamanan tidak bisa dihapus meski semua instans CVM sudah dikembalikan?

Periksa apakah ada instans CVM yang masih ada di tempat sampah. Jika grup keamanan masih terikat ke instans CVM di tempat sampah, grup keamanan tersebut tidak bisa dihapus.

### Bisakah nama grup keamanan kloning sama dengan nama grup keamanan di wilayah target?

Tidak. Namanya harus berbeda dari nama grup keamanan yang ada di wilayah target.

### Bisakah grup keamanan dikloning ke pengguna yang berbeda?

Tidak. Untuk sekarang, fitur ini tidak didukung.

### Apakah ada Tencent Cloud API yang mendukung kloning grup keamanan di seluruh proyek dan wilayah?

Meski dukungan MC disediakan untuk membantu pelanggan yang menggunakan Konsol, saat ini tidak ada Tencent Cloud API yang bisa langsung digunakan untuk tujuan ini. Anda bisa menggunakan Tencent Cloud API asli guna mengimpor dan mengekspor batch aturan grup keamanan untuk mengkloning grup keamanan di seluruh proyek dan wilayah secara tidak langsung.

### Jika saya mengkloning grup keamanan di seluruh proyek dan wilayah, apakah instans CVM yang dikelola oleh grup keamanan juga akan disalin?

Tidak. Jika grup keamanan dikloning di seluruh wilayah, hanya aturan masuk dan keluar dari grup keamanan asli yang akan disalin. Oleh karena itu, Anda perlu mengikat instans CVM ke grup keamanan secara terpisah.

### Apa itu grup keamanan?
Grup keamanan adalah firewall virtual yang menampilkan pemfilteran paket data stateful. Ini digunakan untuk mengonfigurasi kontrol akses jaringan CVM, Cloud Load Balancer, TencentDB, dan instans lainnya sambil mengontrol lalu lintas keluar dan masuknya. Ini adalah sarana penting untuk isolasi keamanan jaringan.

Setiap instans CVM minimal terikat ke satu grup keamanan, yang harus ditentukan pada saat instans dibuat. Instans CVM saling berhubungan dalam grup keamanan yang sama tapi tidak bisa berkomunikasi dengan instans CVM di seluruh grup keamanan. Namun, Anda bisa mengotorisasi interkoneksi antara dua grup keamanan. Untuk informasi selengkapnya, lihat [Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

### Mengapa saya harus memilih grup keamanan saat membuat instans CVM?
Sebelum membuat instans CVM, Anda harus memilih grup keamanan untuk mempartisi domain keamanan lingkungan aplikasi dan mengotorisasi aturan grup keamanan agar bisa menerapkan isolasi keamanan jaringan dengan benar.

### Apa yang harus saya lakukan saat membuat instans CVM jika belum membuat grup keamanan?
Dalam hal ini, Anda bisa membuat grup keamanan.
Grup keamanan mendukung aturan berikut. Anda bisa membuka IP dan port sesuai kebutuhan.
- ICMP: membuka protokol ICMP dan memungkinkan ping server melalui jaringan publik.
- TCP:80: membuka port 80 dan mengizinkan akses ke layanan Web melalui HTTP.
- TCP:22: membuka port 22 dan memungkinkan koneksi jarak jauh ke CVM Linux melalui SSH.
- TCP:443: membuka port 443 dan mengizinkan akses ke layanan Web melalui HTTPS.
- TCP:3389: membuka port 3389 dan memungkinkan koneksi jarak jauh ke CVM Windows melalui RDP.
- Buka jaringan pribadi: membuka jaringan pribadi dan mengizinkan akses jaringan pribadi di antara berbagai sumber daya cloud (IPv4).


### Dalam situasi seperti apa aturan grup keamanan default akan digunakan untuk grup keamanan?
Aturan grup keamanan default akan digunakan dalam situasi berikut:
- Jika Anda membeli dan membuat instans CVM dengan **Custom Configuration**, (Konfigurasi Kustom) grup keamanan default yang menggunakan aturan keamanan default akan dibuat secara otomatis. Aturan masuknya membuka semua port dan aturan keluarnya mengizinkan semua akses.
Namun, karena alasan keamanan, kami sarankan agar Anda mengaitkan CVM dengan grup keamanan baru yang hanya membuka port saat benar-benar dibutuhkan untuk menghindari risiko keamanan yang tidak perlu.
- Anda bisa memilih templat saat membuat grup keamanan di Konsol CVM. Saat ini, templat yang didukung termasuk login Windows, login Linux, Ping, HTTP(80) dan HTTPS(443).
