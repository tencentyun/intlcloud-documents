Subnet adalah ruang jaringan di VPC, yang membawa semua deployment sumber informasi cloud. VPC memiliki setidaknya satu subnet. Subnet akan dibuat bersama dengan VPC. Anda juga dapat membuat lebih banyak subnet di VPC sesuai dengan kebutuhan bisnis Anda.
Subnet khusus untuk zona ketersediaan. VPC memungkinkan subnet di zona ketersediaan yang berbeda, dan subnet ini dapat berkomunikasi satu sama lain melalui jaringan pribadi secara default. Dokumen ini memandu Anda melalui cara membuat subnet di VPC.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Subnet** di bilah sisi kiri untuk mengakses halaman pengelolaan.
3. Pilih wilayah dan VPC tempat subnet akan dibuat, lalu klik **+New** (+Baru)[](id:langkah3).
4. Konfigurasikan parameter subnet di kotak dialog pop-up.
    ![](https://main.qcloudimg.com/raw/fefbd7d65e21194d342728770f964a6b.png)
   + Jaringan: VPC tempat subnet berada. VPC yang dipilih di [langkah 3](#langkah3) akan ditampilkan secara otomatis. Atau, Anda dapat memilih VPC dari daftar pilihan.
   + Nama Subnet: masukkan nama subnet kustom dalam 60 karakter.
   + Rentang IP VPC: blok CIDR dari VPC yang dipilih akan ditampilkan secara otomatis.
   + CIDR: mengatur blok CIDR dari subnet, yang harus menjadi bagian dari blok CIDR VPC dan tidak boleh tumpang tindih dengan blok CIDR dari subnet lain yang ada di bawah VPC.
>? Rencanakan rentang IP subnet yang sesuai dengan skala bisnis Anda. Alamat IP pribadi dalam subnet yang ditentukan akan secara otomatis ditetapkan ke instans CVM yang Anda buat. IP pribadi utama CVM dapat dimodifikasi.Untuk informasi selengkapnya, lihat [Memodifikasi IP Pribadi Utama](https://intl.cloud.tencent.com/document/product/576/18541)
   + Zona Ketersediaan: pilih zona ketersediaan tempat subnet berada.
   + Tabel rute yang terhubung: pilih tabel rute yang akan dihubungkan. Subnet harus dihubungkan dengan tabel rute untuk mengontrol lalu lintas keluar. Tabel rute default VPC akan dihubungkan secara default untuk memastikan interkoneksi jaringan pribadi di VPC. Anda juga dapat memilih tabel rute lain di dalam VPC.
   + Tambahkan baris: klik **Add a line** (Tambahkan baris) untuk membuat beberapa subnet sekaligus. Klik ![](https://main.qcloudimg.com/raw/ae1ede733a45968e89f58c56aee3099f.png) untuk menghapus pengaturan subnet yang dipilih.
   + Opsi Lanjutan: Anda dapat secara opsional mengatur tag untuk subnet agar mengelola sumber informasi subnet dengan lebih baik. Klik **Add** (Tambahkan) untuk mengatur beberapa tag sekaligus. Anda dapat mengeklik ikon di kolom **Operation** (Operasi) untuk menghapus pengaturan tag yang dipilih.
5. Setelah konfigurasi selesai, klik **Create** (Buat). Kemudian subnet yang telah berhasil dibuat akan ditampilkan dalam daftar, seperti ditunjukkan gambar di bawah ini.
![](https://main.qcloudimg.com/raw/fe8df992288fce35a67b0bac6861c58b.png)

## Operasi Berikutnya
Setelah membuat subnet, Anda dapat men-deploy sumber informasi termasuk CVM dan CLB di dalamnya.
Klik ikon seperti ditunjukkan gambar di bawah ini untuk langsung membeli CVM di halaman pembelian CVM. Untuk informasi selengkapnya, lihat [Membangun VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
![](https://main.qcloudimg.com/raw/8fae00dfa94664159b9e98e283a2316f.png)
