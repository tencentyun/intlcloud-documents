## Skenario

Layanan Windows Time (W32Time) menyinkronkan waktu antara sistem lokal dan server sumber jam. Layanan ini menggunakan NTP untuk menyinkronkan jam komputer di jaringan. Berikut ini menggunakan CVM yang menjalankan Windows Server 2012 sebagai contoh untuk menjelaskan cara mengaktifkan layanan NTP dan mengubah alamat IP server sumber jam.

## Petunjuk

1. Login ke CVM Windows.
2. Di desktop, pilih <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > **Task Manager** (Pengelola Tugas) > **Services** (Layanan) untuk membuka jendela **Services** (Layanan).
3. Di jendela **Services** (Layanan) yang muncul, klik dua kali **Windows Time** (Waktu Windows), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
4. Di jendela **Windows Time Properties (Local Computer)** (Properti Waktu Windows (Komputer Lokal)) yang muncul, atur **Startup type** (Jenis startup) ke **Automatic** (Otomatis) dan **Service status** (Status layanan) ke **Running** (Berjalan), lalu klik **OK** (OKE), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
5. Di bilah tugas desktop, klik ikon waktu di sudut kanan bawah dan klik **Change date and time settings…** (Ubah pengaturan tanggal dan waktu…), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)
6. Di jendela **Date and Time** (Tanggal dan Waktu) yang muncul, klik tab **Internet Time** (Waktu Internet), lalu klik **Change settings** (Ubah pengaturan), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)
7. Di jendela **Internet Time Settings** (Pengaturan Waktu Internet) yang muncul, masukkan nama domain atau alamat IP server sumber jam target di kotak teks **Server** (Server) dan klik **OK** (OKE), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)



