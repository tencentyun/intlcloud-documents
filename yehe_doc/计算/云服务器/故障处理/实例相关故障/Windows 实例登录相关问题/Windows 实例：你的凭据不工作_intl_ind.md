## Masalah

Pesan kesalahan berikut muncul saat mencoba login ke CVM Windows dari jarak jauh melalui protokol RDP, seperti menggunakan MSTSC.
Kredensial yang digunakan untuk menghubungkan ke `XXX.XXX.XXX.XXX` tidak berfungsi. Harap masukkan kredensial baru.
![](https://main.qcloudimg.com/raw/47a299873e3df8f1f160c1594fc56644.png)

## Solusi
>? Dokumen ini menggunakan CVM Tencent Cloud dengan sistem operasi Windows Server 2012 sebagai contoh. Prosedurnya mungkin sedikit berbeda sesuai dengan versi sistem operasi.
> Ikuti petunjuk di bawah ini dan coba hubungkan ke CVM Windows Anda setelah setiap langkah. Jika masalah berlanjut, lanjutkan ke langkah berikutnya.

### Langkah 1: ubah kebijakan akses jaringan
1. [Login ke instans Windows menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Setelah Anda login, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> untuk membuka jendela **Windows PowerShell**.
3. Di jendela **Windows PowerShell**, masukkan **gpedit.msc** dan tekan **Enter**. Jendela **Local Group Policy Editor** (Editor Kebijakan Grup Lokal) muncul.
4. Di bilah sisi kiri, perluas direktori berikut secara berurutan: **Computer Configuration** (Konfigurasi Komputer) > **Windows Settings** (Pengaturan Windows) > **Security Settings** (Pengaturan Keamanan) > **Local Policies** (Kebijakan Lokal) > **Security Options** (Opsi Keamanan).
5. Cari dan buka **Network access: Sharing and security model for local accounts** (Akses jaringan: Berbagi dan model keamanan untuk akun lokal) di bawah **Security Options** (Opsi Keamanan), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4ffb48c55d2f4aeedee127d97a4378ee.png)
6. Pilih **Classic - local users authenticate as themselves** (Klasik - pengguna lokal mengautentikasi sebagai diri mereka sendiri) dan klik **OK** (Oke), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/0f460bef7a7e35e1295149bb1f5f0d03.png)
7. Periksa apakah Anda dapat terhubung ke CVM Windows Anda sekarang.
 - Jika ya, masalah telah terpecahkan.
 - Jika tidak, lanjutkan ke “Langkah 2: ubah delegasi kredensial”.

### Langkah 2: ubah delegasi kredensial
1. Di bilah sisi kiri **Local Group Policy Editor** (Editor Kebijakan Grup Lokal), perluas direktori berikut secara berurutan: **Computer Configuration** (Konfigurasi Komputer) > **Administrative Templates** (Templat Administratif) > **System** (Sistem) > **Credentials Delegation** (Delegasi Kredensial).
2. Cari dan buka **Allow delegating saved credentials with NTLM-only server authentication** (Izinkan pendelegasian kredensial yang disimpan dengan autentikasi server khusus NTLM) di bawah **Credentials Delegation** (Delegasi Kredensial), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7643737fdfa2be299c21f6bc82b0165b.png)
3. Di jendela pop-up, pilih **Enabled** (Diaktifkan). Klik **Show…** (Tampilkan...) di bawah **Options** (Opsi), masukkan `TERMSRV/*` untuk **Show Contents** (Tampilkan Konten) dan klik **OK** (Oke), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/6a9af6aa4c3c3b3c4d1b9eba53d202b1.png)
4. Klik **OK** (Oke).
5. Di desktop, klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> untuk membuka jendela **Windows PowerShell**.
6. Di jendela **Windows PowerShell**, masukkan **gpupdate /force** dan tekan **Enter** untuk memperbarui kebijakan grup, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/98d0b757e65e3617145c05513ba652dc.png)
7. Periksa apakah Anda dapat terhubung ke CVM Windows Anda sekarang.
 - Jika ya, masalah telah terpecahkan.
 - Jika tidak, lanjutkan ke “Langkah 3: konfigurasikan kredensial lokal”.

### Langkah 3: konfigurasikan kredensial lokal
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> dan navigasikan ke **Control Panel** (Panel Kontrol) > **Users Accounts** (Akun Pengguna) > **Credential Manager** (Manajer Kredensial). Klik **Windows Credentials** (Kredensial Windows) untuk menampilkan kredensial Windows, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/2726e3d109fdaadd1d90a1f3e692601a.png)
2. Periksa apakah kredensial yang Anda gunakan untuk login ke CVM Windows Anda ada.
 - Jika tidak, lanjutkan ke langkah berikutnya untuk menambahkan kredensial Windows.
 - Jika ya, lanjutkan ke "Langkah 4: nonaktifkan berbagi yang dilindungi kata sandi".
3. Klik **Add a Windows credential** (Tambahkan kredensial Windows) untuk membuka jendela **Add a Windows Credential** (Tambahkan Kredensial Windows), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/87077862379ea7d9e86d5fdc7e0af1da.png)
4. Masukkan alamat IP, nama pengguna, dan kata sandi instans CVM, lalu klik **OK** (Oke).
>?
> - Alamat IP mengacu pada alamat IP publik instans CVM Anda. Untuk informasi selengkapnya, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
> - Nama pengguna default untuk instans Windows adalah `Administrator` dan kata sandi diatur saat Anda membuat instans. Jika lupa kata sandi, Anda dapat [mengatur ulang sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
>
5. Periksa apakah Anda dapat terhubung ke CVM Windows Anda sekarang.
 - Jika ya, masalah telah terpecahkan.
 - Jika tidak, lanjutkan ke “Langkah 4: nonaktifkan berbagi yang dilindungi kata sandi”.

### Langkah 4: nonaktifkan berbagi yang dilindungi kata sandi
1. Di desktop, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> dan navigasikan ke **Control Panel** (Panel Kontrol) > **Network and Sharing Center** (Pusat Jaringan dan Berbagi) > **Advanced sharing settings** (Pengaturan berbagi lanjutan), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d1cc8fd023642654091d1b152bb67ef1.png)
2. Luaskan tab **All Networks** (Semua Jaringan) , pilih **Turn off password protected sharing** (Nonaktifkan berbagi yang dilindungi kata sandi) di bawah **Password protected sharing** (Berbagi yang dilindungi kata sandi), dan klik **Save changes** (Simpan perubahan).
3. Periksa apakah Anda dapat terhubung ke CVM Windows Anda sekarang.
 - Jika ya, masalah telah terpecahkan.
 - Jika tidak, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) untuk bantuan.


