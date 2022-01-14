## Menerapkan HA di Beberapa AZ
Instance CLB mendukung pemulihan bencana di seluruh zona ketersediaan.Misalnya, beberapa kluster dapat di-deploy di dua zona ketersediaan di wilayah yang sama:Zona 1 Hong Kong (Tiongkok) dan Zona 2 Hong Kong (Tiongkok).Hal ini mendukung tercapainya pemulihan bencana seluruh zona ketersediaan di wilayah yang sama.Dengan fitur ini, instance CLB dapat meneruskan lalu lintas akses frontend ke zona ketersediaan lainnya di wilayah yang sama dalam 10 detik apabila seluruh zona ketersediaannya gagal sehingga memulihkan kemampuan layanan.

## Pertanyaan Umum dan Kasus Penggunaan
#### Pertanyaan 1:Apabila instance CLB `test1` dikonfigurasi untuk Zona 1 dan Zona 2 Hong Kong (Tiongkok), apa kebijakan untuk lalu lintas jaringan publik masuk klien?
Zona 1 dan Zona 2 Hong Kong (Tiongkok) mempunyai sepasang kumpulan sumber daya IP, yang dapat dianggap sebagai sumber daya IP dengan kemampuan penyeimbangan beban yang setara.Developer tidak perlu menentukan antara kluster master dan kluster slave.Ketika developer membeli instance CLB dan mengikatnya ke CVM, dua set peraturan akan dibuat dan dituliskan ke dalam dua kluster tersebut sehingga memberikan ketersediaan yang tinggi.

#### Pertanyaan 2:Misalkan instance CLB test1 dikonfigurasikan untuk Zona 1 dan 2 Hong Kong (Tiongkok), dan diikat ke 100 server asli di setiap zona ketersediaan.Selama operasi bisnis, 1 juta koneksi persisten HTTP (dengan tetap mengaktifkan koneksi TCP) akan tersambung di setiap zona.Apabila seluruh kluster CLB di Zona 1 gagal dan menjadi tidak tersedia, apa yang akan terjadi pada bisnis?
Ketika instance CLB di Zona 1 Hong Kong (Tiongkok) gagal, semua koneksi persistent pada saat itu akan ditutup, sementara koneksi non-persisten tidak akan terpengaruh.Arsitektur pemulihan bencana akan secara otomatis mengikat 100 server di setiap zona ke instance CLB di Zona 2 Hong Kong (Tiongkok) dalam 10 detik sehingga segera memulihkan kemampuan bisnis tanpa memerlukan intervensi manual.

#### Pertanyaan 3:Jenis CLB mana yang kompatibel dengan pemulihan bencana multi-AZ?Apakah dikenakan biaya tambahan?
Pemulihan bencana multi-AZ tersedia secara gratis.Fitur ini tersedia untuk instance CLB jaringan publik dan jaringan pribadi, kecuali instance CLB jaringan pribadi yang dibuat di Guangzhou sebelum 29 April 2020, di Shanghai sebelum 19 Desember 2019, dan di Beijing sebelum 18 Desember 2019.

