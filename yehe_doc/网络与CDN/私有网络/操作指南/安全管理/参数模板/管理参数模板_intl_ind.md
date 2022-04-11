Dokumen ini menjelaskan cara membuat dan memelihara templat parameter (alamat IP, grup alamat IP, port protokol, dan grup port protokol) di konsol dan cara menggunakannya di grup keamanan.


## Membuat Templat Parameter

### Membuat templat parameter alamat IP
Tambahkan IP dengan kebutuhan yang sama atau yang sering diedit ke objek alamat IP ini.

#### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Parameter Template** (Templat Parameter) di bilah sisi kiri untuk membuka halaman pengelolaan.
3. Pilih tab **IP Address** (Alamat IP) dan klik **+ New** (+ Baru).
4. Pada jendela pop-up, masukkan nama dan alamat IP, lalu klik **Submit** (Kirim).
 Anda dapat menambahkan beberapa alamat IPv4 dalam rentang berikut dan memisahkannya menurut jeda baris:
 - Alamat IP tunggal: seperti `10.0.0.1`;
 - Blok CIDR: seperti `10.0.1.0/24`; 
 - Rentang IP: seperti `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)

### Membuat templat parameter grup alamat IP
Anda dapat menambahkan beberapa objek alamat IP ke grup alamat IP untuk pengelolaan terpadu.

#### Petunjuk
1. Pilih tab **IP Address Group** (Grup Alamat IP) dan klik **+ New** (+ Baru).
	![](https://qcloudimg.tencent-cloud.cn/raw/333211f6e4bb94b7611cb6d4bb327c98.png)
2. Pada jendela pop-up, masukkan nama, pilih objek alamat IP yang ingin Anda tambahkan, lalu klik **Submit** (Kirim).
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### Membuat templat parameter port protokol
Tambahkan port protokol dengan kebutuhan yang sama atau yang sering diedit ke objek port protokol ini.

#### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Parameter Template** (Templat Parameter) di bilah sisi kiri untuk membuka halaman pengelolaan.
3. Pilih tab **Protocol Port** (Port Protokol) dan klik **+ New** (+ Baru).
4. Pada jendela pop-up, masukkan nama dan port protokol, dan klik **Submit** (Kirim).
   Anda dapat menambahkan beberapa port protokol dalam rentang berikut dan memisahkannya dengan jeda baris:
	- Port tunggal: seperti `TCP:80`;
	- Beberapa port: seperti `TCP:80,443`;
	- Rentang port: seperti `TCP:3306-20000`;
	- Semua port: seperti `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)

### Membuat templat parameter grup port protokol
Anda dapat menambahkan beberapa objek port protokol yang dibuat ke grup port protokol untuk pengelolaan terpadu.
#### Petunjuk	
1. Pilih tab **Protocol Port Group** (Grup Port Protokol) dan klik **+ New** (+ Baru).
	![](https://qcloudimg.tencent-cloud.cn/raw/5101e8b5139198a06f6d2a28036af32a.png)
2. Pada jendela pop-up, masukkan nama, pilih objek port protokol yang akan ditambahkan, lalu klik **Submit** (Kirim).
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Memodifikasi Templat Parameter
Jika Anda perlu memodifikasi templat parameter yang dibuat, misalnya, untuk menambah/menghapus alamat IP atau port protokol, ikuti langkah-langkah di bawah ini.

### Petunjuk
1. Klik alamat IP, grup alamat IP, port protokol, atau templat parameter grup port protokol yang dibuat dan klik **Edit** (Edit) di sebelah kanan. Misalnya, gambar berikut menunjukkan cara memodifikasi objek alamat IP.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cbb3cb328b614baad17cd236fbe5cb61.png)
2. Di jendela pop-up, modifikasi parameter yang sesuai dan klik **Submit** (Kirim).
   
## Menghapus Templat Parameter
Jika Anda tidak lagi menggunakan templat parameter, Anda dapat menghapusnya. Saat templat ini dihapus, semua konfigurasi kebijakan yang memuatnya dalam grup keamanan akan dihapus secara bersamaan. Harap evaluasi dan lanjutkan dengan hati-hati.

### Petunjuk
1. Klik **Delete** (Hapus) di sebelah kanan templat parameter yang dibuat.
   ![](https://qcloudimg.tencent-cloud.cn/raw/bc33be2141b5b267ba2d56cd40793258.png)
2. Saat templat ini dihapus, semua kebijakan yang berisi alamat IP atau port protokol yang sesuai juga akan dihapus. Setelah mengonfirmasi bahwa semua langkah sudah benar, klik **Delete** (Hapus) di jendela pop-up **Confirm Deletion** (Konfirmasi Penghapusan).

## Mengimpor Templat Parameter ke dalam Grup Keamanan
Setelah membuat templat parameter, Anda dapat langsung mengimpornya saat menambahkan aturan dalam grup keamanan untuk menambahkan sumber IP atau port protokol dengan cepat, yang membantu meningkatkan efisiensi Anda dalam menambahkan aturan grup keamanan.

### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Security** (Keamanan) > **Security Group** (Grup Keamanan) di bilah sisi kiri untuk membuka halaman pengelolaan.
3. Dalam daftar, temukan grup keamanan tempat templat parameter perlu diimpor, dan klik ID-nya untuk masuk ke halaman detail.
4. Pada tab **Inbound/Outbound Rules** (Aturan Masuk/Keluar), klik **Add Rule** (Tambahkan Aturan).
5. Di jendela pop-up, pilih jenis **Custom** (Kustom), pilih templat parameter yang dibuat di **Source** (Sumber) dan **Protocol Port** (Port Protokol), lalu klik **Complete** (Selesai). Untuk informasi selengkapnya tentang cara menambahkan aturan masuk/keluar, harap lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35513).
>?Jika Anda perlu menambahkan alamat IP atau port protokol baru di masa mendatang, Anda hanya perlu menambahkannya ke grup alamat IP atau grup port protokol yang sesuai, dan tidak perlu memodifikasi aturan grup keamanan atau membuat grup keamanan lain.
>
 ![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

## Melihat Grup Keamanan yang Dihubungkan
Anda dapat melihat semua instans grup keamanan yang mengimpor templat parameter dalam langkah-langkah berikut.
1. Klik **View Association** (Lihat Hubungan) di sebelah kanan templat parameter yang dibuat.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1a56775ee22def20e25cb6d54548712d.png)
2. Daftar grup keamanan terhubung yang muncul menampilkan semua instans grup keamanan yang terhubung dengan templat parameter ini.
   ![](https://qcloudimg.tencent-cloud.cn/raw/128b47cf7b2c8e2e9bf0f6a3bbbd37cf.png)
