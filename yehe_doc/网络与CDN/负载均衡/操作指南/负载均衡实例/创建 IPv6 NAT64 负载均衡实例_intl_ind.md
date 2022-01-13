>
>- CLB IPv6 NAT64 hanya bisa dibuat di tiga wilayah:Beijing, Shanghai, dan Guangzhou.
>- CLB IPv6 NAT64 tidak mendukung CLB klasik.
>- CLB IPv6 NAT64 tidak mendukung pengambilan IP klien.
>- Implementasi IPv6 masih berada di tahap awal di seluruh internet, dan SLA tidak dijamin.Jika terjadi kegagalan akses, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) untuk memperoleh bantuan.

CLB mendukung pembuatan instance CLB IPv6 NAT64.Tencent Cloud akan memberikan alamat IP publik IPv6, yaitu, VIP edisi IPv6, ke suatu instance, dan VIP akan meneruskan permintaan dari klien IPv6 ke instance CVM IPv4 nyata.

## Ikhtisar Instance CLB IPv6 NAT64
Instance CLB IPv6 NAT64 adalah penyeimbang beban yang diimplementasikan berdasarkan teknologi jembatan IPv6 NAT64.Melalui instance CLB IPv6 NAT64, server asli bisa diakses dengan cepat oleh pengguna IPv6 tanpa memerlukan modifikasi IPv6.

## Arsitektur CLB IPv6 NAT64
Arsitektur CLB IPv6 NAT64 seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/e86896cc8286b53e8198facc8d28076f.png)
Jika CLB IPv6 NAT64 diakses dari jaringan IPv6, CLB dapat dengan lancar mengonversi alamat IPv6 ke alamat IPv4 untuk beradaptasi dengan layanan yang ada dan mengimplementasikan transformasi IPv6 dengan cepat.

## Keunggulan CLB IPv6 NAT64
CLB IPv6 NAT64 Tencent Cloud memiliki keunggulan sebagai berikut saat membantu bisnis Anda terhubung dengan cepat ke IPv6:
- **Koneksi cepat:** CLB mengaktifkan koneksi ke IPv6 dalam hitungan detik dan tersedia pada saat pembelian.
- **Transisi bisnis lancar:** untuk mentransmisikan bisnis Anda ke IPv6 dengan lancar, Anda hanya perlu mentransformasikan klien tanpa perlu modifikasi untuk server asli.CLB IPv6 NAT64 mendukung akses dari klien IPv6 dan mengonversi pesan IPv6 menjadi pesan IPv4.Transisi IPv6 tidak terlihat oleh aplikasi di server asli, yang tetap bekerja dengan cara aslinya.
- **Kemudahan penggunaan:** CLB IPv6 NAT64 kompatibel dengan proses operasi CLB IPv4 dan mudah digunakan tanpa memerlukan biaya pembelajaran tambahan.

## Panduan Pengoperasian
### Membuat instance CLB IPv6 NAT64
1.Masuk di situs resmi Tencent Cloud dan buka [halaman pembelian CLB](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-k9gii1kb).
2.Pilih opsi untuk parameter berikut dengan benar:
- Wilayah: hanya Beijing, Shanghai, dan Guangzhou yang didukung.
- Jenis Instance:CLB.
- Jenis Jaringan: jaringan publik.
- Versi IP:IPv6 NAT64.
- Jaringan:VPC.
- Konfigurasi lainnya sama seperti konfigurasi instance umum.
3.Setelah mengatur item-item konfigurasi di halaman pembelian, klik **Buy Now** (Beli Sekarang) untuk kembali ke [halaman daftar instance CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), tempat Anda bisa melihat instance CLB IPv6 NAT64 yang baru saja Anda beli.

### Memakai CLB IPv6 NAT64
Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) dan klik ID instance untuk masuk ke halaman detail.Di tab “Manajemen Pendengar”, Anda bisa mengonfigurasi pendengar dan meneruskan aturan dan mengikat instance CVM.Untuk informasi selengkapnya, silakan lihat [Memulai CLB](https://intl.cloud.tencent.com/document/product/214/8975).
![](https://main.qcloudimg.com/raw/2cacac7c34a7fa241dbd6f9127570391.png)
