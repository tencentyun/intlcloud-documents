## Skenario Operasi
Mengambil jaringan yang diperlukan dalam deployment CVM dengan akses Internet sebagai contoh, dokumen ini menjelaskan setiap langkah secara detail, mulai dari membuat VPC dan subnet, hingga membeli CVM, menetapkan alamat IP publik, dan terakhir menggunakan grup keamanan untuk mengontrol lalu lintas masuk dan keluar dari CVM.
![](https://main.qcloudimg.com/raw/82eefc24e8eeded09773ef7a5b6ab077.png)

## Prasyarat
1. Sebelum menggunakan produk Tencent Cloud, Anda perlu [mendaftarkan akun Tencent Cloud](https://intl.cloud.tencent.com/register).
2. Konfirmasi [wilayah dan zona ketersediaan](https://intl.cloud.tencent.com/document/product/215/31786) tempat VPC akan di-deploy berdasarkan kebutuhan bisnis Anda.
3. Pahami konfigurasi dasar dari dua jenis CVM Tencent Cloud: [Memulai CVM Linux](https://intl.cloud.tencent.com/document/product/213/2936) dan [Memulai CVM Windows](https://intl.cloud.tencent.com/document/product/213/2764).

## Langkah
### Langkah 1: (Opsional) Buat VPC dan subnet.
Anda dapat membuat VPC dan subnet kustom, atau Anda dapat melewati langkah ini dengan memilih agar sistem secara otomatis membuat VPC dan subnet default saat membeli CVM.
VPC mencakup setidaknya satu subnet. Saat VPC dibuat, sistem akan membuat subnet awal, dan sumber informasi layanan cloud hanya dapat ditambahkan di subnet.
Fitur VPC default sama dengan fitur VPC kustom yang Anda buat.

1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Setelah memilih wilayah VPC di bilah atas, klik **+New** (+Baru).
3. Masukkan informasi VPC dan informasi subnet awal, lalu klik **OK** (Oke). Jika Anda membutuhkan beberapa subnet, lihat [Membuat Subnet](https://intl.cloud.tencent.com/document/product/215/31806#.E5.88.9B.E5.BB.BA.E5.AD.90.E7.BD.91).

>Blok CIDR (rentang IP) dari instans dan subnet VPC tidak dapat diubah setelah dibuat. Dengan demikian, selesaikan [perencanaan jaringan](https://intl.cloud.tencent.com/document/product/215/31795) terlebih dahulu.

### Langkah 2: beli CVM.
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm).
2. Klik **Create** (Buat) di sudut kiri atas halaman daftar untuk membuka halaman pembelian CVM.
3. Untuk informasi tentang konfigurasi CVM, lihat [Konfigurasi Kustom untuk CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517) dan [Konfigurasi Kustom untuk CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).
4. Pilih VPC dan subnet. Ada dua metode pemilihan:
- **Using custom VPC and subnet** (Menggunakan VPC dan subnet kustom)
Di **1. Select the region and model** (1. Pilih wilayah dan model) di **Custom Configuration** (Konfigurasi Kustom), Anda dapat memilih VPC dan subnet yang dibuat pada Langkah 1 di opsi **Network** (Jaringan), dan CVM akan dibuat di VPC dan subnet kustom.

- **Using default VPC and subnet** (Menggunakan VPC dan subnet default)
Di **1. Select the region and model** (1. Pilih wilayah dan model) di **Custom Configuration** (Konfigurasi Kustom), Anda dapat memilih VPC default (Default-VPC) dan subnet (Default-subnet) di opsi **Network** (Jaringan), dan CVM akan dibuat di VPC dan subnet default.


>Kami merekomendasikan Anda menetapkan alamat IP publik gratis saat membeli CVM. Jika tidak ada alamat IP publik yang ditetapkan selama pembelian, Anda dapat mengikat CVM ke alamat IP publik elastis di Konsol CVM.

### Langkah 3: konfigurasikan grup keamanan.
Saat membeli CVM, Anda dapat memilih grup keamanan default (Default) sistem. Grup keamanan ini mengizinkan semua lalu lintas secara default. Anda dapat mengatur aturan grup keamanan berdasarkan kebutuhan Anda.
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm).
2. Klik **Security Group** (Grup Keamanan) di bilah sisi kiri untuk membuka halaman manajemen.
3. Temukan grup keamanan default dalam daftar dan klik **Modify Rules** (Modifikasi Aturan).
4. Modifikasi aturan masuk dan keluar grup keamanan di halaman ini.

Untuk informasi selengkapnya tentang mengonfigurasi aturan grup keamanan, lihat [Membuat Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35506) dan [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35519).

### Langkah 4: konfigurasikan tabel rute.
Setelah selesai mengonfigurasi CVM dan grup keamanan, Anda perlu mengonfigurasi tabel rute yang terhubung dengan subnet.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Route Tables** (Tabel Rute) di bilah sisi kiri untuk membuka halaman manajemen.
3. Temukan tabel rute default VPC default dalam daftar dan klik ID-nya untuk membuka halaman detail.
4. Klik **+Add Routing Policy** (+Tambahkan Kebijakan Perutean) di **Routing Policy** (Kebijakan Perutean).
5. Masukkan rentang alamat IP tujuan Anda untuk mengakses Internet dan pilih **CVM's Public IP** (IP Publik CVM) untuk jenis hop selanjutnya. Ini menunjukkan bahwa saat CVM di subnet yang terikat dengan tabel rute ini mengakses rentang alamat IP ini, mereka akan selalu menggunakan alamat IP publik CVM.

>Anda dapat membeli NAT gateway untuk menyediakan akses Internet ke CVM tanpa alamat IP publik. Untuk informasi selengkapnya, lihat [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015).
