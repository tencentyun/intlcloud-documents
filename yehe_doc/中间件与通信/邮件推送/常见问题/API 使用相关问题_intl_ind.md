### Apa yang dimaksud dengan parameter `ReplyToAddresses`?
Parameter ini menunjukkan alamat email tujuan pengiriman pesan balasan. Misalnya, ketika seseorang menerima email Anda dan mengeklik “balas”, email balasan akan dikirim ke alamat yang Anda tentukan di `ReplyToAddresses`.

### Ketika mencoba mengirim email, saya mendapatkan kesalahan "FailedOperation.ExceedSendLimit", yang menunjukkan bahwa batas pengiriman email harian telah tercapai. Apa batasnya? Bisakah saya meningkatkan batasnya?
Setiap akun dapat mengirim paling banyak 300.000 email per hari secara default. Untuk meningkatkan batasnya, hubungi [Dukungan Teknis Tencent Cloud](https://console.cloud.tencent.com/workorder/category).

### Bagaimana cara memasukkan `Template.TemplateData` di API `SendEmail`?
`{}` berarti tidak ada variabel yang diteruskan. Untuk mengetahui detailnya, lihat bidang [TemplateData](https://intl.cloud.tencent.com/document/product/1084/39418#Template) di dokumentasi API.
