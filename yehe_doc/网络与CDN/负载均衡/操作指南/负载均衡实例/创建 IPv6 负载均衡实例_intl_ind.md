>?
>- CLB IPv6 saat ini dalam pengujian beta.Jika Anda ingin menggunakannya, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) untuk mendaftar.
>- Saat ini, instance CLB IPv6 dapat dibuat di wilayah Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Hong Kong (Tiongkok), Singapura, dan Virginia.
>- CLB IPv6 tidak mendukung CLB klasik.
>- CLB IPv6 mendukung upaya mendapatkan alamat sumber IPv6 klien, yang dapat langsung diperoleh dengan CLB IPv6 lapisan 4 atau melalui header `X-Forwarded-For` dari HTTP CLB IPv6 lapisan 7.
>- Saat ini, CLB IPv6 sepenuhnya diimplementasikan pada jaringan publik, jadi klien di VPC yang sama tidak bisa mengakses CLB IPv6 melalui jaringan pribadi.
>- Implementasi IPv6 masih berada di tahap dasar di seluruh internet.Jika terjadi kegagalan akses, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1).SLA tidak dijamin selama periode pengujian beta.

## Ikhtisar
CLB IPv6 adalah penyeimbangan beban yang diimplementasikan berdasarkan teknologi tumpukan tunggal IPv6.Itu bisa berkolaborasi dengan CLB IPv4 untuk mengimplementasikan komunikasi dua tumpukan IPv6/IPv4.Instance CLB IPv6 terikat ke alamat IPv6 dari instance CVM dan memberikan alamat VIP IPv6.
### Keunggulan CLB IPv6
CLB IPv6 memiliki keunggulan sebagai berikut saat membantu bisnis Anda terhubung dengan cepat ke IPv6:
- Koneksi cepat:CLB mengaktifkan koneksi ke IPv6 dalam hitungan detik dan tersedia pada saat pembelian.
- Kemudahan penggunaan:CLB IPv6 kompatibel dengan proses operasi CLB IPv4 dan mudah digunakan tanpa memerlukan biaya pembelajaran tambahan.
- Komunikasi IPv6 menyeluruh:CLB IPv6 berkomunikasi dengan instance CVM melalui IPv6, yang membantu aplikasi yang di-deploy di instance CVM ditingkatkan dengan cepat ke IPv6 dan mengimplementasikan komunikasi IPv6 menyeluruh.

### Arsitektur CLB IPv6
CLB mendukung pembuatan instance CLB IPv6.Tencent Cloud akan memberikan alamat IP publik IPv6, yaitu, VIP edisi IPv6, ke instance CLB IPv6, dan VIP akan meneruskan permintaan dari klien IPv6 ke instance CVM IPv6 nyata.

Instance CLB IPv6 bisa mendukung akses cepat pengguna jaringan publik IPv6 dan berkomunikasi dengan server asli melalui IPv6, yang membantu aplikasi in-cloud ditingkatkan dengan cepat ke IPv6 dan mengimplementasikan komunikasi IPv6 menyeluruh.

Arsitektur CLB IPv6 seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/d86205a385506928dc13ef9646a91243.png)

## Panduan Pengoperasian
### Langkah 1.Buat instance CLB IPv6
1.Masuk ke situs web resmi Tencent Cloud dan masuk ke [halaman pembelian CLB](https://buy.cloud.tencent.com/lb).
2.Pilih opsi untuk parameter berikut dengan benar:
- Cara Penagihan: hanya mendukung penagihan bayar sesuai pemakaian.
- Wilayah: pilih wilayah.
- Versi IP:IPv6.
- Jenis ISP:BGP.
- Jaringan: silakan pilih VPC dan subnet yang sudah mendapatkan CIDR IPv6.
3.Setelah mengatur item-item konfigurasi di halaman pembelian, klik **Buy Now** (Beli Sekarang) untuk kembali ke [halaman daftar instance CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), tempat Anda bisa melihat instance CLB IPv6 yang baru saja Anda beli.

### Langkah 2.Buat pendengar CLB IPv6
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3) dan klik ID instance CLB IPv6 untuk masuk ke halaman detail.
2.Pilih tab **Listener Management** (Manajemen Pendengar) dan klik **Create** (Buat) untuk membuat pendengar, misalnya, pendengar TCP.
>? CLB mendukung pembuatan pendengar CLB IPv6 (TCP/UDP/TCP SSL) lapisan 4 dan (HTTP/HTTPS) lapisan 7.Untuk informasi selengkapnya, silakan lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>
3.Di "Konfigurasi Dasar", konfigurasikan nama, port protokol pendengaran, dan metode penyeimbangan, dan klik **Next** (Berikutnya).
![](https://main.qcloudimg.com/raw/dce7a8870add7556a229c10990444e78.png)
4.Konfigurasikan pemeriksaan kesehatan dan klik **Next** (Berikutnya).
![](https://main.qcloudimg.com/raw/7e425de32751160382b602752c302f19.png)
5.Konfigurasikan persistensi sesi dan klik **Submit** (Kirim).
![](https://main.qcloudimg.com/raw/e4d910a5904e1c8fb890d594bb64ba72.png)
6.Setelah pendengar dibuat, pilih dan klik **Bind** (Ikat) di sebelah kanan.
>?Sebelum mengikat pendengar ke instance CVM, silakan periksa apakah instance sudah memperoleh alamat IPv6.
>
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)
7.Di kotak pop-up, pilih instance CVM IPv6 nyata untuk berkomunikasi, konfigurasikan port dan bobot layanannya, dan klik **OK**.
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)
