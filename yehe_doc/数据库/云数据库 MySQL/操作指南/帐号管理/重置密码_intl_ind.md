## Skenario Operasi
Jika Anda lupa kata sandi akun database Anda atau perlu mengubahnya saat menggunakan TencentDB for MySQL, Anda dapat mengatur ulang kata sandi di konsol.
>?
>- Untuk TencentDB for MySQL, fungsi pengaturan ulang kata sandi telah terhubung ke [CAM](https://intl.cloud.tencent.com/document/product/236/14469); oleh karena itu, sebaiknya lakukan kontrol yang lebih ketat atas izin ke API pengaturan ulang kata sandi atau sumber daya sensitif instans TencentDB for MySQL dengan memberikan izin tersebut hanya kepada personel yang sesuai.
>- Untuk keamanan data, sebaiknya atur ulang kata sandi secara berkala minimal tiga bulan sekali.


## Petunjuk
1. Login ke [Konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom "Operasi" untuk masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Manajemen Database) > **Manage Account** (Kelola Akun), cari akun yang akan digunakan untuk mengatur ulang kata sandi, dan pilih **More** (Lainnya) > **Reset Password** (Atur Ulang Kata Sandi).
![](https://main.qcloudimg.com/raw/f8ff03d7b57ab9c96231f98920704441.png)
3. Di kotak dialog pop-up, masukkan dan konfirmasi kata sandi baru, lalu klik **OK** (OKE).
>?Kata sandi database harus berisi 8–64 karakter yang setidaknya dua jenis karakter berikut: huruf, angka, dan simbol khusus (_+-&=!@#$%^*()).
> 
![](https://main.qcloudimg.com/raw/8a2a4d08a1d14cfbcbb683f804bfeb78.png)

## API Terkait

| Nama API | Deskripsi |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | Memodifikasi kata sandi akun TencentDB |
