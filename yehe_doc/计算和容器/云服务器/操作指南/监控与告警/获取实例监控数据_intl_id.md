## Ikhtisar

Tencent Cloud menyediakan fitur Cloud Monitor untuk semua pengguna secara default. Fitur ini membantu memantau dan mengumpulkan data dari produk Tencent Cloud yang Anda gunakan. Dokumen ini menjelaskan cara mendapatkan data pemantauan.

## Petunjuk
<dx-tabs>
::: Memperoleh data pemantauan dari konsol CVM
<dx-alert infotype="explain" title="">
Konsol CVM menyediakan halaman pemantauan, tempat Anda dapat melihat data pemantauan CPU, memori, bandwidth jaringan, dan disk dalam periode yang ditentukan.
</dx-alert>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di halaman pengelolaan instans, klik ID/Nama CVM untuk masuk ke halaman detailnya dan melihat data pemantauan.
3. Klik tab **Monitoring** (Pemantauan) untuk mendapatkan data pemantauan instans.
:::
::: Memperoleh data pemantauan dari konsol Cloud Monitor
<dx-alert infotype="explain" title="">
Konsol Cloud Monitor menyediakan data pemantauan semua produk Tencent Cloud. Di konsol, Anda dapat melihat data pemantauan CPU, memori, bandwidth jaringan, dan disk dalam periode yang ditentukan.
</dx-alert>
1. Login ke [Konsol Monitor Cloud](https://console.cloud.tencent.com/monitor/overview).
2. Pilih **Cloud Product Monitoring** (Cloud Product Monitoring) > **Cloud Virtual Machine** (Cloud Virtual Machine) di bilah sisi kiri.
3. Klik ID/Nama instans CVM untuk masuk ke halaman detailnya dan melihat data pemantauan.
:::
::: Memperoleh data pemantauan dari dasbor Cloud Monitor
Tentukan metrik CVM yang diperlukan dan buat dasbor, tempat Anda dapat melihat data pemantauan dalam bagan intuitif, yang membantu Anda menganalisis metrik melalui tren dan nilai luar biasa.
1. Login ke konsol Cloud Monitor, lalu pilih **dashboard** (dasbor) > [**Default Dashboard**] (Dasbor Default)(https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8).
2. Buat dasbor seperti yang diinstruksikan di [Buat Dasbor](https://intl.cloud.tencent.com/document/product/248/35282) dan dapatkan data pemantauan.
:::
::: Memperoleh data pemantauan melalui API
Anda dapat menggunakan `GetMonitorData` API untuk mendapatkan data pemantauan untuk semua produk Tencent Cloud. Untuk informasi selengkapnya, lihat [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/33881).
:::
</dx-tabs>
