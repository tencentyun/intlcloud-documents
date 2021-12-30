Tencent Cloud memberi Anda berbagai metode untuk mengakses Internet, seperti melalui alamat IP publik umum, EIP, NAT gateway, dan Cloud Load Balancer (CLB). 

## Alamat IP Publik Umum
Saat membuat instans CVM, Anda dapat menetapkan alamat IP publik umum ke instans. Sistem akan menetapkan alamat IP ke CVM Anda untuk memungkinkannya mengakses Internet serta dapat diakses melalui Internet. 
Alamat IP publik umum tidak dapat secara dinamis terikat atau tidak terikat dengan sumber daya seperti CVM, tetapi Anda dapat mengonversinya menjadi EIP. Untuk mengetahui detailnya, lihat [Mengonversi Alamat IP Publik menjadi EIP](https://intl.cloud.tencent.com/document/product/213/16586).

## Alamat IP Elastis
Tidak seperti alamat IP publik yang perlu diterapkan dan dirilis dengan CVM, alamat IP elastis (EIP) adalah sumber informasi cloud independen yang dipisahkan dari siklus pemakaian CVM dan dapat dioperasikan secara terpisah. 
Untuk informasi tentang cara mengajukan, mengikat, dan melepaskan EIP, lihat [EIP - Langkah](https://intl.cloud.tencent.com/document/product/213/16586). 
EIP menawarkan keuntungan sebagai berikut: 
- Sumber informasi cloud independen 
Anda dapat mengoperasikan EIP secara mandiri, tanpa perlu membelinya dengan CVM. 
- Pengikatan dan pemutusan ikatan elastis dengan sumber informasi 
EIP dapat terikat dan tidak terikat dengan CVM dan sumber daya lainnya kapan saja. 

## NAT Gateway
NAT Gateway menyediakan fitur SNAT dan DNAT, yang memungkinkan Anda membuat jalan keluar Internet dengan mudah dan menyediakan layanan untuk CVM di VPC untuk mengakses Internet dengan alamat IP publik yang sama. 
Untuk informasi tentang cara mengonfigurasi NAT gateway, lihat [NAT Gateway - Ikhtisar Operasi](https://intl.cloud.tencent.com/document/product/1015/30235).
NAT Gateway menawarkan keuntungan sebagai berikut: 
- Akses Internet yang aman 
NAT Gateway menyediakan fitur SNAT dan DNAT untuk menyembunyikan alamat IP CVM di VPC selama komunikasi Internet, memastikan keamanan. 
- Ketersediaan tinggi 
NAT Gateway menampilkan pencadangan panas master/slave, peralihan panas otomatis, dan penerusan cepat dengan kecepatan hingga 5 Gbps. Selain itu, mereka mendukung aplikasi Internet skala besar. 
- Konfigurasi fleksibel 
Anda dapat mengubah spesifikasi NAT gateway sesuai kebutuhan kapan saja. 

## Cloud Load Balancer
Cloud Load Balancer (CLB) mendistribusikan lalu lintas ke beberapa CVM untuk meningkatkan kemampuan layanan eksternal sistem aplikasi. Ini menghilangkan satu titik kegagalan untuk memastikan sistem aplikasi yang sangat tersedia.
Untuk informasi tentang cara membeli dan mengonfigurasi CLB, lihat [CLB - Memulai](https://intl.cloud.tencent.com/document/product/214/8975).
CLB menawarkan keuntungan sebagai berikut: 
- Kluster tunggal performa tinggi 
Sebuah kluster CLB terdiri dari beberapa server fisik, dengan ketersediaan hingga 99,95%. Sistem kluster dapat menghapus instans yang salah dan memilih instans yang sehat untuk memastikan layanan berjalan dengan benar di server sebenarnya.
- Keamanan dan stabilitas tinggi
Dengan sistem anti-DDoS BGP, CLB dapat bertahan terhadap sebagian besar serangan jaringan (seperti serangan DDoS) dan membersihkan serangan lalu lintas dalam hitungan detik, mencegah alamat IP yang diblokir atau konsumsi bandwidth penuh.

## Gateway Publik
Gateway Publik adalah CVM dengan fitur penerusan yang diaktifkan. Dalam VPC, CVM tanpa alamat IP publik dapat mengakses Internet melalui gateway publik pada subnet yang berbeda. Gateway publik dapat menyembunyikan alamat sumber lalu lintas Internet dari CVM lain ke alamat IP mereka sendiri.
Untuk informasi tentang cara mengonfigurasi gateway publik, lihat [Mengonfigurasi Gateway Publik](https://intl.cloud.tencent.com/document/product/215/33404).
