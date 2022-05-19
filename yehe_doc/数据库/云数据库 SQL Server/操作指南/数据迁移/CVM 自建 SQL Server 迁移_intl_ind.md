## Skenario Operasi
TencentDB for SQL Server mendukung migrasi data dari database SQL Server yang dibuat sendiri berbasis CVM ke instans TencentDB for SQL Server. Dokumen ini menjelaskan cara mengonfigurasi dan menjalankan tugas migrasi tersebut.
>!
>- Sebelum migrasi, pastikan bahwa versi SQL Server dari instans target tidak di bawah instans sumber.
>- Mendukung pengunggahan file bak tunggal dan file terkompresi tar untuk pemulihan.
>- Nama database yang dimigrasikan tidak boleh sama dengan nama instans TencentDB for SQL Server.

## Petunjuk
### Langkah 1. Buat tugas migrasi
1. Login ke [Konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) dan pilih **Data Transfer** (Transfer Data) di bilah sisi kiri.
2. Klik **Create Task** (Buat Tugas), masukkan nama tugas, informasi database sumber, dan informasi database target, lalu pilih **CVM-based self-created SQL Server database** (Database SQL Server berbasis CVM yang dibuat secara mandiri) sebagai jenis instans sumber.
![](https://main.qcloudimg.com/raw/7897cdebc4f35752e5029ea472fda64d.png)
3. Setelah mengklik **Next** (Selanjutnya), Anda perlu [mengonfigurasi instans SQL Server sumber](#step2) terlebih dahulu, lalu [mengonfigurasi tugas migrasi](#step3).
>?Jika muncul pesan kesalahan "Pemeriksaan info instans sumber gagal!", periksa item berikut untuk pemecahan masalah:
>- Apakah akun sa dari instans SQL Server sumber sudah ada.
>- Apakah kata sandi akun sa dari instans SQL Server sumber sudah benar.
>- Apakah konektivitas IP dan port dari instans SQL Server sumber berfungsi dengan baik.

<span id = "step2"></span>
### Langkah 2. Konfigurasikan instans SQL Server sumber
1. Aktifkan akun sa untuk instans SQL Server sumber.
2. Pilih **Allow remote connections to this server** (Izinkan koneksi jarak jauh ke server ini) di **Connections** (Koneksi) dan tetapkan periode waktu tunggu kueri jarak jauh yang wajar.

3. Pilih **SQL Server and Windows authentication mode** (mode autentikasi SQL Server dan Windows) di **Security** (Keamanan).

4. Aktifkan TCP/IP.

5. Aktifkan akun bawaan dan pilih **localsystem** (localsystem).

6. Izinkan komunikasi port SQL Server dan buka port 445 (untuk jaringan dasar) atau 49001 (untuk VPC) di Windows Firewall.
7. (Opsional) Jika **VPC** (VPC) dipilih sebagai **CVM Network** (Jaringan VPC), Anda perlu mengonfigurasi alat freeSSHd.
 1. Unduh dan instal [freeSSHd](http://www.freesshd.com/freeSSHd.exe) dengan opsi default dan setuju untuk memulai layanan freeSSHd.
 2. Klik dua kali ikon freeSSHd di desktop. Kemudian, klik kanan ikon freeSSHd di bilah tugas untuk membuka halaman Pengaturan untuk konfigurasi.
 3. Pilih tab **SSH** (SSH) dan atur port ke 49001 (port default di sini adalah 22, yang harus diubah menjadi 49001). ![](https://main.qcloudimg.com/raw/72d8780b85afa18524dc2fb81bcd6baf.png)
 4. Pilih tab **Server status** (Status server) dan mulai server SSH.
 5. Pilih tab **Authentication** (Autentikasi) dan pilih **Allowed** (Diizinkan) untuk autentikasi kata sandi.
 6. Pilih tab **Users** (Pengguna) dan masukkan pengguna `tencent_vpc_migrate` (nama pengguna ini tidak dapat diubah) dan kata sandi `tencent_vpc_migrate` (kata sandi ini tidak dapat diubah) seperti yang ditunjukkan di bawah ini:
 ![](https://main.qcloudimg.com/raw/9d8658d6f44517e7554c3416780f0a58.png)
 7. Gunakan `D:\dbbackup\` (**jalur ini tidak dapat diubah**) sebagai folder cadangan yang digunakan selama migrasi SQL Server. Pilih tab **SFTP** (SFTP) dan konfigurasikan jalur ini sebagai "jalur beranda SFTP".

<span id = "step3"></span>
### Langkah 3. Konfigurasikan tugas migrasi
Pilih jenis migrasi, atur database (dengan memilih database/tabel yang akan dimigrasikan), lalu klik **Save and Verify** (Simpan dan Verifikasi). Jika verifikasi gagal, Anda dapat memecahkan masalah seperti yang diminta.


### Langkah 4. Mulai tugas migrasi
Setelah tugas dibuat, kembali ke daftar tugas. Pada titik ini, status tugas adalah **Initializing** (Menginisialisasi). Pilih tugas dan klik **Start** (Mulai) untuk menyinkronkan tugas.

### Langkah 5. Selesaikan tugas migrasi
Setelah sinkronisasi data selesai (yaitu, bilah kemajuan menunjukkan 100%), Anda perlu mengklik **Complete** (Selesai) untuk mengakhiri proses sinkronisasi. Jika memilih **Incremental Synchronization** (Sinkronisasi Tambahan) saat mengonfigurasi tugas migrasi, Anda harus mengklik **Complete** (Selesai) saat bilah kemajuan menunjukkan 99%. Anda dapat memeriksa apakah migrasi berhasil di **Status** (Status).
 - Jika status tugas adalah **task successful* (tugas berhasil), artinya migrasi data berhasil.
 - Jika statusnya **task failed* (tugas gagal), artinya migrasi data gagal. Harap periksa informasi kegagalan, perbaiki dengan benar, lalu migrasikan lagi.
