
## Ikhtisar
TencentDB for MySQL memungkinkan Anda membuat satu atau beberapa instans baca saja untuk membentuk grup RO, yang cocok untuk pemisahan baca/tulis dan skenario aplikasi satu-sumber-banyak-replika dan dapat meningkatkan kapasitas beban baca database Anda secara signifikan.

Grup RO adalah kumpulan instans baca saja yang memiliki alamat jaringan pribadi yang sama. Anda dapat mengatur bobotnya untuk menyeimbangkan beban lalu lintas, mengatur kebijakan untuk menghapus instans baca saja yang tertunda, dan melakukan konfigurasi lainnya. Anda dapat men-deploy grup RO sesuai kebutuhan dan mengirim permintaan baca yang sesuai ke instans baca saja sesuai dengan aturan tertentu. Selain itu, Anda dapat menerapkan pemulihan bencana dengan mengonfigurasi beberapa instans baca saja dalam grup RO yang sama.

## Prasyarat
- Instans sumber harus dibuat terlebih dahulu sebelum instans baca saja dapat dibuat. Untuk informasi selengkapnya, lihat [Panduan Pembelian](https://intl.cloud.tencent.com/document/product/236/5160).
- Sebelum digunakan, instans TencentDB for MySQL perlu diinisialisasi. Untuk informasi selengkapnya, lihat [Menginisialisasi Instans TencentDB for MySQL](/doc/product/236/3128).

## Petunjuk
### Membuat grup RO
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman manajemen instans.
2. Klik **Add Read-Only Instans** (Tambahkan Instans Baca Saja) di bagian **Instance Architecture Diagram** (Diagram Arsitektur Instans) pada tab **Instance Details** (Detail Instans) atau klik **Create** (Buat) pada tab **Read-Only Instance** (Instans Baca Saja).
![](https://main.qcloudimg.com/raw/83e817ae1b9205d6cdf061684f7d3c12.png)
3. Pada halaman pembelian yang ditampilkan, tentukan konfigurasi instans baca saja berikut, konfirmasikan bahwa semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
 - **Specify RO Group** (Tentukan Grup RO): pilih **Create RO group** (Buat grup RO). Jika beberapa instans dibeli sekaligus, semuanya akan ditetapkan ke grup RO baru ini, dan bobotnya akan dialokasikan oleh sistem secara otomatis secara default.
 - **RO Group Name** (Nama Grup RO): nama grup RO tidak harus unik dan dapat berisi hingga 60 huruf, angka, tanda hubung, garis bawah, dan titik.
 - **Remove Delayed RO Instances** (Hapus Instans RO Tertunda): opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika instans baca saja dihapus, bobotnya akan secara otomatis diatur ke 0.
 Jika instans baca saja dihapus saat penundaannya melebihi ambang batas, instans tersebut akan menjadi tidak aktif, bobotnya akan diatur ke 0 secara otomatis, dan pemberitahuan peringatan akan dikirim (untuk informasi selengkapnya tentang cara mengonfigurasi alarm penghapusan instans baca saja dan penerima, lihat [Kebijakan Alarm (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)). Instans akan dimasukkan kembali ke grup RO saat penundaannya berada di bawah ambang batas.
 Terlepas dari apakah penghapusan instans baca saja yang tertunda diaktifkan, instans baca saja yang dihapus karena kegagalan instans akan bergabung kembali dengan grup RO saat diperbaiki.
 - **Delay Threshold** (Ambang Batas Penundaan): ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup RO.
 - **Least RO Instances** (Instans RO Terkecil): ini adalah jumlah minimum instans yang harus dipertahankan dalam grup RO. Ketika ada lebih sedikit instans dalam grup RO, meski melebihi ambang batas penundaan, instans tidak akan dihapus.
 - **Assign Read Weight** (Tetapkan Bobot Baca): ditetapkan oleh sistem.
 - **Billing Mode** (Mode Penagihan): instans baca saja adalah bayar sesuai pemakaian.
![](https://main.qcloudimg.com/raw/a8f80ce3f01cbaa1847978bec455aa0d.png)
 - **Region** (Wilayah): sama dengan instans sumber secara default.
 - **Database Version** (Versi Database): secara default sama dengan instans sumber.
 - **Architecture** (Arsitektur): ini adalah node tunggal. Meskipun arsitektur node tunggal hemat biaya, ada risiko titik kegagalan tunggal. Sebaiknya beli setidaknya dua instans baca saja di grup RO bisnis Anda yang memerlukan ketersediaan tinggi.
 - **Data Replication Mode** (Mode Replikasi Data): secara default sama dengan instans sumber.
 - **AZ** (AZ): jika ada beberapa AZ di wilayah saat ini, Anda dapat memilih satu sesuai kebutuhan.
>?Keterlambatan jaringan di seluruh AZ di wilayah yang sama, di wilayah yang berbeda, dan di wilayah di luar daratan Tiongkok masing-masing sekitar beberapa milidetik, puluhan milidetik, dan lebih dari 100 milidetik, jadi Anda harus memilih AZ dengan hati-hati.
5. Kembali ke daftar instans. Status instans yang dibuat adalah **Delivering** (Mengirim). Jika statusnya berubah menjadi **Running** (Berjalan), artinya instans baca saja telah berhasil dibuat.

### Mengonfigurasi grup RO
Pada halaman konfigurasi grup RO, Anda dapat mengonfigurasi informasi dasar grup seperti ID, nama, replikasi tertunda, kebijakan penghapusan, ambang batas penundaan, instans baca saja paling sedikit, dan bobot baca.
>?
>- Instans Baca Saja dalam grup RO dapat menggunakan spesifikasi yang berbeda, dan bobot lalu lintas bacanya juga dapat berbeda.
>- Instans Baca Saja dalam grup RO yang sama dapat memiliki tanggal kedaluwarsa dan mode penagihan yang berbeda.
>- Setelah diaktifkan, replikasi tertunda akan berlaku untuk semua instans baca saja di grup RO ini, tetapi tidak akan mengubah status replikasinya.
>- Opsi penundaan replikasi hanya akan muncul setelah replikasi tertunda diaktifkan.
>
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Di daftar instans, klik ID instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja), cari grup RO yang diinginkan, dan klik **Configuration** (Konfigurasi) untuk masuk ke halaman konfigurasi grup RO.
![](https://main.qcloudimg.com/raw/f03a6fc7e5460181e1e933157b4922cb.png)
3. Pada halaman konfigurasi grup RO, konfigurasikan informasi grup RO dan klik **OK** (OKE).
   Anda dapat mengatur replikasi tertunda dan memilih untuk memutar ulang dengan posisi flashback atau pengidentifikasi transaksi global (GTID) selama penundaan untuk secara efisien mengembalikan data dan memperbaiki kegagalan.
   - **Replication Delay** (Penundaan Replikasi): Anda dapat mengonfigurasi waktu replikasi tertunda antara instans baca saja dan instans sumbernya. Rentang nilainya adalah 1–259200 detik.
   - **Remove Delayed RO Instances** (Hapus Instans RO Tertunda): opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika instans baca saja dihapus saat penundaannya melebihi ambang batas, bobotnya akan diatur ke 0 secara otomatis, dan alarm akan dikirim (untuk informasi selengkapnya tentang cara mengonfigurasi alarm dan penerima penghapusan instans baca saja, lihat [Alarm Kebijakan (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
   - **Delay Threshold** (Ambang Batas Penundaan): ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup RO.
   - **Least RO Instances** (Instans RO Terkecil): ini adalah jumlah minimum instans yang harus dipertahankan dalam grup RO. Ketika ada lebih sedikit instans dalam grup RO, meski melebihi ambang batas penundaan, instans tidak akan dihapus.
   - **Assign Read Weight** (Tetapkan Bobot Baca): grup RO mendukung dua metode penetapan bobot: penetapan otomatis oleh sistem dan penetapan kustom. Nilai bobot harus berupa bilangan bulat antara 0 dan 100. Di bawah ini adalah daftar bobot baca yang secara otomatis diatur untuk instans MySQL dua node dan tiga node oleh sistem:
<table>
<thead><tr>
<th>Spesifikasi Memori (MB)</th>
<th>1000</th><th>2000</th><th>4000</th><th>8000</th><th>12000</th><th>16000</th><th>24000</th><th>32000</th><th>48000</th><th>64000</th><th>96000</th><th>128000</th><th>244000</th><th>488000</th>
</tr></thead>
<tbody><tr>
<td>Bobot</td>
<td>1</td><td>1</td><td>2</td><td>2</td><td>4</td><td>4</td><td>8</td><td>8</td><td>10</td><td>12</td><td>14</td><td>16</td><td>26</td><td>50</td></tr>
</tbody></table>
 - **Rebalance** (Penyeimbangan Ulang):
    - Memodifikasi bobot hanya akan memengaruhi beban baru jika penyeimbangan ulang dinonaktifkan. Operasi tidak berdampak pada instans baca saja yang diakses oleh koneksi persisten yang ada dan tidak menyebabkan pemutusan database semantara.
    - Jika penyeimbangan ulang diaktifkan, semua koneksi ke database akan terputus sementara, dan beban koneksi yang baru ditambahkan akan diseimbangkan sesuai dengan bobot yang ditetapkan.
<img src="https://main.qcloudimg.com/raw/94a42aa7ed813d8ba68560c40749998f.png"  style="zoom:55%;">


### Menghentikan dan menghapus grup RO
>?
>
>- Grup RO tidak dapat dihapus secara manual.
>- Grup RO akan dihapus secara otomatis saat instans baca saja terakhir di dalamnya dihilangkan.
>- Grup RO yang kosong tidak dapat dipertahankan.
>
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Di daftar instans, klik ID instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih tab **Read-Only Instance** (Instans Baca Saja), cari grup RO yang diinginkan, dan hapus semua instans baca saja dengan mengklik **Terminate/Return** (Hentikan/Kembali) di sebelah kanan.
![](https://qcloudimg.tencent-cloud.cn/raw/ef06e1a956370519e0c0b652b8a07c72.png)
3. Di jendela pop-up, baca dan setujui **Termination Rules** (Aturan Penghentian) dan klik **Terminate Now** (Hentikan Sekarang).

