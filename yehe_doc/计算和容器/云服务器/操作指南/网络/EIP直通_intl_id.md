## Kasus Penggunaan
Saat ingin mengakses Internet melalui EIP, Anda dapat memilih mode NAT atau mode koneksi langsung. Mode default adalah mode NAT.
- Dalam mode NAT, EIP tidak terlihat di mesin lokal.
- Dalam mode koneksi langsung, EIP terlihat di mesin lokal. Anda tidak perlu menambahkan alamat EIP secara manual untuk setiap konfigurasi, yang dapat meminimalkan biaya pengembangan.
- Mode NAT dapat memenuhi sebagian besar persyaratan. Namun, jika ingin memeriksa IP publik pada CVM, Anda perlu menggunakan mode koneksi langsung EIP.

## Batasan Penggunaan
- Saat ini, koneksi langsung EIP sedang dalam pengujian beta dan hanya tersedia untuk pengguna yang diizinkan. Koneksi ini hanya mendukung perangkat di VPC. Anda dapat [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk mengajukan fitur ini.
- Gateway NAT dapat diikat dengan EIP yang diaktifkan dengan koneksi langsung, tetapi koneksi langsung tidak dapat diimplementasikan.
- Pada CVM, koneksi langsung EIP tidak dapat diterapkan bersamaan dengan gateway NAT. Jika tabel perutean yang terkait dengan subnet tempat CVM Anda berada dikonfigurasi dengan kebijakan perutean mengakses jaringan publik melalui gateway NAT, koneksi langsung tidak dapat diimplementasikan melalui EIP pada CVM. Anda dapat mengizinkan CVM mengakses jaringan publik melalui EIP-nya dengan [menyesuaikan prioritas gateway NAT dan EIP](https://intl.cloud.tencent.com/document/product/1015/32734). Dalam hal ini, koneksi langsung EIP dapat diimplementasikan.

## Petunjuk
Untuk menggunakan koneksi langsung EIP, Anda harus mengaktifkannya di konsol dan menambahkan IP ke ENI di sistem operasi. Anda juga perlu mengonfigurasi perutean di sistem operasi sesuai dengan aplikasi Anda. Oleh karena itu, kami menyediakan skrip untuk mengonfigurasi IP agar lalu lintas jaringan pribadi melewati IP pribadi dan lalu lintas jaringan publik melewati IP publik.
>Untuk aplikasi lain, konfigurasikan perutean yang sesuai.
>
### Mengonfigurasi koneksi langsung EIP di CVM Linux
>
>- Skrip untuk Linux mendukung CentOS 6 dan yang lebih baru, serta Ubuntu.
>- Skrip untuk Linux hanya mendukung ENI primer (eth0) dan tidak mendukung ENI sekunder.
>- Jika IP publik yang terikat ke ENI primer bukan EIP, Anda perlu mengonversi IP publik ke EIP. Untuk informasi selengkapnya, lihat [Mengonversi IP publik ke EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Skenario
Skrip untuk Linux berlaku untuk skenario berikut: IP pribadi dan IP publik keduanya terikat ke ENI primer (eth0), tempat alamat jaringan publik diakses melalui IP publik, dan alamat jaringan privat diakses melalui IP pribadi.

#### Langkah 1: unduh skrip untuk koneksi langsung EIP
Koneksi langsung EIP dapat menyebabkan gangguan jaringan. Dengan demikian, Anda perlu mengunduh skrip untuk koneksi langsung EIP dan mengunggahnya ke CVM terlebih dahulu. Anda dapat memperoleh skrip dengan menggunakan salah satu metode berikut:
- **Method 1: upload the script for EIP direct connection** (Metode 1: Unggah skrip untuk koneksi langsung EIP)
 (1) Unduh skrip konfigurasi untuk koneksi langsung EIP dari Unduh Script untuk Linux
 (2) Setelah skrip untuk Linux diunduh ke mesin lokal, unggah ke CVM yang memerlukan koneksi langsung EIP.
- **Method 2: directly use a command** (Metode 2: langsung gunakan perintah)
Login ke CVM, dan jalankan perintah berikut pada CVM untuk mengunduh skrip:
```
wget https://network-data-1255486055.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

#### Langkah 2: jalankan skrip untuk koneksi langsung EIP
1. Login ke CVM yang memerlukan koneksi langsung EIP.
2. Jalankan skrip untuk koneksi langsung EIP sebagai berikut:
 (1) Jalankan perintah berikut untuk menambahkan izin eksekusi:
```
chmod +x eip_direct.sh
```
 (2) Jalankan perintah berikut untuk menjalankan skrip:
```
./eip_direct.sh install XX.XX.XX.XX
```
Di sini, XX.XX.XX.XX menunjukkan alamat EIP (opsional). Anda dapat membiarkannya kosong dan menjalankan `./eip_direct.sh install` secara langsung.

#### Langkah 3: aktifkan koneksi langsung EIP
1. Login ke [Konsol EIP](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Temukan EIP target, dan pilih **More** (Lainnya) -> **Direct connection** (Koneksi langsung) di kolom **Operation** (Operasi) di sebelah kanan.


### Mengonfigurasi koneksi langsung EIP pada CVM Windows
>
>- Untuk menggunakan koneksi langsung EIP di Windows, Anda memerlukan satu ENI untuk IP pribadi dan satu ENI untuk IP publik, lalu ikat IP publik ke ENI primer dan ikat IP pribadi ke ENI sekunder.
>- Selama konfigurasi koneksi langsung EIP di Windows, koneksi internet Anda bisa saja terputus. Dengan demikian, sebaiknya [login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
- Jika IP publik yang terikat ke ENI primer bukan EIP, Anda perlu mengonversi IP publik ke EIP. Untuk informasi selengkapnya, lihat [Mengonversi IP publik ke EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Skenario
Skrip untuk Windows berlaku untuk skenario berikut ini: Lalu lintas jaringan publik melewati ENI primer, dan lalu lintas jaringan pribadi melewati ENI sekunder.

#### Langkah 1: unduh skrip untuk koneksi langsung EIP<span id="step1" />
Selama konfigurasi koneksi langsung EIP, koneksi internet akan terganggu. Dengan demikian, Anda perlu mengunduh skrip untuk koneksi langsung EIP dan mengunggahnya ke CVM terlebih dahulu.
Buka tautan berikut di browser CVM untuk mengunduh skrip untuk koneksi langsung EIP:
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat
```

#### Langkah 2: konfigurasikan ENI sekunder
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/overview).
2. Pada halaman **Instances** (Instans), klik CVM ID yang dikonfigurasi untuk membuka halaman **Basic Information** (Informasi Dasar).
3. Pilih tab **ENI** (ENI), lalu klik **Bind ENI** (Ikat ENI) untuk membuat ENI yang berada di subnet yang sama dengan ENI primer.
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. Di jendela pop-up, pilih **Create and Bind an ENI** (Buat dan Ikat ENI), masukkan informasinya, pilih **Automatic Assignment** (Penetapan Otomatis) di bagian **Assign IP** (Tetapkan IP) dan klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### Langkah 3: konfigurasikan koneksi langsung EIP untuk ENI primer
1. Login ke [Konsol EIP](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Temukan EIP yang terikat ke ENI primer dan pilih **More** (Lainnya) -> **Direct Connection** (Koneksi Langsung) di kolom **Operation** (Operasi) di sebelah kanan.

#### Langkah 4: konfigurasikan IP di CVM
1. Login ke CVM. Operasi ini dapat menyebabkan gangguan jaringan publik. Dengan demikian, Anda perlu [Login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Pada halaman sistem operasi, pilih <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px"> di pojok kiri bawah dan klik <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;"> untuk membuka jendela **Windows PowerShell** (Windows PowerShell). Masukkan `firewall.cpl`, lalu tekan Enter untuk membuka halaman **Windows Firewall** (Windows Firewall).
3. Klik **Turn Windows Firewall on or off** (Aktifkan atau nonaktifkan Windows Firewall) untuk membuka halaman **Customize Settings** (Sesuaikan Pengaturan).
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. Pilih **Turn off Windows Firewall** (Nonaktifkan Windows Firewall) baik di panel **Private network settings** (Pengaturan jaringan pribadi) dan panel **Public network settings** (Pengaturan jaringan publik).
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. Klik dua kali untuk menjalankan skrip yang diunduh di [Langkah 1](#step1). Masukkan alamat IP publik dan tekan Enter dua kali.
6. Masukkan `ipconfig` di jendela **Windows PowerShell** (Windows PowerShell), lalu tekan Enter. Anda dapat melihat bahwa alamat IPv4 pada ENI primer akan berubah menjadi alamat jaringan publik.

>Saat koneksi langsung diaktifkan, Anda tidak dapat menetapkan IP pribadi ke ENI primer. Jika tidak, CVM tidak dapat mengakses jaringan publik.
