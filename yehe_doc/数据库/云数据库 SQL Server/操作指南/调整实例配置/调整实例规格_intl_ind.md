Dokumen ini menjelaskan cara menyesuaikan spesifikasi instans di konsol TencentDB for SQL Server.

## Spesifikasi Instans
Untuk informasi selengkapnya tentang spesifikasi instans yang didukung oleh TencentDB for SQL Server dan harganya, lihat [Harga Produk](https://intl.cloud.tencent.com/document/product/238/8294).

## Prasyarat
Anda dapat menyesuaikan konfigurasi instans TencentDB for SQL Server dan instansnya yang terkait hanya jika mereka dalam status normal (Berjalan) dan tidak menjalankan tugas apa pun.

## Proses Penyesuaian Spesifikasi
**Penskalaan**
Setelah Anda menyesuaikan konfigurasi di konsol, sistem akan memutuskan untuk menyelesaikan perubahan dengan penskalaan atau migrasi data. Proses penyesuaian konfigurasi adalah sebagai berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/49f03015ca1012cd1be81ca83e442425.png)

## Dampak Penyesuaian Konfigurasi
### Penyesuaian Item Tunggal
Penyesuaian Item Tunggal mengacu pada penyesuaian spesifikasi atau disk, yang memiliki dampak sebagai berikut:
<table>
<tbody>
<tr><th width=12%>Edisi</th><th width=12%>Item Penyesuaian</th><th width=12%>Keputusan Penyesuaian</th><th>Dampak Penyesuaian</th><th width=19%>Waktu</th></tr>
<tr>
<td rowspan="1">Edisi Dasar</td>
<td>Peningkatan spesifikasi<br>or<br>Perluasan kapasitas disk<br>atau<br>Penurunan spesifikasi</td><td>Peningkatan dan penurunan</td><td>1. Instans akan dimulai ulang selama penyesuaian konfigurasi. <br>2. Layanan akan menjadi tidak tersedia selama sekitar 3 menit. <br>3. Lakukan penyesuaian selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>        
<tr>
<td rowspan="4">Edisi Ketersediaan Tinggi/Edisi Kluster</td>
<td>Pengurangan kapasitas disk</td><td>Penurunan</td><td>1. Kapasitas disk instans akan dikurangi selama penyesuaian konfigurasi. <br>2. Migrasi data dan mulai ulang instans tidak akan dilakukan, dan tidak akan terjadi pemutusan sementara. <br>3. Penyesuaian yang diajukan akan segera berlaku tanpa memengaruhi bisnis. </td><td>Penyesuaian yang dikirimkan akan segera dijalankan.</td></tr>
<tr>
<td>Penurunan spesifikasi</td><td>Penurunan</td><td>1. Spesifikasi instans akan diturunkan selama penyesuaian konfigurasi. <br>2. Layanan akan menjadi tidak tersedia selama sekitar 1 menit. <br>3. Lakukan penyesuaian selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
<tr>
<td>Peningkatan spesifikasi<br>atau<br>perluasan kapasitas disk</td><td>Migrasi dan peningkatan</td><td>1. Migrasi data akan terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini. <br>2. Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang. <br>3. Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
<tr>
<td>Peningkatan spesifikasi<br>atau<br>perluasan kapasitas disk</td><td>Peningkatan</td><td>1. Spesifikasi instans atau kapasitas disk akan ditingkatkan atau diperluas selama penyesuaian konfigurasi. <br>2. Migrasi data dan mulai ulang instans tidak akan dilakukan, dan tidak akan terjadi pemutusan sementara. <br>3. Penyesuaian yang diajukan akan segera berlaku tanpa memengaruhi bisnis. </td><td>Penyesuaian yang diajukan akan segera dijalankan.</td></tr>
</tbody></table>

### Penyesuaian kombo
Penyesuaian kombo mengacu pada penyesuaian spesifikasi dan kapasitas disk, yang berdampak sebagai berikut:
<table>
<tbody>
<tr><th width=12%>Edisi</th><th width=12%>Item Penyesuaian</th><th width=12%>Keputusan Penyesuaian</th><th>Dampak Penyesuaian</th><th width=19%>Waktu</th></tr>
<tr>
<td rowspan="1">Edisi Dasar</td>
<td>Peningkatan spesifikasi<br>Perluasan kapasitas disk<br>Penurunan spesifikasi</td><td>Peningkatan dan penurunan</td><td>1. Instans akan dimulai ulang selama penyesuaian konfigurasi. <br>2. Layanan akan menjadi tidak tersedia selama sekitar 3 menit. <br>3. Lakukan penyesuaian selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>        
<tr>
<td rowspan="6">Edisi Ketersediaan Tinggi/Edisi Kluster</td>
<td>Peningkatan spesifikasi + perluasan kapasitas disk</td><td>Peningkatan</td><td>1. Spesifikasi instans atau kapasitas disk akan ditingkatkan atau diperluas selama penyesuaian konfigurasi. <br>2. Migrasi data dan mulai ulang instans tidak akan dilakukan, dan tidak akan terjadi pemutusan sementara. <br>3. Penyesuaian yang diajukan akan segera berlaku tanpa memengaruhi bisnis. </td><td>Penyesuaian yang diajukan akan segera dijalankan.</td></tr>
<tr>
<td>Peningkatan spesifikasi + perluasan kapasitas disk</td><td>Migrasi dan peningkatan</td><td>1. Migrasi data akan terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini. <br>2. Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang. <br>3. Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
<tr>
<td>Peningkatan spesifikasi + perluasan kapasitas disk</td><td>Peningkatan dan penurunan</td><td>1. Spesifikasi instans akan ditingkatkan dan kapasitas disk akan dikurangi selama penyesuaian konfigurasi. <br>2. Migrasi data dan mulai ulang instans tidak akan dilakukan, dan tidak akan terjadi pemutusan sementara. <br>3. Penyesuaian yang diajukan akan segera berlaku tanpa memengaruhi bisnis. </td><td>Penyesuaian yang diajukan akan segera dijalankan.</td></tr>
<tr>
<td>Peningkatan spesifikasi + pengurangan kapasitas disk</td><td>Migrasi, peningkatan, dan penurunan</td><td>1. Migrasi data akan terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini. <br>2. Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang. <br>3. Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
</tr>
<td>Penurunan spesifikasi + perluasan kapasitas disk</td><td>Peningkatan dan penurunan, atau migrasi, peningkatan, dan penurunan</td><td>1. Layanan mungkin menjadi tidak tersedia selama sekitar 1 menit, dan migrasi data mungkin terlibat selama penyesuaian konfigurasi instans, dan semakin tinggi volume data, semakin lama waktu migrasi data. Akses ke instans tidak akan terpengaruh selama periode ini. <br>2. Peralihan akan dilakukan setelah migrasi selesai, yang disertai dengan pemutusan dari database yang berlangsung hanya beberapa detik. Pastikan bisnis Anda memiliki mekanisme koneksi ulang. <br>3. Selama pemutusan sementara, sebagian besar operasi yang terkait dengan database, akun, dan jaringan tidak dapat dijalankan. Dengan demikian, pastikan untuk melakukan peralihan selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
</tr>
<td>Penurunan spesifikasi + pengurangan kapasitas disk</td><td>Penurunan</td><td>1. Spesifikasi instans akan diturunkan selama penyesuaian konfigurasi. <br>2. Layanan akan menjadi tidak tersedia selama sekitar 1 menit. <br>3. Lakukan penyesuaian selama jam normal. </td><td>Anda harus memilih waktu untuk memberlakukannya.</td></tr>
</tbody></table>

## Petunjuk
1. Login ke [konsol TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver), pilih wilayah dan instans target dalam daftar instans, dan klik **Adjust Configuration** (Sesuaikan Konfigurasi) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. Di jendela **Adjust Configuration** (Sesuaikan Konfigurasi) yang muncul, pilih CPU, memori, dan kapasitas disk yang diinginkan, lalu klik **Confirm** (Konfirmasi).
>?
>- ?Pilih **Time to Take Effect** (Waktu untuk Berlaku) dari penyesuaian konfigurasi dan klik catatan berwarna jingga.
> - Selama waktu pemeliharaan: Anda dapat memodifikasi waktu pemeliharaan di halaman detail instans.
> - Sesuaikan sekarang: penyesuaian konfigurasi akan segera dilakukan.
>- Jika pengurangan kapasitas disk terlibat, untuk menghindari kegagalan, ruang disk baru harus lebih besar atau sama dengan 2 kali ruang disk yang digunakan saat ini.
>- Jika instans yang akan disesuaikan dihubungkan dengan instans lain (instans baca saja) dan melibatkan migrasi data, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a7b802d9713230b55bbf5642d341facd.png)
3. Pada halaman pembayaran tempat Anda diarahkan, konfirmasi informasi konfigurasi dan biaya dan klik **Submit Order** (Kirim Pesanan).
4. Anda akan diarahkan ke daftar instans. Saat status instans berubah dari **Switching (after configuration adjustment)** (Beralih (setelah penyesuaian konfigurasi)) menjadi **Running** (Berjalan), peningkatan spesifikasi selesai. Anda dapat mengkueri dan memeriksa spesifikasi baru di halaman **Instance List** (Daftar Instans) atau **Instance Details** (Detail Instans).


