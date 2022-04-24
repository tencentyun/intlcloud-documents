Tencent Cloud menawarkan dua cara untuk membeli instans CVM: bayar sesuai pemakaian dan instans spot. Setiap metode disesuaikan untuk memenuhi kebutuhan pelanggan yang berbeda.
Tabel berikut membandingkan dua paket penagihan:

| Paket penagihan instans | Bayar sesuai pemakaian | Instans spot |
|---------|:---------:|:---------:|
| Metode pembayaran | [Deposit](https://intl.cloud.tencent.com/document/product/555/12039) setelah pembelian, dibebankan per jam | [Deposit](https://intl.cloud.tencent.com/document/product/555/12039) setelah pembelian, dibebankan per jam |
| Unit pembayaran | USD/detik | USD/detik |
| Harga satuan | Relatif lebih tinggi | Harga fluktuatif. Dalam kebanyakan kasus, harganya sekitar 10-20% dari harga instans bayar sesuai pemakaian dengan spesifikasi yang sama. |
| Waktu penggunaan minimal | Dikenakan biaya per detik dan ditagihkan per jam. Beli dan rilis kapan saja. | Dikenakan biaya per detik dan ditagihkan per jam. Beli dan rilis kapan saja. Dapat diambil alih oleh sistem. |
| Mengubah konfigurasi instans | Tidak terbatas. Ubah kapan saja. | Tidak didukung. |
| Kasus penggunaan | Terbaik untuk kasus penggunaan di mana permintaan bisnis sangat fluktuatif, seperti flash sale ecommerce. | Terbaik untuk kasus penggunaan seperti layanan online dan situs web yang menggunakan komputasi data besar dan load balancing. |


## Bayar Sesuai Pemakaian

Bayar sesuai pemakaian adalah paket penagihan fleksibel untuk instans CVM. Anda dapat mengaktifkan dan menghentikan instans CVM kapan saja. Anda hanya perlu membayar yang anda gunakan sampai hitungan waktu per detik dan tidak perlu pembayaran di muka. Sumber daya bayar sesuai pemakaian akan dibebankan pada jam tersebut. Paket penagihan ini cocok untuk kasus penggunaan di mana permintaan bisnis sangat fluktuatif, seperti flash sale ecommerce.

Saat mengaktifkan instans CVM bayar sesuai pemakaian, biaya satu jam (termasuk biaya untuk CPU, memori, dan disk data) akan dibekukan di saldo akun sebagai deposit. Biaya kemudian akan dibebankan per jam (waktu Beijing) untuk penggunaan selama satu jam terakhir. Saat membeli instans CVM, harga akan dicantumkan sebagai biaya per jam. Namun, Anda sebenarnya akan **billed by the second** (dibebankan per detik) dan biaya akan dibulatkan ke dua desimal terdekat. Penagihan dimulai dari saat instans dibuat dan berhenti saat instans dihentikan.

Saat instans CVM bayar sesuai pemakaian dibuat, biaya satu jam akan dibekukan di saldo akun sebagai deposit. Saat mengubah konfigurasi CVM, deposit saat ini akan dilepaskan dan deposit baru akan dibekukan berdasarkan harga satuan konfigurasi baru. Deposit akan dikembalikan ke akun saat instans CVM dihentikan.

Anda dapat mengaktifkan Tanpa Biaya Saat Pematian untuk instans bayar sesuai pemakaian untuk menghentikan penagihan biaya CPU dan memori setelah instans menjalankan pematian. Untuk batasan fitur ini, rujuk kepada [Tidak Ada Biaya Saat Pematian untuk Instans Bayar Sesuai Pemakaian](https://intl.cloud.tencent.com/document/product/213/19918). 

## Instans Spot

Instans spot adalah cara baru untuk menggunakan dan membayar instans CVM. Mirip dengan bayar sesuai pemakaian, instans ini memungkinkan biaya per detik dan penagihan per jam. Harga instans spot fluktuatif sesuai permintaan pasar yang memberikan diskon besar (diskon sekitar 80-90% dari harga instans bayar sesuai pemakaian dengan spesifikasi yang sama). Namun, instans spot dapat diambil alih secara otomatis oleh sistem karena kekurangan inventaris atau tawaran yang lebih tinggi dari pengguna lain.
- Untuk informasi selengkapnya tentang kebijakan instans spot, kasus penggunaan, dan batasan, rujuk kepada [Instans Spot](https://intl.cloud.tencent.com/document/product/213/17816).

