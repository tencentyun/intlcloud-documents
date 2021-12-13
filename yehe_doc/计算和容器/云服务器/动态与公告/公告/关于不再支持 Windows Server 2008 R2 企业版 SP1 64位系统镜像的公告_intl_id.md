## Petunjuk Penggunaan
Microsoft secara resmi telah mengakhiri dukungan untuk Windows Server 2008 sejak 14 Januari 2020, dengan demikian, Tencent Cloud juga telah menonaktifkan citra publik Windows Server 2008 R2 Enterprise Edition SP1 64-bit pada 16 Maret 2020. Tencent CVM yang menggunakan citra ini tidak dapat lagi menerima pembaruan dan patch keamanan dari Microsoft, dan mungkin menghadapi risiko kompatibilitas, stabilitas, dan keamanan program.

Citra ini sekarang tidak dapat digunakan untuk membuat atau menginstal ulang instans CVM, tetapi Anda dapat terus menggunakan citra khusus, citra marketplace, atau mengimpor citra. Untuk memastikan keamanan dan stabilitas bisnis, Anda sebaiknya memigrasi instans Windows Server 2008 R2 Enterprise Edition SP1 64-bit CVM ke Windows Server 2012 atau versi yang lebih baru.

## Risiko
Karena Microsoft tidak lagi menyediakan pembaruan dan patch keamanan, masalah sistem operasi tidak dapat diselesaikan. Jika Anda bersikeras menggunakan sistem operasi Windows Server 2008 R2 Enterprise Edition SP1 64-bit, perhatikan risiko berikut:
1. Setelah 16 Maret 2020, Tencent CVM dengan sistem operasi Windows Server 2008 R2 Enterprise Edition SP1 64-bit tidak dapat lagi menerima pembaruan dan patch dari Microsoft. Penggunaan sistem operasi ini secara berkelanjutan dapat menimbulkan risiko terhadap aplikasi dan bisnis Anda, termasuk namun tidak terbatas pada inkompatibilitas aplikasi, ketidaksesuaian, dan kemungkinan masalah keamanan nonfungsional.
2. Jika terus menggunakan CVM dengan sistem operasi Windows Server 2008 setelah 16 Maret 2020, Tencent Cloud tidak akan bertanggung jawab atas kegagalan, masalah keamanan, inkompatibilitas, atau risiko lain dari sistem operasi karena kurangnya dukungan dari Microsoft. Anda akan bertanggung jawab atas semua konsekuensi yang timbul darinya.

## Petunjuk Layanan
Karena Microsoft tidak lagi menyediakan pembaruan dan patch keamanan untuk Windows Server 2008, Tencent Cloud tidak dapat menyelesaikan masalah sistem operasinya dan tidak bertanggung jawab atas kasus berikut:
1. Instans dengan sistem operasi Windows Server 2008 R2 Enterprise Edition SP1 64-bit mungkin mengalami kegagalan, masalah keamanan, inkompatibilitas, pengecualian operasi, atau bahkan sistem tidak berfungsi.
2. Jika aplikasi yang berjalan pada instans Windows Server 2008 R2 Enterprise Edition SP1 64-bit memiliki pengecualian dan memerlukan patch atau dukungan OS dari Microsoft, kami hanya dapat memberikan bantuan pemecahan masalah tetapi bukan solusi lengkap.
3. Karena kompatibilitas perangkat keras dan keterbatasan terkait driver, rilis baru Tencent Cloud CVM mungkin tidak dapat mendukung menjalankan image Windows Server 2008.

