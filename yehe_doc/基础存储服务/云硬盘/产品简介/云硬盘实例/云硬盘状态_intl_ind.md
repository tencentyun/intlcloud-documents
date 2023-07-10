Disk cloud memiliki status berikut:

<table>
<tr>
<th>Status</th>
<th>Atribut</th>
<th>Deskripsi</th>
</tr>
<tr>
<td nowrap="nowrap">Akan dipasang</td>
<td nowrap="nowrap">Status stabil</td>
<td>Status setelah disk cloud dibuat dan sebelum dipasang ke CVM.</td>
</tr>
<tr>
<td>Sedang dipasang</td>
<td>Status sementara</td>
<td>Saat disk cloud sedang dipasang, disk memasuki status **mounting** (sedang dipasang).</td>
</tr>
<tr>
<td>Sudah dipasang</td>
<td>Status stabil</td>
<td>Status saat disk cloud telah dipasang ke CVM di zona ketersediaan yang sama.</td>
</tr>
<tr>
<td>Sedang dilepas</td>
<td>Status sementara</td>
<td>Saat disk cloud sedang dilepas, disk memasuki status **unmounting** (sedang dilepas).</td>
</tr>
<tr>
<td>Akan diambil alih</td>
<td>Status stabil</td>
<td>Status ketika disk cloud yang belum diperbarui dalam periode yang ditentukan setelah kedaluwarsa, atau disk cloud dengan langganan bulanan yang telah dihentikan secara manual, dikirim ke keranjang sampah setelah ditangguhkan (disk tidak tersedia, dan hanya dapat menyimpan data) dan dipaksa untuk dilepas.</td>
</tr>
<tr>
<td>Dihentikan</td>
<td>Status stabil</td>
<td>Disk cloud tidak diperbarui dan diambil sebelum waktu penyimpanannya di keranjang sampah berakhir, atau operasi penghentian selesai.Disk cloud asli tidak ada lagi, dan data telah dihapus sepenuhnya.</td>
</tr>
</table>

Hubungan konversi antara status cloud disk ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/096ea77e63990160092f22bcc3ff69ad.png)
