## Pesan Kesalahan

Para pengguna di wilayah yang berbeda menerima konten yang berbeda untuk URL sumber daya yang sama.

## Kemungkinan Penyebab

- Sebab 1:Kunci cache dikonfigurasikan ke **Filter All** (Filter Semua) untuk nama domain, dan server asal diatur untuk mengembalikan sumber daya yang berbeda sesuai dengan parameter.
Dalam hal ini, simpul yang berbeda mungkin meng-cache konten yang berbeda akibat parameter yang berbeda dalam permintaan akses yang pertama diterima.Jika permintaan yang sama mengakses simpul yang berbeda, konten yang dikembalikan akan berbeda.

- Sebab 2:Sumber daya yang diminta tidak dibersihkan setelah diperbarui di server asal.
CDN meng-cache sumber daya berdasarkan URL.Jika konten di server asal diperbarui, tetapi URL-nya tidak diubah, ketika seorang pengguna mengirim permintaan ke URL tersebut, konten yang di-cache sebelumnya pada simpul akan dikembalikan.Begitu pula, frekuensi akses bervariasi menurut wilayah sehingga validitas cache sumber daya mungkin berbeda di setiap wilayah.Ketika suatu permintaan pengguna mengakses simpul cache, jika sumber daya yang diminta di simpul tersebut sudah kedaluwarsa, permintaan tersebut akan diteruskan ke server asal, dan konten terbaru ditarik dan dikembalikan.Sebagian simpul memiliki konten terbaru, dan sebagian memiliki konten lama.

## Solusi

1.Jangan mengatur server asal untuk mengembalikan sumber daya yang berbeda sesuai dengan parameter URL jika menggunakan kunci cache "Filter All" (Filter Semua).
2.Bersihkan sumber daya URL setelah diperbarui di server asal.

## Prosedur Penanggulangan Masalah

Langkah 1.Periksa apakah server asal Anda mengembalikan sumber daya yang berbeda sesuai dengan parameter URL.
- Jika ya, silakan teruskan ke [Langkah 2](##step2).
- Jika tidak, silakan teruskan ke [Langkah 4](#step4).

[](id:step2)
Langkah 2.Masuk ke [konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di kanan nama domain untuk masuk ke halaman konfigurasinya.Buka tab **Cache Configuration** (Konfigurasi Cache) untuk mencari bagian **Cache Key Configuration** (Konfigurasi Kunci Cache), dan periksa apakah **String Abaikan Permintaan** dikonfigurasikan sebagai **Not Filter** (Bukan Filter).

- Jika tidak, silakan teruskan ke [Langkah 3](##step3).
- Jika ya, silakan teruskan ke [Langkah 4](#step4).



[](id:step3)
Langkah 3.Klik **Modify** (Ubah) di sebelah kanan aturan, centang **Not Filter** (Bukan Filter), dan klik **Save** (Simpan).

> ?Jika operasi ini tidak cocok untuk bisnis Anda, Anda bisa menggunakan fitur **Reserve Specified Parameter** (Sisihkan Parameter Tertentu) sesuai kebutuhan.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Kunci Cache](https://intl.cloud.tencent.com/document/product/228/35316).

[](id:step4)
Langkah 4.Klik **Purge and Prefetch** (Bersihkan dan Pramuat) di bilah samping kiri untuk membersihkan sumber daya yang diperbarui di server asal.

> ?Anda juga bisa mengikat API untuk pembersihan sumber daya sehingga sumber daya dapat segera dibersihkan di seluruh jaringan setelah diperbarui sehingga menjamin konsistensi konten yang akan diakses.Untuk informasi selengkapnya, silakan lihat [PurgeUrlsCache](https://intl.cloud.tencent.com/document/product/228/33601) dan [PurgePathCache](https://intl.cloud.tencent.com/document/product/228/33602).
