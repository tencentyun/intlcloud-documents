## 1.LATAR BELAKANG
Modul ini berlaku jika Anda menggunakan Platform TI (“Fitur”). Modul ini tergabung dalam Perjanjian Privasi dan Keamanan Data yang berada di  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Istilah-istilah yang digunakan, tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku meskipun terjadi inkonsistensi.

## 2.PEMROSESAN
Kami akan memproses data berikut sehubungan dengan Fitur:

<table>
<thead>
<tr>
<th><b>Informasi Pribadi</b></th>
<th><b>Tujuan Penggunaan</b></th>
</tr>
</thead>
<tbody>
<tr>
<td><b>Data Log Pelatihan</b> (Catatan selama pelatihan algoritma).</td>
<td rowspan="2">Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. 
Harap dicatat bahwa data ini terintegrasi dengan fitur Cloud Block Storage (CBS), TDSQL for MySQL (TDSQL), Message Queue CKafka (CKafka), dan Elasticsesarch Service (ES) untuk tujuan ini. Data ini juga terintegrasi dengan, dan disimpan dan dicadangkan dalam ruang penyimpanan yang Anda beli dalam fitur Cloud Object Storage (COS) kami.    
</td>
</tr>
<tr>
<td><b>Data Log Inferensi</b> (Catatan dalam proses berjalan setelah algoritma online)</td>
</tr>
<tr>
<td><b>Data Konfigurasi Tugas Pelatihan</b> (Parameter untuk tugas pelatihan algoritma)</td>
<td rowspan="2">Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. 
Harap diperhatikan bahwa data ini terintegrasi dengan fitur TDSQL, CKafka, dan ES kami untuk tujuan ini. 
</td>
</tr>
<tr>
<td><b>Data Konfigurasi Layanan Inferensi</b> (Parameter untuk tugas pelatihan algoritma online)</td>
</tr>
<tr>
<td><b>Data Anotasi Pengguna</b> (Label untuk data beranotasi pengguna (dari fitur platform))</td>
<td>Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. 
Harap diperhatikan bahwa data ini terintegrasi dengan fitur TDSQL, CKafka, dan ES kami untuk tujuan ini. Data ini juga terintegrasi dengan, dan disimpan serta dicadangkan dalam fitur COS kami. 
</td>
</tr>
<tr>
<td><b>Data Model Pelatihan</b> (File model yang dihasilkan setelah pelatihan algoritma)</td>
<td>Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda. 
Harap diperhatikan bahwa data ini terintegrasi dengan fitur TDSQL, CKafka, dan ES kami untuk tujuan ini. Data ini juga terintegrasi dengan, dan disimpan serta dicadangkan dalam ruang penyimpanan yang Anda beli di fitur COS kami.
</td>
</tbody></table>

## 3.WILAYAH LAYANAN
Sebagaimana ditentukan dalam DPSA.
## 4.SUB-PROSESOR
Sebagaimana ditentukan dalam DPSA.
## 5.RETENSI DATA
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
<td><b>Data Log Pelatihan</b></td>
<td>Kami menyimpan data ini selama 7 hari. Anda juga dapat memilih untuk meningkatkan periode retensi dengan mendapatkan layanan fitur Cloud Log Service (CLS) kami.</td>
</tr>
<tr>
<td><b>Data Log Inferensi</b></td>
<td>Kami menyimpan data ini selama 7 hari. Anda juga dapat memilih untuk meningkatkan periode retensi dengan mendapatkan layanan fitur CLS kami.</td>
</tr>
<tr>
<td><b>Data Konfigurasi Tugas Pelatihan</b></td>
<td>Kami menyimpan data tersebut selama batas waktu retensi data yang Anda pilih, atau hingga Anda menghapus notebook atau tugas pelatihan secara manual. Atau, apabila Anda menghapus akun atau menghentikan penggunaan Fitur, kami akan menghapus data tersebut setelah 7 hari.</td>
</tr>
<tr>
<td><b>Data Konfigurasi Layanan Inferensi</b></td>
<td>Kami menyimpan data tersebut selama batas waktu retensi data yang Anda pilih, atau hingga Anda menghapus notebook atau tugas pelatihan secara manual. Atau, apabila Anda menghapus akun atau menghentikan penggunaan Fitur, kami akan menghapus data tersebut setelah 7 hari.</td>
</tr>
<tr>
<td><b>Data Anotasi Pengguna</b></td>
<td>Data ini tidak disimpan.</td>
</tr>
<tr>
<td><b>Data Model Pelatihan</b></td>
<td>Data ini tidak disimpan.</td>
</tbody></table>





Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.
## 6.PERSYARATAN KHUSUS
Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah yurisdiksi tempat pengguna akhir berada.
