## Ikhtisar
Dokumen ini menjelaskan cara login ke instans Windows dari perangkat seluler yang berbeda menggunakan Microsoft Remote Desktop.

## Perangkat Seluler yang Berlaku
Perangkat iOS dan Android

## Prasyarat
- Instans CVM dalam status **Running** (Berjalan).
- Anda sudah memiliki akun administrator dan kata sandi untuk login ke instans.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
 - Jika lupa kata sandi, Anda dapat [atur ulang sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
- IP publik telah dibeli untuk instans CVM Anda, dan port 3389 terbuka. Port ini terbuka secara default untuk instans CVM yang dibeli dengan konfigurasi cepat.

## Petunjuk
>? Dokumen ini menggunakan perangkat iOS sebagai contoh. Langkah-langkah untuk perangkat Android hampir sama.
>
1. Unduh Microsoft Remote Desktop dan mulai.
2. Di halaman **PC** (PC), ketuk **+** (+) di sudut kanan atas, lalu ketuk **Add PC** (Tambahkan PC).
2. Konfigurasikan informasi login untuk menambahkan PC.
 - **PC name** (Nama PC): alamat IP publik instans CVM Anda. Untuk informasi selengkapnya, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
 - **User account** (Akun pengguna): secara default, **Ask when required** (Tanya saat diperlukan) dipilih.
4. Ketuk **Save** (Simpan).
5. Di halaman **PCs** (PC), pilih instans untuk login dan masukkan akun administrator dan kata sandinya.
 - **User name** (Nama pengguna): masukkan akun administrator `Administrator`.
 - **Password** (Kata sandi): masukkan kata sandi login instans.
6. Ketuk **Continue** (Lanjutkan). Jika halaman yang ditunjukkan pada gambar berikut ditampilkan, artinya login berhasil.
 ![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)
