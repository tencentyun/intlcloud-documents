
## Ikhtisar Konfigurasi

CDN Tencent Cloud mendukung konfigurasi batas kecepatan downstream untuk mengatur kecepatan throughput downstream maksimum melalui satu URL tunggal di server.
Konfigurasi batas kecepatan downstream dapat mengontrol bandwidth puncak CDN ke tingkat tertentu. Konfigurasi ini sering digunakan dalam skenario seperti promosi e-niaga dan rilis serta pembaruan versi game baru.

>! Setelah batas kecepatan downstream dikonfigurasi, pengalaman akses pengguna dan efek akselerasi CDN akan terpengaruh. Oleh karena itu, silakan gunakan dengan hati-hati.

## Panduan Konfigurasi

### Batasan konfigurasi

- Jumlah maksimum aturan batas kecepatan downstream: 10
- Satuan: KB/dtk; rentang nilai: 1-1.000.000 (hanya bilangan bulat)
- Jenis aturan yang didukung: semua konten, jenis file tertentu, folder tertentu, dan file tertentu. Pencocokan reguler saat ini tidak didukung.
- Aturan dijalankan dari bawah ke atas. Aturan di bagian bawah memiliki prioritas lebih tinggi.

### Petunjuk konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, lalu klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya. Pilih tab **Access Control** (Kontrol Akses) untuk menemukan konfigurasi batas kecepatan downstream, yang dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/c9ea85be753b60096b8088b048ac626a.png)
Klik **Add Speed Limit Rule** (Tambahkan Aturan Batas Kecepatan) untuk mengonfigurasi aturan:
![](https://main.qcloudimg.com/raw/02e033c829da553acc5eeb9bca864528.png)
Konfigurasi keseluruhan akan dinonaktifkan setelah aturan ditambahkan sehingga layanan yang sedang berjalan tidak akan terpengaruh:
![](https://main.qcloudimg.com/raw/e0006ace8527cc13c381666b22f21790.png)
Anda dapat mengaktifkan switch untuk men-deploy aturan batas kecepatan yang dikonfigurasi ke simpul di seluruh jaringan CDN:
![](https://main.qcloudimg.com/raw/4b9685cb889210accb67d11f1b389ae8.png)

## Sampel Konfigurasi

Konfigurasi batas kecepatan downstream `cloud.tencent.com` adalah sebagai berikut:
![](https://qcloudimg.tencent-cloud.cn/raw/814d50bbc8ca84e86bb5ac8c36dffc15.png)
Jika pengguna mengakses sumber daya `http://cloud.tencent.com/test.mp4`, server akan mengembalikan konten dengan kecepatan downstream yang dikonfigurasi sebesar 200 KB/dtk.
Jika pengguna mengakses sumber daya `http://cloud.tencent.com/test.flv`, server akan mengembalikan konten pada kecepatan downstream yang dikonfigurasi sebesar 400 KB/dtk.
