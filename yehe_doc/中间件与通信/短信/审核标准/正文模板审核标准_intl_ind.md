>!Jika Anda melanggar Persyaratan Layanan, Tencent Cloud berhak untuk secara sepihak mengambil tindakan, seperti membatasi, menangguhkan, atau mengakhiri layanan yang diberikan kepada Anda atau menangguhkan akun Anda (tanpa aktivasi ulang) setiap saat sesuai dengan Persyaratan Layanan. Untuk paket berlangganan, tidak ada pembatalan langganan/pengembalian dana yang diizinkan, baik untuk paket yang telah maupun belum digunakan. Tencent Cloud berhak meminta Anda untuk bertanggung jawab secara hukum atas segala dampak atau konsekuensi serius yang timbul karenanya. Harap patuhi secara ketat Persyaratan Layanan, perkuat keamanan bisnis Anda, dan kirim pesan SMS yang mematuhi persyaratan.

Tinjauan templat isi SMS umumnya terdiri dari bagian-bagian berikut:
- [Tinjauan konten](#konten): kepatuhan konten templat SMS ditinjau.
- [Tinjauan variabel](#variabel): kepatuhan variabel templat SMS ditinjau.
- [Tinjauan berdasarkan spesifikasi spesifik](#khusus): kepatuhan berbagai jenis pesan SMS (pemberitahuan, kode verifikasi, SMS pemasaran, dll.) dengan spesifikasi khusus ditinjau.

## Spesifikasi Umum
### Spesifikasi konten[](id:content)

| Jenis | Spesifikasi |
|---------|---------|
| Batasan format | <li>Panjang total pesan SMS (berisi nilai sebenarnya dari tanda tangan dan variabel) tidak boleh melebihi 500 karakter. Setiap karakter, huruf, angka, tanda baca bahasa Mandarin (dalam bentuk fullwidth atau halfwidth), atau spasi akan dihitung sebagai satu karakter. </li><li>"[]" tidak didukung untuk menghindari kebingungan dengan tanda tangan. </li><li>¥, ★, dan simbol kombinasi khusus yang dimasukkan dengan penekanan tombol (seperti ^_^&, ☞, &#10003;, dan ※) tidak didukung karena dapat menyebabkan teks berantakan dalam pesan SMS.</li> |
| Spesifikasi konten | Templat harus mencerminkan bisnis aktual, dan makna dan skenario pesan harus dapat diidentifikasi melalui konten teks (dengan mengecualikan variabel). <li>Konten terkait keuangan (kode verifikasi, pemberitahuan, dan SMS pemasaran) tidak diperbolehkan. </li><li>Dilarang mengirim konten yang melanggar hukum dan tidak mematuhi persyaratan layanan. </li><li>Dilarang mengirim undangan yang tidak diminta, seperti undangan untuk mendaftar atau undangan keanggotaan. </li><li>Untuk industri real estat dan pendidikan, saat ini hanya kode verifikasi yang dapat dikirim. </li><li>Tautan apa pun dalam pesan harus berupa URL dengan izin ICP dalam bentuk konstan (nilai tetap). </li><li>Dilarang mengirim pesan terkait hal-hal berikut: persediaan, migrasi, wawancara rekrutmen, lotre, rabat, undian berhadiah, pinjaman, penagihan utang, manajemen investasi dan kekayaan, perjudian, pemenang lotre, narkoba, politik, perlindungan hak hukum, penggalangan dana, sumbangan amal, agama, takhayul, pemakaman, click farming, situs web untuk mengirim paket kosong, undian berhadiah satu dolar, penjualan kilat satu dolar, produk palsu, perawatan kesehatan, operasi plastik, kecantikan, klub, bar, pijat kaki, kekerasan, intimidasi, pornografi, bulu, kecurangan saat ujian, dekorasi (termasuk bahan bangunan dan perabot rumah tangga), pendaftaran merek dagang, bergabung dengan grup, penambahan teman di QQ atau WeChat, kencan, penjualan informasi pribadi, saluran SMS promosi, promosi game, promosi pameran, promosi situs web, promosi kupon, promosi kartu, promosi asuransi, peningkatan batas kredit, cashback dan rabat, faktur, undangan ulasan positif, alkohol, akuisisi pengguna, dan pengaktifan kembali pengguna.</li> |

### Spesifikasi variabel[](id:variable)
Templat isi SMS dapat berisi variabel, yang dapat Anda gunakan untuk memasukkan konten SMS kustom.

| Jenis | Spesifikasi |
|---------|---------|
| Format | `{Digit}` dalam urutan `{1}`, `{2}`, dan seterusnya. |
| Spesifikasi lainnya | <li>Sebuah templat tidak boleh hanya berisi variabel. </li><li>Untuk templat isi yang dibuat oleh pengguna individu, nilai untuk setiap variabel dapat berisi hingga 12 karakter. Untuk templat isi yang dibuat oleh pengguna organisasi, tidak ada batasan panjang nilai untuk setiap variabel. </li><li>Templat tidak boleh berisi variabel tautan apa pun (termasuk URL pendek), seperti `www.{1}.com`. </li><li>Variabel tidak dapat digunakan untuk melewati tautan (termasuk URL pendek), yang berarti nilai variabel tidak dapat diatur ke tautan (termasuk URL pendek). </li> |

## Spesifikasi Khusus[](id:special)
Selain spesifikasi umum, ada juga spesifikasi khusus untuk berbagai jenis templat isi SMS seperti yang dijelaskan di bawah ini:

<table>
     <tr>
         <th width="20%">Jenis SMS</th>  
         <th nowrap="nowrap">Spesifikasi Konten</th>  
     </tr>
	 <tr>      
         <td nowrap="nowrap">SMS Biasa (kode verifikasi)</td>   
	 <td><li>Pesan kode verifikasi SMS Tiongkok Daratan harus berisi kata kunci <b>kode verifikasi</b>, dan pesan kode verifikasi SMS Global harus berisi kata kunci <b>kode</b>. </li><li>Variabel dalam templat kode verifikasi SMS hanya boleh berisi 0–6 digit. </li><li>Selain spesifikasi umum, pengiriman konten dan tautan pemasaran dan promosi, termasuk informasi promosi bisnis internal ISP, juga dilarang.</li></td>   
     </tr> 
	<tr> 
	     <td nowrap="nowrap">SMS Biasa (pemberitahuan)</td>   
	     <td>Selain spesifikasi umum, pengiriman konten dan tautan pemasaran dan promosi, termasuk informasi promosi bisnis internal ISP, juga dilarang.</td>   
     </tr> 
	 <tr>
	     <td>SMS Pemasaran</td>   
	     <td><li>Templat isi harus menyertakan metode berhenti berlangganan di bagian akhir yang mendukung balasan "TD", "T", "N", dll. untuk berhenti berlangganan. </li><li>Selain spesifikasi umum, empat jenis pesan SMS pemasaran lainnya (pendidikan, real estat, keuangan, dan pinjaman) dilarang. </li><li>Selain spesifikasi umum, pesan SMS pemasaran kepada pengguna non-anggota dilarang. </li><li>Pesan SMS pemasaran harus dikirim antara pukul 8.00 dan 22.00 dan pengiriman pesan pada malam hari sebisa mungkin harus dihindari untuk mengurangi keluhan pengguna. </li></td>   
     </tr> 
</table>

## Informasi Terkait

- [Proses peninjauan](https://intl.cloud.tencent.com/document/product/382/40653)
- [Aturan penangguhan](https://intl.cloud.tencent.com/document/product/382/40653)
- [Signature review standards (Standar peninjauan tanda tangan)](https://intl.cloud.tencent.com/document/product/382/40658)
- [Pertanyaan Umum tentang templat isi](https://intl.cloud.tencent.com/document/product/382/13301)

Jika Anda memiliki pertanyaan tentang standar peninjauan templat isi, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).

