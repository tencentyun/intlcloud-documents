## Catatan
- Anda harus memiliki izin admin di domain pengirim.
- Jika domain Anda dihosting di Tencent Cloud, silakan login ke [Konsol DNSPod](https://console.cloud.tencent.com/cns) untuk mengonfigurasi domain. Jika domain Anda dihosting pada penyedia layanan domain lain, konfigurasikan sesuai dengan daftar periksa.
- Setelah domain dikonfigurasi, sinkronisasi dapat memakan waktu 5 menit hingga 2 jam. Harap menunggu dengan sabar hingga verifikasi selesai.
- Setelah verifikasi domain selesai, jangan hapus atau ubah data SPF dan MX yang dikonfigurasi, jika tidak, kesalahan dapat terjadi saat mengirim email.
- Jangan gunakan domain email perusahaan untuk menghindari konflik antara data SPF dan MX. Anda dapat membuat dan menggunakan domain tingkat kedua di bawah domain email perusahaan yang ada.
- Setiap akun Tencent Cloud dapat dikonfigurasi hingga 10 domain.

<span id ="Step1"></span>
## Langkah 1. Login ke konsol
Login ke [konsol SES](https://console.cloud.tencent.com/ses). Jika Anda belum memiliki akun Tencent Cloud, silakan lihat [Mendaftar untuk Akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) untuk membuatnya.

<span id ="Step2"></span>
## Langkah 2. Lakukan verifikasi organisasi
Jika Anda belum menyelesaikan verifikasi identitas untuk akun Anda, silakan buka [Pusat Akun](https://console.cloud.tencent.com/developer) untuk verifikasi identitas. Untuk informasi selengkapnya, pelajari [Panduan Verifikasi Identitas](https://intl.cloud.tencent.com/document/product/378/3629).

<span id ="Step3"></span>
## Langkah 3. Aktifkan SES
Jika Anda telah menyelesaikan verifikasi identitas untuk akun Anda, klik **Activate** (Aktifkan) untuk mengaktifkan SES. Setelah aktivasi berhasil, Anda akan mendapatkan tier gratis 1.000 email.
Setelah tier gratis habis, paket Anda akan digunakan secara otomatis. Jika tidak ada paket yang tersedia, Anda akan dikenakan biaya sesuai pemakaian.

<span id ="Step4"></span>
## Langkah 4. Konfigurasikan domain pengirim
>!Jika domain telah didaftarkan untuk Tencent Exmail, domain tersebut tidak dapat digunakan sebagai domain pengirim.
1. Login ke [Konsol SES](https://console.cloud.tencent.com/ses) ) dan klik **Sender Domain** (Domain Pengirim).
2. Pada halaman **Sender Domain** (Domain Pengirim), klik **Create** (Buat).
3. Masukkan domain pengirim di bidang **Domain**, misalnya, `mail.qcloud.com`, dan klik **Submit** (Kirim).
    
>!Domain pengirim adalah dasar dari alamat email dan mewakili identitas perusahaan pengirim. Untuk memverifikasi domain pengirim, Anda perlu mengonfigurasi informasi DNS untuk domain tersebut. Oleh karena itu, Anda harus memiliki izin admin di domain tersebut.
   
4. Setelah menyelesaikan konfigurasi DNS, klik **Verify** (Verifikasi).
5. Di kotak dialog **Sender Domain Configuration** (Konfigurasi Domain Pengirim), klik **Submit** (Kirim) untuk memverifikasi domain pengirim.

<span id ="Step5"></span>
## Langkah 5. Konfigurasikan alamat pengirim

1. Kembali ke halaman **Overview** (Ikhtisar) dan klik **Sender Address** (Alamat Pengirim).
2. Pada halaman **Sender Address** (Alamat Pengirim), klik **Create** (Buat).
3. Atur parameter berikut:
	- Domain Pengirim: pilih domain pengirim **verified** (terverifikasi) yang dibuat di [langkah 4](#Step4).
	- Awalan Email: misalnya, `test`.
	- Nama Pengirim: misalnya, `Lil C`.
>!Alamat pengirim Anda harus berupa alamat email lengkap yang diakhiri dengan domain pengirim **verified** (terverifikasi).
>Misalnya, <code>test@example.qcloudmail.com</code>.

4. Klik **Submit** (Kirim) untuk menyelesaikan konfigurasi.

<span id ="Step6"></span>
## Langkah 6. Konfigurasikan templat
1. Kembali ke halaman **Overview** (Ikhtisar) dan klik **Email Template** (Templat Email).
2. Pada halaman **Email Template** (Templat Email), klik **Create** (Buat).
3. Atur parameter berikut:
	- Nama Templat: misalnya, `test`.
	- Jenis Templat: pilih **HTML rich text**.
	- Ringkasan Email: misalnya, `templat email notifikasi`.
	- Badan Email: klik **Choose a file** (Pilih file) dan pilih file HTML sebagai badan email.
>?Isi email bisa dalam format teks biasa atau teks kaya. Format teks kaya membutuhkan kode HTML yang disiapkan terlebih dahulu. Setelah templat dikirimkan, maka akan memasuki tahap peninjauan dan dapat digunakan setelah disetujui. Peninjauan akan selesai dalam satu hari kerja.

4. Klik **Preview** (Pratinjau) untuk melihat pratinjau templat email.

5. Klik **Submit** (Kirim) untuk menyelesaikan konfigurasi templat.

<span id ="Step7"></span>
## Langkah 7. Kirim email
Setelah pendaftaran domain selesai dan templat disetujui, Anda dapat mengirim email melalui konsol SES atau panggilan API.
1. Klik **Email Sending** (Pengiriman Email) untuk membuka halaman pengiriman email.
>? Halaman ini hanya untuk menguji pengiriman email. Diiizinkan hingga 20 alamat penerima untuk satu pengujian. Anda dapat mengirim email ke lebih banyak penerima sekaligus melalui panggilan API. Untuk informasi selengkapnya, harap lihat [di sini](https://intl.cloud.tencent.com/document/product/1084/39408).
2. Atur parameter berikut:
 - Templat: pilih template yang **approved** (disetujui) yang dibuat di [langkah 6](#Step6).
 - Subjek: masukkan subjek email yang sesuai.
 - Dari: pilih alamat pengirim yang dikonfigurasi di [langkah 5](#Step5).
 - Kepada: masukkan alamat email yang ingin Anda kirimi email.
 - Variabel: masukkan variabel yang sesuai.
3. Setelah email berhasil dikirim, klik [Statistik](https://console.cloud.tencent.com/ses/stats) untuk melihat statistik.

