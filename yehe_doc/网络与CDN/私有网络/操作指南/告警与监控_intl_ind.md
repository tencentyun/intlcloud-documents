Dengan mengonfigurasi kebijakan alarm, Anda dapat memantau status sumber daya pada VPC, seperti NAT gateway, VPN gateway, direct connect gateway, EIP, dll., untuk menemukan sumber daya cloud yang berjalan tidak normal dengan tepat waktu, menemukan dan memecahkan masalah SECEPAT MUNGKIN.

## Mengonfigurasi Kebijakan Alarm
1. Login ke [Konsol Cloud Monitor](https://console.cloud.tencent.com/monitor/overview).
2. Pilih **Alarm Configuration** (Konfigurasi Alarm) > **Alarm Policy** (Kebijakan Alarm) di bilah sisi kiri untuk masuk ke halaman konfigurasi kebijakan alarm.
3. Klik **Create** (Buat), masukkan nama kebijakan, pilih sumber daya cloud VPC yang akan dikonfigurasi untuk jenis kebijakan, seperti **VPC** (VPC) > **EIP** (EIP), lalu konfigurasikan aturan alarm dan pemberitahuan alarm.
![]()
4. Klik **Complete** (Selesai). Anda dapat melihat kebijakan alarm yang diatur dalam daftar kebijakan alarm.
>? Untuk menghapus kebijakan alarm, Anda harus melepas ikatan semua sumber daya terlebih dahulu.
>
5. Saat alarm dipicu, Anda akan menerima pemberitahuan alarm melalui saluran alarm yang dipilih (SMS/email/Pusat Pesan, dll.).

Konfigurasi kebijakan alarm untuk sumber daya cloud yang berbeda dijelaskan secara mendetail di bawah ini:
- Direct Connect: [Mengonfigurasi Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/216/38402) 
- NAT Gateway: - [Mengatur Alarm](https://intl.cloud.tencent.com/document/product/1015/30242) 
- VPN Connection: [Mengatur Alarm](https://intl.cloud.tencent.com/document/product/1037/32699) 

## Melihat Informasi Pemantauan
Anda dapat melihat informasi pemantauan sumber daya cloud yang sesuai di konsol VPC untuk membantu Anda memecahkan masalah kegagalan jaringan. Lihat:
- Direct Connect: [Melihat Data Pemantauan](https://intl.cloud.tencent.com/document/product/216/38401) 
- CCN: [Lihat Informasi Pemantauan](https://intl.cloud.tencent.com/document/product/1003/30071) 
- NAT Gateway: [Melihat Informasi Pemantauan](https://intl.cloud.tencent.com/document/product/1015/30241) 
- Peering Connection: [Melihat Data Pemantauan Lalu Lintas Jaringan Melalui Peering Connection Lintas Wilayah](https://intl.cloud.tencent.com/document/product/553/18842) 
- VPN Connection: [Melihat Data Pemantauan](https://intl.cloud.tencent.com/document/product/1037/32698) 
