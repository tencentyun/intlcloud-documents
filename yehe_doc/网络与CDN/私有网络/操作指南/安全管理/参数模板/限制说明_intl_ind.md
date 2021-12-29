### Batasan Penggunaan
- Format yang didukung oleh templat alamat IP adalah sebagai berikut:
 - Alamat IP tunggal: seperti `10.0.0.1`;
 - Alamat IP beruntun: seperti `10.0.0.1`-`10.0.0.100`;
 - Rentang IP: seperti `10.0.1.0/24`.
- Format yang didukung oleh templat port adalah sebagai berikut:
 - Port tunggal: seperti `TCP:80`;
 - Beberapa port: seperti `TCP:80,443`;
 - Rentang port: seperti `TCP:3306-20000`;
 - Semua port: seperti `TCP:ALL`.

### Batasan Kuota 
<table>
<thead>
<tr>
<th></th>Instans
<th>Batas Atas</th>
</tr>
</thead>
<tbody><tr>
<td>Objek alamat IP (ipm)</td>
<td>1.000 per penyewa</td>
</tr>
<tr>
<td>Objek grup alamat IP (ipmg)</td>
<td>1.000 per penyewa</td>
</tr>
<tr>
<td>Objek port protokol (ppm)</td>
<td>1.000 per penyewa</td>
</tr>
<tr>
<td>Objek grup port protokol (ppmg)</td>
<td>1.000 per penyewa</td>
</tr>
<tr>
<td>Anggota alamat IP dalam objek alamat IP (ipm)</td>
<td>20 per penyewa</td>
</tr>
<tr>
<td>Anggota objek alamat IP (ipm) dalam objek grup alamat IP (ipmg)</td>
<td>20 per penyewa</td>
</tr>
<tr>
<td>Anggota port protokol dalam objek grup port protokol (ppm) </td>
<td>20 per penyewa</td>
</tr>
<tr>
<td>Anggota objek port protokol (ppm) dalam objek grup port protokol (ppmg)</td>
<td>20 per penyewa</td>
</tr>
<tr>
<td>Objek grup alamat IP (ipmg) yang dapat mereferensikan objek alamat IP yang sama (ipm)</td>
<td>50 per penyewa</td>
</tr>
<tr>
<td>Objek grup port protokol (ppmg) yang dapat mereferensikan objek port protokol yang sama (ppm)</td>
<td>50 per penyewa</td>
</tr>
</tbody></table>

>?Jika templat parameter direferensikan oleh grup keamanan, IP dan port dalam templat akan dikonversi ke beberapa aturan grup keamanan (hingga 2000).

