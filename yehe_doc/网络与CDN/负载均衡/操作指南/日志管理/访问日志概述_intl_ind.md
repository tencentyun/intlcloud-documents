CLB mendukung konfigurasi log akses untuk mengumpulkan dan mencatat detail setiap permintaan klien, seperti waktu permintaan, jalur permintaan, IP dan port klien, kode pengembalian, dan waktu respons. Fitur ini dapat membantu Anda lebih memahami permintaan klien, memecahkan masalah, dan menganalisis perilaku pengguna.
>?
>- Hanya CLB Lapisan 7 yang mendukung konfigurasi log akses.
>- Fitur ini hanya tersedia di wilayah yang tercantum di bawah ini.

## Metode Penyimpanan
- Log akses CLB dapat disimpan di [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): CLS adalah platform layanan log lengkap yang menyediakan beragam layanan log termasuk kumpulan log, penyimpanan, pencarian, analisis, ekspor real-time, dan pengiriman. Layanan ini akan membantu Anda menerapkan operasi bisnis, pemantauan keamanan, audit log, dan analisis log.

<table class="table">
<thead>
<tr>
<th>Item</th>
<th>Menyimpan Log Akses di CLS</th>
</tr>
</thead>
<tbody>
<tr>
<td>Detail waktu untuk menampilkan log</td>
<td>Menit</td>
</tr>
<tr>
<td>Pencarian online</td>
<td>Didukung</td>
</tr>
<tr>
<td>Sintaks pencarian</td>
<td>Pencarian khusus teks, pencarian nilai kunci, pencarian kata kunci fuzzy, dll. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/614/37882">Sintaks Pencarian CLS Warisan</a>.</td>
</tr>
<tr>
<td>Wilayah yang didukung</td>
<td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (Tiongkok), Singapura, Mumbai, Seoul, Tokyo, Silicon Valley, Virginia, Toronto, Frankfurt. </td>
</tr>
<tr>
<td>Tipe CLB yang didukung</td>
<td>CLB jaringan publik/jaringan privat</td>
</tr>
<tr>
<td>Tautan upstream dan downstream</td>
<td>Log CLS dapat dikirimkan ke COS, dan diekspor ke CKafka untuk diproses lebih lanjut.</td>
</tr> 
<tr>
<td>Retensi log</td>
<td>Tencent Cloud tidak menyimpan log akses secara default. Fitur penyimpanan dapat dikonfigurasi sesuai kebutuhan.</td>
</tr>
</tbody></table>

## Operasi yang Relevan
- [Menyimpan Log Akses di CLS](https://intl.cloud.tencent.com/document/product/214/35063)
