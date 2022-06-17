[](id:que1) 

### Mekanisme autentikasi apa yang didukung SES?
SES mendukung semua mekanisme autentikasi standar industri, termasuk DomainKeys Identified Mail (DKIM), Sender Policy Framework (SPF), dan Domain-Based Message Authentication, Reporting and Conformance (DMARC).

[](id:que2) 
### Bagaimana cara mengonfigurasi domain pengirim?
<dx-tabs>
::: Langkah 1. Konfigurasi di halaman DNS
1. Pada halaman konfigurasi [Domain Pengirim](https://console.cloud.tencent.com/ses/domain), klik **Create** (Buat), masukkan nama domain, lalu kirim.
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. Konfigurasikan informasi verifikasi di [konsol DNSPod](https://console.cloud.tencent.com/cns).
3. [](id:step2)Kembali ke halaman konfigurasi [Domain Pengirim](https://console.cloud.tencent.com/ses/domain) dan klik **Verify** (Verifikasi).
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
4. Klik alamat domain pengirim untuk masuk ke halaman detail konfigurasi, tempat Anda dapat melihat nilai domain.
5. Tempel alamat domain pengirim di [langkah 3](#step3) ke halaman [DNSPod](https://console.cloud.tencent.com/cns) untuk menambahkan catatan. Pastikan untuk menghindari penggunaan spasi.
 - Autentikasi DKIM:
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - Autentikasi SPF:
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - Catatan _dmarc:
Masukkan `v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;` sebagai nilai catatan.
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
 <dx-alert infotype="explain"> `xxx@163.com` hanya sebagai contoh. Di sini, Anda perlu mengganti contoh dengan alamat pengirim Anda.</dx-alert>
6. Kembali ke halaman detail konfigurasi [Domain Pengirim](https://console.cloud.tencent.com/ses/domain) dan klik **Submit** (Kirim).
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: Langkah 2. Verifikasi hasilnya
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: Tambahan: ketika domain pengirim adalah domain tingkat ketiga
1. Pada halaman konfigurasi [Domain Pengirim](https://console.cloud.tencent.com/ses/domain), klik **Create** (Buat), masukkan nama domain, lalu kirim.
2. Konfigurasikan informasi verifikasi di [konsol DNSPod](https://console.cloud.tencent.com/cns).
:::
</dx-tabs>

>?
>- Setelah konfigurasi dan verifikasi di atas, jika masalah berlanjut, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mendapatkan bantuan.
>- Jika resolusi DNSPod terdaftar, tetapi tidak dapat ditemukan dengan perintah `dig`, alasannya mungkin karena verifikasi identitas untuk domain belum diselesaikan (sehingga registri menghentikan resolusinya).
