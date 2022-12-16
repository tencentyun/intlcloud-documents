## 1\. LATAR BELAKANG
Modul ini berlaku jika Anda menggunakan Data Lake Compute (“Fitur”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di ("[DPSA](https://intl.cloud.tencent.com/document/product/301/17347))". Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku apabila terjadi inkonsistensi.

## 2\. PEMROSESAN
Kami akan memproses data berikut sehubungan dengan Fitur:
<table>
<thead>
<tr>
<th><b>Informasi Pribadi</b></th>
<th><b>Penggunaan</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Sumber Data</b>: file data (data terstruktur atau semi terstruktur seperti CVS, Avro, Parquet, ORC, json) yang diunggah oleh Anda ke Fitur ini (jika file Anda berisi data pribadi)</td>
<td>Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br>Harap diperhatikan bahwa data ini diintegrasi, disimpan, dan dicadangkan dalam fitur Cloud Object Storage kami.
<br>Harap dicatat bahwa kami tidak memiliki kontrol atas data pribadi (jika ada) yang disimpan dalam database.</td>
</tr>
<tr>
<td><b>Data Penjadwalan Tugas</b>: UIN, ID tugas, jam operasional</td>
<td>Kami hanya memproses data ini dengan tujuan menyediakan Fitur kepada Anda sesuai dengan konfigurasi Anda, termasuk untuk memungkinkan Anda mengelola tugas dan melakukan tugas berulang.</td>
</tr>
<tr>
<td><b>Data Manajemen Akses</b>: UIN, APPID, informasi kelompok kerja, informasi akses</td>	
<td>Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda, termasuk untuk memungkinkan Anda mengelola otorisasi pengguna.</td>
</tr>
<tr>
<td><b>Data Catatan Operasi</b>: UIN, APPID, ID tugas, jam operasi, instruksi Anda (SQL, spark)</td>
<td>Kami hanya memproses data ini dengan tujuan menyediakan Fitur kepada Anda, termasuk untuk merekam tugas eksekusi Anda dan pengguna yang berwenang serta status berjalan dari tugas.</td>
</tr>
</tbody></table>

## 3\. WILAYAH LAYANAN
Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR
Sebagaimana ditentukan dalam DPSA, termasuk Aceville Pte. Ltd.

## 5\. RETENSI DATA
Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:
<table>
<thead>
<tr>
<th><b>Informasi Pribadi</b></th>
<th><b>Kebijakan Retensi</b></th>
</tr>
</thead>
<tbody>
<tr>
<td>Sumber Data</td>
<td>Kami menyimpan data sampai Anda menghapus data tersebut secara manual (kecuali jika Anda memiliki biaya layanan terutang untuk Fitur, dalam hal ini kami akan menghapus data 120 hari setelah jumlah terutang jatuh tempo tetapi belum dibayarkan). Jika tidak, kami akan menghapus data tersebut saat Anda menghapus akun Anda.</td>
</tr>
<tr>
<td>Data Penjadwalan Tugas<br>Data Catatan Operasi</td>
<td>Kami menyimpan data tersebut selama 45 hari (kecuali Anda meminta penghapusan data tersebut, di mana kami akan menghapusnya dalam 30 hari). </td>
</tr>
<tr>
<td>Data Manajemen Akses</td>	
<td>Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Atau, apabila Anda menghapus akun, kami akan menghapus data tersebut dalam 30 hari.</td>
</tr>
</tbody></table>
Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS
Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah hukum tempat pengguna akhir berada.

Fitur ini tidak dimaksudkan untuk pemrosesan data sensitif. Anda harus memastikan bahwa Fitur ini tidak digunakan untuk mentransfer atau memproses data sensitif apa pun oleh Anda atau pengguna akhir, termasuk (namun tidak terbatas pada) opini politik, agama, atau keyakinan filosofis yang berkaitan dengan pengguna akhir, di mana pemrosesan tersebut dapat mengakibatkan risiko reputasi terhadap bisnis kami di dalam dan di luar yurisdiksi tempat pengguna akhir berada.

Anda menyatakan, menjamin, dan berjanji bahwa Anda akan memperoleh dan memelihara semua persetujuan yang diperlukan dari subjek data dalam hubungan dengan pemrosesan data pribadi mereka (sebagaimana berlaku) terkait dengan Fitur (termasuk untuk tujuan penyediaan Fitur), sesuai dengan hukum yang berlaku dan agar memungkinkan kami mematuhi hukum yang berlaku. Anda setuju bahwa Anda akan mengganti rugi dan membebaskan Tencent dari dan terhadap semua klaim, kewajiban, biaya, pengeluaran, kerugian atau kerusakan (termasuk kerugian konsekuensial, kehilangan laba, rugi reputasi, dan semua bunga, penalti, dan biaya serta pengeluaran profesional lainnya) yang dikeluarkan oleh Tencent yang timbul secara langsung atau tidak langsung dari pelanggaran persyaratan ini.
