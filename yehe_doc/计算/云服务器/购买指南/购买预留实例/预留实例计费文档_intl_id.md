### Ikthisar

Penawaran Instans Cadangan adalah diskon penagihan yang diterapkan pada penggunaan instans CVM bayar sesuai pemakaian di akun Anda. RI secara otomatis berlaku untuk menjalankan instans bayar sesuai pemakaian dengan atribut yang cocok sehingga instans ini akan mendapatkan keuntungan dari diskon selama jangka waktu RI. Anda dapat membeli dan mengaktifkan RI untuk CVM yang ada atau membelinya bahkan sebelum membeli CVM. RI memberi Anda fleksibilitas dan penghematan yang signifikan dibandingkan dengan mode penagihan bayar sesuai pemakaian.

**Produk yang Didukung**

CVM

**Membeli RI**

- RI memungkinkan Anda memilih jenis CVM yang paling sesuai dengan kebutuhan dan anggaran. Anda dapat memilih jenis (model dan konfigurasi), metode pembayaran, wilayah, jangka waktu, dan jumlah RI Anda.

- Saat ini, Anda dapat membeli RI melalui TencentCloud API atau konsol. Untuk informasi selengkapnya, lihat [dokumentasi CVM](https://intl.cloud.tencent.com/document/product/213).

- RI tidak dapat dikembalikan.

**Jenis dan Harga Instans yang didukung RI**
Untuk informasi selengkapnya tentang konfigurasi, aturan pencocokan, dan harga jenis instans yang didukung RI, lihat [dokumentasi CVM](https://intl.cloud.tencent.com/document/product/213).
Untuk informasi selengkapnya tentang zona ketersediaan dan jenis instans yang didukung RI, lihat [Harga CVM](https://intl.cloud.tencent.com/pricing/cvm) atau API [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575). 
Untuk informasi selengkapnya, harap lihat [Aturan pencocokan RI](https://intl.cloud.tencent.com/document/product/213/37265) dan [Ikhtisar Instans Cadangan](https://intl.cloud.tencent.com/document/product/213/30571).
CVM mendukung RI. Untuk informasi selengkapnya tentang harga, lihat [Ikhtisar Harga Instans Cadangan CVM (Linux)](https://intl.cloud.tencent.com/document/product/213/30619). 

**Metode Pembayaran**

- Semua di Muka: Anda membayar seluruh jangka waktu RI dengan satu pembayaran di muka. Opsi ini memberi Anda diskon terbesar dibandingkan dengan dua opsi lain di bawah ini.

- Sebagian Di Muka: Anda melakukan sebagian pembayaran di muka kemudian membayar biaya instans dengan tarif bulanan atau tarif per jam yang didiskon selama jangka waktu RI.

- Tanpa Pembayaran Di Muka: Anda tidak melakukan pembayaran di muka kemudian membayar biaya instans dengan tarif bulanan atau tarif per jam yang didiskon selama jangka waktu RI.

Harap perhatikan bahwa Anda membayar seluruh jangka waktu RI terlepas dari penggunaan sebenarnya.

**Terms** (Jangka Waktu)

1 tahun

Misal Anda membeli CVM R1 berjangka waktu 1 tahun pada 25 Mei 2019 11:15:24, RI akan berlaku sejak 25 Mei 2019 11:00:00 hingga 25 Mei 2020 11:59:59.

Catatan: instans bayar sesuai pemakaian yang cocok terus berjalan saat RI kedaluwarsa, tetapi diskon penagihan berhenti.

**Aturan Penagihan**

- RI ditagih setiap jam (3.600 detik) selama jangka waktu yang dipilih. Misalnya, 10:00:00 hingga 10:59:59 adalah satu jam. Manfaat penagihan RI dapat diterapkan ke beberapa instans yang memenuhi syarat secara bersamaan hingga maksimum 3600 detik dalam satu jam. Perinciannya akan dijelaskan dalam tagihan Anda.

- RI ditagih setiap jam selama jangka waktu yang dipilih, terlepas dari apakah RI cocok dengan instans bayar sesuai pemakaian. Oleh karena itu, Anda sebaiknya memilih opsi pembayaran yang sesuai berdasarkan anggaran dan sumber daya Anda. RI berlaku pada jam sebelumnya dari waktu pembuatan dan kedaluwarsa pada jam berikutnya dari waktu kedaluwarsa. Misalnya, jika Anda membeli CVM RI jangka waktu 1 tahun pada 25 Mei 2019 11:15:24, penagihan RI dimulai sejak 25 Mei 2019 11:000:00, dan berakhir pada 25 Mei 2020 11:59: 59. Jika Anda sudah memiliki sumber daya CVM yang cocok pada saat pembelian, siklus penagihan RI pertama adalah 11:000:00-11:59:59, 25 Mei 2019, dan akan ditagihkan setiap jam.

**Diskon RI:**

Diskon penagihan diterima saat RI yang dibeli disesuaikan dengan instans yang didukung.
