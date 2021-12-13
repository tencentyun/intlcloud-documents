Dokumen ini menjelaskan batas bandwidth keluar dan masuk dari instans CVM, dan membandingkan bandwidth puncak dalam mode penagihan yang berbeda.

## Batas Bandwidth keluar (Bandwidth Hilir)

Batas bandwidth jaringan publik mengacu pada batas atas bandwidth keluar, yaitu bandwidth yang keluar dari instans CVM. Batas bandwidth publik berbeda-beda tergantung pada mode penagihan jaringan. Lihat di bawah untuk detailnya:
- Aturan berikut berlaku untuk instans yang dibuat setelah pukul 00:00, 24 Februari 2020:
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">Metode Penagihan Jaringan</th><th colspan="2">Instans</th><th rowspan="2" style="width:35%">Rentang Batas Bandwidth (Mbps)</th></tr>
<tr><th style="
    width: 20%;
">Mode Penagihan Instans</th><th style="
    width: 25%;
">Konfigurasi Instans</th></tr>
<tr><td>Tagihan per lalu lintas</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Tagihan per bandwidth</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Paket bandwidth</td><td colspan="2">Semua</td><td>0-2000</td></tr>
</tbody></table>

- Aturan berikut berlaku untuk instans yang dibuat sebelum pukul 00:00, 24 Februari 2020:
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">Metode Penagihan Jaringan</th><th colspan="2">Instans</th><th rowspan="2" style="width:35%">Rentang Batas Bandwidth (Mbps)</th></tr>
<tr><th style="
    width: 20;
">Mode Penagihan Instans</th><th style="
    width: 25%;
">Konfigurasi Instans</th></tr>
<tr><td rowspan="1">Tagihan per lalu lintas</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td rowspan="3">Tagihan per bandwidth</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Paket bandwidth</td><td>Semua</td><td>0-1000</td></tr>
</tbody></table>



## Batas Bandwidth Masuk (Bandwidth Hulu)

Bandwidth masuk jaringan publik mengacu pada bandwidth yang mengalir ke instans CVM.
- Jika bandwidth yang Anda beli lebih besar dari 10 Mbps, Tencent Cloud akan menetapkan bandwidth masuk jaringan publik sama dengan bandwidth yang dibeli.
- Jika bandwidth yang dibeli kurang dari atau sama dengan 10 Mbps, Tencent Cloud akan menetapkan bandwidth masuk jaringan publik 10-Mbps.

## Bandwidth Puncak
Bandwidth puncak berlaku untuk tagihan per lalu lintas dan tagihan per bandwidth, tetapi artinya berbeda dalam dua kasus sebagai berikut:

<table>
       <tbody><tr>
			 <th width="17%">Mode Penagihan</th>
			 <th>Perbedaan</th>
			 <th>Catatan</th>
       </tr>
			 <tr>
			 <td>Tagihan per lalu lintas</td>
			 <td>Bandwidth puncak hanya dianggap sebagai <strong>potensi bandwidth puncak maksimum</strong>, dan tidak sebagai bandwidth yang ditetapkan. Dalam kasus konflik sumber daya, bandwidth puncak mungkin tidak mencapai nilai ini.</td> 
			 <td>Jumlah bandwidth puncak dari semua instans tagihan per lalu lintas yang berjalan (seperti CVM, EIP, alamat IPv6 elastis) tidak bisa melebihi 5 Gbps di satu wilayah. Jika aplikasi Anda memerlukan bandwidth yang dijamin atau lebih tinggi, pilih tagihan per bandwidth.</td> 
			 </tr>
       <tr>          
            <td>Tagihan per bandwith<br/> (termasuk langganan bandwidth bulanan dan bandwidth per jam)</td>
            <td>Bandwidth puncak ini adalah bandwidth yang ditetapkan, dan dijamin jika terjadi konflik sumber daya.</td>
						<td>Jumlah bandwidth puncak dari semua instans yang berjalan seperti CVM dan EIP yang dibebankan pada bandwidth tetap (termasuk bandwidth berlangganan bulanan dan bandwidth per jam) tidak boleh melebihi 50 Gbps di satu wilayah. Jika memerlukan bandwidth yang lebih tinggi, hubungi perwakilan penjualan Anda.

</td> 
            </tr> 
</tbody></table>


## Referensi
[Menyesuaikan Bandwidth Jaringan](https://intl.cloud.tencent.com/document/product/213/15517)
