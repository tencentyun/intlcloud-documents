## Skenario Operasi
Untuk menonaktifkan akun database yang ada, akun tersebut harus dihapus di Konsol TencentDB for MySQL.
>!
>- Akun database tidak dapat dipulihkan setelah dihapus.
>- Untuk menghindari penghapusan yang tidak disengaja mengganggu operasi normal bisnis, Anda perlu memastikan bahwa akun database yang akan dihapus tidak lagi digunakan oleh aplikasi apa pun.

## Petunjuk
1. Login ke [Konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom "Operasi" untuk masuk ke halaman manajemen instans.
2. Pilih tab **Database Management** (Manajemen Database) > **Manage Account** (Kelola Akun), cari akun yang akan dihapus, dan pilih **More** (Lainnya) > **Delete Account** (Hapus Akun).
![](https://main.qcloudimg.com/raw/8925fb7e9e11aa87466a5c9134773689.png)
3. Di kotak dialog pop-up, klik **OK** (OKE) untuk menghapus akun.
![](https://main.qcloudimg.com/raw/c1680eda4e1abd7fb7b16d061475ada7.png)

## API Terkait
| Nama API                                                      | Deskripsi     |
| -------------------------------------------------------- | -------- |
| [DeleteAccounts](https://intl.cloud.tencent.com/document/product/236/17501) | Menghapus akun TencentDB |

