
Jika Anda telah menetapkan `Tindakan` maupun `Sumber Daya` untuk membuat suatu kebijakan khusus, Anda dapat memanggil API untuk menjalankan operasi untuk sumber daya yang diinginkan.Dokumen ini menguraikan tautan di antara fitur-fitur konsol dan `Tindakan`.

>!
> - Tencent Cloud CDN dapat mengizinkan sumber daya berdasarkan nama domain.Otorisasi tidak membedakan antara wilayah layanan di dan di luar Tiongkok daratan dengan nama domain yang sama.
> - Jika Anda memindahkan layanan ECDN ke konsol CDN, kebijakan izin ECDN API secara otomatis akan ditautkan ke kebijakan izin CDN API yang sesuai.Namun, untuk kebijakan izin tingkat-sumber daya, Anda harus mengaturnya lagi di CDN setelah migrasi.

## Ikhtisar Layanan

Ikhtisar layanan dapat dikategorikan sebagai berikut berdasarkan konten yang ditampilkan:

| Fitur     | Tindakan yang Diotorisasi                             | Catatan                                            |
| ------------ | --------------------------------------- | ---------------------------------------------------- |
| Penggunaan layanan | DescribeCdnData<br/>DescribeBillingData | Jika tidak semua nama domain diberi izin, penggunaan setiap nama domain harus dikueri secara terpisah |
| Statistik nama domain | DescribeDomains                         | Total jumlah nama domain yang diizinkan yang akan dikembalikan                                 |
| Status tagihan     | DescribePayType                         | Izin untuk mengubah cara penagihan tidak dapat diberikan ke subakun saat ini                        |
| Statistik paket lalu lintas | DescribeTrafficPackages                 | Status paket lalu lintas adalah data tingkat-akun, dan semua sumber daya terkait bisa diminta       |

## Pengelolaan Nama Domain

| Fitur         | Tindakan yang Diotorisasi                                  | Catatan                                                     |
| ---------------- | -------------------------------------------- | ------------------------------------------------------------ |
| Daftar dan kueri nama domain   | DescribeDomains                              | Item konfigurasi dasar suatu nama domain bisa dikueri, ditampilkan, dan diunduh<br/> Untuk mendapatkan semua item konfigurasi yang terperinci, `DescribeDomainsConfig` harus diberi izin |
| Menambah nama domain         | DescribeDomains                              | Nama domain dapat ditambahkan di semua wilayah layanan akselerasi                                  |
| Menonaktifkan nama domain         | StopCdnDomain                                | -                                                            |
| Mengaktifkan nama domain         | StartCdnDomain                               | -                                                            |
| Menghapus nama domain         | DeleteCdnDomain                              | -                                                            |
| Mengubah proyek nama domain | UpdateDomainConfig                           | Proyek nama domain terdapat di konfigurasi nama domain<br/>Semua item konfigurasi suatu nama domain dapat diubah setelah otorisasi |
| Pengelolaan konfigurasi nama domain     | UpdateDomainConfig<br/>DescribeDomainsConfig | Semua item konfigurasi suatu nama domain dapat dilihat/diubah setelah otorisasi                               |

## Pengelolaan Sertifikat

| Fitur         | Tindakan yang Diotorisasi                                  | Catatan                                                     |
| ------------ | --------------------- | ------------------------ |
| Mengueri daftar sertifikat | DescribeDomainsConfig | Semua item konfigurasi suatu nama domain dapat dilihat setelah otorisasi |
| Konfigurasi sertifikat     | UpdateDomainConfig    | Semua item konfigurasi suatu nama domain dapat diubah setelah otorisasi |
| Mengonfigurasi sertifikat secara batch | UpdateDomainsHttps    | Ini digunakan untuk mengonfigurasi sertifikat secara batch         |

## Analisis Statistik

| Fitur                                                     | Tindakan yang Diotorisasi        | Catatan                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Mengueri data akses terperinci                                              | DescribeCdnData    | Semua metrik data akses suatu nama domain dapat dikueri setelah otorisasi |
| Mengueri data tarik-asal terperinci                                              | DescribeOriginData | Semua metrik data tarik-asal suatu nama domain dapat dikueri setelah otorisasi |
| Mengueri lalu lintas/permintaan teratas<br/>Mengueri nama domain teratas<br/>Mengueri peringkat kode status nama domain<br/>Mengueri peringkat penggunaan berdasarkan provinsi di Tiongkok daratan<br/>Mengueri peringkat penggunaan berdasarkan ISP di Tiongkok daratan<br/>Mengueri peringkat penggunaan di luar Tiongkok daratan | ListTopData        | Peringkat metrik dan dimensi data yang berbeda dapat dikueri setelah otorisasi  |
| Mengueri jumlah IP yang unik                                               | DescribeIpVisit    | -                                |

## Pembersihan dan Pramuat

| Fitur     | Tindakan yang Diotorisasi        |
| ------------ | ------------------ |
| Mengirim URL untuk pembersihan | PurgeUrlsCache     |
| Mengirim direktori untuk pembersihan | PurgePathCache     |
| Mengueri rekaman pembersihan | DescribePurgeTasks |
| Mengirim tugas pramuat | PushUrlsCache      |
| Mengueri rekaman pramuat | DescribePurgeTasks |

## Layanan Log

| Fitur       | Tindakan yang Diotorisasi           |
| ---------------- | --------------------- |
| Mengueri tautan unduh log | DescribeCdnDomainLogs |

## Ikhtisar Status Jaringan

Halaman pemantauan status seluruh jaringan pada konsol dapat dilihat oleh semua subakun tanpa perlu izin.

## Laporan Operasi

| Fitur                                                     | Tindakan yang Diotorisasi        | Catatan                         |
| ------------------------------------------------------------ | ------------------ | -------------------------------- |
| Mengueri data akses terperinci                                              | DescribeCdnData    | Semua metrik data akses suatu nama domain dapat dikueri setelah otorisasi |
| Mengueri data tarik-asal terperinci                                              | DescribeOriginData | Semua metrik data tarik-asal suatu nama domain dapat dikueri setelah otorisasi |
| Mengueri lalu lintas/permintaan teratas<br/>Mengueri nama domain teratas<br/>Mengueri peringkat kode status nama domain<br/>Mengueri peringkat penggunaan berdasarkan provinsi di Tiongkok daratan<br/>Mengueri peringkat penggunaan berdasarkan ISP di Tiongkok daratan<br/>Mengueri peringkat penggunaan di luar Tiongkok daratan | ListTopData        | Peringkat metrik dan dimensi data yang berbeda dapat dikueri setelah otorisasi  |
| Mengueri jumlah IP yang unik                                               | DescribeIpVisit    | -                                |

## Pengelolaan Paket Lalu Lintas

| Fitur       | Tindakan yang Diotorisasi             | Catatan                                           |
| -------------- | ----------------------- | -------------------------------------------------- |
| Mengueri daftar paket lalu lintas | DescribeTrafficPackages | Konten yang dikembalikan oleh API tidak sesuai dengan `Sumber Daya`.Daftar dapat diminta untuk sumber daya yang diberi izin |

> !Saat ini, logika pembaruan paket lalu lintas dan pembatalan pembaruan tidak dapat diberi izin.

## Kueri Kepemilikan IP

| Fitur                     | Tindakan yang Diotorisasi   | Catatan                                           |
| ---------------------------- | ------------- | -------------------------------------------------- |
| Mengueri apakah IP milik Tencent Cloud CDN | DescribeCdnIp | Konten yang dikembalikan oleh API tidak sesuai dengan `Sumber Daya`.Daftar dapat diminta untuk sumber daya yang diberi izin |

## Alat Diagnosis Mandiri

Saat ini, alat diagnosis mandiri tidak dapat diberi izin untuk subakun.
