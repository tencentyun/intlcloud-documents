### Batasan Penggunaan
- Penempatan HAVIP dapat ditentukan oleh CVM backend, tetapi Anda tidak dapat secara manual mengikat HAVIP ke server tertentu di konsol (pengalaman sejalan dengan komputer fisik tradisional.)
- RS backend tetapi bukan HAVIP yang menentukan apakah akan bermigrasi berdasarkan negosiasi file konfigurasi.
- Hanya instans VPC yang didukung, dan jaringan dasar tidak didukung.
- Deteksi heartbeat harus dilakukan oleh aplikasi pada CVM, tetapi tidak oleh HAVIP yang hanya berfungsi sebagai alamat IP floating yang ditentukan oleh ARP (pengalaman sejalan dengan mesin fisik tradisional.)

### Batasan Kuota
<table style="width:450px !important">
<thead>
<tr>
<th width="70%">Sumber daya</th>
<th>Batas</th>
</tr>
</thead>
<tbody><tr>
<td>Kuota HAVIP default di setiap VPC</td>
<td>10</td>
</tr>
</tbody></table>
