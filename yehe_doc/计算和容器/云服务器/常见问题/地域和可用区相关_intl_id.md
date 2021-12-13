### Bagaimana cara melihat wilayah dan zona ketersediaan?

Untuk melihat wilayah dan zona ketersediaan, coba langkah-langkah berikut:
- Lihat dokumen [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091).
- Gunakan API untuk menanyakan wilayah dan zona ketersediaan.
 - Untuk melihat wilayah, gunakan [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708) API.
 - Untuk melihat zona ketersediaan, gunakan [DescribeZones](https://intl.cloud.tencent.com/document/product/213/35071) API.


### Wilayah CVM dan zona ketersediaan apa yang tersedia dan bagaimana memilihnya?

Untuk informasi selengkapnya tentang wilayah CVM yang tersedia dan zona ketersediaan, lihat [Wilayah dan Zona Ketersediaan](http://intl.cloud.tencent.com/document/product/213/6091).
Untuk informasi selengkapnya tentang cara memilih wilayah dan zona ketersediaan, lihat [Cara Memilih Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091#.E5.A6.82.E4.BD.95.E9.80.89.E6.8B.A9.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.8F.AF.E7.94.A8.E5.8C.BA).


### Dapatkah saya mengubah wilayah CVM yang dibeli?

Tidak. Anda tidak dapat mengubah wilayah CVM yang dibeli. Jika Anda perlu men-deploy CVM yang sudah ada ke wilayah atau zona ketersediaan lain, coba langkah berikut:
- [Hentikan instans](https://intl.cloud.tencent.com/document/product/213/4930) lalu beli yang baru.

- Buat citra kustom untuk instans asli. Kemudian, gunakan citra kustom untuk membuat instans, luncurkan, dan perbarui konfigurasinya di zona ketersediaan baru.
  1. Buat citra kustom untuk instans saat ini. Untuk informasi selengkapnya, lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
  2. Jika [lingkungan jaringan](https://intl.cloud.tencent.com/document/product/213/5227) instans saat ini adalah VPC dan Anda perlu mempertahankan alamat IP pribadi setelah migrasi, hapus subnet di zona ketersediaan saat ini, lalu buat subnet di zona ketersediaan baru dengan rentang alamat IP yang sama dengan subnet asli.
  > Jika subnet yang akan dihapus berisi instans yang tersedia, migrasikan semua instans di subnet ke subnet baru terlebih dahulu.
  >
  3. Gunakan citra kustom yang baru dibuat untuk membuat instans baru di zona ketersediaan baru.
  Anda dapat memilih jenis dan konfigurasi instans yang sama dengan instans asli, atau mengonfigurasi yang baru untuk instans baru. Untuk informasi selengkapnya, lihat [Membuat Instans](https://intl.cloud.tencent.com/document/product/213/4855).
  4. Jika alamat IP publik elastis dikaitkan dengan instans asli, maka pisahkan dari instans asli dan kaitkan dengan instans baru. Untuk informasi selengkapnya, lihat [Alamat IP Elastis (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).
  5. (Opsional) Jika [mode penetapan harga](https://intl.cloud.tencent.com/document/product/213/2180) instans asli adalah bayar sesuai pemakaian, Anda dapat menghentikannya. Untuk informasi selengkapnya, lihat [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).

### Dapatkah pengguna Tencent Cloud di Tiongkok menikmati kualitas produk dan layanan yang sama untuk sumber daya yang dibeli di Tiongkok dan wilayah atau negara lain?
Ya. Tencent Cloud China Console memberikan kualitas produk dan layanan yang sama kepada semua pengguna. Wilayah pembelian tidak akan memengaruhi hak pengguna Anda di konsol.

### Dapatkah saya menggunakan fitur replikasi citra kustom untuk memigrasikan CVM di Daratan Tiongkok ke negara atau wilayah lain?
- Tidak. Citra hanya dapat direplikasi di negara atau wilayah yang sama. Untuk mereplikasi citra antar negara, [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) untuk mendaftar.

### Apa perbedaan antara instans di dalam dan di luar Daratan Tiongkok, dan bagaimana cara menentukan wilayah mana yang paling cocok untuk saya?
Instans di negara atau wilayah lain diterapkan di luar Daratan Tiongkok, memberikan keuntungan geografis dan pasar bagi pengguna global. Jaringan lokal yang cepat juga dapat memenuhi kebutuhan pelanggan internasional, yang cocok untuk pengguna yang menjalankan bisnis di negara atau wilayah lain.

- Untuk informasi selengkapnya tentang wilayah yang didukung, lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091).

### Dapatkah saya mengubah antara sistem operasi Linux dan Windows untuk instans CVM yang dibeli di luar wilayah Daratan Tiongkok?
Tidak. Beralih OS antara Windows dan Linux hanya tersedia untuk instans CVM di Daratan Tiongkok.

### Bagaimana cara mengajukan layanan purna jual untuk produk yang dibeli di luar wilayah Daratan Tiongkok?
Jika Anda membeli produk di situs web resmi Tencent Cloud, hubungi hotline layanan Tencent Cloud 24/7 (4009100100) atau [kirim tiket](https://console.cloud.tencent.com/workorder/category).

### Bagaimana cara menerapkan instans CVM di luar wilayah Daratan Tiongkok?
Instans CVM di luar wilayah Tiongkok memiliki metode deployment yang sama jika mereka memiliki jenis sistem operasi yang sama.

### Dapatkah saya memigrasikan instans ke wilayah di luar Daratan Tiongkok?
Wilayah dan zona ketersediaan instans tidak dapat diubah. Untuk menggunakan instans di negara atau wilayah lain, Anda perlu membeli instans lain.

### Mengapa beberapa jenis instans hanya dapat dibeli di wilayah Tiongkok?
Beberapa wilayah mungkin tidak mendukung jenis instans tertentu. Untuk informasi tentang jenis instans yang didukung, buka [halaman pembelian CVM](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.78908498.770173325.1571651505) untuk melihat informasi pembelian instans.

### Jika saya membuat situs web menggunakan instans CVM dari wilayah di luar Daratan Tiongkok dan pengguna saya mengakses situs web melalui nama domain, apakah nama domain ini memerlukan pengajuan ICP?
Untuk situs web di wilayah Daratan Tiongkok, pengajuan ICP diperlukan untuk nama domain. Untuk situs web di negara atau wilayah lain, pengajuan ICP tidak diperlukan. 

### Apakah instans di berbagai wilayah memiliki harga yang sama?
Harga instans CVM mencakup spesifikasi, penyimpanan, bandwidth jaringan, dll. Harga komponen ini berbeda-beda tergantung wilayahnya, sehingga harga instans akan berbeda.
Untuk informasi selengkapnya tentang harga, lihat [Harga](https://buy.cloud.tencent.com/price/cvm/calculator).
