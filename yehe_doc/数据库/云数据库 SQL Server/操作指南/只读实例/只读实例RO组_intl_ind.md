## Ikhtisar
TencentDB for SQL Server memungkinkan Anda membuat satu atau beberapa instans baca saja untuk membentuk grup baca saja, yang cocok untuk pemisahan baca/tulis dan skenario aplikasi satu-sumber-banyak-replika dan dapat meningkatkan kapasitas beban baca database Anda secara signifikan.

## Prasyarat
Instans utama harus dibuat terlebih dahulu sebelum instans baca saja dapat dibuat. Untuk informasi selengkapnya, lihat [Membuat Instans TencentDB for SQL Server](https://intl.cloud.tencent.com/document/product/238/31571).

## Petunjuk
### Membuat grup Baca Saja
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail.
2. Klik **Add Read-Only Instance** (Tambahkan Instans Baca Saja) di **Instance Architecture Diagram** (Diagram Arsitektur Instans) di halaman detail instans untuk masuk ke halaman pembelian.
![](https://qcloudimg.tencent-cloud.cn/raw/6acf3d61af70824bae20cbc668e96463.png)
3. Di halaman pembelian yang ditampilkan, tentukan konfigurasi instans baca saja berikut, konfirmasikan bahwa semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
>?Jika opsi **Specify RO Group** (Tentukan Grup RO) dikonfigurasi sebagai **Create RO group** (Buat grup RO), informasi dasar grup baca saja berikut harus dimasukkan di halaman pembelian.
- Nama Grup RO: nama grup tidak harus unik dan dapat berisi hingga 60 huruf, angka, tanda hubung, garis bawah, dan titik.
- **Hapus Instans RO Tertunda**: opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika penundaan instans baca saja melebihi ambang batas, instans tersebut akan dihapus dan menjadi tidak aktif, dan bobotnya akan diatur ke 0. Instans akan dimasukkan kembali ke grup baca saja saat penundaannya berada di bawah ambang batas. Terlepas dari apakah penghapusan instans baca saja yang tertunda diaktifkan, instans baca saja yang dihapus karena kegagalan instans akan bergabung kembali dengan grup baca saja saat diperbaiki.
- Ambang Batas Penundaan: ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup baca saja.
- Instans RO Terkecil: ini adalah jumlah minimum instans yang harus dipertahankan dalam grup baca saja. Ketika ada lebih sedikit instans dalam grup baca saja, meski melebihi ambang batas penundaan, instans tidak akan dihapus.
>![](https://qcloudimg.tencent-cloud.cn/raw/c95128691098cb6eec01c4d55ac2eae7.png)
>
<table><tr><th width="25%">Tentukan Grup Baca Saja</th><th width="75%">Deskripsi</th></tr>
<tr>
<td>Ditetapkan oleh sistem (tidak ditentukan)</td>
<td>Jika beberapa instans dibeli sekaligus, masing-masing akan ditetapkan ke grup baca saja independen, dan bobotnya akan ditetapkan secara otomatis oleh sistem secara default.</td></tr>
<tr>
<td>Buat grup baca saja</td>
<td>Buat grup baca saja. Jika beberapa instans dibeli sekaligus, semuanya akan ditetapkan ke grup baca saja yang baru ini, dan bobotnya akan dialokasikan oleh sistem secara otomatis secara default.</td></tr>
<tr>
<td>Grup baca saja yang ada</td>
<td>Tentukan grup baca saja yang ada. Jika beberapa instans dibeli sekaligus, semuanya akan ditetapkan ke grup baca saja ini. Bobot mereka akan dialokasikan sebagaimana dikonfigurasi dalam grup baca saja. Jika penetapan oleh sistem diatur untuk grup baca saja, instans akan ditambahkan ke grup secara otomatis sesuai dengan spesifikasi yang dibeli. Jika diatur ke alokasi kustom, bobotnya akan menjadi nol secara default. <b>Karena IP pribadi yang sama dibagikan dalam grup baca saja, jika VPC digunakan, pengaturan grup keamanan yang sama akan dibagikan. Jika grup baca saja ditentukan, tidak mungkin untuk menyesuaikan grup keamanan apa pun saat instans dibeli.</b></td></tr>
</table>
4. Kembali ke daftar instans. Status instans baca saja yang dibuat adalah **Mengirim**. Jika statusnya berubah menjadi **Berjalan**, artinya instans telah berhasil dibuat.

### Mengonfigurasi grup baca saja
Pada halaman konfigurasi grup baca saja, Anda dapat mengonfigurasi informasi dasar grup seperti ID, nama, kebijakan penghapusan, ambang batas penundaan, instans baca saja paling sedikit, dan bobot baca.
>?
>- Instans Baca Saja dalam grup baca saja dapat menggunakan spesifikasi yang berbeda, dan bobot lalu lintas bacanya juga dapat berbeda.
>- Instans Baca Saja dalam grup baca saja yang sama dapat memiliki tanggal kedaluwarsa dan mode penagihan yang berbeda.
>
1. Di [daftar instans](https://console.cloud.tencent.com/sqlserver), pilih instans utama yang akan diatur grup baca saja, dan klik **ID instance** (Instans ID) atau **Manage** (Kelola) di kolom **Operation** (Operasi) di sebelah kanan untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja) dan klik **Configuration** (Konfigurasi) untuk masuk ke halaman konfigurasi grup baca saja.
![](https://qcloudimg.tencent-cloud.cn/raw/2e8489adca2b2bdb29ed9cf7e0b13882.png)
3. Di jendela pop-up, konfigurasikan opsi grup baca saja.
![](https://qcloudimg.tencent-cloud.cn/raw/5b08812f65c695e216c01a9f8dce9647.png)
   - Nama Grup RO: nama grup tidak harus unik dan dapat berisi hingga 60 huruf, angka, tanda hubung, garis bawah, dan titik.
   - Hapus Instans RO Tertunda: opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika instans baca saja dihapus, bobotnya akan secara otomatis diatur ke 0.
   - Ambang Batas Penundaan: ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup baca saja.
   - Instans RO Terkecil: ini adalah jumlah minimum instans yang harus dipertahankan dalam grup baca saja. Ketika ada lebih sedikit instans dalam grup baca saja, meski melebihi ambang batas penundaan, instans tidak akan dihapus.
   - Tetapkan Bobot Baca: grup baca saja memungkinkan dua jenis penetapan bobot: bobot yang ditetapkan sistem dan bobot khusus. Angka antara 0 dan 100 harus digunakan sebagai nilai bobot. Sistem secara otomatis menetapkan bobot baca untuk instans SQL Server, seperti yang terlihat di bawah ini.
<table>
<tr><th>Spesifikasi Instans</th><th>Bobot</th></tr>
<tr>
<td>Memori 2.000 MB</td><td>1</td></tr>
<tr>
<td>Memori 4.000 MB</td><td>2</td></tr>
<tr>
<td>Memori 8.000 MB</td><td>2</td></tr>
<tr>
<td>Memori 12.000 MB</td><td>4</td></tr>
<tr>
<td>Memori 16.000 MB</td><td>4</td></tr>
<tr>
<td>Memori 24.000 MB</td><td>8</td></tr>
<tr>
<td>Memori 32.000 MB</td><td>8</td></tr>
<tr>
<td>Memori 48.000 MB</td><td>10</td></tr>
<tr>
<td>Memori 64.000 MB</td><td>12</td></tr>
<tr>
<td>Memori 96.000 MB</td><td>14</td></tr>
<tr>
<td>Memori 128.000 MB</td><td>16</td></tr>
<tr>
<td>Memori 244.000 MB</td><td>26</td></tr>
<tr>
<td>Memori 488.000 MB</td><td>50</td></tr>
</table> 
 - Penyeimbangan Ulang:
 Memodifikasi bobot hanya akan memengaruhi beban baru jika penyeimbangan ulang dinonaktifkan. Operasi tidak berdampak pada instans baca saja yang diakses oleh koneksi persisten yang ada dan tidak menyebabkan pemutusan database sementara.
    Jika penyeimbangan ulang diaktifkan, semua koneksi ke database akan terputus sementara, dan beban koneksi yang baru ditambahkan akan diseimbangkan sesuai dengan bobot yang ditetapkan.

### Menghentikan dan menghapus grup baca saja
>- Grup Baca Saja tidak dapat dihapus secara manual.
>- Grup baca saja akan dihapus secara otomatis saat instans baca saja terakhir di dalamnya dihilangkan.
- Grup baca saja kosong tidak dapat dipertahankan.
