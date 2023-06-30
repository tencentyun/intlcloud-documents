### Bagaimana cara meningkatkan/menurunkan konfigurasi CVM?

Anda hanya dapat menyesuaikan konfigurasi instans **whose system disks and data disks are both cloud disks** (yang disk sistem dan disk datanya merupakan disk cloud). 
- Untuk informasi selengkapnya tentang cara meningkatkan/menurunkan konfigurasi instans, lihat [Mengubah Konfigurasi Instans](https://intl.cloud.tencent.com/document/product/213/2178).
- Untuk informasi selengkapnya tentang cara menyesuaikan bandwidth/konfigurasi jaringan, lihat [Menyesuaikan Konfigurasi Jaringan](https://intl.cloud.tencent.com/document/product/213/15517).

Jika penyesuaian konfigurasi Anda tidak berlaku, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi kami.

### Bagaimana cara memeriksa catatan penyesuaian konfigurasi?

1. Login ke [Konsol CloudAudit](https://console.cloud.tencent.com/cloudaudit).
2. Di halaman **Event history** (Riwayat peristiwa), atur filter seperti nama pengguna, jenis sumber daya, dan nama sumber daya sesuai kebutuhan untuk melihat daftar catatan.
Untuk informasi selengkapnya, lihat [Memulai](https://intl.cloud.tencent.com/document/product/1021/30338).

### Apakah saya bisa menyesuaikan konfigurasi instans CVM?
Ya. Anda bisa menyesuaikan konfigurasi instans yang disk sistem dan disk datanya merupakan disk cloud. Untuk instans berbasis pembayaran sesuai pemakaian, Anda dapat meningkatkan atau menurunkan konfigurasinya sebanyak yang diinginkan.

### Berapa kali maksimum saya dapat menurunkan konfigurasi CVM?
- Anda dapat meningkatkan atau menurunkan versi konfigurasi instans berbasis pembayaran sesuai pemakaian sebanyak yang Anda inginkan.

### Apakah saya bisa meningkatkan spesifikasi dan konfigurasi instans berbasis pembayaran sesuai pemakaian?

Ya. Anda bisa meningkatkan konfigurasi instans CVM berbasis pembayaran sesuai pemakaian dengan mengikuti petunjuk yang tercantum di [Mengubah Konfigurasi Instans](https://intl.cloud.tencent.com/document/product/213/2178) atau melalui API [ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239).

### Berapa lama waktu yang dibutuhkan untuk meningkatkan instans CVM?

Sekitar 1 sampai 2 menit.

### Bagaimana perhitungan biaya yang dikeluarkan untuk peningkatan instans CVM?

Anda dapat melihat detail biaya di [Pusat Tagihan](https://console.cloud.tencent.com/expense) setelah meningkatkan spesifikasi atau konfigurasi instans CVM.

### Apakah peningkatan instans CVM akan memengaruhi konfigurasi bisnis saya di instans?

Setelah meningkatkan instans CVM, Anda harus memulai ulang untuk memvalidasi konfigurasi baru. Operasi peningkatan akan mengganggu bisnis Anda selama waktu yang singkat. Sebaiknya Anda tingkatkan versi instans saat bisnis sedang lambat. Setelah ditingkatkan versinya, instans akan melanjutkan bisnis Anda dengan lancar dan tidak memerlukan konfigurasi ulang lingkungan.

### Mengapa perkiraan pengembalian dana untuk downgrade CVM 0?

Salah satu kemungkinan alasannya adalah Anda membeli instans dengan harga diskon tetapi konfigurasi yang diturunkan dihitung sesuai dengan harga asli instans. Jika harga instans yang dibeli dengan diskon lebih rendah dari atau sama dengan harga asli instans, perkiraan pengembalian dana akan ditampilkan sebagai 0.

### Mengapa peningkatan instans tidak berlaku?

Setelah meningkatkan instans, Anda harus memulai ulang di Konsol atau melalui API.


