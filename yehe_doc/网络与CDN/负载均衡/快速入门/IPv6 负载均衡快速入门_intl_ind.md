CLB mendukung tiga versi IP:IPv4, IPv6, dan IPv6 NAT64.CLB IPv6 mendukung protokol TCP, UDP, TCP SSL, HTTP, dan HTTPS serta memberikan kemampuan meneruskan yang fleksibel berdasarkan nama domain dan jalur URL.Dokumen ini menjelaskan kepada Anda cara memulai IPv6 CLB.
>?CLB IPv6 saat ini dalam pengujian beta.Jika Anda ingin menggunakannya, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) untuk mendaftar.

## Prasyarat
1.CLB hanya meneruskan lalu lintas tetapi tidak dapat memproses permintaan; oleh karena itu, Anda harus membuat instance CVM yang memproses permintaan pengguna terlebih dahulu lalu menyelesaikan konfigurasi IPv6 untuknya.
2.Dokumen ini mengambil penerusan HTTP sebagai contoh.Server web yang sesuai (seperti Apache, Nginx, atau IIS) harus di-deploy pada instance CVM, dan port yang digunakan server harus mendengarkan IPv6.

## Petunjuk
- Saat ini, instance CLB IPv6 dapat dibuat di wilayah Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Hong Kong (Tiongkok), Singapura, dan Virginia.
- CLB IPv6 tidak mendukung CLB klasik.
- CLB IPv6mendukung upaya mendapatkan alamat sumber IPv6 klien, yang dapat langsung diperoleh dengan lapisan-4 CLB IPv6 atau melalui header `X-Forwarded-For` dari HTTP lapisan-7 IPv6 CLB.
- Saat ini, CLB IPv6 menyeimbangkan muatan sepenuhnya lewat jaringan publik.Klien di VPC yang sama tidak dapat mengakses CLB IPv6 lewat jaringan privat.
>- Implementasi IPv6 masih berada di tahap awal di seluruh internet.Jika terjadi kegagalan akses, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category).SLA tidak dijamin selama periode pengujian beta.

## Langkah 1.Buat instance CVM dan konfigurasikan IPv6
1.Masuk ke [Konsol CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1), masuk ke instance CVM, lalu selesaikan konfigurasi IPv6 dasar.
2.Pada instance CVM, jalankan perintah berikut secara berurutan untuk men-deploy dan memulai ulang layanan Nginx.
```
yum instal nginx
mulai ulang layanan nginx
```
3. <span id="check" />Periksa apakah layanan Nginx yang di-deploy pada instance CVM mendengarkan IPv6.
1.Jalankan perintah berikut untuk pemeriksaan.
```
netstat -tupln
```
![](https://main.qcloudimg.com/raw/5bbe14c9e654b5a451828fa1e4157ac8.png)
2.Jalankan perintah berikut untuk membuka file konfigurasi Nginx untuk pemeriksaan.
```
vim  /etc/nginx/nginx.conf
```
![](https://main.qcloudimg.com/raw/ff7718571c02a45f02646ab330c21ee2.png)

## Langkah 2.Buat instance CLB IPv6
1.Masuk ke situs web resmi Tencent Cloud dan masuk ke [halaman pembelian CLB](https://buy.cloud.tencent.com/lb).
2.Pilih opsi untuk parameter berikut dengan benar:
- Cara Penagihan: hanya mendukung penagihan bayar sesuai pemakaian.
- Wilayah: pilih wilayah.
- Versi IP:IPv6.
- Jenis ISP:BGP.
- Jaringan: silakan pilih VPC dan subnet yang sudah mendapatkan CIDR IPv6.
3.Pilih item konfigurasi masing-masing di halaman pembelian dan klik **Buy Now** (Beli Sekarang).
4.Di halaman "CLB Instance List" (Daftar Instance CLB), pilih wilayah yang sesuai untuk melihat instance yang baru saja dibuat.
![](https://main.qcloudimg.com/raw/f53a0d3da88b82071960522de6c2fdb8.png)

## Langkah 3.Buat pendengar CLB IPv6
### Mengonfigurasi protokol pendengar dan port HTTP
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2.Di "CLB Instance List" (Daftar Instance CLB), cari instance CLB yang dibuat dan klik ID-nya untuk masuk ke halaman detail.
3.Di modul "Basic Information" (Informasi Dasar), Anda dapat mengeklik ikon modifikasi di samping nama instance untuk mengganti namanya.
4.Di **HTTP/HTTPS Listeners** (Pendengar HTTP/HTTPS) di "Manajemen Pendengar", klik **Create** (Buat) untuk membuat pendengar CLB.
![](https://main.qcloudimg.com/raw/301fbda84ff54f2026f79cf7063d3413.png)
5.Di jendela pop-up, konfigurasikan berikut ini:
- Atur nama ke "IPv6test", misalnya.
- Atur protokol dan port pendengar ke `HTTP:80`.
6.Klik **Submit** (Kirim) untuk membuat pendengar CLB.

### Mengonfigurasi aturan meneruskan pendengar
1.Di "Manajemen Pendengar", pilih pendengar baru IPv6test dan klik **+** untuk menambahkan aturan.
2.Di jendela pop-up, konfigurasikan nama domain, jalur URL, dan metode penyeimbangan, lalu klik **Next** (Selanjutnya).
- Nama Domain: nama domain yang digunakan oleh server asli Anda, yang bisa berisi kartubebas.Dalam contoh ini, `www.qcloudipv6test.com` digunakan.Untuk informasi selengkapnya, silakan lihat [Lapisan-7 Meneruskan Aturan Nama Domain dan URL](https://intl.cloud.tencent.com/document/product/214/9032).
- Jalur URL: jalur akses server asli Anda. `/` digunakan dalam contoh ini.
- Pilih "WRR" untuk mode penyeimbang muatan.
![](https://main.qcloudimg.com/raw/9061484f81b8a09bf194b8e0935d28b9.png)
3.Konfigurasikan pemeriksaan kesehatan: aktifkan pemeriksaan kesehatan, periksa nama domain dan jalur meneruskan default yang digunakan oleh nama domain, lalu klik **Next** (Selanjutnya).
![](https://main.qcloudimg.com/raw/f55355ac26ed08260c631d4e665efbd6.png)
4.Konfigurasikan persistensi sesi: aktifkan persistensi sesi, konfigurasikan periode persistensi, lalu klik **Submit** (Kirim).
![](https://main.qcloudimg.com/raw/e5f710e4dd821a06ef4a6f3d77e0370f.png)

Untuk informasi selengkapnya tentang pendengar CLB, lihat [Ikhtisar Pendengar CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>?
>- Pendengar (yaitu protokol:port yang mendengarkan) dapat dikonfigurasi dengan beberapa nama domain, dan nama domain dapat dikonfigurasi dengan beberapa jalur URL.Pilih nama pendengar atau domain dan klik **+** untuk membuat aturan baru.
>- Persistensi sesi: jika persistensi sesi dinonaktifkan dan metode round-robin digunakan untuk menyusun jadwal, permintaan akan ditetapkan ke berbagai server asli secara berurutan; jika persistensi sesi diaktifkan, atau dinonaktifkan tetapi penjadwalan ip_hash digunakan, permintaan akan selalu ditetapkan ke server asli yang sama.

### Mengikat instance CVM
>?Sebelum mengikat pendengar ke instance CVM, silakan periksa apakah instance sudah memperoleh alamat IPv6.

1.Di halaman "Listener Management" (Manajemen Pendengar), pilih dan perluas pendengar yang barusan dibuat lalu pilih nama domain dan jalur URL, sedangkan informasi IPv6 dari instance CVM yang terikat ke jalur URL akan ditampilkan di sisi kanan.Klik **Bind** (Ikat).
2.Di jendela pop-up, pilih instance CVM, atur port layanan Nginx default ke 80, atur bobot (10 secara default), dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/463dfdd5c8bb6772374597673614f2d9.png)
3.Setelah instance CVM berhasil diikat, lakukan berikut ini:
- Periksa apakah status port "healthy" (sehat) atau tidak; dan jika sehat, silakan lanjut ke [Langkah 4.Uji IPv6 CLB](#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E6.B5.8B.E8.AF.95-ipv6-.E8.B4.9F.E8.BD.BD.E5.9D.87.E8.A1.A1).
![](https://main.qcloudimg.com/raw/1e3fe96b91748271b04f191e7be5a7a6.png)
- Jika status port "exceptional" (luar biasa), periksa apakah pendengar terikat ke port layanan Nginx yang benar dari instance CVM, dan masuk ke instance CVM untuk memeriksa apakah port mendengar IPv6 secara normal atau tidak.Anda dapat melakukan pemeriksaan sesuai petunjuk di [sublangkah 3 di langkah 1](#check) untuk melakukan pemeriksaan.
![](https://main.qcloudimg.com/raw/c28a8b4fc331127b8fc5fcc1294f0df9.png)

## Langkah 4.Uji IPv6 CLB
Setelah mengonfigurasi instance IPv6 CLB, Anda dapat memverifikasi aktif tidaknya arsitektur dengan memeriksa apakah nama domain dan URL yang berbeda-beda di dalam instance CLB dapat mengakses server asli yang berlainan, yaitu memeriksa apakah fitur perutean berbasis konten sudah tersedia atau belum.

Gunakan klien dengan kemampuan akses jaringan publik IPv6 untuk mengakses nama domain atau alamat IPv6 dari instance CLB.Jika dapat mengakses layanan web instance CVM sebagaimana mestinya, instance CLB IPv6 sudah bekerja normal.
