## Ikhtisar
Anda dapat mengelola izin akun database yang ada di konsol TencentDB for MySQL. Secara khusus, Anda dapat memberikan atau menghapus akun database global serta izin tingkat objek.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pilih tab **Database Management** (Manajemen Database) > **Manage Account** (Kelola Akun), temukan akun yang izinnya akan dimodifikasi, dan klik **Modify Permissions** (Modifikasi Izin).
![](https://main.qcloudimg.com/raw/144f93c6415892d0fe828f3cf267c94e.png)
3. Di kotak dialog pop-up, pilih atau batalkan pilihan izin dan klik **OK** (OKE) untuk menyelesaikan modifikasi.
 - **Global Privileges** (Hak Istimewa Global): memberikan izin global ke semua database dalam instans.
 - **Object Level Privileges** (Hak Istimewa Tingkat Objek): memberikan izin ke database tertentu dalam instans.
![](https://main.qcloudimg.com/raw/19e5e35796516b6a3cd5a346ce4dcd74.png)

## API Terkait
| Nama API                                                      | Deskripsi     |
| ------------------------------------------------------------ | ------------ |
| [ModifyAccountPrivileges](https://intl.cloud.tencent.com/document/product/236/17496) | Mengubah izin akun instans TencentDB |

