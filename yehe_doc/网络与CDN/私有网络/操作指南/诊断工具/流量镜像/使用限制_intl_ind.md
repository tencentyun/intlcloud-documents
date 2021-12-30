Pertimbangkan informasi berikut dan pertahankan bisnis Anda tetap utuh saat Anda menggunakan cermin lalu lintas.
- Cermin lalu lintas saat ini dalam uji beta. Untuk menerapkannya, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category). Sebaiknya simpan tautan ke Konsol Cermin Lalu Lintas, sehingga Anda dapat login ke Konsol tanpa mendaftar lagi.
- Cermin lalu lintas menggunakan sumber informasi CVM seperti CPU, memori, dan bandwidth secara pro rata.
  Lalu lintas yang dicerminkan diperhitungkan terhadap bandwidth instans. Dampaknya tergantung volume dan jenis lalu lintas. Misalnya, jika Anda mencerminkan antarmuka jaringan yang memiliki lalu lintas masuk 1 Gbps dan lalu lintas keluar 1 Gbps. Dalam hal ini, instans perlu menangani 1 Gbps lalu lintas masuk dan 3 Gbps lalu lintas keluar (1 Gbps untuk lalu lintas keluar, 1 Gbps untuk lalu lintas masuk yang dicerminkan dan 1 Gbps untuk lalu lintas keluar yang dicerminkan).
- Flow log tidak menangkap lalu lintas yang dicerminkan.
- Batasan mengenai grup keamanan:
 - Sumber: lalu lintas yang dicerminkan tidak tunduk pada kebijakan grup keamanan. 
 - Target: lalu lintas yang diterima tunduk pada kebijakan grup keamanan.
- Cermin lalu lintas tidak tersedia untuk:
 - Protokol resolusi alamat
 - DHCP
 - Layanan metadata instans
 - NTP
 - Aktivasi Windows
- Cermin lalu lintas mendukung pengumpulan lalu lintas dari ENI pada jenis CVM berikut:
Standar S1, Standar S2, Standar S3, Memori yang Dioptimalkan M1, Memori yang Dioptimalkan M2, Memori yang Dioptimalkan M3, IO Tinggi I1, IO Tinggi I2, IO Tinggi I3, Komputasi C2, Komputasi C3, CN3 yang dioptimalkan untuk Jaringan Komputasi, dan Big Data D1.

