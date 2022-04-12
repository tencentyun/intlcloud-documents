Tabel rute terdiri dari beberapa kebijakan perutean yang mengontrol arah lalu lintas keluar dari subnet di VPC. Setiap subnet hanya dapat dihubungkan dengan satu tabel rute, sedangkan setiap tabel rute dapat dihubungkan dengan beberapa subnet. Anda dapat membuat beberapa tabel rute untuk subnet dengan rute lalu lintas yang berbeda.

## Jenis
Ada dua jenis tabel rute: default dan kustom. 
- **Default route table** (Tabel rute default): saat Anda membuat VPC, sistem secara otomatis menghasilkan tabel rute default yang akan dihubungkan ke subnet yang dibuat nanti jika tidak ada tabel rute kustom yang dipilih. Anda tidak dapat menghapus tabel rute default, tetapi dapat menambahkan, menghapus, dan mengubah kebijakan perutean di dalamnya.
- **Custom route table** (Tabel rute kustom): Anda dapat membuat atau menghapus tabel rute kustom di VPC. Tabel rute kustom ini dapat dihubungkan ke semua subnet untuk menerapkan kebijakan perutean yang sama.
![](https://main.qcloudimg.com/raw/a86260ffb40bec52c9f64a307d956691.png)  
>?Anda dapat menghubungkan tabel rute saat [membuat subnet](https://intl.cloud.tencent.com/document/product/215/31806), atau [mengubah tabel rute](https://intl.cloud.tencent.com/document/product/215/40090) setelah subnet dibuat.
>

## Kebijakan Perutean
Tabel rute mengontrol rute lalu lintas dengan menggunakan kebijakan perutean. Kebijakan perutean terdiri dari tujuan, jenis hop selanjutnya, dan hop selanjutnya.
- **Destination** (Tujuan): menentukan rentang IP tujuan yang Anda inginkan untuk meneruskan lalu lintas. Tujuan harus berupa rentang IP. Jika Anda ingin memasukkan satu alamat IP, atur mask ke `32` (misalnya, `172.16.1.1/32`). Tujuan tidak boleh berupa rentang IP untuk VPC tempat tabel rute, karena rute lokal telah mengizinkan interkoneksi jaringan pribadi di VPC ini.
>?Jika Anda telah men-deploy [layanan TKE](https://intl.cloud.tencent.com/document/product/457/6759) di VPC, tujuan yang Anda konfigurasikan dalam kebijakan perutean subnet VPC tidak boleh berada dalam blok CIDR VPC atau berisi rentang IP TKE.
>Misalnya, jika blok CIDR VPC adalah `172.168.0.0/16` dan blok TKE CIDR adalah `192.168.0.0/16`, rentang IP tujuan tidak boleh berada dalam `172.168.0.0/16`, atau berisi `192.168 .0.0/16` saat Anda mengonfigurasi kebijakan perutean untuk subnet VPC.
>
- **Next-hop type** (Jenis hop selanjutnya): menunjukkan jalan keluar paket data untuk VPC. Jenis VPC hop selanjutnya mendukung **NAT Gateway** (NAT Gateway), **Peering connection** (Peering connection), **VPN gateway** (VPN gateway), **Direct connect gateway** (Direct connect gateway), **CVM** (CVM), dan lainnya.
- **Next hop** (Hop selanjutnya): menentukan instans hop selanjutnya (diidentifikasi dengan ID hop selanjutnya) yang menjadi tujuan penerusan lalu lintas, seperti NAT Gateway di VPC.


### Prioritas kebijakan perutean
Ketika ada beberapa kebijakan perutean dalam tabel rute, prioritas perutean berikut berlaku, dari tinggi ke rendah:
- Lalu lintas dalam VPC: lalu lintas dalam VPC dicocokkan terlebih dahulu.
- Rute yang sama persis (pencocokan awalan terpanjang): ketika ada beberapa rute di tabel rute yang dapat cocok dengan IP tujuan, rute dengan mask terpanjang (persis) dicocokkan untuk menentukan hop selanjutnya.
- IP Publik: jika tidak ada kebijakan perutean yang cocok, instans CVM dapat mengakses internet melalui alamat IP publiknya.
**Use case:** (Kasus penggunaan:)
Ketika subnet dihubungkan ke NAT Gateway, dan CVM di subnet memiliki IP publik (atau EIP), CVM mengakses internet melalui NAT Gateway secara default (karena prioritas rute yang sama persis lebih tinggi dari prioritas IP publik). Namun, Anda dapat mengatur kebijakan perutean untuk mengizinkan CVM mengakses internet menggunakan alamat IP publiknya. Untuk informasi detailnya, lihat [Menyesuaikan Prioritas NAT Gateway dan EIP](https://intl.cloud.tencent.com/document/product/1015/32734).

## ECMP 
Equal-cost Multipath Routing (ECMP) berarti ada beberapa rute dengan biaya yang sama ke satu tujuan. Teknologi perutean tradisional hanya menggunakan satu jalur untuk mentransfer paket ke tujuan yang sama, sedangkan jalur yang tersisa dalam status siaga atau tidak valid. Ketika jalur gagal, perlu waktu untuk menggunakan jalur lain. Sebaliknya, ECMP menggunakan beberapa rute dengan biaya yang sama di lingkungan jaringan untuk meningkatkan bandwidth transmisi, menyeimbangkan lalu lintas melalui beberapa rute, dan mencapai pencadangan dengan tautan yang berlebihan.

VPC mendukung ECMP untuk jenis rute yang sama, seperti yang dijelaskan secara mendetail di bawah ini.

| Jenis hop selanjutnya     | Mendukung ECMP (jenis rute yang sama)  |  Jumlah maksimum ECMP |
| -------------- | ----------------------- | --------------------------- |
| NAT Gateway        | Tidak                       | T/A                 |
| IP publik CVM | Tidak                     | T/A                 |
| CVM       | Ya                    | 8       |
| Peering connection       | Tidak                     | T/A                 |
| Direct connect gateway       | Ya                     | 8       |
| CCN         | Tidak                    | T/A                 |
| HAVIP   | Ya                    | 8       |
| VPN gateway        | Ya                      | 8       |

<dx-alert infotype="explain" title="">
CCN mendukung satu ECMP dengan direct connect gateway atau peering connection.
</dx-alert>


### Kasus penggunaan
ECMP sering digunakan untuk menyeimbangkan beban lalu lintas melalui gateway dengan bandwidth terbatas. Asumsikan Anda memerlukan 2000 Mbps untuk menghubungkan bisnis berbasis VPC dan IDC Anda, tetapi bandwidth VPN maksimum saat ini adalah 1000 Mbps. Untuk mencapai tujuan, Anda dapat membuat dua VPN gateway 1000-Mbps dan dua tunnel VPN.

## Rute Primer/Sekunder
Rute primer/sekunder mengacu pada dua jalur atau lebih ke tujuan yang sama, dengan satu jalur aktif dan jalur siaga atau tidak valid. Asumsikan bahwa ada dua rute VPC ke IDC, yaitu jalur A dan jalur B. Semua paket dikirim ke tujuan melalui jalur A, sedangkan jalur B tidak valid atau siaga. Saat jalur A mengalami kegagalan penautan, Anda dapat mengaktifkan jalur B untuk mengambil alih lalu lintas dari jalur A, sehingga memastikan ketersediaan aplikasi. Dalam hal ini, jalur A dan B disebut rute primer dan sekunder.

Jenis hop selanjutnya menentukan prioritas rute. Saat menambahkan kebijakan perutean ke tabel rute VPC, Anda dapat mengonfigurasi berbagai jenis gateway untuk bertindak sebagai rute primer dan sekunder ke satu tujuan. Kemudian, pemeriksaan jaringan VPC dapat digunakan untuk memeriksa kualitas penautan dan aksesibilitas. Setelah mengonfigurasi kebijakan alarm, Anda dapat segera mendeteksi pengecualian penautan apa pun dan beralih antara rute primer dan sekunder dengan cepat untuk memenuhi persyaratan ketersediaan tinggi.
>?
>+ Fitur prioritas rute saat ini dalam versi beta. Untuk menggunakannya, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).
>+ Jenis hop selanjutnya menentukan prioritas rute di tabel rute VPC. Secara default, prioritas rute dari tingkat tinggi ke rendah adalah CCN, direct connect gateway, VPN gateway, dan lainnya.
>+ Saat ini, Anda tidak dapat menyesuaikan prioritas rute di konsol. Jika diperlukan, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).

Tabel berikut menjelaskan dukungan primer/sekunder dari berbagai jenis rute VPC.

| Jenis hop selanjutnya         | Dukungan untuk rute primer/sekunder                                            |
| ------------------ | ------------------------------------------------------- |
| NAT Gateway            | Tidak                                                      |
| IP publik CVM     | Tidak                                                      |
| CVM          | Ya, dengan CCN, VPN gateway, direct connect gateway, atau HAVIP  |
| Peering connection (dalam wilayah) | Tidak                                                      |
| Peering connection (lintas wilayah) | Tidak                                                      |
| Direct connect gateway          | Ya, dengan CCN, VPN gateway, HAVIP, atau CVM  |
| CCN          | Ya, dengan VPN gateway, direct connect gateway, HAVIP, atau CVM  |
| HAVIP          | Ya, dengan CCN, VPN gateway, direct connect gateway, atau CVM  |
| VPN gateway         | Ya, dengan CCN, direct connect gateway, HAVIP, atau CVM  |


### Kasus penggunaan
Rute primer/sekunder sering digunakan untuk meneruskan lalu lintas dengan lancar saat penautan gateway gagal.
+ Direct connect gateway (primer) berbasis VPC dan VPN gateway untuk VPC (sekunder)
  **Scenario** (Skenario): interkoneksikan Tencent Cloud VPC dan IDC lokal melalui direct connect gateway berbasis VPC. Sementara itu, buat tunnel VPN melalui VPN gateway untuk bertindak sebagai penautan komunikasi sekunder antara IDC dan VPC.
   ![](https://main.qcloudimg.com/raw/683779ec1aef376985b027df945fe54c.png)
+ Direct connect gateway (primer) berbasis CCN dan VPN gateway untuk VPC (sekunder)
  **Scenario** (Skenario): interkoneksikan Tencent Cloud VPC dan IDC lokal melalui instans CCN. Sementara itu, buat tunnel VPN melalui VPN gateway untuk bertindak sebagai penautan komunikasi sekunder antara IDC dan VPC.
	![](https://main.qcloudimg.com/raw/7e21527a285edb29c7e57df566723acb.png)
