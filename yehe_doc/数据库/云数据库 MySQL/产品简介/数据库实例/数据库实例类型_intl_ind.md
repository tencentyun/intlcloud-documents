Instans TencentDB for MySQL adalah lingkungan database yang berjalan secara independen di Tencent Cloud. Ini adalah unit dasar bagi Anda untuk membeli layanan TencentDB for MySQL. Anda dapat membuat, memodifikasi, dan menghapus instans di konsol.
Setiap instans tidak bergantung satu sama lain dengan sumber daya yang terisolasi. Tidak ada masalah awal CPU, memori, dan IO di antara instans. Setiap instans memiliki karakteristiknya sendiri seperti tipe dan versi database, dan sistem memiliki parameter yang sesuai untuk mengontrol perilaku instans.

Ada tiga jenis instans yang tersedia di TencentDB for MySQL:

<table>
<thead><tr>
<th>Jenis Instans</th><th width="20%">Definisi</th><th width="15%">Arsitektur</th><th>Terlihat di Daftar Instans</th><th>Fitur</th></tr></thead>
<tbody><tr>
<td>Contoh sumber</td><td>Instans yang dapat dibaca dan ditulis ke</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Node tunggal</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Dua Node</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">Tiga Node</a></td>
<td>Ya</td><td>Instans sumber dapat memasang instans baca saja dan instans pemulihan bencana untuk pemisahan baca/tulis dan pemulihan bencana jarak jauh</td></tr>
<tr>
<td>Instans Baca Saja</td><td>Instans yang hanya dapat dibaca dari</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Node tunggal</a></td><td>Ya</td>
<td>Instans baca saja tidak dapat berdiri sendiri. Sebaliknya, instans ini harus berafiliasi dengan instans sumber. Data hanya berasal dari sinkronisasi dengan instans sumber, dan harus berada di wilayah yang sama dengan instans sumber</td></tr>
<tr>
<td>Instans pemulihan bencana</td><td>Instans yang mendukung pemulihan bencana di seluruh AZ dan wilayah</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Dua Node</a><td>Ya</td>
<td>Instans pemulihan bencana bersifat baca saja saat disinkronkan dengan instans sumber. Instans ini dapat secara aktif menghentikan sinkronisasi dan dipromosikan ke instans sumber untuk akses baca/tulis. Instans pemulihan bencana harus berada di wilayah yang berbeda dengan instans sumber</td></tr>
</tbody></table>

### Referensi
- Untuk informasi selengkapnya tentang pembuatan dan catatan pada instans baca saja, lihat [Membuat Instans Baca Saja](https://intl.cloud.tencent.com/document/product/236/7270).
- Untuk informasi selengkapnya tentang cara membuat dan mengonfigurasi grup RO untuk instans baca saja, lihat [Grup RO untuk Instans Baca Saja](https://intl.cloud.tencent.com/document/product/236/11361).
- Untuk informasi selengkapnya tentang pembuatan dan catatan tentang instans pemulihan bencana, lihat [Instans Pemulihan Bencana](https://intl.cloud.tencent.com/document/product/236/7272).
