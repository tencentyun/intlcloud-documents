<table>
   <tr>
      <th width="0px" style="text-align:center">Kategori Kesalahan</td>
      <th width="0px" style="text-align:center">Subkategori Kesalahan</td>
      <th width="0px"  style="text-align:center">Deskripsi</td>
      <th width="0px"  style="text-align:center">Solusi</td>
   </tr>
   <tr>
      <td style="text-align:center">Kesalahan Jenis SMS</td>
      <td>Jenis SMS salah</td>
      <td>Tentukan jenis SMS sebagai pemberitahuan untuk pesan pemasaran.</td>
      <td>Pilih jenis SMS yang benar sesuai dengan konten pesan.</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='9'>Kesalahan Konten SMS</td>
      <td rowspan='2'>Format variabel salah</td>
      <td rowspan='2'>Format variabel salah</td>
      <td>Gunakan “{digit}” (dalam bentuk halfwidth) sebagai variabel dengan urutan “{1}”, “{2}”, dan seterusnya.</td>
   </tr>
	    <tr>
      <td>Jangan mengatur variabel lokal, seperti “www.${1}.cn” dan “186${2}1234”.</td>
   </tr>
   <tr>
      <td style="text-align:center">Berisi simbol yang tidak didukung.</td>
      <td>Simbol yang tidak didukung (seperti ￥, ★, ^_^, &, √, dan ※) dapat mengakibatkan konten pesan berantakan.</td>
      <td><li>Hapus simbol yang tidak didukung di templat.</li><br><li>Hapus simbol “【】” di templat. Jika tidak, pesan akan gagal terkirim.</li><br></td>
   </tr>
   <tr>
      <td style="text-align:center">Konten tidak jelas.</td>
      <td>Templat yang hanya berisi variabel, atau templat yang berisi sedikit teks tetap dan terlalu banyak variabel. Nilai variabel terlalu besar sehingga sulit untuk mengidentifikasi skenario bisnis.</td>
      <td>Templat yang hanya berisi variabel tidak didukung. Silakan atur variabel berdasarkan kebutuhan aktual Anda dan gunakan teks tetap sebanyak mungkin agar konten pesan dan skenario bisnis lebih dapat diidentifikasi.</td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='2'>Kurang kata kunci yang diperlukan.
</td>
      <td >Tidak ada kata kunci untuk berhenti berlangganan (TD, T, atau N) dalam pesan pemasaran.</td>
      <td>Pesan pemasaran harus mencantumkan kata kunci (TD, T, atau N) sehingga penerima dapat membalas pesan dengan kata kunci untuk berhenti berlangganan.</td>
   </tr>
   <tr>
  <td>Kata kunci "kode verifikasi" (dalam bahasa Mandarin) tidak ada dalam pesan kode verifikasi Tiongkok Daratan, atau kata kunci "kode" tidak ada dalam pesan kode verifikasi global.</td>
      <td>Silakan tambahkan kata kunci "kode verifikasi" (dalam bahasa Mandarin) ke pesan kode verifikasi Tiongkok Daratan dan kata kunci "kode" ke pesan kode verifikasi global.</td>
   </tr>
   <tr>
      <td style="text-align:center">Berisi konten terlarang.</td>
      <td>Selain konten pemberitahuan, pesan pemberitahuan juga berisi konten pemasaran.</td>
      <td>Silakan hapus konten pemasaran.</td>
   </tr>
   <tr>
      <td style="text-align:center">Berisi variabel lain.</td>
      <td>Selain kode verifikasi, pesan kode verifikasi juga berisi variabel panjang lainnya.</td>
      <td>Jangan atur konten lain sebagai variabel. Ajukan templat pesan kode verifikasi untuk pendaftaran dan modifikasi kata sandi secara terpisah.</td>
   </tr>
   <tr>
      <td style="text-align:center">Tautan dalam pesan tidak valid atau tidak mematuhi persyaratan layanan.</td>
      <td>Tautan tidak relevan dengan konten pesan, atau tautan tidak valid./td>
      <td><li>Hanya tautan teks tetap yang didukung sehingga kami dapat meninjau konten tautan.</li><br><li>Jika tautan tidak valid atau tidak dapat dibuka, silakan periksa lebih dahulu apakah konten tautan benar.</li><br><li>Jika konten tautan tidak konsisten dengan konten templat, pesan tidak dapat dikirim.</li></td>
   </tr>
   <tr>
      <td style="text-align:center" rowspan='10'>Konten SMS yang Tidak Didukung atau Tidak Mematuhi Persyaratan Layanan</td>
      <td>Konten yang terkait dengan wawancara rekrutmen tidak didukung</td>
      <td>-</td>
      <td>Saat ini, pesan pemberitahuan rekrutmen atau wawancara tidak dapat dikirim.</td>
   </tr>
   <tr>
      <td style="text-align:center">Konten yang terkait dengan game, keuangan, asuransi, dll., tidak didukung.</td>
      <td>-</td>
      <td>Saat ini, pesan yang terkait dengan game, keuangan, dan asuransi, tidak dapat dikirim.</td>
   </tr>
   <tr>
      <td style="text-align:center">Konten kencan tidak didukung.</td>
      <td>-</td>
      <td>Saat ini, pesan kencan tidak dapat dikirim.</td>
   </tr>
   <tr>
      <td style="text-align:center">Pesan pengingat pembayaran tidak dapat dikirim.</td>
      <td>-</td>
      <td>Pesan pengingat pembayaran tidak dapat dikirim.</td>
   </tr>
   <tr>
      <td style="text-align:center">Untuk industri real estat atau pendidikan, hanya pesan kode verifikasi yang dapat dikirim.</td>
      <td>-</td>
      <td>Untuk industri real estat atau pendidikan, hanya pesan kode verifikasi yang dapat dikirim, sedangkan pesan pemberitahuan atau pemasaran tidak dapat dikirim.</td>
   </tr>
   <tr>
      <td style="text-align:center">Templat melibatkan jenis konten yang dilarang dalam Standar Peninjauan Templat Isi.</td>
      <td>-</td>
      <td>Dilarang mengirim pesan terkait konten berikut: persediaan, migrasi, wawancara rekrutmen, lotre, rabat, undian berhadiah, pinjaman, penagihan kredit, investigasi kredit, investasi dan manajemen kekayaan, perjudian, pemenang lotre, narkoba, politik, perlindungan hak hukum, penggalangan dana, sumbangan amal, agama, takhayul, pemakaman, click farming, situs web untuk mengirim paket kosong, undian satu dolar, penjualan kilat satu dolar, produk palsu, perawatan kesehatan, operasi plastik, kecantikan, klub, bar, pijat kaki, kekerasan, intimidasi, pornografi, bulu, kecurangan saat ujian, dekorasi (termasuk bahan bangunan dan perabot rumah tangga), pendaftaran merek dagang, bergabung dengan grup, penambahan teman di QQ atau WeChat, kencan, penjualan informasi pribadi, saluran SMS promosi, promosi game, promosi pameran, promosi situs web, promosi kupon, promosi kartu, promosi asuransi, peningkatan batas kredit, cashback dan rabat, penerbitan faktur, undangan ulasan positif, alkohol, akuisisi pengguna, dan pengaktifan kembali pengguna. Templat SMS yang berisi salah satu konten di atas akan ditolak.</td>
   </tr>
   <tr>
      <td style="text-align:center">Tautan digunakan sebagai variabel.</td>
      <td>-</td>
      <td>Tautan tidak dapat digunakan sebagai variabel. Silakan gunakan sebagai teks tetap.</td>
   </tr>
   <tr>
      <td style="text-align:center">Pengiriman bom SMS.</td>
      <td>Templat berisi konten promosi dan akuisisi pengguna tanpa deskripsi anggota.</td>
      <td><li>Tambahkan nama anggota ke templat untuk mengonfirmasi keanggotaan.</li><br><li>Dilarang mengirim pesan SMS dengan konten, seperti promosi pembukaan, pengenalan bisnis, atau promosi perusahaan. Pesan semacam itu akan dianggap sebagai pengiriman bom SMS karena keanggotaan penerimanya tidak dapat diverifikasi.</li><br></td>
   </tr>
   <tr>
      <td style="text-align:center">Konten tidak mutakhir.</td>
      <td>Misalnya, templat promosi yang dirancang untuk festival penting dikirimkan setelah festival berlalu.</td>
      <td>Setiap templat iklan festival (seperti Hari Buruh atau Hari Kemerdekaan) harus dikirim terlebih dahulu untuk mendapatkan persetujuan. Jika tidak, pesan tidak terkirim tepat waktu.</td>
   </tr>
</table>
