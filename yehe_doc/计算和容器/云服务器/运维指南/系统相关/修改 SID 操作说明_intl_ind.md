## Skenario

Sistem operasi Microsoft menggunakan pengidentifikasi keamanan (SID) untuk mengidentifikasi komputer dan pengguna. Instans CVM yang dibuat dengan citra yang sama akan memiliki SID yang sama dan mungkin mengalami masalah login domain. Jika perlu membangun lingkungan domain Windows, Anda perlu memodifikasi SID.
Dokumen ini mengambil CVM dengan sistem operasi Windows Server 2012 sebagai contoh untuk menjelaskan cara memodifikasi SID menggunakan alat sysprep dan sidchg dari sistem.

## Catatan

- Ini hanya berlaku untuk Windows Server 2008 R2, Windows Server 2012, dan Windows Server 2016.
- Untuk memodifikasi SID secara massal, Anda dapat membuat citra kustom (pilih "jalankan sysprep untuk membuat citra").
- Memodifikasi SID dapat menyebabkan kehilangan data atau kerusakan sistem. Sebaiknya buat snapshot atau citra disk sistem terlebih dahulu.

## Petunjuk

### Menggunakan sysprep untuk memodifikasi SID

> 
> - Setelah menggunakan sysprep untuk mengubah SID, atur ulang beberapa parameter sistem secara manual, termasuk informasi konfigurasi IP.
> - Saat Anda menggunakan sysprep untuk memodifikasi SID, C:\Users\ Administrator akan diatur ulang dan beberapa data pada disk sistem akan dihapus. Harap cadangkan data.
> 
1. [Login ke CVM Linux melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Di antarmuka sistem operasi, klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run** (Jalankan), masukkan **cmd** (cmd), dan tekan **Enter** (Enter) untuk membuka baris perintah Admin.
3. <span id="step_03">Di baris perintah admin, jalankan perintah berikut untuk menyimpan konfigurasi jaringan saat ini.</span>
```
ipconfig /all
```
4. Di baris perintah admin, jalankan perintah berikut untuk membuka alat sysprep.
```
C:\Windows\System32\Sysprep\sysprep.exe
```
5. Di jendela “System Preparation Tool 3.14” (Alat Penyiapan Sistem 3.14) yang muncul, buat konfigurasi berikut.
 - Atur **System Cleanup Action** (Tindakan Pembersihan Sistem) menjadi **Enter System Out-of-Box Experience (OOBE)** (Masukkan Pengalaman Pertama Penggunaan Sistem (OOBE)) dan centang **General** (Umum).
 - Atur **Shutdown Options** (Opsi Pematian) ke **Reboot** (Boot ulang).
6. Klik **OK** (OKE), dan sistem akan dimulai ulang secara otomatis.
7. Setelah startup selesai, ikuti wizard untuk menyelesaikan konfigurasi (memilih bahasa, mengatur ulang kata sandi, dll).
8. Di antarmuka sistem operasi, klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Run** (Jalankan), masukkan **cmd** (cmd), dan tekan **Enter** (Enter) untuk membuka baris perintah Admin.
9. Jalankan perintah berikut untuk memverifikasi apakah SID telah dimodifikasi.
```
whoami /user
```
Jika pesan yang mirip dengan berikut ini ditampilkan, SID telah diubah.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
10. Atur ulang informasi ENI (seperti alamat IP, alamat gateway, DNS, dll.) berdasarkan informasi konfigurasi jaringan yang disimpan di [Langkah 3](#step_03).


### Menggunakan sidchg untuk memodifikasi SID

1. Login ke CVM.
2. Akses dan unduh fitur sidchg melalui browser IE.
Alamat unduhan fitur sidchg: `http://www.stratesave.com/html/sidchg.html`
3. Menggunakan baris perintah admin untuk menjalankan perintah berikut dan membuka fitur sidchg, seperti yang ditunjukkan di bawah ini:
Misalnya, fitur sidchg disimpan di drive C: dan namanya adalah sidchg64-2.0p.exe.
![](https://main.qcloudimg.com/raw/284926ae1eae88228fb009f247b82068.png)
`/R` berarti mulai ulang otomatis setelah modifikasi, dan` /S` berarti pematian setelah modifikasi. Untuk detailnya, harap lihat [Petunjuk Resmi SIDCHG](http://www.stratesave.com/html/sidchg.html).
4. Masukkan kunci lisensi atau kunci uji coba seperti yang diminta oleh halaman, dan tekan **Enter** (Enter).
5. Masukkan **Y** (Y) seperti yang diminta oleh halaman, dan tekan **Enter** (Enter), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/43c19634475517b183402d15fa32e962.png)
6 Di kotak perintah untuk memodifikasi SID, klik [OK] untuk mengatur ulang SID, seperti yang ditunjukkan di bawah ini:
Sistem akan dimulai ulang selama pengaturan ulang.
![](https://main.qcloudimg.com/raw/b59ec21417cc0de1fd7d851fcd8a2a3b.png)
7. Setelah startup selesai, klik kanan <img src = "https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style = "margin: 0;">> **Run** (Jalankan), masukkan **cmd** (cmd), dan tekan **Enter** (Enter) untuk membuka baris perintah admin.
8. Jalankan perintah berikut untuk memverifikasi apakah SID telah dimodifikasi.
```
whoami /user
```
Jika pesan yang mirip dengan berikut ini ditampilkan, SID telah diubah.
![](https://main.qcloudimg.com/raw/34efb1f4128c753e6c0546f3e8d58678.png)
