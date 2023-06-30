## Ikhtisar

Dokumen ini menjelaskan cara mengunggah file dari komputer Windows lokal ke CVM Windows menggunakan Microsoft Terminal Services Client (MSTSC). 

## Prasyarat

Pastikan CVM Windows dapat mengakses jaringan publik.

## Petunjuk
>? Dokumen ini mengambil komputer Windows 7 sebagai contoh. Prosedurnya mungkin sedikit berbeda sesuai dengan versi sistem operasi.
>
### Mendapatkan IP publik
Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index), buka halaman **Instances** (Instans), dan catat IP publik CVM tempat Anda ingin mengunggah file.

### Mengunggah file
1. Tekan **Windows + R** (Windows + R) di komputer lokal untuk membuka jendela **Run** (Jalankan).
2. Di jendela pop-up **Run** (Jalankan), masukkan **mstsc** (mstsc), dan klik **OK** (OKE) untuk membuka kotak dialog **Remote Desktop Connection** (Koneksi Desktop Jarak Jauh).
3. Di kotak dialog pop-up, masukkan alamat IP publik CVM dan klik **Show Options** (Tampilkan Opsi).
4. Pada tab **General** (Umum), masukkan alamat IP publik CVM dan nama pengguna “Administrator”.
5. Pilih tab **Local Resources** (Sumber Daya Lokal) dan klik **More** (Lainnya).
6. Di jendela pop-up **Local devices and resources** (Perangkat dan sumber daya lokal), pilih modul **Drives** (Drive), periksa disk lokal tempat file yang akan diunggah, dan klik **OK** (OKE).
7. Setelah konfigurasi lokal selesai, klik **Connect** (Hubungkan) untuk login ke Windows CVM dari jarak jauh.
8. Pilih <img src="https://main.qcloudimg.com/raw/ef8fb18be7880d8b48ce402b973f22dc.png" style="margin:-3px 0px"> dan klik **Computer** (Komputer) pada Windows CVM, dan Anda dapat melihat disk lokal terpasang.
>? Langkah ini menggunakan CVM Tencent Cloud Windows dengan sistem operasi Windows Server 2016 sebagai contoh. Prosedurnya mungkin sedikit berbeda sesuai dengan versi sistem operasi.
>
9. Klik dua kali untuk membuka disk lokal yang terpasang. Salin file lokal yang diinginkan ke drive lain dari CVM Windows.
Misalnya, salin file A dari disk lokal (E) ke drive C CVM Windows.

### Mengunduh file
Untuk mengunduh file dari Windows CVM ke komputer Anda, Anda hanya perlu menyalin file yang diinginkan dari CVM ke disk lokal yang terpasang.


