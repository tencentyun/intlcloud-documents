
Anda dapat menggunakan satu VIP untuk mengakses instans TencentDB for Redis multi-AZ yang di-deploy dengan cara yang sama seperti cara Anda mengakses instans AZ tunggal yang di-deploy.

## Akses Lintas-AZ
VIP yang disediakan oleh instans TencentDB for Redis dapat diakses di seluruh wilayah. Jika Anda mengakses VIP yang sama di AZ yang berbeda di wilayah yang sama, Anda dapat mengakses instans yang sama.

Setelah failover node layanan Redis terjadi, proses layanan yang terkait dengan VIP akan diperbarui secara otomatis di latar belakang, sehingga Anda tidak perlu mengubah VIP.

## Melihat VIP Instans
Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis) dan lihat VIP instans di daftar instans.
![](https://main.qcloudimg.com/raw/3d4787cf07be40f20ca35a050e5424e0.png)
Atau, klik ID instans di daftar instans dan lihat VIP instans di halaman detail instans.
![](https://main.qcloudimg.com/raw/c470985bf8dc39e46f483849202901ba.png)

## Mengakses Instans Multi-AZ yang di-deploy 
Untuk informasi selengkapnya, silakan lihat [Menghubungkan ke Instans TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/9897).
