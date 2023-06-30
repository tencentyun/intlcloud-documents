### Tidak ada koneksi jaringan setelah saya masuk ke CVM. Bagaimana cara mengatasi masalah ini?
Jika tidak ada akses jaringan (misalnya, halaman web tidak dapat diakses) setelah Anda masuk ke CVM, Anda perlu memeriksa konfigurasi DNS. Atur CVM untuk mendapatkan alamat DNS secara otomatis dengan mengikuti petunjuk di bawah ini.
> Operasi berikut menggunakan contoh Windows Server 2012.
> 
1. Login ke Windows CVM.
2. Di desktop, klik <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"> dan pilih **Control panel** (Panel kontrol) -> **Network and Internet** (Jaringan dan Internet) -> **View network status and tasks** (Lihat status dan tugas jaringan) -> **Change adapter settings** (Ubah pengaturan adaptor).
3. Klik kanan **Ethernet** (Ethernet) dan pilih **Properties** (Properti) untuk membuka jendela “Ethernet Properties” (Properti Ethernet).
4. Di jendela “Ethernet Properties” (Properti Ethernet), klik dua kali dan buka jendela **Internet Protocol Version 4 (TCP/IPv4) Properties** (Properti Internet Protocol Version 4 (TCP/IPv4)).
5. Di jendela **Internet Protocol Version 4 (TCP/IPv4) Properties** (Properti Internet Protocol Version 4 (TCP/IPv4)), pilih **Obtain an IP address automatically** (Dapatkan alamat IP secara otomatis) dan **Obtain DNS server address automatically** (Dapatkan server DNS secara otomatis), dan klik **OK** (OKE), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/8a597efe05adc2f96d4b40b6cd633ca4.png)

### Dapatkah instans VPC terhubung dengan instans jaringan klasik?

#### Ya, tetapi memiliki batasan berikut:
Rentang alamat IP VPC (CIDR) harus 10.0.0.0/16 - 10.0.47.0/16 (termasuk subset). Jika tidak, akan ada konflik.

#### Petunjuk
Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1), klik ID/nama VPC untuk mengakses halaman detailnya, lalu klik tab **Classiclink** untuk mengaitkan CVM jaringan klasik agar saling terhubung. 

### Bagaimana cara melihat CVM jaringan klasik yang saling terhubung dengan CVM VPC?
Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1), klik ID/nama VPC untuk mengakses halaman detailnya, dan lihat CVM jaringan klasik yang saling terhubung dengan CVM VPC di **Classiclink**.

### Dapatkah CVM dialihkan ke jaringan luar negeri?
Setelah dibeli, jaringan tidak dapat diubah untuk CVM. Jika Anda membutuhkan jaringan luar negeri, kami sarankan Anda mengembalikan CVM dan membeli CVM luar negeri.

### Bagaimana cara mengonfirmasi DNS jaringan pribadi?
Harap lihat [Akses Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225).

### Dalam rentang IP yang sama, VPN dapat memperoleh alamat IP dari rentang IP tetapi tidak dapat mengakses internet. Bagaimana cara mengatasi masalah ini?

Periksa apakah konfigurasi berikut sudah benar:
1. Apakah IP yang ditambahkan secara manual dan IP yang diperoleh secara otomatis berada dalam subnet IP yang sama? Apakah subnet mask-nya sama? Apakah gateway default-nya sudah dikonfigurasi? Apakah alamat gateway default-nya sudah benar?
2. Apakah DNS dikonfigurasi dan apakah alamat DNS-nya sudah benar?
3. Jika semua konfigurasi di atas benar, periksa apakah alamat IP yang dikonfigurasi secara statis memiliki konflik IP.
  
Jika konfigurasi di atas tidak ada yang berhasil, [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk menghubungi kami.

### Bagaimana cara menambahkan CVM pada akun A dan B ke subnet yang sama?

Secara default, akun tidak saling terhubung oleh jaringan. Untuk menghubungkan akun, lihat [Membuat Koneksi Peering Lintas Akun](https://intl.cloud.tencent.com/document/product/553/35190) atau [Akun Lintas Interkoneksi Instans Jaringan](https://intl.cloud.tencent.com/document/product/1003/31987).
