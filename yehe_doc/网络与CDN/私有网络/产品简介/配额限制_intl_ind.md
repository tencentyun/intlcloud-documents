### VPC dan Subnet
<table>
<thead>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
</thead>
<tbody><tr>
<td>Jumlah VPC per akun per wilayah</td>
<td align="center">20</td>
</tr>
<tr>
<td>Jumlah subnet per VPC</td>
<td align="center">100</td>
</tr>
<tr>
<td>Jumlah blok CIDR sekunder per VPC</td>
<td align="center">5</td>
</tr>
<tr>
<td>Jumlah instans CVM jaringan klasik yang dikaitkan dengan setiap VPC</td>
<td align="center">100</td>
</tr>
</tbody></table>

### Tabel Rute
<table>
<thead>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
</thead>
<tbody><tr>
<td>Jumlah tabel rute per VPC</td>
<td align="center">10</td>
</tr>
<tr>
<td>Jumlah tabel rute yang dikaitkan ke setiap subnet</td>
<td align="center">1</td>
</tr>
<tr>
<td>Jumlah kebijakan perutean per tabel rute</td>
<td align="center">50</td>
</tr>
</tbody></table>

### ENI
<table>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
<tr>
<td>Jumlah ENI sekunder per VPC</td>
<td>1.000</td>
</tr>
</table>

### HAVIP
<table >
<thead>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
</thead>
<tbody><tr>
<td>Jumlah HAVIP default per VPC</td>
<td>10</td>
</tr>
</tbody></table>

### Grup Keamanan
<table>
<tr><th width="70%">Item</th><th width="30%">Deskripsi</th></tr>
<tr><td>Jumlah grup keamanan</td><td>50 per wilayah</td></tr>
<tr><td>Jumlah aturan dalam grup keamanan</td><td>100 untuk aturan masuk dan 100 untuk aturan keluar</td></tr>
<tr><td>Jumlah instans CVM yang dikaitkan dengan grup keamanan</td><td>2.000</td></tr>
<tr><td>Jumlah grup keamanan yang dikaitkan dengan instans CVM</td><td>5</td></tr>
<tr><td>Jumlah grup keamanan yang dapat diimpor oleh grup keamanan</td><td>10</td></tr>
</table>

### ACL Jaringan
<table >
<thead>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Pembatasan</th>
</tr>
</thead>
<tbody><tr>
<td>Jumlah ACL jaringan per VPC</td>
<td>50 partisi</td>
</tr>
<tr>
<td>Jumlah aturan per jaringan ACL</td>
<td>Masuk: 20<br>Keluar: 20</td>
</tr>
<tr>
<td>Jumlah ACL jaringan yang dikaitkan ke setiap subnet</td>
<td>1 partisi</td>
</tr>
</tbody></table>

### Templat Parameter
<table>
<thead>
<tr>
<th width="70%">Jenis Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
</thead>
<tbody><tr>
<td>Objek alamat IP (ipm)</td>
<td>Maks.: 1.000</td>
</tr>
<tr>
<td>Objek grup alamat IP (ipmg)</td>
<td>Maks.: 1.000</td>
</tr>
<tr>
<td>Objek port protokol (ppm)</td>
<td>Maks.: 1.000</td>
</tr>
<tr>
<td>Objek grup port protokol (ppmg)</td>
<td>Maks.: 1.000</td>
</tr>
<tr>
<td>Anggota alamat IP dalam objek alamat IP (ipm)</td>
<td>Maks.: 20</td>
</tr>
<tr>
<td>Anggota objek alamat IP (ipm) dalam objek grup alamat IP (ipmg)</td>
<td>Maks.: 20</td>
</tr>
<tr>
<td>Anggota port protokol dalam objek grup port protokol (ppm) </td>
<td>Maks.: 20</td>
</tr>
<tr>
<td>Anggota objek port protokol (ppm) dalam objek grup port protokol (ppmg)</td>
<td>Maks.: 20</td>
</tr>
<tr>
<td>Objek grup alamat IP (ipmg) yang dapat mereferensikan pada objek alamat IP (ipm) yang sama</td>
<td>Maks.: 50</td>
</tr>
<tr>
<td>Objek grup port protokol (ppmg) yang dapat mereferensikan objek port protokol yang sama (ppm)</td>
<td>Maks.: 50</td>
</tr>
</tbody></table>

### Probe Jaringan 
<table >
<thead>
<tr>
<th width="70%">Sumber Daya</th>
<th width="30%">Batas Kuota</th>
</tr>
</thead>
<tbody><tr>
<td>Jumlah probe jaringan yang dibuat di setiap VPC</td>
<td>50</td>
</tr>
</tbody></table>
