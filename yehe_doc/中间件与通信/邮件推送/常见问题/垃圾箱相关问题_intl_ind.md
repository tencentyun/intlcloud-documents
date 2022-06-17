[](id:que1) 
### Mengapa email saya masuk ke folder spam?
Folder spam adalah kebijakan penilaian yang komprehensif dari penerima. Jika email Anda berakhir di folder spam, Tencent Cloud menyarankan agar Anda memeriksa situasi berikut untuk pemecahan masalah:

<table id="case">
<tr><th width=8%>Tidak.</th><th>Deskripsi</th></tr>
<tr>
<td>Kasus 1</td>
<td>Anda menggunakan domain publik atau IP publik untuk mengirim email. Dalam hal ini, reputasi Anda dibagikan dan tidak terlindungi dengan baik. Oleh karena itu, email Anda mungkin dianggap sebagai spam oleh penyedia layanan email lain dan dimasukkan ke dalam folder spam.</td>
</tr><tr>
<td>Kasus 2</td>
<td>Anda menggunakan domain atau IP baru. Karena IP baru tidak memiliki reputasi apa pun, email Anda memiliki peluang tertentu untuk masuk ke folder spam di awal. Namun, setiap penyedia layanan email memiliki proses belajar mandiri. Ketika mereka menemukan bahwa email Anda aman, seperti email verifikasi, mereka akan secara bertahap memindahkannya ke kotak masuk.</td>
</tr><tr>
<td>Kasus 3</td>
<td>Anda telah mengirim banyak email dalam waktu singkat menggunakan IP baru tanpa proses warm-up, misalnya, mengirim 100.000 email pada hari pertama. Dalam hal ini, kemungkinan besar penyedia layanan email dengan pembatasan ketat seperti Hotmail dan Yahoo Mail akan menolak dan menganggap email ini sebagai spam.</td>
</tr><tr>
<td>Kasus 4</td>
<td>Tingkat status valid alamat email Anda tinggi, yang akan sangat merusak reputasi pengirim Anda. Tencent Cloud dapat menghentikan Anda secara otomatis untuk mengirim email saat 8% email Anda diblokir untuk melindungi reputasi IP Anda.</td>
</tr><tr>
<td>Kasus 5</td>
<td>Email Anda diidentifikasi sebagai spam oleh penyedia layanan email karena berisi konten yang dibatasi seperti pornografi atau iklan. Sebaiknya rancang email Anda berdasarkan rasio 2:8 antara gambar dan teks, dengan tidak lebih dari 3 gambar dalam satu email (jangan sertakan konten seperti pornografi dan iklan).</td>
</tr></table>

[](id:que2) 
### Apa yang dapat saya lakukan untuk menghindari email masuk ke folder spam?
Cara terbaik untuk mencegah email masuk ke folder spam adalah **hindari [lima kasus](#case) yang disebutkan di atas**.
Faktor termasuk konten email, reputasi domain, tingkat terbuka, dan keluhan pengguna memengaruhi apakah email masuk ke folder spam. Penyedia layanan email yang berbeda memiliki kebijakan folder spam yang berbeda, yang tidak dapat kami kontrol. Namun, Tencent Cloud SES dapat menjamin kualitas IP pengirim.
Domain baru tidak memiliki reputasi dengan penyedia layanan email, jadi email yang dikirim dari domain tersebut masuk ke folder spam adalah hal yang wajar. Jika tidak ada masalah dengan isi email Anda, keadaan akan membaik asalkan Anda melakukan warm-up minimal satu bulan, memperhatikan tingkat terbuka, dan mengurangi tingkat keluhan.

[](id:que3) 
### Bagaimana cara mengetahui bahwa email telah masuk ke folder spam?
Anda dapat menggunakan alamat email Anda untuk menguji, atau login ke konsol dan memeriksa tingkat pengiriman email dan tingkat terbuka untuk menentukan apakah email Anda telah masuk ke folder spam. Jika tingkat pengiriman email dan tingkat terbuka keduanya rendah, mungkin email Anda telah masuk di folder spam.

[](id:que4) 
### Apa yang harus saya lakukan jika email saya masuk ke folder spam selama tahap pengujian?
Folder spam adalah kebijakan penilaian yang komprehensif dari penerima. Ikuti petunjuk di bawah ini:
1. Pastikan Anda belum pernah menggunakan domain Anda untuk mengirim spam sebelumnya. Jika reputasi domain Anda rendah, email Anda mungkin secara otomatis masuk ke folder spam.
2. Penerima mungkin menganggap email Anda sebagai spam karena subjek dan konten email yang tidak sesuai. Anda dapat [menggunakan alat penguji email](https://www.mail-tester.com/) untuk menguji konten email hingga Anda mendapatkan skor lebih tinggi dari 8.
