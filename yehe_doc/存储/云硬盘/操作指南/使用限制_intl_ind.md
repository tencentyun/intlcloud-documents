## Batas Penggunaan pada Disk Cloud
<table>
<tr>
<th width="22%">Jenis Batas</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Penggunaan Enhanced SSD</td>
<td> 1.Saat ini, Enhanced SSD hanya tersedia di beberapa zona ketersediaan. <br>2.Kinerja Enhanced SSD hanya dijamin jika SSD tersebut terlampir ke model S5, M5, dan SA2 yang dibuat setelah 1 Agustus 2020, dan semua model generasi selanjutnya. <br>3.Enhanced SSD tidak dapat digunakan sebagai disk sistem.<br>4.Enhanced SSD tidak dapat dienkripsi.<br>5.Enhanced SSD tidak dapat ditingkatkan dari jenis disk lain.</td>
</tr>
<tr>
<td>Penggunaan SSD Sangat Besar</td>
<td> 1.Saat ini, Tremendous SSD hanya tersedia di zona ketersediaan tertentu, seperti yang ditunjukkan di halaman pembelian CBS.Ini akan didukung di lebih banyak zona ketersediaan.<br>2. <b>Tremendous SSD hanya dapat dibeli dengan instance CVM Standard Storage Optimized S5se.</b><br>3.Tremendous SSD tidak dapat dibeli secara terpisah.<br>4.Tremendous SSD tidak dapat digunakan sebagai disk sistem.<br>5.Tremendous SSD tidak dapat dienkripsi.<br>6.Tremendous SSD tidak dapat ditingkatkan dari jenis disk lain.</td>
</tr>
<tr>
<td>Kemampuan disk cloud elastis</td>
<td>Mulai Mei 2018, semua disk data yang dibeli setelah pembuatan CVM adalah disk cloud elastis.Anda dapat melepasnya dari dan memasangkannya kembali ke CVM.Fitur ini didukung di semua zona ketersediaan.</td>
</tr>
<tr>
<td>Kinerja disk cloud</td>
<td>Spesifikasi I/O berlaku untuk kinerja input dan output secara bersamaan.<br/>Misalnya, jika SSD 1 TB memiliki IOPS acak maksimum 26.000, berarti kinerja baca dan tulisnya dapat mencapai nilai ini.Karena batasan kinerja, jika ukuran blok dalam contoh ini adalah 4 KB atau 8 KB, IOPS maksimum dapat dicapai.Jika ukuran blok 16 KB, IOPS maksimum tidak dapat dicapai (throughput telah mencapai batas 260 MB/dtk).</td>
</tr>
<tr>
<td>Disk cloud elastis maksimum yang dapat dilampirkan per CVM</td>
<td>Satu CVM dapat memiliki maksimum 20 disk cloud yang dilampirkan.</td>
</tr>
<tr>
<td>Melampirkan</td>
<td>Sebuah disk cloud hanya dapat dilampirkan ke CVM di zona ketersediaan yang sama.</td>
</tr>
</table>

## Batas Penggunaan pada Snapshot
<table>

<th width="22%">Jenis Batas</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Jenis disk yang didukung</td>
<td>Anda hanya dapat menggunakan snapshot disk data untuk membuat disk cloud elastis, saat menggunakan snapshot disk sistem untuk membuat image khusus.</td>
</tr>
<tr>
<td>Kapasitas disk cloud yang dibuat menggunakan snapshot</td>
<td>Kapasitas disk cloud yang dibuat menggunakan snapshot harus lebih besar atau sama dengan kapasitas snapshot.</td>
</tr>
<tr>
<td>Pengembalian snapshot</td>
<td>Data snapshot hanya dapat dikembalikan ke disk cloud sumber tempat snapshot dibuat.Jika Anda ingin membuat disk cloud dengan data dalam snapshot yang ada, lihat <a href="https://intl.cloud.tencent.com/document/product/362/5757">Membuat Disk Cloud Menggunakan Snapshot<a> .
</td>
</tr>
<tr>
<td>Total ukuran snapshot</td>
<td>Tidak ada batasan</td>
</tr>
<tr>
<td>Kuota snapshot dalam satu wilayah</td>
<td>64 + jumlah disk cloud di wilayah tersebut * 64.</td>
</tr>
</table>

## Batas Penggunaan pada Kebijakan Snapshot Terjadwal
<table>
<tr>
<th width="40%">Jenis Batas</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Kuota kebijakan snapshot terjadwal di satu wilayah</td>
<td>Satu akun Tencent Cloud dapat menetapkan maksimum 30 kebijakan snapshot terjadwal di setiap wilayah.</td>
</tr>
<tr>
<td>Jumlah kebijakan snapshot terjadwal yang dikaitkan dengan satu disk cloud</td>
<td>Sebuah disk cloud dapat dikaitkan dengan maksimum 10 kebijakan snapshot terjadwal di wilayah yang sama.</td>
</tr>
<tr>
<td>Jumlah disk cloud yang dikaitkan dengan satu kebijakan snapshot terjadwal</td>
<td>Kebijakan snapshot terjadwal dapat dikaitkan dengan maksimum 200 disk cloud di wilayah yang sama.</td>
</tr>
</table>
