Virtual Private Cloud (VPC) adalah dasar untuk menggunakan layanan Tencent Cloud. Saat membeli instans seperti CVM, CLB, atau TencentDB di wilayah yang belum memiliki VPC, VPC dan subnet default akan dibuat secara otomatis. 
![](https://main.qcloudimg.com/raw/98878feb887075f6535eca50a76d3d0c.png)
VPC dan subnet default dibuat bersama dengan instans Anda, dan tidak mengurangi kuota Anda di wilayah tersebut. Mereka bekerja sama seperti yang dibuat secara manual. Hanya ada satu VPC dan subnet default di setiap wilayah. Anda dapat menghapus VPC dan subnet default jika Anda tidak lagi membutuhkannya.
![](https://main.qcloudimg.com/raw/a67ac7a3ac09b41905e11925f11bfa51.png)
![](https://main.qcloudimg.com/raw/907d836a6fe2e41ec2dc6a9b2796ad3a.png)
Anda dapat merujuk ke dokumen ini untuk membuat instans VPC di konsol jika VPC default atau yang sudah ada tidak sesuai.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah di bagian atas halaman **VPC**, dan klik **+New** (+Baru).
3. Masukkan informasi VPC dan informasi subnet di pop-up **Create VPC** (Buat VPC).
>?Blok CIDR dari VPC dan subnet tidak dapat diubah setelah dibuat.
>
 - Blok CIDR VPC dapat berupa salah satu dari rentang IP berikut. Agar VPC dapat berkomunikasi satu sama lain melalui jaringan pribadi, blok CIDR-nya tidak boleh tumpang tindih.
    - `10.0.0.0` - `10.255.255.255` (rentang mask antara 16 hingga 28)
    - `172.16.0.0` - `172.31.255.255` (rentang mask antara 16 hingga 28)
    - `192.168.0.0` - `192.168.255.255` (rentang mask antara 16 hingga 28)
 - Blok CIDR subnet harus berada di dalam atau sama dengan blok CIDR VPC.
   Misalnya, jika rentang IP VPC adalah `10.0.0.0/16`, maka rentang IP subnetnya dapat berupa `10.0.0.0/16`, `10.0.0.0/24`, dll.
 - Zona ketersediaan: subnet khusus untuk zona ketersediaan. Pilih zona ketersediaan tempat subnet berada. VPC memungkinkan subnet di zona ketersediaan yang berbeda dan secara default subnet ini dapat berkomunikasi satu sama lain melalui jaringan pribadi.
 - Tabel rute yang terhubung: subnet harus dihubungkan dengan tabel rute untuk penerusan lalu lintas. Tabel rute default akan dikaitkan untuk memastikan interkoneksi jaringan pribadi di VPC.
 - Opsi lanjutan: Anda dapat menambahkan tag untuk mengelola izin sumber informasi sub-pengguna dan kolaborator dengan lebih baik.
4. Setelah konfigurasi selesai, klik **OK** (Oke). VPC yang berhasil dibuat akan ditampilkan dalam daftar, seperti yang ditampilkan di bawah ini. VPC baru memiliki subnet dan tabel rute default.
![](https://main.qcloudimg.com/raw/269317b3b2b8220fde33fd01e77be65e.png)

## Operasi Berikutnya
Setelah VPC dan subnet dibuat, Anda dapat men-deploy sumber informasi termasuk CVM dan CLB di dalam VPC.
Klik ikon seperti ditunjukkan gambar di bawah ini untuk langsung membeli CVM di halaman pembelian CVM. Untuk informasi selengkapnya, lihat [Membangun VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8374f8704f9ac1731ba84eb9d3570254.png)
