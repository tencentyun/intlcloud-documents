
## Ikhtisar
TencentDB for MySQL mendukung pengimporan file SQL di konsol. Fitur ini memungkinkan Anda menjalankan pernyataan SQL dalam database yang dipilih. Anda juga dapat menggunakan fitur ini untuk membuat database/tabel dan mengubah struktur tabel untuk menginisialisasi atau memodifikasi instans.
>?Hanya instans TencentDB for MySQL dua node dan tiga node yang mendukung pengimporan file SQL.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Pilih **Database Management** (Pengelolaan Database) > **Database List** (Daftar Database) dan klik **Import Data** (Impor Data).
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
3. Pada halaman pop-up, klik **Add File** (Tambahkan File) untuk mengimpor file. Setelah pengunggahan selesai, klik **Next** (Selanjutnya).
>?
>- Untuk menghindari ketidaktersediaan database yang disebabkan oleh kerusakan tabel sistem, mohon jangan mengimpor data dari tabel sistem seperti tabel `mysql.user`. 
>- Hanya impor tambahan yang didukung. Jika ada data usang dalam database, hapus data sebelum operasi pengimporan.
>- Satu file SQL yang akan diimpor tidak boleh melebihi 2 GB. Nama file hanya boleh berisi huruf, angka, dan garis bawah.
>- File yang diunggah berlaku selama 14 hari dan akan dihapus secara otomatis setelah habis masa berlakunya.
>
<img src="https://main.qcloudimg.com/raw/fd6c70707a8722ca64a87f71978e2a2a.png">
4. Pada halaman pemilihan database, pilih database target dan klik **Next** (Selanjutnya).
5. Pada halaman konfirmasi, setelah mengonfirmasi bahwa data yang diimpor sudah benar, masukkan akun dan kata sandi dan klik **Impor** (Impor).
>!
>- Proses impor tidak dapat dikembalikan. Harap konfirmasikan informasi impor.
>- Jika Anda lupa kata sandi, harap atur ulang seperti yang diinstruksikan di [Mengatur Ulang Kata Sandi](https://intl.cloud.tencent.com/document/product/236/31901).
> 
![](https://main.qcloudimg.com/raw/e21ccbe6c1f0a95cd46b4387fea1fab1.png)

