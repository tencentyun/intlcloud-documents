# Mengonfigurasi Informasi Dasar
Pada halaman detail aplikasi, Anda dapat melihat dan memodifikasi informasi aplikasi. Pada halaman **Basic Configuration** (Konfigurasi Dasar), Anda dapat mengonfigurasi ambang batas pengiriman pesan, batas pengiriman pesan SMS global, callback peristiwa, dan batas frekuensi pengiriman sesuai kebutuhan, serta mengelola penerima alarm.

## Pengaturan Ambang Batas Pengiriman Pesan
1. Login ke [SMS console (Konsol SMS)](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fsmsv2).
2. Anda dapat masuk ke tab **Basic Configuration** (Konfigurasi Dasar) dengan cara berikut:
- Pilih **Application Management** > **Application List** (Manajemen Aplikasi > Daftar Aplikasi) di bilah sisi kiri dan klik blok aplikasi target untuk masuk ke halaman detailnya. Kemudian, klik **Basic Configuration** (Konfigurasi Dasar).
- Pilih **Application Management** > **Basic Configuration** (Manajemen Aplikasi > Konfigurasi Dasar) di bilah sisi kiri.
3. Pilih **current application** (aplikasi saat ini) sebagai aplikasi target yang akan dimanipulasi.
4. Klik **Set** (Atur) di **Message Sending Threshold Settings** (Pengaturan Ambang Batas Pengiriman Pesan) untuk mengatur ambang batas alarm pengiriman pesan. Penerima alarm dapat menerima pemberitahuan alarm ketika ambang batas tercapai. Anda juga dapat mengatur batas pengiriman pesan agar aplikasi berhenti mengirim pesan saat batas tersebut tercapai pada hari itu.
![](https://qcloudimg.tencent-cloud.cn/raw/dde38d44364076d2ce64eeb48ed90fc2.png)
5. Klik **Set** (Atur) untuk menyimpan.
Setelah itu, silakan konfigurasikan para penerima alarm di **Notifications & Alarms** (Pemberitahuan & Alarm) sehingga mereka dapat menerima pemberitahuan ketika ambang batas tercapai.
![](https://qcloudimg.tencent-cloud.cn/raw/bab6b1bc059170bad7612e7fe998911c.png)

## Pengaturan Batas Pengiriman Pesan SMS Global
<dx-alert infotype="notice" title="">
Fitur ini hanya didukung untuk pengguna organisasi.
</dx-alert>

1. Klik **Set** (Atur) di **Global SMS Message Sending Limit Settings** (Pengaturan Batas Pengiriman Pesan SMS Global) untuk menentukan negara/wilayah mana yang dapat menerima pesan SMS dan mengatur batas pengiriman pesan dalam satu hari kalender untuk setiap negara/wilayah.

![](https://qcloudimg.tencent-cloud.cn/raw/004b0e6423c3214962c0d7cdad7ee984.png)

2. Anda dapat memilih negara/wilayah satu per satu dari daftar drop-down atau mengimpor beberapa negara/wilayah dengan mengeklik **Batch Import** (Impor Batch). Klik **Download Template** (Unduh Template) untuk mendapatkan template impor batch.
![](https://qcloudimg.tencent-cloud.cn/raw/fd0ebeef9e68b6bd55e0b84e56010a7e.png)

<dx-alert infotype="notice" title="">
- Batas pengiriman pesan untuk satu negara/wilayah dalam satu hari kalender tidak boleh melebihi batas total untuk semua negara/wilayah.
- Jika dibiarkan kosong, batas tersebut akan sama dengan batas total secara default.
- Dengan pengaturan ini, aplikasi hanya dapat mengirim pesan ke negara/wilayah tertentu.
</dx-alert>

3. Klik **Set** (Atur) untuk menyimpan.
Jika Anda ingin memodifikasi batas pengiriman pesan untuk satu negara/wilayah dalam satu hari kalender, klik **Edit** di kolom **Operation** (Operasi). Anda juga dapat menghapus atau mengekspor negara/wilayah yang dikonfigurasi.

## Konfigurasi Callback Peristiwa

1. Klik **Set** (Atur) di **Event Callback Configuration** (Konfigurasi Callback Peristwa), pilih callback status pesan sesuai kebutuhan, lalu masukkan URL callback yang sesuai (API penerimaan informasi callback).
![](https://qcloudimg.tencent-cloud.cn/raw/8df55c41c5d708b2199e21849f4bb879.png)

<dx-alert infotype="explain" title="">
Format isi yang dibawa oleh informasi callback adalah JSON.
</dx-alert>

2. Klik **Set** (Atur) untuk menyimpan.
Setelah konfigurasi berhasil, Anda akan lebih memahami detail pengiriman SMS. Misalnya, setelah Anda mengonfigurasi alamat callback status penerima pesan, Tencent Cloud akan segera meneruskan informasi callback yang diterima dari operator ke alamat callback yang Anda tentukan. Setelah itu, Anda dapat menulis kode yang sesuai untuk menerima, mengurai, dan memanfaatkan secara lebih maksimal informasi callback yang diteruskan oleh SMS Tencent Cloud.

![](https://qcloudimg.tencent-cloud.cn/raw/c2a11dac4c5cf3a3ab6ec18b42db488b.png)

## Mengatur Batas Frekuensi Pengiriman
Untuk memastikan keamanan bisnis dan saluran serta meminimalkan kerugian finansial yang disebabkan oleh panggilan berbahaya dari API SMS, batas frekuensi default untuk mengirim pesan SMS diatur sebagai berikut:
- Pesan SMS dengan konten yang sama dapat dikirim ke satu nomor ponsel hanya sekali dalam waktu 30 detik.
- Hingga 10 pesan dapat dikirim ke nomor ponsel yang sama dalam satu hari kalender.

<dx-alert infotype="notice" title="">
 Pengguna individu tidak memiliki izin untuk memodifikasi batas frekuensi. Untuk menggunakan fitur ini, ubah "Individual Verification" (Verifikasi Individu) menjadi "Organization Verification" (Verifikasi Organisasi).
</dx-alert>

1. Klik **Set** (Atur) di **Sending Frequency Limit** (Mengirim Batas Frekuensi), pilih batas sesuai kebutuhan, dan atur ambang batas yang sesuai untuk setiap batas.
![](https://qcloudimg.tencent-cloud.cn/raw/16424c4a2e847d0ca1e4027ac3834b93.png)

2. Klik **Set** (Atur) untuk menyimpan.
![](https://qcloudimg.tencent-cloud.cn/raw/6d7f779f88d4ffb51a4fa3af5412c660.png)

## Mengatur Daftar Izin Batas Frekuensi

<dx-alert infotype="explain" title="">
 Nomor ponsel dalam daftar izin tidak tunduk pada kebijakan batas frekuensi. Daftar izin dapat berisi hingga 300 nomor ponsel.
</dx-alert>

### Menambahkan nomor ponsel ke daftar izin
1. Klik **Set** (Atur) di **Frequency Limit Allowlist** (Daftar Izin Batas Frekuensi) dan masukkan satu nomor ponsel per baris. Anda dapat menambahkan hingga 300 nomor ponsel ke daftar izin.
![](https://qcloudimg.tencent-cloud.cn/raw/1ceb74b7513e133789522bc71cdb337d.png)

2. Klik **Set** (Atur) untuk menyimpan pengaturan.
![](https://qcloudimg.tencent-cloud.cn/raw/72c2f32c724fc4335db26b5e1592523a.png)

### Menghapus nomor ponsel dari daftar izin
1. Klik **Delete** (Hapus) di baris nomor ponsel target di **Frequency Limit Allowlist** (Daftar Izin Batas Frekuensi).
![](https://qcloudimg.tencent-cloud.cn/raw/12bfff56e54349fe94fb1cb7f69b03db.png)
2. Klik **Delete** (Hapus).




