## Ikhtisar

Dokumen ini mengambil PuTTY sebagai contoh untuk menjelaskan cara login ke instans Linux dari Windows menggunakan perangkat lunak login jarak jauh.


## OS yang Berlaku

Windows

## Metode Autentikasi

**Password** (Kata Sandi) atau **Key** (Kunci)

## Prasyarat
- Anda harus sudah memiliki akun admin dan kata sandi (atau kunci) untuk login ke instans.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
 - Jika lupa kata sandi Anda, harap [atur ulang kata sandi instans Anda](https://intl.cloud.tencent.com/document/product/213/16566).
- IP publik telah dibeli dan diperoleh untuk instans CVM Anda, dan port 22 terbuka (ini terbuka secara default untuk CVM yang dibeli dengan konfigurasi cepat).


## Petunjuk
<dx-tabs>
::: Logging\sin\swith\sa\spassword[](id:passwordLogin)
1. Unduh perangkat lunak login jarak jauh Windows, yaitu PuTTY.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">Klik di sini untuk mengunduh PuTTY</a></div>
2. Klik dua kali **putty.exe** (putty.exe) untuk membuka klien PuTTY.
3. Di jendela **PuTTY Configuration** (Konfigurasi PuTTY), masukkan konten berikut, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
Konfigurasikan parameter sebagai berikut:
 - **Host Name (or IP address)** (Nama Host (atau alamat IP)): IP publik untuk CVM. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk mendapatkan IP publik dari daftar instans dan halaman detail.
 - **Port** (Port): port CVM, yang harus “22”.
 - **Connection type** (Jenis koneksi): pilih **SSH** (SSH).
 - **Saved Sessions** (Sesi Tersimpan): masukkan nama sesi, seperti `test`.
 Setelah mengonfigurasi **Host Name** (Nama Host), konfigurasikan dan simpan **Saved Sessions** (Sesi Tersimpan). Anda dapat mengklik dua kali nama sesi yang disimpan di bawah **Saved Sessions** (Sesi Tersimpan) untuk login ke CVM.
4. Klik **Open** (Buka) untuk masuk ke antarmuka **PuTTY** (PuTTY). Command prompt **login as:** (login sebagai:) akan muncul.
5. Masukkan nama pengguna setelah **login as:** (login sebagai:), lalu tekan **Enter** (Enter).
6. Masukkan kata sandi setelah **Password** (Kata Sandi), lalu tekan **Enter** (Enter).
Kata sandi yang dimasukkan tidak ditampilkan secara default, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
Setelah login, Anda dapat melihat informasi tentang CVM tempat Anda masuk saat ini di sebelah kiri command prompt.
:::
::: Logging\sin\swith\sa\skey[](id:keyLogin)
1. Unduh perangkat lunak login jarak jauh Windows, yaitu PuTTY. Baik putty.exe dan puttygen.exe diperlukan.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">Unduh PuTTY</a></div><div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe" target="_blank" style="color: white; font-size:16px;">Unduh PuTTYgen</a></div>
2. Klik dua kali **puttygen.exe** (puttygen.exe) untuk membuka klien Putty Key.
3. Klik **Load** (Muat), pilih dan akses jalur penyimpanan kunci pribadi yang diunduh. Anda harus mengunduh dan menyimpan kunci pribadi Anda setelah membuat pasangan kunci. Untuk informasi selengkapnya, lihat [Mengelola Kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691)
Misalnya, pilih dan buka file kunci pribadi `david`, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>Di jendela **PuTTY Key Generator** (Pembuat Kunci PuTTY), masukkan nama kunci dan kata sandi kunci pribadi terenkripsi (opsional), dan klik **Save private key** (Simpan kunci pribadi), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. Di jendela pop-up, pilih jalur tempat kunci akan disimpan. Di bidang **File name** (Nama file), masukkan “Key Name.ppk”, lalu klik **Save** (Simpan). Misalnya, simpan file kunci pribadi `david` sebagai `david.ppk`, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/fad925e85923ac1d41afacde4a9c690c.png)
6. Klik dua kali **putty.exe** (putty.exe) untuk membuka klien PuTTY.
7. Di bilah sisi kiri, buka **Connection** (Koneksi) > **SSH** (SSH) > **Auth** (Auth), lalu masuk ke antarmuka konfigurasi **Auth** (Auth).
8. Klik **Browse** (Jelajahi), lalu pilih dan akses jalur tempat kunci disimpan, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
9. Beralih ke antarmuka konfigurasi **Session** (Sesi). Konfigurasikan CVM IP, port, dan jenis koneksi, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - **Host Name (or IP address)** (Nama Host (atau alamat IP)): IP publik untuk CVM. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk mendapatkan IP publik dari daftar instans dan halaman detail.
 - **Port** (Port): port CVM, yang harus “22”.
 - **Connection type** (Jenis koneksi): pilih **SSH** (SSH).
 - **Saved Sessions** (Sesi Tersimpan): masukkan nama sesi, seperti `test`.
 Setelah mengonfigurasi **Host Name** (Nama Host), konfigurasikan dan simpan **Saved Sessions** (Sesi Tersimpan). Anda dapat mengklik dua kali nama sesi yang disimpan di bawah **Saved Sessions** (Sesi Tersimpan) untuk login ke CVM.
9. Klik **Open** (Buka) untuk masuk ke antarmuka **PuTTY** (PuTTY). Command prompt **login as:** (login sebagai:) akan muncul.
10. Masukkan nama pengguna setelah **login as:** (login sebagai:), lalu tekan **Enter** (Enter).
11. Masukkan kata sandi yang dikonfigurasi di [Langkah 4](#Step4) setelah **Passphrase for key "imported-openssh-key":** (Frasa sandi untuk kunci "imported-openssh-key":), lalu tekan **Enter** (Enter).
Kata sandi yang dimasukkan tidak ditampilkan secara default, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
Setelah login, Anda dapat melihat informasi tentang CVM tempat Anda masuk saat ini di sebelah kiri command prompt.
:::
</dx-tabs>

## Operasi Selanjutnya

Setelah login ke CVM, Anda dapat membangun situs web atau forum pribadi atau melakukan operasi lain. Untuk informasi selengkapnya, lihat:
- [Menyiapkan WordPress](https://intl.cloud.tencent.com/document/product/213/33469)
- [Membuat Forum Discuz!](https://intl.cloud.tencent.com/document/product/213/34278)

