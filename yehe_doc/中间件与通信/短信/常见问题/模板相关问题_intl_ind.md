### Apa yang harus saya lakukan jika pesan SMS ditolak dengan kesalahan "Currently, messages in XX type cannot be send" (Saat ini, pesan jenis XX tidak dapat dikirim)?
Periksa kemungkinan adanya konten yang tidak sesuai dengan ketentuan di templat. Untuk informasi lebih lanjut tentang industri dan konten yang dilarang, lihat [Body Template Review Standards (Standar Peninjauan Templat Isi)](https://intl.cloud.tencent.com/document/product/382/40659).

### Bagaimana cara mengetahui jenis pesan SMS yang dapat dikirim dan yang tidak dapat dikirim?

Silakan ajukan permohonan tanda tangan dan templat sesuai dengan standar peninjauan [tanda tangan](https://intl.cloud.tencent.com/document/product/382/40658) dan [templat isi](https://intl.cloud.tencent.com/document/product/382/40659).

### Bagaimana cara memasukkan nama templat?
Anda dapat memasukkan nama templat sesuai dengan kebutuhan, dan tidak ada persyaratan khusus.

### Apa yang harus saya masukkan sebagai keterangan templat?
Jika konten templat singkat, memiliki definisi yang tidak jelas, atau memiliki terlalu banyak variabel, Anda perlu menambahkan keterangan untuk kasus penggunaannya; jika tidak, personel peninjau mungkin tidak dapat mengonfirmasi konten SMS dan kasus penggunaannya.
Misalnya, jika konten templat adalah `Kode verifikasi Anda adalah {1}. Harap masukkan kode verifikasi dalam {2} menit. Jika Anda tidak membuat permintaan ini, silakan hubungi layanan pelanggan di {3}.`, Anda dapat memasukkan "Kode verifikasi Anda adalah 123456. Harap masukkan kode verifikasi dalam 5 menit. Jika Anda tidak membuat permintaan ini, silakan hubungi layanan pelanggan di XXXX." sebagai keterangan templat.

### Apakah saya dapat langsung memasukkan tautan sebagai parameter templat?
Anda tidak dapat memasukkan tautan (termasuk URL pendek) sebagai parameter variabel templat. Jika perlu melakukannya, Anda sebaiknya langsung menggunakan URL dengan izin ICP sebagai konstanta di templat SMS dan menggunakannya setelah templat disetujui.

### Apakah ada batasan jumlah templat SMS?[](id:Q6)
Anda dapat memiliki maksimum 200 templat SMS. Anda dapat memilih templat yang berbeda untuk mengirim pesan SMS sesuai dengan kebutuhan.

### Apakah ada batasan jumlah karakter untuk setiap variabel dalam templat isi SMS?
- Dalam templat isi SMS yang dibuat oleh pengguna individu, setiap variabel dapat berisi hingga 12 karakter, dan templat tidak boleh berisi variabel saja.
- Untuk pengguna organisasi, tidak ada batasan jumlah karakter untuk setiap variabel, tetapi templat tidak boleh hanya berisi variabel.

Untuk informasi selengkapnya, lihat [Spesifikasi Variabel](https://intl.cloud.tencent.com/document/product/382/40659#variable).

### Apakah saya dapat menambahkan hyperlink dalam konten SMS?
Ya. Hyperlink dapat ditambahkan ke pesan SMS umum dan pemasaran. Alamat tautan dapat berupa konstanta saja (tetap), dan konten SMS perlu dikirim untuk ditinjau, tetapi hanya dapat dikirim setelah disetujui. Jika ditemukan konten SMS yang melanggar Perjanjian Layanan SMS Tencent Cloud, akun Anda akan diblokir.


### Berapa lama waktu yang dibutuhkan untuk meninjau aplikasi pesan SMS?
Umumnya, hasil peninjauan akan disampaikan dalam waktu sekitar 2 jam setelah Anda mengajukan tanda tangan atau templat isi SMS (jam peninjauan: 9.00–23.00 setiap hari).
Jika Anda perlu menggunakan fitur SMS dalam waktu mendesak, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) agar kami dapat mempercepat peninjauan.
Templat isi yang telah disetujui tidak menjamin pesan akan berhasil dikirim (karena ISP juga memiliki mekanisme peninjauan berbasis sampel). Jika pesan SMS Anda gagal terkirim, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.

### Apa yang harus saya lakukan jika jumlah karakter suatu variabel templat SMS melebihi batas?
Untuk pengguna individu, variabel templat saat ini dapat berisi hingga 12 karakter. Jika batas terlampaui, kami menyarankan Anda untuk melakukan peningkatan ke pengguna organisasi.

### Bagaimana format kurung kurawal dalam variabel templat? Bagaimana cara memasukkan variabel?
Gunakan `{digit}` sebagai variabel dalam urutan `{1}`, `{2}`, dan seterusnya.
Misalnya, `Kode verifikasi Anda adalah {1}, yang berlaku selama {2} menit dan tidak boleh diungkapkan kepada orang lain. Jika Anda tidak membuat permintaan ini, abaikan pesan ini.`

### Apakah saya dapat mengubah templat SMS?
Templat yang telah disetujui tidak dapat diubah. Jika diperlukan, Anda dapat mengirimkan templat baru untuk ditinjau. Templat yang sedang ditinjau atau telah ditolak dapat diubah.


### Apakah saya dapat menggunakan variabel dalam templat isi SMS?
Konten variabel (misalnya nama, tanggal, dan kode verifikasi) dalam templat SMS dapat diganti dengan parameter variabel `{1}`. Jika ada beberapa variabel, Anda harus memasukkan variabel mulai dari 1; tetapi templat tidak boleh hanya berisi variabel.

### Templat isi SMS saya tidak lulus peninjauan, dan saya diminta untuk menambahkan "Balas "TD" untuk berhenti berlangganan". Mengapa hal ini terjadi?
Templat isi untuk pesan SMS pemasaran harus mencantumkan metode untuk berhenti berlangganan agar penerima dapat membalas "TD", "T", atau "N" untuk berhenti berlangganan; jika tidak, pesan mungkin diblokir oleh ISP.


