## 1\. LATAR BELAKANG
Modul ini berlaku jika Anda menggunakan Real User Monitoring (“Fitur”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di [DPSA](https://intl.cloud.tencent.com/document/product/301/17347). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, maka Modul inilah yang akan berlaku apabila terjadi inkonsistensi.

## 2\. PEMROSESAN
Kami akan memproses data berikut sehubungan dengan Fitur:

<table>
   <tr>
      <th>Informasi Pribadi</th>
      <th>Penggunaan</th>
   </tr>
   <tr>
      <td><b>Data Log Asli:</b> Log kesalahan JS, kesalahan Promise, pengecualian pemuatan JS, log permintaan antarmuka, model perangkat, jenis operator, jenis jaringan, sistem operasi, wilayah, merek perangkat, data peristiwa kustom (data dari peristiwa pelaporan yang Anda tentukan) </td>
      <td>Kami menggunakan informasi ini untuk tujuan menyediakan Fitur ini kepada Anda.
<br/>Perhatikan bahwa data ini terintegrasi, disimpan, dan dicadangkan di fitur Cloud Log Service (CLS), TencentDB for Redis (Redis), dan TencentDB for MySQL kami.</td>
</td>
   <tr>
      <td><b>Data indikator:</b> Data log asli yang terorganisir dan diagregasi (kinerja halaman, pemantauan API, pemantauan sumber daya statis, jumlah kejadian tidak normal)</td>
     <td>Kami menggunakan informasi ini untuk tujuan menyediakan Fitur ini kepada Anda.
<br/>Perhatikan bahwa data ini terintegrasi, disimpan, dan dicadangkan di fitur CLS, Redis, dan TencentDB for MySQL kami. Perhatikan bahwa jika Anda mengaktifkan dan membeli fitur Cloud Monitor (CM) kami, CM juga akan mengumpulkan data ini untuk menyediakan Fitur kepada Anda (dengan memberi tahu Anda saat data indikator tidak normal).</td>
</td>
   <tr>
     <td><b>Data Proyek:</b> nama proyek, deskripsi proyek, jenis proyek, alamat situs web, peringkat proyek, data PV/UV.</td>
     <td>Kami menggunakan informasi ini untuk tujuan menyediakan Fitur ini kepada Anda.
<br/>Perhatikan bahwa data ini terintegrasi, disimpan, dan dicadangkan di fitur CLS, Redis, dan TencentDB for MySQL kami. </td>
</tr>
   <tr> 
</table> 



## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR
Sebagaimana ditentukan dalam DPSA, termasuk Aceville Pte Ltd.

## 5\. RETENSI DATA
Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

<table>
   <tr>
      <th>Informasi Pribadi</th>
      <th>Kebijakan Retensi</th>
​        </tr>
   <tr>
      <td>Data Log Asli</td>
      <td>Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Jika tidak, data tersebut disimpan selama 30 hari.</tr>
   </tr>
   <tr>
      <td>Data Indikator</td>
      <td>Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Jika tidak, data tersebut disimpan selama 15 hari.</tr>
      </tr>
   <tr> 
      <td>Data Proyek</td>
      <td>Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Jika tidak, kami menyimpan data tersebut selama 1 tahun (selain peringkat proyek dan data PV/UV yang disimpan selama 90 hari).</td>
</table>


Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS
Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah hukum tempat pengguna akhir berada.