## 1.LATAR BELAKANG
Modul ini berlaku jika Anda menggunakan IoT Hub (“**Fitur**”). Modul ini tergabung dalam Perjanjian Privasi dan Keamanan Data yang berada di  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)"). Istilah-istilah yang digunakan, tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku meskipun terjadi inkonsistensi.

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
<td><b>Data Log</b>: log perangkat (jika Anda mengaktifkan pengumpulan data ini) </td>
<td>Kami hanya memproses data ini sesuai dengan konfigurasi Anda untuk memfasilitasi debugging atau pemecahan masalah oleh Anda.
Harap diperhatikan bahwa data ini disimpan dan dicadangkan dengan fitur Elasticsearch Service kami. Selain itu, Anda juga dapat menggunakan fitur Cloud Log Dump kami untuk menyimpan dan menganalisis data.
</td>
</tr>
<tr>
<td><b>Data Konfigurasi</b>: pengaturan produk (nama produk, ID produk), perangkat (nama perangkat, kunci/sertifikat perangkat), dan aturan (pernyataan SQL)</td>
<td>Kami hanya memproses data ini untuk memfasilitasi identifikasi dan pengelolaan produk dan/atau perangkat oleh Anda.
Harap diperhatikan bahwa data ini disimpan dan dicadangkan dengan fitur TencentDB for MySQL kami.
</td>
</tr>
<tr>
<td><b>Data Pemantauan</b>: statistik perangkat online, pesan perangkat, bayangan perangkat, mesin aturan, dan firmware</td>
<td>Kami hanya memproses data ini untuk memberi Anda statistik penggunaan Fitur oleh Anda.
Harap dicatat bahwa data ini disimpan dengan dan dikelola oleh fitur Cloud Monitor kami. Data ini dicadangkan dengan fitur TencentDB for MySQL kami.
</td>
</tr>
<tr>
<td><b>Data Sumber Daya</b>: sumber daya yang terkait dengan platform dan perangkat yang diunggah oleh Anda (jika Anda menyertakan data pribadi dalam sumber daya tersebut)</td>
<td>Kami hanya memproses data ini untuk memungkinkan Anda memberikan data tersebut kepada pengguna akhir Anda.
Harap diperhatikan bahwa data ini disimpan dan dicadangkan dengan fitur Cloud Object Storage kami.
</td>
</tr>
<tr>
<td><b>Data Perangkat yang Dipublikasikan</b>: jenis perangkat, status perangkat, aturan, dan perintah untuk mengendalikan perangkat dengan pernyataan SQL</td>
<td>Kami hanya memproses data ini untuk verifikasi perangkat dan penerusan pesan sebagaimana diinstruksikan oleh Anda.
Harap diperhatikan bahwa kami tidak memiliki akses ke data ini. Data ini ditransfer ke layanan lain sebagaimana diinstruksikan oleh Anda.
</td>
</tr>
<tr>
<td><b>Data Perangkat Pelanggan</b>: pesan perintah perangkat </td>
<td>Kami hanya memproses data ini untuk memfasilitasi kontrol perangkat oleh pengguna akhir Anda.
Harap diperhatikan bahwa kami tidak memiliki akses ke data ini. Data ini ditransfer ke layanan lain sebagaimana diinstruksikan oleh Anda. 
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
<td><b>Data Log</b></td>
<td>Disimpan selama 7 hari dengan fitur Elasticsearch Service kami.
Selain itu, Anda juga dapat menyimpan data dengan fitur Cloud Log Dump kami untuk jangka waktu yang ditentukan oleh Anda.</td>
</tr>
<tr>
<td><b>Data Konfigurasi</b></td>
<td>Disimpan sampai Anda meminta penghapusan akun. Setelahnya, data tersebut tersebut akan dihapus dalam waktu 30 hari. Jika Anda tidak meminta penghapusan, data tersebut akan dihapus dalam waktu 30 hari sejak tanggal ketika jumlah yang jatuh tempo menjadi terutang di akun Anda, penghentian penggunaan Fitur ini, atau penutupan Fitur ini, mana pun yang lebih awal.</td>
</tr>
<tr>
<td><b>Data Sumber Daya</b></td>
<td>Disimpan sampai Anda meminta penghapusan akun. Setelahnya, data tersebut tersebut akan dihapus dalam waktu 30 hari. Jika Anda tidak meminta penghapusan, data tersebut akan dihapus dalam waktu 30 hari sejak tanggal ketika jumlah yang jatuh tempo menjadi terutang di akun Anda, penghentian penggunaan Fitur ini, berakhirnya langganan Fitur, atau penutupan Fitur ini, mana pun yang lebih awal.</td>
</tr>
<tr>
<td><b>Data Pemantauan</b></td>
<td>Disimpan selama 7 hari.</td>
</tr>
<tr>
<td><b>Data Perangkat yang Dipublikasikan</b></td>
<td>Tidak disimpan.</td>
</tr>
<tr>
<td><b>Data Perangkat Pelanggan</b></td>
<td>Tidak disimpan. </td>
</tbody></table>

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6.PERSYARATAN KHUSUS
Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang memungkinkan individu untuk menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah yurisdiksi tempat pengguna akhir berada.
