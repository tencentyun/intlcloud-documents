## Ikhtisar Jaringan
Tencent Cloud menawarkan [VPC](https://intl.cloud.tencent.com/document/product/215) (disarankan) dan lingkungan jaringan klasik. VPC adalah ruang jaringan yang terisolasi secara logis yang dapat dikustomisasi di Tencent Cloud. Mirip dengan jaringan tradisional yang dijalankan di IDC, VPC adalah tempat untuk mengelola sumber daya layanan Tencent Cloud Anda, seperti [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), dan [TencentDB](https://intl.cloud.tencent.com/document/product/236/5147).
Untuk perbedaan antara VPC dan jaringan klasik, lihat [VPC dan Jaringan Klasik](https://intl.cloud.tencent.com/document/product/215/35505).
Untuk operasi umum pada VPC dan subnet, lihat [Mengelola VPC dan Subnet](https://intl.cloud.tencent.com/document/product/215/31805).

## Konfigurasi Jaringan Redis
1. Login ke [Konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan klik **Create Instance** (Buat Instans) di daftar instans.
2. Di "Jenis Jaringan" pada halaman pembelian, Anda dapat memilih jaringan klasik atau **VPC** (disarankan).
![](https://main.qcloudimg.com/raw/8be0e67db61e588d2b8ec4bc43ef2c1f.png)

## Perubahan Jaringan Redis
>!Untuk memastikan ketersediaan layanan dan menjaga bisnis Anda tidak terganggu selama perubahan jaringan, segera perbarui alamat IP sesuai kebutuhan dan berhati-hatilah dalam merilis alamat IP lama.
>
1. Login ke [Konsol Redis](https://console.cloud.tencent.com/redis) dan klik ID instans di daftar instans untuk masuk ke halaman detail instans.
2. Dalam modul "Info Jaringan", Anda dapat melihat jaringan dan IP pribadi dari instans TencentDB for Redis saat ini. Anda juga dapat mengeklik **Change Network** (Ubah Jaringan) untuk mengubah dari jaringan klasik ke VPC atau dari VPC saat ini ke VPC lain.
![](https://main.qcloudimg.com/raw/882d495354b725a4fa0b4d9b6b513d29.png)
3. Pada kotak dialog pop-up, konfigurasikan informasi jaringan baru dan klik **OK** (OKE).
  - IP baru: Anda dapat memilih untuk menetapkan atau menentukan alamat secara otomatis.
  - IP Lama: Anda dapat memilih untuk merilisnya segera atau dalam beberapa hari guna memastikan kelangsungan bisnis selama perubahan jaringan.
![](https://main.qcloudimg.com/raw/1befc1f612813a27792cd811b7c2f8c1.png)

