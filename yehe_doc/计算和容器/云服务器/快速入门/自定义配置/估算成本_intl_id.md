Selain model CVM dan konfigurasi VPC Anda, faktor berikut juga memengaruhi biaya layanan Anda:
- Metode penagihan
- Sumber daya yang digunakan
- Kuantitas

### Metode penagihan
- **Pay as you go** (Bayar sesuai pemakaian) adalah metode penagihan fleksibel untuk instans CVM. Anda dapat meluncurkan/mengakhiri CVM kapan saja dan ditagih berdasarkan penggunaan CVM yang sebenarnya. Anda membayar per detik dan tidak diperlukan pembayaran di muka. Tagihan dibuat setiap jam. Metode penagihan ini cocok untuk kasus penggunaan seperti promo kilat e-commerce saat permintaan sumber daya sangat berfluktuasi.
- **Spot Instance** (Instans Spot) adalah cara baru untuk menggunakan dan membayar instans CVM. Mirip dengan Bayar sesuai pemakaian, Anda membayar Instans Spot per detik, setiap jam. Harga Instans Spot berfluktuasi sesuai dengan permintaan pasar. Anda mendapatkan diskon yang cukup besar saat permintaannya rendah (biasanya 10 hingga 20%). Namun, harganya mungkin diambil alih secara otomatis oleh sistem karena permintaannya tinggi.

### Sumber daya yang digunakan
- Wilayah:
	- Harganya sama untuk model instans yang sama di berbagai wilayah di Tiongkok Daratan.
	- Harga mungkin sama untuk model instans yang sama di berbagai wilayah di luar Tiongkok Daratan.
- Citra:
	- Citra publik: semua citra publik di Tiongkok Daratan yang dihosting oleh Tencent Cloud gratis. Citra Windows di luar Tiongkok Daratan memerlukan biaya lisensi.
	- Citra kustom: membuat citra kustom, mengimpor citra kustom, dan menyalin citra kustom di seluruh wilayah tidak dikenakan biaya.
	- Citra yang dibagikan: citra yang dibagikan dari pengguna Tencent Cloud lainnya tidak dikenakan biaya.
Jaringan:
	- VPC, Subnet, Tabel Rute, ACL Jaringan, Grup Keamanan, Gateway Direct Connect, VPN Tunnel, dan Gateway Pelanggan tidak dikenakan biaya.
	- Biaya bandwidth tidak berlaku untuk komunikasi antar-instans dalam subnet yang berbeda. Koneksi peering dalam wilayah juga tidak dikenakan biaya.
	- Lihat [artikel ini](https://intl.cloud.tencent.com/document/product/213/10578) untuk detail tentang metode penagihan jaringan publik.
	- Untuk detail tentang biaya untuk NAT Gateway, VPN Gateway, dan koneksi Peering Lintas wilayah.
- Penyimpanan:
	Untuk mengetahui harga disk lokal dan disk cloud, lihat [artikel ini](https://intl.cloud.tencent.com/document/product/362/2413)


### Kuantitas

Jumlah CVM yang Anda beli juga memengaruhi harga yang dibayar. Semakin banyak CVM berarti harganya semakin tinggi.
