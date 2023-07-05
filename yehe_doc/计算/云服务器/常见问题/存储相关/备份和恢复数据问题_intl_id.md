## Bagaimana cara mencadangkan data CVM?

- Jika CVM menggunakan disk cloud, Anda dapat mencadangkan data bisnis dengan membuat citra kustom disk sistem dan snapshot disk data. 
  - Untuk informasi selengkapnya tentang cara membuat citra kustom, lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
  - Untuk informasi selengkapnya tentang cara membuat snapshot, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755)
- Jika CVM menggunakan disk lokal, Anda dapat mencadangkan data pada disk sistem dengan membuat citra kustom. Untuk data bisnis di disk data Anda, Anda masih perlu menyesuaikan kebijakan pencadangan. 
  Anda dapat menggunakan FTP untuk mencadangkan data di server ke tempat lain. Untuk metode deployment FTP tertentu, lihat: 
  - Untuk Windows: [Membangun Layanan FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)
  - Untuk Linux: [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912) 

## Apa solusi pencadangan dan pemulihan data yang umum?

Solusi pencadangan dan pemulihan data berbeda-beda menurut skenario aplikasi dan bisnis. Rekomendasi berikut dapat digunakan berdasarkan kebutuhan Anda yang sebenarnya:
- Cadangkan instans secara berkala menggunakan fitur [CBS Snapshot](https://intl.cloud.tencent.com/document/product/362/5757).
- Deploy komponen utama aplikasi di beberapa zona ketersediaan, dan salin data sesuai kebutuhan.
- Gunakan [IP Publik Elastis](https://intl.cloud.tencent.com/document/product/213/5733) untuk pemetaan nama domain guna memastikan bahwa IP layanan dapat dengan cepat dialihkan ke instans CVM lain saat server tidak tersedia.
- Lihat data pemantauan secara teratur dan konfigurasikan alarm yang sesuai. Untuk informasi selengkapnya, lihat [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- Proses permintaan darurat dengan penskalaan otomatis. Untuk informasi selengkapnya, lihat [Penskalaan Otomatis](https://intl.cloud.tencent.com/document/product/377).
