### Apa itu ENI?

[Elastic Network Interface](https://intl.cloud.tencent.com/product/eni) (ENI) adalah antarmuka jaringan elastis yang terikat ke CVM dalam VPC, yang bisa dimigrasikan di antara beberapa CVM. ENI sangat berguna untuk mengonfigurasi jaringan manajemen dan membangun solusi jaringan yang sangat andal.

ENI memiliki atribut VPC, zona ketersediaan, dan subnet. Anda hanya bisa mengikatnya ke CVM di bawah zona ketersediaan yang sama. CVM bisa diikat dengan beberapa ENI, dan jumlah maksimal yang diizinkan berbeda-beda tergantung spesifikasi CVM.

### Apa pembatasan untuk menggunakan ENI pada CVM?

Untuk detailnya, lihat bagian batas penggunaan di [Ikhtisar Batas Penggunaan](https://intl.cloud.tencent.com/document/product/213/15379).

### Apa informasi dasar dari ENI?

Silakan lihat **Concepts** (Konsep) di [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514).

### Bagaimana cara membuat ENI?

Silakan lihat [Membuat ENI](https://intl.cloud.tencent.com/document/product/576/18534).

### Bagaimana cara melihat informasi ENI?

Silakan lihat [Melihat Informasi ENI](https://intl.cloud.tencent.com/document/product/576/18533).

### Bagaimana cara mengikat ENI ke instans CVM?

Silakan lihat [Mengikat dan Mengonfigurasi CVM](http://intl.cloud.tencent.com/document/product/576/18535).

### Bagaimana cara mengonfigurasi ENI di instans CVM?

Silakan lihat [Mengikat dan Mengonfigurasi CVM](http://intl.cloud.tencent.com/document/product/576/18535).

### Bagaimana cara mengubah atau menyesuaikan IP pribadi ENI?

CVM di VPC mendukung modifikasi dan penyesuaian IP pribadi ENI. Ikuti langkah-langkah di bawah ini:

1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Di bilah sisi kiri, klik **IP and Interface** (IP dan Antarmuka) > **ENI** untuk login ke halaman daftar ENI.
3. Klik **ID/Name** (ID/Nama) dari ENI untuk login ke halaman detailnya guna melihat informasinya.
4. Pilih tab **IPv4 address management** (Pengelolaan alamat IPv4) dan klik **Assign Private IP** (Tetapkan IP Pribadi).
5. Di jendela pop-up, pilih metode penetapan IP sebagai **Enter manually** (Masukkan secara manual) untuk memasukkan alamat IP yang ingin Anda ubah.
6. Klik **OK** untuk menyelesaikan proses.

Setelah modifikasi dilakukan di konsol, Anda juga perlu memodifikasi file konfigurasi ENI. Untuk informasi selengkapnya, lihat [Mengikat dan Mengonfigurasi CVM](https://intl.cloud.tencent.com/document/product/576/18535).
