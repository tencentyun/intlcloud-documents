## Ikhtisar
Tencent Cloud mendukung [jaringan klasik dan VPC](https://intl.cloud.tencent.com/document/product/215/31807), yang mampu menawarkan beragam layanan yang lancar. Atas dasar ini, kami menyediakan layanan yang lebih fleksibel seperti yang ditunjukkan di bawah ini untuk membantu Anda mengelola konektivitas jaringan dengan mudah.
- **Network switch** (Beralih Jaringan)
  - Beralih dari jaringan klasik ke VPC: satu instans sumber TencentDB dapat dialihkan dari jaringan klasik ke VPC.
  - Beralih dari VPC A ke VPC B: satu instans sumber TencentDB dapat dialihkan dari VPC A ke VPC B.
- **Custom IP and port** (IP dan port khusus)
  - IP dan port instans sumber kustom: IP dan port instans sumber dapat disesuaikan pada halaman detail instans di konsol.
  - IP dan port instans baca saja kustom: IP dan port instans baca saja dapat disesuaikan pada halaman detail instans di konsol.

## Catatan
- Mengalihkan jaringan dapat menyebabkan perubahan IP pribadi instans. IP asli akan menjadi tidak valid setelah waktu kepemilikan kembali berlalu. Harap segera modifikasi IP instans pada klien.
Waktu kepemilikan kembali default untuk IP asli adalah 24 jam dan waktu kepemilikan kembali terlama bisa 168 jam. Jika "Valid Hours of Old IPs" (Jam Valid IP Lama) diatur ke 0 jam, IP dilepaskan segera setelah jaringan diubah.
- Peralihan dari jaringan klasik ke VPC tidak dapat diubah. Setelah beralih ke VPC, instans TencentDB tidak dapat berkomunikasi dengan layanan Tencent Cloud di VPC atau jaringan klasik lainnya.
- Setelah Anda mengalihkan jaringan instans sumber, jaringan instans baca saja yang terkait dengan instans sumber tidak akan dialihkan secara otomatis, artinya, Anda perlu mengalihkannya secara manual.

## Petunjuk
### Beralih jaringan
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Klik **Switch to VPC** (Beralih ke VPC) atau **Change Network** (Ubah Jaringan) setelah **Network** (Jaringan) di bagian **Basic Info** (Info Dasar).
3. Di jendela pop-up, pilih VPC dan subnet, lalu klik **OK** (OKE).
>?
>- Jika tidak ada alamat IP yang ditentukan, alamat IP akan ditetapkan secara otomatis oleh sistem.
>- Anda hanya dapat memilih VPC di wilayah instans.
>- Kami sarankan agar VPC tempat instans CVM berada harus dipilih; jika tidak, instans CVM tidak akan dapat mengakses TencentDB for MySQL melalui jaringan pribadi, kecuali instans [peeering connection](https://intl.cloud.tencent.com/document/product/553/18827) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) dibuat di antara kedua VPC.
>
   - **Switch from classic network to VPC** (Beralih dari jaringan klasik ke VPC)
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **Switch from VPC A to VPC B** (Beralih dari VPC A ke VPC B)
![](https://main.qcloudimg.com/raw/d0df57066adb8398e599a6206db7cd56.png)
4. Kembali ke halaman detail instans tempat Anda dapat melihat jaringan instans.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)

### Menyesuaikan IP dan port
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk masuk ke halaman detail instans.
2. Klik <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> setelah **Private Network Address** (Alamat Jaringan Pribadi) dan **Private Port** (Port Pribadi) di bagian **Basic Info** (Info Dasar).
>!Memodifikasi alamat jaringan pribadi dan port memengaruhi bisnis database yang sedang diakses.
3. Di jendela pop-up, tentukan IP dan port dan klik **OK** (OKE).
