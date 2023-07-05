
### Instans
Instans adalah Cloud Virtual Machine (CVM), yang merupakan sumber daya komputasi virtual yang berisi CPU, memori, OS, jaringan, disk, dan komponen komputasi dasar lainnya.
Instans CVM menyediakan layanan komputasi yang aman, andal, dan elastis di cloud untuk memenuhi persyaratan komputasi. Seiring perubahan tuntutan bisnis, sumber daya komputasi dapat diskalakan secara real-time untuk menurunkan biaya perangkat lunak dan perangkat keras Anda serta menyederhanakan pekerjaan OPS TI.

### Jenis Instans
Tencent Cloud menyediakan berbagai konfigurasi CPU, MEM, penyimpanan, dan kapasitas jaringan untuk instans CVM. Untuk informasi selengkapnya, lihat [Jenis Instans](https://intl.cloud.tencent.com/document/product/213/11518).

### Citra
Citra adalah templat yang telah dikonfigurasi sebelumnya yang berisi sistem operasi dan aplikasi yang menjalankan instans CVM. Tencent Cloud CVM menyediakan citra yang telah dikonfigurasi sebelumnya untuk Windows, Linux, dll.

### Cloud Block Storage
Cloud Block Storage (CBS) adalah perangkat penyimpanan blok dengan ketersediaan tinggi, sangat andal, hemat biaya, dan dapat disesuaikan. Perangkat ini dapat digunakan sebagai disk mandiri dan dapat diperluas untuk CVM, yang menyediakan perangkat [penyimpanan](https://intl.cloud.tencent.com/document/product/213/4952) yang efisien dan andal.

### VPC
VPC adalah ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud.

### Alamat IP
Tencent Cloud menyediakan [alamat IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225) dan [alamat IP publik](https://intl.cloud.tencent.com/document/product/213/5224). Alamat IP pribadi adalah untuk interkoneksi instans CVM dalam LAN yang sama, sedangkan alamat IP publik berfungsi untuk layanan yang dapat diakses oleh publik.

### IP Elastis
IP Elastis (Elastic IP/EIP) adalah alamat IP jaringan publik statis yang dirancang khusus untuk jaringan dinamis guna memenuhi permintaan pemecahan masalah yang cepat.
EIP adalah alamat IP publik yang dapat diterapkan secara mandiri. EIP ini mendukung pengikatan dan pelepasan dinamis. Anda dapat mengikatnya atau melepaskannya dari CVM (atau instans NAT Gateway) pada akun Anda. Kegunaan utamanya adalah:
- Untuk mempertahankan IP. Pencatatan nama domain ICP diperlukan untuk IP dan DNS Tiongkok daratan.
- Untuk menutupi kegagalan instans. Misalnya, nama DNS dipetakan ke alamat IP melalui pemetaan DNS dinamis. Mungkin diperlukan waktu hingga 24 jam untuk menyebarkan pemetaan ini ke seluruh Internet, sementara IP elastis memungkinkan pemetaan ulang IP dengan cepat dari satu CVM ke CVM lainnya. Ketika satu CVM gagal, Anda dapat memulai dan memetakan ulang instans lain untuk merespons kegagalan instans dengan cepat.

### Grup Keamanan
Grup keamanan adalah firewall virtual yang menampilkan pemfilteran paket data stateful. Firewall ini digunakan untuk mengonfigurasi kontrol akses jaringan CVM. Anda dapat menambahkan instans CVM dengan persyaratan isolasi keamanan jaringan yang sama di wilayah yang sama ke grup keamanan yang sama, untuk memfilter lalu lintas masuk dan keluar CVM melalui kebijakan jaringan grup keamanan.

### Metode Login
Kata sandi adalah kredensial login unik untuk instans CVM. Untuk memastikan keamanan instans, Tencent Cloud menyediakan dua metode login terenkripsi berikut:
- [Pasangan kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092) lebih mudah digunakan. Anda bisa login ke instans dari jarak jauh dengan beberapa langkah konfigurasi sederhana di konsol dan klien lokal Anda, dan tidak perlu memasukkan kata sandi saat login lagi.
- [Kata sandi login](https://intl.cloud.tencent.com/document/product/213/6093) memungkinkan siapa saja yang memiliki kata sandi untuk login ke instans CVM dari jarak jauh melalui alamat jaringan publik yang diizinkan oleh grup keamanan.

### Wilayah dan Zona Ketersediaan
Lokasi fisik tempat instans CVM dan sumber daya lainnya berada dan diluncurkan.
- Wilayah mengacu pada lokasi geografis tempat pusat data yang dihosting oleh Tencent Cloud berada. Setiap wilayah memiliki beberapa zona ketersediaan.
- Zona ketersediaan adalah Tencent Cloud IDC dengan catu daya dan jaringan independen di wilayah di atas. Zona ini dapat memastikan stabilitas bisnis, karena kegagalan di satu AZ diisolasi tanpa memengaruhi AZ lain di wilayah yang sama.



