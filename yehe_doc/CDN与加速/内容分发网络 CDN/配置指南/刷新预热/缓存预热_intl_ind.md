## Ikhtisar Fitur

Setelah nama domain terhubung ke layanan CDN, nama domain tersebut awalnya tidak memiliki sumber daya pada simpul cache CDN di seluruh jaringan.Sumber daya akan di-cache setelah dipicu oleh permintaan pengguna.Jika sumber daya yang diminta kedaluwarsa atau tidak di-cache pada simpul cache, simpul perantara CDN akan ditarik untuk sumber daya tersebut.Jika sumber daya tersebut kedaluwarsa atau tidak di-cache pada simpul perantara, server asal pengguna akan ditarik.

Fitur pramuat CDN memungkinkan Anda mengirimkan daftar sumber daya untuk memuat sumber daya ke simpul cache tanpa permintaan pengguna.

- Ketika sebuah simpul memuat sumber daya, jika ada sumber daya yang valid (tidak kedaluwarsa) dengan nama yang sama sudah di-cache pada simpul, sumber daya tersebut tidak akan dimuat.Kami sarankan Anda untuk membersihkan sumber daya sepenuhnya di seluruh jaringan sebelum Anda memperbarui sumber daya apa pun dengan nama yang sama.
- Simpul memuat sumber daya dari server asal, yang bandwidth-nya akan meningkat setelah sejumlah besar tugas pramuat dikirimkan.
- Layanan nama domain akselerasi di-deploy dalam mekanisme akselerasi lapisan ganda secara default.Melakukan pramuat pada sumber daya di Tiongkok Daratan, sumber daya dimuat ke simpul perantara di dalam Tiongkok Daratan secara default, sementara melakukan pramuat pada sumber daya di wilayah di luar Tiongkok Daratan, sumber daya dimuat ke server edge di luar Tiongkok Daratan secara default.

> Catatan:
>
> Melakukan pramuat pada sumber daya di wilayah di luar Tiongkok Daratan, sumber daya dimuat ke server edge di luar Tiongkok Daratan secara default, dan lalu lintas yang terjadi pada lapisan edge dikenai biaya.

## Kasus Penggunaan

### Rilis paket instalasi

Sebelum merilis edisi baru atau pembaruan paket instalasi, Anda dapat melakukan pramuat pada sumber daya terlebih dahulu ke simpul cache CDN.Setelah paket dirilis secara resmi, permintaan unduhan besar-besaran dari pengguna akan diambil alih oleh simpul cache CDN, meningkatkan kecepatan unduhan dan mengurangi tekanan pada server asal.

### Peristiwa pemasaran

Sebelum memulai peristiwa pemasaran apa pun, Anda dapat melakukan pramuat pada sumber daya statis web terkait ke simpul cache CDN.Setelah peristiwa dimulai secara resmi, semua sumber daya statis web yang diminta akan dikembalikan dari simpul cache CDN, menjamin ketersediaan layanan untuk pengalaman pengguna yang lebih baik melalui cadangan bandwidth yang melimpah.

## Panduan Pengoperasian

### Cara penggunaan

1.Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), klik **Purge and Pramuat** (Pembersihan dan Pramuat) di bilah samping kiri, buka tab **Pramuat URL** (Bersihkan URL) untuk mengumpulkan tugas pembersihan.
2.Anda dapat menentukan wilayah target untuk melakukan pramuat pada sumber daya.
- Untuk nama domain akselerasi di Tiongkok Daratan, hanya **Chinese Mainland** (Tiongkok Daratan) yang dapat ditentukan untuk akselerasi.
- Untuk nama domain akselerasi di luar Tiongkok Daratan, hanya **Overseas** (Luar Negeri) (yaitu, wilayah di luar Tiongkok Daratan) yang dapat ditentukan untuk akselerasi.
- Untuk nama domain akselerasi global, **Global**, **Chinese Mainland** (Tiongkok Daratan), dan **Overseas** (Luar Negeri) (yaitu, wilayah di luar Tiongkok Daratan) dapat ditentukan untuk akselerasi.


![](https://main.qcloudimg.com/raw/410621be989e1f0f65c46fd907b6dc6a.png)


3.Di tab **History** (Riwayat), Anda dapat membuat kueri tugas pramuat berdasarkan periode waktu dan istilah tertentu.Kueri istilah hanya mendukung kueri dengan nama domain atau URL lengkap:
![](https://main.qcloudimg.com/raw/5f4d32e7d79a1a8d0a6390e8fecbc0ec.png)

### Tindakan pencegahan

#### Batas pramuat

- Hingga 1.000 URL dapat dipramuat per hari untuk setiap akun di setiap wilayah akselerasi, dan hingga 20 URL dapat dipramuat sekaligus.Setelah tugas pramuat global dilakukan, kuota untuk wilayah di dalam dan di luar Tiongkok Daratan akan digunakan secara bersamaan.
- Anda perlu menambahkan pengidentifikasi protokol `http://` atau `https://` saat mengirimkan tugas pramuat.
- URL dalam format `http://*.test.com` tidak dapat dipramuat.
- URL yang berisi karakter bahasa Mandarin tidak dapat dipramuat.


#### Konfigurasi izin subpengguna

- Pramuat URL dan kueri riwayat pramuat telah diintegrasikan ke sistem izin terbaru dan mendukung konfigurasi izin di tingkat sumber daya (nama domain).
- Untuk metode penetapan izin, silakan lihat [Izin Konsol](https://intl.cloud.tencent.com/document/product/228/35229).



