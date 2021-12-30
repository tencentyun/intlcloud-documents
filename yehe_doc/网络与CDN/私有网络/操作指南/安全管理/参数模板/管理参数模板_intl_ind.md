Templat parameter terdiri dari satu set parameter. Anda dapat menyimpan alamat IP dan port protokol sebagai templat sehingga Anda dapat langsung mengimpor templat saat menambahkan aturan grup keamanan. Templat parameter, jika digunakan dengan benar, dapat meningkatkan efisiensi Anda dalam menggunakan grup keamanan.
Tencent Cloud mendukung empat jenis templat parameter:
- Alamat IP (ipm): mendukung alamat IP tunggal, blok CIDR, dan rentang alamat IP.
- Grup alamat IP (ipmg): mendukung sekelompok objek alamat IP.
- Port protokol (ppm): mendukung satu port, beberapa port, port berurutan, dan semua port. Protokol yang didukung adalah TCP, UDP, ICMP, dan GRE.
- Grup port protokol (ppmg): mendukung sekelompok objek port protokol.

## Skenario
Templat parameter berlaku untuk skenario berikut:
- Mengelola beberapa alamat IP atau grup port protokol dengan persyaratan yang sama.
- Mengelola beberapa alamat IP atau grup port protokol dengan kebutuhan pengeditan berulang.

## Langkah 1: Buat Templat Parameter
### 1. Buat templat parameter alamat IP
Tambahkan alamat IP dengan persyaratan yang sama atau kebutuhan pengeditan berulang ke objek alamat IP.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Parameter Template** (Templat Parameter) di bilah sisi kiri untuk membuka halaman manajemen.
3. Pada halaman tab **IP Address** (Alamat IP), klik **+New** (+Baru).
4. Pada kotak pop-up, masukkan nama dan alamat IP, lalu klik **Submit** (Kirim).
Untuk menambahkan beberapa alamat IP, pisahkan dengan jeda baris. Hanya alamat IPv4 dalam format berikut yang didukung:
 - Alamat IP tunggal, misalnya, `10.0.0.1`;
 - Rentang IP, misalnya, `10.0.1.0/24`; 
 - Alamat IP beruntun, misalnya, `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)
5. (Opsional) Anda dapat menambahkan beberapa alamat IP yang dibuat ke grup untuk membuat grup alamat IP.
	1. Klik tab **IP Address Group** (Grup Alamat IP) untuk masuk ke halaman manajemen. Di halaman ini, klik **+Baru** (+New).
	2. Pada kotak pop-up, masukkan nama, pilih alamat IP yang ingin Anda tambahkan, dan klik **Submit** (Kirim).
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### 2. Buat templat parameter port protokol
Tambahkan port protokol dengan persyaratan yang sama atau kebutuhan pengeditan berulang ke objek port protokol.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Parameter Template** (Templat Parameter) di bilah sisi kiri untuk membuka halaman manajemen.
3. Klik tab **Protocol Port** (Port Protokol) untuk masuk ke halaman tab **Protocol Port** (Port Protokol). Pada halaman tag ini, klik **+New** (+Baru).
4. Pada kotak pop-up, masukkan nama dan port protokol, dan klik **Submit** (Kirim).
Untuk menambahkan beberapa port protokol, pisahkan dengan jeda baris. Format port protokol berikut ini didukung:
	- Satu port, misalnya, `TCP:80`;
	- Beberapa port terpisah, misalnya, `TCP:80,443`;
	- Port berurutan, misalnya, `TCP:3306-20000`;
	- Semua port, misalnya, `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)
5. (Opsional) Anda dapat menambahkan beberapa port protokol yang dibuat ke grup untuk membuat grup port protokol.
	1. Klik tab **Protocol Port Group** (Grup Port Protokol) untuk masuk ke halaman manajemen. Di halaman ini, klik **+Baru** (+New).
	2. Pada kotak pop-up, masukkan nama, pilih port protokol yang ingin Anda tambahkan, dan klik **Submit** (Kirim).
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Langkah 2: Impor Templat Parameter di Grup Keamanan
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Security Group** (Grup Keamanan) di bilah sisi kiri untuk membuka halaman manajemen.
3. Dalam daftar, temukan grup keamanan tempat templat parameter perlu diimpor, dan klik ID-nya untuk masuk ke halaman detail.
4. Pada halaman tab **Inbound Rules or Outbound Rules** (Aturan Masuk atau Aturan Keluar, klik **Add Rules** (Tambah Aturan).
5. Pada kotak pop-up, pilih templat parameter yang sesuai untuk port sumber dan protokol. Untuk petunjuk mendetail dalam menambahkan aturan masuk dan keluar, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35513).
>? Selanjutnya, jika perlu menambahkan alamat IP atau port protokol baru, Anda hanya perlu menambahkannya di grup alamat IP atau grup port protokol yang sesuai tanpa harus mengubah aturan grup keamanan atau membuat grup keamanan lain.
>
![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

