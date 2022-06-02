[](id:que1) 
### Bagaimana cara mengonfigurasi DNS?
- Jika Anda menggunakan layanan Tencent Cloud DNS, login ke [konsol Tencent Cloud](https://console.cloud.tencent.com/cns) untuk mengonfigurasi.
- Jika Anda menggunakan layanan DNS yang disediakan oleh penyedia layanan domain lain, Anda dapat mentransfer domain Anda ke Tencent Cloud untuk resolusi DNS.
- Dalam kasus lain, konfigurasikan di penyedia layanan domain Anda.


[](id:que2) 
### Mengapa validasi gagal setelah saya mengonfigurasi DNS sesuai kebutuhan?
 Biasanya diperlukan waktu 10 menit untuk menyinkronkan DNS. Namun, mungkin ada penundaan tertentu tergantung pada TTL Anda. Gunakan alat untuk memeriksa apakah DNS yang dikonfigurasi sudah benar. Jika tidak ada masalah, harap tunggu.

[](id:que3) 
### Apakah saya harus mendapatkan pengajuan ICP untuk domain saya agar dapat menggunakan SES?
- Anda tidak harus melakukannya jika Anda hanya menggunakan domain untuk mengirim email.
- Jika Catatan domain Anda mengarah ke server daratan Tiongkok, Anda harus melengkapi pengajuan ICP untuk domain tersebut.

[](id:que4) 
### Dapatkah saya menggunakan domain email perusahaan sebagai domain email SES?
Untuk menghindari konflik antara data SPF dan MX, jangan gunakan domain email perusahaan Anda sebagai domain email SES.
Jika harus menggunakannya bersama, Anda perlu menggabungkan data SPF. Anda juga dapat membuat dan menggunakan domain tingkat kedua berdasarkan domain pengirim yang ada.

[](id:que5) 
### Dapatkah subdomain di bawah domain utama yang sama digunakan di SES?
Ya.

[](id:que6) 
### Apakah ada efek jika subdomain yang berbeda menggunakan layanan email yang berbeda?
Tidak.
