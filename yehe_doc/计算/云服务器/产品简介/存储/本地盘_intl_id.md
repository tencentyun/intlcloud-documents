## Ikhtisar
Disk lokal adalah perangkat penyimpanan di server fisik yang sama dengan instans CVM. Ini fitur IO baca/tulis tinggi dan latensi rendah.
Disk lokal adalah perangkat penyimpanan lokal di server fisik yang sama dengan instans CVM. Ini adalah ruang penyimpanan yang dicadangkan di server fisik (saat ini hanya tersedia untuk IO tinggi dan CVM big data). Keandalan data yang disimpan pada disk lokal bergantung pada server fisik. Mungkin ada satu titik kegagalan.



>! 
> - Jika terjadi kegagalan perangkat keras pada server fisik instans CVM, disk lokal mungkin kehilangan data berharga. Kami merekomendasikan redundansi data pada lapisan aplikasi untuk memastikan keandalan. Jika aplikasi Anda tidak mendukung ini, pertimbangkan untuk menggunakan [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) untuk meningkatkan keandalan data.
> - Anda tidak dapat mengupgrade perangkat keras (CPU, memori, penyimpanan) dari instans CVM hanya dengan disk lokal. Anda hanya dapat mengupgrade bandwidth-nya.
> 

## Skenario
- **Aplikasi intensif IO**: untuk database relasional besar, NoSQL, ElasticSearch, dan aplikasi intensif I/O lainnya yang lebih sensitif terhadap latensi, Anda dapat menggunakan disk lokal NVME SSD yang dilengkapi dengan IO CVM tinggi, tetapi gunakan perhatikan bahwa itu membawa risiko satu titik kegagalan.
- **Aplikasi big data**: untuk aplikasi big data seperti EMR yang kurang sensitif terhadap latensi dan menampilkan redundansi data di lapisan atas untuk mentolerir satu titik kegagalan, Anda dapat menggunakan disk HDD SATA yang disertakan dengan big data CVM.


## Siklus pemakaian
Siklus pemakaian disk lokal sama dengan siklus pemakaian instans CVM tempat disk tersebut dipasang. Oleh karena itu, disk lokal diluncurkan dan diakhiri dengan instans CVM.

## Jenis

Disk lokal adalah perangkat penyimpanan lokal di server fisik yang sama dengan instans CVM. Ada dua jenis disk lokal berdasarkan media: HDD SATA dan SSD NVME.

| CVM | Spesifikasi dan Performa |
|---------|---------|
| Disk lokal HDD SATA | [CVM big data](https://intl.cloud.tencent.com/document/product/213/11518#D) |
| Disk lokal SSD NVME | [CVM IO Tinggi](https://intl.cloud.tencent.com/document/product/213/11518#I) |

## Pembelian
Disk lokal hanya dapat dibeli bersama dengan instans CVM. Untuk informasi selengkapnya tentang membeli instans CVM, lihat [Membuat Instans](https://intl.cloud.tencent.com/document/product/213/4855).

