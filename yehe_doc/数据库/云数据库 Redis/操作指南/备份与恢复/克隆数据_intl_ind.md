## Skenario Operasi
TencentDB for Redis Edisi memori (tidak termasuk v2.8) mendukung klon instans, yaitu membuat instans lengkap berdasarkan file cadangan. Data instans sama dengan yang ada di file cadangan. Anda dapat menggunakan fitur kloning untuk menganalisis data sebelumnya. Anda juga dapat mengembalikan sebuah instans dengan cara menukar IP dari instans baru dan instans yang asli.

## Prasyarat
Data instans telah dicadangkan. Untuk petunjuk tentang pencadangan, silakan lihat [Mencadangkan Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman manajemen instans.
2. Pada halaman manajemen instans, pilih instans yang ingin Anda kloning dan klik **Clone Instance** (Kloning Instans).
![](https://main.qcloudimg.com/raw/e7a2efc796c7682829c9568b2f81fc32.png)
3. Pada halaman pembelian pop-up, tentukan informasi instans berdasarkan kebutuhan Anda dan klik **Buy Now** (Beli Sekarang).
4. Setelah selesai melakukan pembelian, Anda akan dialihkan ke daftar instans. Setelah status instans berubah menjadi **Running** (Berjalan), instans dapat digunakan secara normal.
>?Setelah instans dikloning, instans asli dapat dipertahankan atau dihentikan berdasarkan kebutuhan Anda.

