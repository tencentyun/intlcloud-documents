Cermin lalu lintas menyediakan layanan pengumpulan lalu lintas yang memfilter dan menyalin lalu lintas yang diinginkan dari antarmuka jaringan yang ditentukan ke instans CVM di VPC yang sama. Fitur ini berlaku untuk kasus penggunaan termasuk audit keamanan, pemantauan risiko, pemecahan masalah, dan analisis bisnis.
> ?Namun, cermin lalu lintas menggunakan sumber informasi CVM seperti CPU, memori, dan bandwidth secara pro rata. Misalnya, jika Anda mencerminkan antarmuka jaringan yang memiliki lalu lintas masuk 1 Gbps dan lalu lintas keluar 1 Gbps. Dalam hal ini, instans perlu menangani 1 Gbps lalu lintas masuk dan 3 Gbps lalu lintas keluar (1 Gbps untuk lalu lintas keluar, 1 Gbps untuk lalu lintas masuk yang dicerminkan dan 1 Gbps untuk lalu lintas keluar yang dicerminkan).

## Prosedur
Berikut ini adalah komponen kunci dari cermin lalu lintas, bersama dengan alur kerjanya.
- Sumber: ENI yang ditentukan di VPC yang menerapkan aturan filter seperti jaringan, rentang koleksi, jenis koleksi, dan pemfilteran lalu lintas.
- Target: IP penerima yang mendapatkan lalu lintas yang dikumpulkan.
![](https://main.qcloudimg.com/raw/37ff00d3d5021bb7340d2b233a3182dc.png)

## Kasus Penggunaan
### Audit keamanan
Sistem yang berjalan dapat menyebabkan lalu lintas jaringan yang tidak sehat atau menghasilkan pesan kesalahan karena pengecualian perangkat lunak, kesalahan perangkat keras, virus komputer, atau penggunaan yang tidak tepat. Untuk menemukan penyebab masalah ini, Anda dapat menggunakan cermin lalu lintas untuk menganalisis pesan jaringan.

### Pemeriksaan intrusi
Untuk memastikan kerahasiaan, integritas, dan ketersediaan sumber daya sistem jaringan, Anda dapat menggunakan cermin lalu lintas untuk menyalin lalu lintas ke kluster CVM untuk analisis real-time.

### Analisa bisnis
Gunakan cermin lalu lintas untuk menyajikan mode lalu lintas bisnis dengan jelas dan visual.
