### Bagaimana cara login ke instans CVM menggunakan VNC?

Tencent Cloud memungkinkan pengguna untuk login ke instans CVM denganmenggunakan klien web VNC. Jika Anda tidak menginstal klien login jarak jauh atau tidak dapat login dengan menggunakan klien, Anda dapat menggunakan klien web VNC untuk login ke instans CVM. Anda dapat menggunakan klien web untuk login dari jarak jauh, melihat status instans CVM, dan melakukan manajemen instans dasar. Untuk membaca petunjuk terperinci, lihat dokumen berikut:
- [Login ke Instans Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32494)
- [Login ke Instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496)

### Bagaimana cara mengaktifkan login jarak jauh multi-pengguna di server Windows?

Server Windows mendukung login jarak jauh multi-pengguna. Untuk membaca petunjuk konfigurasi terperinci, lihat [Menyiapkan Login Jarak Jauh Multi-pengguna untuk CVM Windows](https://intl.cloud.tencent.com/document/product/213/32497).
Jika Anda gagal mengaktifkan login jarak jauh multi-pengguna di server Windows setelah mengikuti petunjuk pada dokumen di atas, mulai ulang instans dan coba login lagi.

### Bagaimana cara login ke instans yang menjalankan Ubuntu sebagai root?

Pengguna default untuk Ubuntu adalah `ubuntu`. `root` tidak diaktifkan secara default selama proses penginstalan. Jika perlu, Anda dapat mengaktifkan `root` dengan mengikuti petunjuk berikut ini:
1. Login ke instans CVM menggunakan `ubuntu`.
2. <span id="Step2"></span>Jalankan perintah berikut untuk mengatur kata sandi `root`:
```
root kata sandi sudo
```
3. Masukkan kata sandi `root` dan tekan **Enter**.
4. Masukkan kata sandi lagi dan tekan **Enter**.
Jika pesan berikut ditampilkan, kata sandi berhasil diatur:
```
kata sandi: kata sandi berhasil diperbarui
```
5. Jalankan perintah berikut untuk membuka `sshd_config`:
```
sudo vi /etc/ssh/sshd_config 
```
6. Tekan **i** untuk beralih ke mode pengeditan. Temukan `#Authentication` dan ubah nilai `PermitRootLogin` menjadi `ya`, seperti yang ditunjukkan pada gambar berikut:
> Jika `PermitRootLogin` dikomentari, hapus tanda komentar (`#`).
> 
![](https://main.qcloudimg.com/raw/359242f7e5df666d43459fe74abce72a.png)
7. Tekan **Esc** dan masukkan **:wq** untuk menyimpan file dan keluar dari vi.
8. Jalankan perintah berikut untuk memulai ulang layanan SSH.
```
mulai ulang ssh layanan sudo
```
9. Lihat [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436) tentang cara menggunakan informasi berikut untuk login ke instans CVM Anda yang menjalankan Ubuntu.
 - **Username** (Nama pengguna): root
 - **Password** (Kata Sandi): kata sandi yang diatur di [Langkah 2](#Step2).
 Login berhasil menggunakan root ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a8a6ec3e2499e08d051c9ee11fdcd85e.png)

### Apa yang harus saya lakukan jika saya tidak dapat terhubung (login) ke instans CVM setelah memulai ulang?

Masalah ini mungkin disebabkan oleh penggunaan CPU dan memori yang tinggi pada instans Anda. Untuk informasi selengkapnya, baca dokumen berikut:
- [Gagal Login ke CVM Linux Karena Penggunaan CPU dan Memori yang Tinggi](https://intl.cloud.tencent.com/document/product/213/32387)
- [Gagal Login ke CVM Windows Karena Penggunaan CPU dan Memori yang Tinggi](https://intl.cloud.tencent.com/document/product/213/32405)

### Apa yang harus saya lakukan saat saya terhubung ke instans CVM dari jarak jauh dan waktu koneksi habis?
Pastikan bahwa:
- Instans sedang berjalan.
- Instans dikaitkan dengan grup keamanan yang memiliki aturan grup keamanan yang diperlukan. Untuk membaca informasi terperinci, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
- Instans telah mengaktifkan SSH atau RDP.
- Instans telah membuka port yang sesuai. SSH menggunakan port 22 secara default dan RDP menggunakan port 3389 secara default.

### Mengapa koneksi jarak jauh saya ke instans Linux ditolak?
Pastikan bahwa:
- Instans telah mengaktifkan SSH atau RDP.
- Instans telah membuka port yang sesuai. SSH menggunakan port 22 secara default dan RDP menggunakan port 3389 secara default.

### Mengapa saya mendapatkan pesan nama pengguna atau kata sandi tidak valid saat terhubung dari jarak jauh ke instans Linux?
Pastikan bahwa:
- Anda menggunakan nama pengguna yang benar. Nama pengguna default untuk sebagian besar distribusi Linux adalah `root`. Namun, Ubuntu menggunakan `ubuntu`.
- Anda memasukkan kata sandi dengan benar. Jika Anda lupa kata sandi, atur ulang. Untuk membaca petunjuk terperinci, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Mengapa saya mendapatkan pesan nama pengguna atau kata sandi tidak valid saat terhubung dari jarak jauh ke instans Windows?
Pastikan bahwa:
- Anda menggunakan nama pengguna yang benar. Nama pengguna default untuk Windows adalah `Administrator`.
- Anda memasukkan kata sandi dengan benar. Jika Anda lupa kata sandi, atur ulang. Untuk membaca petunjuk terperinci, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).
- Untuk menggunakan pengguna yang tidak memiliki hak istimewa administrator untuk login, pengguna tersebut harus menjadi bagian dari grup Pengguna Desktop Jarak Jauh.

### Apakah Konsol mendukung login multi-pengguna melalui VNC?
Tidak. Jika satu pengguna sudah login, pengguna lain tidak akan bisa login.

### Apa yang harus saya lakukan jika saya lupa kata sandi login instans CVM?
Anda dapat mengatur ulang kata sandi. Untuk membaca petunjuk terperinci, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).

### Mengapa saya tidak dapat menggunakan Internet Explorer 8.0 untuk login ke instans?
Klien web VNC mendukung Internet Explorer 10 atau yang lebih baru. Harapkan unduh versi terbaru Internet Explorer.
Selain itu, sebaiknya Anda menggunakan Google Chrome karena Tencent Cloud Console menawarkan pengalaman pengguna yang lebih baik di Google Chrome daripada di Internet Explorer.

### Bagaimana cara login ke instans Linux saya dari jarak jauh?
- Tencent Cloud menyarankan [login ke instans Linux menggunakan mode login standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga bisa:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501).
- [Login ke instans Linux menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32494).

### Apa yang harus saya lakukan jika saya tidak dapat terhubung ke instans Linux?
Jika Anda tidak dapat terhubung ke instans Linux, lihat [Kegagalan Login Instans Linux](https://intl.cloud.tencent.com/document/product/213/32500) untuk membaca petunjuk pemecahan masalah.
Jika masalah ini berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### Apa yang harus saya lakukan jika saya tidak dapat terhubung ke instans Windows?
Jika Anda tidak dapat terhubung ke instans Windows, lihat [Kegagalan Masuk CVM](https://intl.cloud.tencent.com/document/product/213/10339) untuk petunjuk pemecahan masalah.
Jika masalah ini berlanjut, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1).

### Apa yang harus saya lakukan jika menemukan bahwa instans CVM saya login dari lokasi yang tidak biasa?
Jika Anda menemukan instans CVM Anda login dari lokasi yang tidak dikenali:
1. Periksa kembali waktu login dari lokasi login yang tidak biasa dan periksa apakah Anda atau administrator lain login pada waktu itu.
2. Jika tidak, ikuti langkah-langkah di bawah ini:
 1. [Atur ulang kata sandi](https://intl.cloud.tencent.com/document/product/213/16566) segera.
 2. Periksa instans Anda dari virus atau trojan.
 3. Gunakan grup keamanan untuk [membatasi login ke alamat IP tertentu](https://intl.cloud.tencent.com/document/product/213/32369).



