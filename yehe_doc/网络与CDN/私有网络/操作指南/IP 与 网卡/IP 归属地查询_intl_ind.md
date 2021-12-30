Fitur kueri lokasi IP membantu Anda memperoleh informasi tentang lokasi geografis dan ISP dari alamat IP publik.
Misalnya, kueri menunjukkan bahwa alamat IP `123.123.123.123` berada di Beijing dan disediakan oleh China Unicom.
>?  
>- Saat ini, fitur kueri lokasi IP sedang dalam uji beta. Untuk mencobanya, harap ajukan kelayakan beta.
>- Fitur ini kini tersedia secara gratis, dan tidak menyediakan SLA. Fitur akan dikenakan biaya setelah komersialisasi.

## Kasus Penggunaan
- Anda dapat mengkueri lokasi dan ISP dari alamat IP CVM tujuan dan memilih CVM sumber agar terhubung. 
- Anda dapat mengkueri lokasi sebenarnya dari IP publik yang Anda beli dari Tencent Cloud atau platform cloud lainnya.

## Pembatasan
Saat ini, kueri lokasi IP hanya tersedia untuk alamat IPv4.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **IP and Interface** (IP dan Antarmuka) > **IP Location Query** (Kueri Lokasi IP) di bilah sisi kiri.
3. Masukkan alamat IP untuk kueri lalu klik <img src="https://main.qcloudimg.com/raw/38242f38a7e37d681899fe37dfbc6423.png" style="margin:-3px 0px">.
>? Anda juga dapat memanggil API [`DescribeIpGeolocationInfos`](https://intl.cloud.tencent.com/document/product/215/39094) atau [`DescribeIpGeolocationDatabaseUrl`](https://intl.cloud.tencent.com/document/product/215/38901) untuk mengkueri lokasi IP.

