## Analisis Proses Pematian CVM

### Proses pematian
>?Lihat [Mematikan Instans](https://intl.cloud.tencent.com/document/product/213/4929) untuk mengetahui operasi terkait.
>
Proses pematian instans Tencent Cloud Windows adalah sebagai berikut:
1. Host mengirimkan perintah pematian melalui libvirt pada protokol QMP ke komponen `qemu`.
2. Komponen `qemu` mentransfer perintah pematian ke CVM dengan mengganggu ACPI (untuk informasi selengkapnya, lihat dokumen teknis di VMCS).
3. Setelah menerima sinyal pematian, instans Windows keluar dari aplikasi dan proses layanan.
4. Tutup proses layanan inti.
5. Mematikan daya.
>! Urutan penutupan aplikasi dan layanan pada langkah 3-4 dapat berbeda-beda tergantung pada pengaturan sistem.

Windows adalah sistem sumber tertutup. Sistem ini menyediakan API yang memungkinkan program mode kernel dan mode pengguna memengaruhi proses pematian. Beberapa layanan Windows yang berjalan juga akan memengaruhi proses pematian, menambah waktu pematian, dan menyebabkan kegagalan pematian.

### Pematian paksa
Dalam skenario virtualisasi, selain metode pematian seperti soft shutdown yang diinisialisasi oleh sinyal sistem dan pemberitahuan pesan, Anda juga dapat mematikan CVM secara paksa melalui **forced shutdown** (pematian paksa).
Pematian paksa dapat memengaruhi Windows dan pengalaman pengguna dalam dua aspek berikut:
1. Pematian paksa mengganggu beberapa layanan dan aplikasi dan menyebabkan operasi berjalan tidak normal seperti dokumen yang belum disimpan dan proses WindowsUpdate yang belum selesai.
2. Selama proses pematian, sistem NTFS (atau sistem FAT32 sebelumnya) Windows menulis data kunci ke disk. Pematian paksa dapat mengakibatkan kegagalan penulisan dan menyebabkan Windows percaya bahwa sistem file NTFS rusak.

Oleh karena itu, sebaiknya **first use soft shutdown** (gunakan soft shutdown terlebih dahulu) pada instans Windows.

## Skenario Kegagalan Pematian
Sistem Windows mungkin mengalami masalah yang memengaruhi proses pematian dan menyebabkan kegagalan pematian, termasuk namun tidak terbatas pada:
1. Proses WindowsUpdate dapat memperpanjang waktu pematian. Sistem Windows dapat melakukan operasi patch selama proses pematian dan memunculkan pesan seperti "Please do not power off or unplug your computer" (Jangan matikan atau mencabut sakelar komputer Anda).
2. Jika sistem Windows mengaktifkan mekanisme "Pelacak Peristiwa Pematian" dan perlu dinonaktifkan karena kesalahan layanan sistem atau driver, sistem akan meminta pengguna untuk mengirimkan deskripsi kesalahan berdasarkan konfigurasi. Sistem akan menunggu Anda menyelesaikan operasi ini sebelum pematian.
3. Windows tidak mendukung pematian tanpa login. Dalam konfigurasi ini, perintah soft shutdown yang dikirim dari virtual host akan dibuang oleh Windows, sehingga Windows tidak akan dimatikan.
4. Sebelum pematian, Windows akan menyiarkan pesan ke setiap layanan dan aplikasi. Jika aplikasi gagal memberikan tanggapan afirmatif, Windows tidak akan memulai pematian. Dalam hal ini, Anda dapat mengonfigurasi Windows untuk mengabaikan proses respons ini.
5. Jika Anda mengonfigurasi manajemen daya di Windows untuk mengabaikan atau tidak melakukan apa pun **When I press the power button** (Saat saya menekan tombol daya), Windows akan mengabaikan peristiwa pematian yang diterima dari host virtual.
6. Berdasarkan pengaturan manajemen daya, Windows akan masuk ke mode Tidur dan mengabaikan peristiwa pematian.
7. Jika sistem Windows itu sendiri rusak karena perangkat lunak berbahaya atau infeksi Trojan atau virus lain, Windows dapat mencegah pematian.

Tencent Cloud telah memecahkan sebagian besar kegagalan pematian saat merilis citra publik Windows untuk memastikan soft shutdown. Namun, jika Windows Anda terinfeksi virus atau Trojan, sistem rusak, atau pengaturan Windows disesuaikan lagi, soft shutdown mungkin gagal.
**Forced shutdown involves risks. Therefore, we recommend that you use it only when you really have to.** (Pematian paksa bisa menimbulkan risiko. Oleh karena itu, sebaiknya gunakan hanya saat Anda harus melakukannya.)


