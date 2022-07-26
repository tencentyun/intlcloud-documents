<span id="que1"></span>
### Apa yang harus saya lakukan jika kode kesalahan -505 ditampilkan untuk campuran streaming setelah push?
Sebelum memulai campuran streaming, harap tunggu sekitar 5 detik setelah push dimulai.


<span id="que2"></span>
### Bagaimana cara mengatasi masalah API campuran streaming menampilkan kode -505?
Jika API campuran streaming melaporkan kode -505, artinya ID streaming tidak memiliki data yang sesuai di backend CSS.
1. Anda dapat melakukan pull pada streaming untuk memeriksa berhasil atau tidaknya push streaming. Jika pull berhasil, push juga akan berhasil.
2. Jika pull dapat dilakukan pada streaming, tetapi API melaporkan kode -505, silakan pastikan bahwa `AppID` yang dimasukkan ke dalam parameter campuran streaming sudah benar.

<span id="que3"></span>
### Apa yang harus saya lakukan jika suara host asisten tidak terdengar setelah campuran streaming di streaming audio?
Periksa `input_type` streaming audio sudah diatur ke 4 atau belum.


<span id="que5"></span>
### Apa yang akan terjadi jika campuran streaming tidak dibatalkan setelah diterapkan?
Campuran streaming akan dilanjutkan hingga perintah untuk membatalkannya diterima.

<span id="que6"></span>
### Apa yang akan terjadi jika streaming input tiba-tiba terhenti selama campuran streaming?
Jika streaming yang terhenti bukan streaming latar belakang, gambar akan terhenti di bingkai terakhir. Jika streaming yang terhenti adalah streaming latar belakang, seluruh gambar video akan terhenti. Jika streaming yang terhenti berhasil di-push kembali dengan ID streaming yang sama dalam waktu 15 menit, campuran streaming akan dilanjutkan secara otomatis.

<span id="que7"></span>
### Bagaimana cara mendapatkan hasil campuran streaming rekaman?
Petunjuk mendetail dapat dilihat di [Creating Recording Task (Membuat Tugas Perekaman)](https://intl.cloud.tencent.com/document/product/267/37309).

<span id="que8"></span>
### Mengapa terdapat bilah berwarna hitam di gambar video setelah campuran streaming?
Kemungkinan penyebabnya mencakup:
1. Streaming asli berisi bilah berwarna hitam.
2. Rasio aspek output di parameter campuran streaming berbeda dengan rasio aspek di streaming asli. Misalnya, jika rasio aspek target campuran streaming 16:9, tetapi rasio aspek video asli 4:3, backend campuran streaming akan menambahkan bilah berwarna hitam ke video asli untuk mengubah rasio aspeknya menjadi 16:9 untuk output.

Anda dapat mencegah munculnya bilah berwarna hitam dengan dua cara berikut:
1. Gunakan rasio aspek video input untuk video output.
2. Gunakan parameter pemotongan sesuai dengan petunjuk penggunaan fitur pemotongan.

<span id="que9"></span>
### Mengapa gambar video host asisten di campuran streaming tidak berada di posisi yang diinginkan?
Secara umum, hal ini disebabkan oleh perubahan resolusi pada streaming input dalam campuran streaming. Misalnya, jika resolusi streaming input 1280x720 selama penerapan campuran streaming, tetapi menjadi 2560x1440 setelah beberapa saat, gambar video output akan berubah dan berada di posisi yang berbeda.

>? Sebaiknya jangan ubah resolusi streaming input selama campuran streaming. Jika diperlukan, hitung parameter posisi dan ajukan permintaan campuran streaming lagi.

<span id="que10"></span>
### Apakah output campuran streaming dapat dikodekan dalam H.265?
Saat ini, campuran streaming hanya mendukung pengodean H.264 untuk streaming output. Meskipun streaming input dikodekan dalam H.265, streaming output hanya dapat dikodekan dalam H.264.

<span id="que11"></span>
### Mengapa kode kesalahan -30300 ditampilkan setelah saya membatalkan campuran streaming sebanyak dua kali?
API untuk membatalkan campuran streaming hanya perlu dipanggil satu kali dan tidak boleh dipanggil lagi setelah pembatalan berhasil.

<span id="que12"></span>
### Kapan campuran streaming akan dibatalkan secara otomatis setelah streaming input terhenti selama campuran streaming?
Kita akan menggunakan campuran dua streaming sebagai contoh. Jika salah satu streaming terhenti, campuran streaming tidak akan dibatalkan secara otomatis. Jika perekaman diaktifkan, perekaman juga akan dilanjutkan. Jika kedua streaming terhenti, campuran streaming akan dibatalkan secara otomatis setelah 15 menit.

<span id="que13"></span>
### Mengapa gambar video sedikit mundur ketika pemanggilan campuran streaming dilakukan?
Mekanisme implementasi campuran streaming akan menyesuaikan gambar video dari beberapa streaming semaksimal mungkin; oleh karena itu, sedikit kemunduran dapat terjadi selama pemrosesan. Agar hal ini tidak memengaruhi bisnis Anda, jangan panggil API campuran streaming secara sering, kecuali jika diperlukan.

<span id="que14"></span>
### Jika mikrofon host dinonaktifkan selama campuran streaming, apakah tata letak campuran streaming akan berubah secara otomatis?
Tidak. Penjadwal campuran streaming tidak akan memodifikasi parameter tata letak Anda. Jika mikrofon host dinonaktifkan, Anda perlu menghitung parameter tata letak dan memulai campuran streaming lagi.
