TencentDB for SQL Server mendukung pencadangan otomatis, dan Anda dapat menyesuaikan siklus pencadangan dengan mengonfigurasi kebijakan pencadangan. Anda juga dapat mencadangkan data secara manual di TencentDB for SQL Server.

>!
>- File cadangan disimpan di ruang cadangan terpisah dan tidak menempati ruang disk lokal instans.
>- Sebaiknya jangan lakukan operasi DDL selama proses pencadangan, untuk menghindari kegagalan pencadangan karena penguncian tabel.
>- Sebaiknya cadangkan data Anda selama jam normal.
>- Jika volume data tinggi, pencadangan mungkin memakan waktu lama.

### Objek Cadangan
| **Cadangan Data**  | **Cadangan Log** |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <li>Saat ini, cadangan penuh didukung. <li>Cadangan reguler (sekali per hari) dan cadangan manual didukung. <li>Cadangan multi-database didukung, yaitu, Anda dapat mencadangkan satu atau beberapa database dalam instans. <li>Cadangan instans didukung, yaitu, Anda dapat mencadangkan semua database di seluruh instans (mode ini digunakan untuk pencadangan terjadwal). <li>File cadangan memiliki periode penyimpanan (tujuh hari) dan akan dihapus secara otomatis setelah kedaluwarsa. Unduh file tepat waktu untuk penyimpanan lokal. <li>File cadangan saat ini tidak dapat dihapus secara manual. | <li>Cadangan log transaksi didukung. <li>Log dicadangkan setiap 30 menit sekali dan diunggah ke cloud untuk penyimpanan. <li>File log saat ini tidak dapat diunduh.</li> |

## Mengatur Pencadangan Manual
>?Sebelum melakukan pencadangan manual, pastikan Anda telah membuat database. Untuk informasi selengkapnya, silakan lihat [Membuat Database](https://intl.cloud.tencent.com/document/product/238/35780).
>
Anda dapat membuat file cadangan secara manual melalui cadangan instans atau cadangan multi-database kapan saja menggunakan langkah-langkah berikut:
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup Management** (Manajemen Cadangan), klik **Manual Backup** (Cadangan Manual).
3. Di kotak dialog pop-up, masukkan nama cadangan dan pilih kebijakan pencadangan.
  - Nama cadangan: masukkan nama cadangan manual.
  - Kebijakan pencadangan: cadangan instans (yaitu, mencadangkan semua database di seluruh instans) atau pencadangan multi-database. Jika memilih opsi terakhir, Anda harus memilih database yang akan dicadangkan.
![](https://main.qcloudimg.com/raw/f33a17aca57a83cb9bbaf262f73d798e.png )

## Mengatur Cadangan Terjadwal
Anda dapat mengatur waktu cadangan terjadwal untuk menerapkan cadangan database otomatis harian menggunakan langkah-langkah berikut:
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup Management** (Manajemen Cadangan), klik **Auto-Backup Settings** (Pengaturan Cadangan Otomatis), atur waktu cadangan terjadwal, dan klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/a9fd8e162a02ec7c11c75b9520d3956c.png)

## Mengatur Tugas Pencadangan
Pengaturan tugas pencadangan mencakup variabel global pencadangan manual dan terjadwal, seperti format file cadangan dan opsi eksekusi tugas cadangan.
- Format file cadangan: Anda dapat menentukan format file cadangan. Secara default, file cadangan (yaitu, file .bak) akan diarsipkan ke dalam file .tar kemudian diunggah ke COS. Jika Anda memilih "unarchived files" (file yang tidak diarsipkan) sebagai format file cadangan, file .bak dari setiap database dalam instans akan langsung diunggah ke COS tanpa diarsipkan.
- Opsi eksekusi tugas pencadangan: Anda dapat memutuskan apakah akan mencadangkan di node utama atau node replika. Secara default, data dicadangkan di node utama.

>?Hanya instans edisi kluster 2017/2019 yang mendukung opsi eksekusi tugas cadangan.

1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup Management** (Manajemen Cadangan), klik **Backup Task Settings** (Pengaturan Tugas Cadangan).
3. Tentukan item konfigurasi di kotak dialog pop-up, lalu klik **Save** (Simpan).
<img src="https://qcloudimg.tencent-cloud.cn/raw/38947de70c67afe4abf614d6aef0b78e.png" style="zoom:50%;" />

## Melihat Tugas Cadangan
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada tab **Backup Management** (Manajemen Cadangan), lihat tugas cadangan di daftar cadangan.
 - Jika file cadangan adalah file arsip, informasi cadangan langsung ditampilkan dalam daftar cadangan, termasuk waktu mulai cadangan, waktu berakhir cadangan, nama cadangan, kebijakan pencadangan, mode cadangan, ukuran cadangan, database, status, dan operasi (unduh, pemulihan, dan penghapusan).</span>
![](https://main.qcloudimg.com/raw/db076dda070a0a3819c547168d53449a.png)
 - Jika file cadangan adalah file yang tidak diarsipkan, informasi cadangan ditampilkan dalam dua daftar nested. Daftar luar menampilkan informasi cadangan dari seluruh instans, termasuk waktu mulai cadangan, waktu berakhir cadangan, nama cadangan, kebijakan pencadangan, mode cadangan, database, dan status. Daftar bagian dalam menampilkan informasi cadangan setiap database dalam instans, termasuk nama database, ukuran cadangan, dan operasi (unduh, pemulihan, dan penghapusan).</span>
![](https://qcloudimg.tencent-cloud.cn/raw/d79de61562248cbee2d73bf71c5385a8.png)

