Sebelum memulai perluasan jaringan dan pembangunan VPC, Anda perlu merencanakan jumlah dan rentang IP VPC yang sesuai dengan kebutuhan bisnis Anda.
- [Bagaimana Cara Merencanakan Kuantitas VPC?](#planVPC)
- [Bagaimana Cara Merencanakan Kuantitas Subnet?](#planSubnet)
- [Bagaimana Cara Merencanakan Rentang IP (Blok CIDR) VPC dan Subnet?](#planCIDR)
- [Bagaimana Cara Merencanakan Kuantitas Tabel Rute?](#planRoute)
- [Bagaimana Cara Merencanakan Jaringan Cloud Hibrida Multi-pusat Lintas Wilayah?](#planExample)

<span id="planVPC"  ></span>
## Bagaimana Cara Merencanakan Kuantitas VPC?

- **Planning one VPC** (Merencanakan satu VPC)
Jika Anda memiliki bisnis skala kecil yang di-deploy di wilayah yang sama tanpa memerlukan isolasi jaringan, sebaiknya Anda merencanakan satu VPC.
Anda dapat membuat beberapa subnet dan tabel rute dalam satu VPC untuk pengelolaan lalu lintas yang mendetail. Selain itu, kami merekomendasikan Anda men-deploy subnet di zona ketersediaan yang berbeda untuk pemulihan bencana AZ.
![](https://main.qcloudimg.com/raw/22c3ea70430c6eaf50c994f5cb5923bc.png)
- **Planning multiple VPCs** (Merencanakan beberapa VPC)
Kami merekomendasikan Anda untuk merencanakan beberapa VPC dalam salah satu skenario berikut:
 - **Your business is deployed in multiple regions** (Bisnis Anda di-deploy di beberapa wilayah)
Jika bisnis Anda di-deploy di beberapa wilayah, Anda perlu merencanakan beberapa VPC dan men-deploy setidaknya satu di setiap wilayah karena VPC tidak dapat di-deploy di seluruh wilayah.
Secara default, VPC tidak saling berhubungan. Untuk saling menghubungkan VPC, gunakan [peering connection](https://intl.cloud.tencent.com/document/product/553) atau [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
![](https://main.qcloudimg.com/raw/8e08edafd53646887f337be56836e56c.png)
 - **Multiple businesses are deployed in the same region and require isolation** (Beberapa bisnis di-deploy di wilayah yang sama dan memerlukan isolasi)
Jika Anda memiliki beberapa bisnis yang di-deploy di wilayah yang sama dan bisnis ini harus diisolasi satu sama lain, Anda perlu merencanakan beberapa VPC dan men-deploy satu VPC untuk setiap bisnis. Melakukan hal ini dapat mengisolasi bisnis karena VPC tidak saling terhubung secara default.
![](https://main.qcloudimg.com/raw/ec02b9e821f2a723a3e2d90bfab553bb.png)

<span id="planSubnet" ></span>
## Bagaimana Cara Merencanakan Kuantitas Subnet?
- Satu VPC dapat memiliki beberapa (100 secara default) subnet. Subnet yang berbeda dalam VPC yang sama dapat berkomunikasi satu sama lain melalui jaringan pribadi secara default.
- Untuk mencapai pemulihan bencana di seluruh zona ketersediaan, kami merekomendasikan Anda membuat setidaknya dua subnet di zona ketersediaan yang berbeda untuk VPC.

<span id="planCIDR"></span>
## Bagaimana Cara Merencanakan Rentang IP (Blok CIDR) VPC dan Subnet?

**Once set, the IP range masks of VPCs and subnets cannot be modified.** (Setelah diatur, mask rentang IP VPC dan subnet tidak dapat dimodifikasi.) Dengan demikian, pastikan untuk merencanakan VPC dan subnet dengan cermat berdasarkan skala bisnis dan skenario komunikasi Anda. Ini akan memfasilitasi penskalaan dan operasi yang lancar di masa mendatang.
#### Merencanakan rentang IP VPC
- **You can use any of the following IP ranges as your VPC IP ranges:** (Anda dapat menggunakan salah satu rentang IP berikut sebagai rentang IP VPC Anda:)
 - **10.0**.0.0 - **10.255**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))
 - **172.16**.0.0 - **172.31**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))
 - **192.168**.0.0 - **192.168**.255.255 (**the mask range must be 16 to 28** (rentang mask harus 16 hingga 28))
- **When planning VPC IP ranges, note that:** (Saat merencanakan rentang IP VPC, perhatikan bahwa:)
 - Jika Anda perlu membuat beberapa VPC yang berkomunikasi satu sama lain atau dengan IDC, pastikan rentang IP VPC tidak tumpang tindih.
 - Jika VPC Anda perlu berkomunikasi dengan jaringan klasik, rentang IP VPC yang Anda buat harus berada dalam `10.[0-47].0.0/16` (termasuk subset).
 - Setelah dibuat, blok CIDR dari VPC dan subnet tidak dapat diubah. Jika salah satu blok CIDR tidak mencukupi, Anda dapat [membuat blok CIDR tambahan](https://intl.cloud.tencent.com/document/product/215/31805).

#### Merencanakan rentang IP subnet
- **Subnet IP range** (Rentang IP Subnet) Anda dapat menggunakan rentang IP VPC atau sebagian darinya sebagai rentang IP subnet. Misalnya, jika rentang IP VPC adalah 10.0.0.0/16, rentang IP subnet dapat berada di antara 10.0.0.0/16-10.0.255.255/28.
- **Subnet size and IP capacity** (Ukuran subnet dan kapasitas IP): setelah dibuat, subnet tidak dapat diubah. Saat membuat subnet, pastikan rentang IP subnet dapat memenuhi kebutuhan bisnis Anda. Namun, Anda juga perlu mengontrol ukuran subnet, yang memungkinkan Anda membuat subnet untuk penskalaan nanti.
- **Business requirements** (Persyaratan bisnis): satu VPC dapat dibagi menjadi subnet berdasarkan segmen bisnis. Misalnya, Anda dapat men-deploy lapisan web, lapisan logis, dan lapisan data di subnet yang berbeda dan menggunakan [ACL jaringan](https://intl.cloud.tencent.com/document/product/215/31850) untuk mengimplementasikan kontrol akses.

>?
>- Jika VPC tempat subnet berada perlu berkomunikasi dengan VPC atau IDC lain, pastikan rentang IP subnet tidak tumpang tindih dengan rentang pasangan IP. Jika tidak, interkoneksi melalui jaringan pribadi mungkin gagal.
>- Jika rentang IP subnet tumpang tindih, Anda [mengubah subnet instans](https://intl.cloud.tencent.com/document/product/213/16565) dan menggunakan CCN, atau membuat VPC baru dan membeli CVM.

<span id="planRoute" ></span>
## Bagaimana Cara Merencanakan Kuantitas Tabel Rute?
Tabel rute digunakan untuk mengontrol arah lalu lintas dalam subnet. Setiap subnet hanya dapat diikat dengan satu tabel rute. Anda dapat menggunakan tabel rute default dan tabel rute kustom di VPC Tencent Cloud.
- **Planning one route table** (Merencanakan satu tabel rute)
Jika subnet yang berbeda di VPC Anda memiliki persyaratan yang sama atau serupa untuk arah lalu lintas, sebaiknya rencanakan satu tabel rute. Kemudian, Anda dapat membuat kebijakan perutean yang berbeda untuk mengontrol arah lalu lintas.
![](https://main.qcloudimg.com/raw/0fdd4b7616e92011e3fd9d8141bc49a4.png)
- **Planning multiple route tables** (Merencanakan beberapa tabel rute)
Jika subnet di VPC Anda memiliki persyaratan berbeda untuk arah lalu lintas, sebaiknya rencanakan beberapa tabel rute. Kemudian, Anda dapat mengikatnya ke subnet yang sesuai dan membuat kebijakan perutean untuk mengontrol arah lalu lintas.
![](https://main.qcloudimg.com/raw/6f13922803b6531e77cdeb983e27b01e.png)

<span id="planExample" ></span>
## Bagaimana Cara Merencanakan Jaringan Cloud Hibrida Multi-pusat Lintas Wilayah?
Jika Anda perlu membuat beberapa VPC yang berkomunikasi satu sama lain atau dengan IDC, pastikan rentang IP VPC tidak tumpang tindih dengan rentang pasangan IP.
Asumsikan Anda memiliki IDC lokal dengan rentang IP `10.1.0.0/16` di Chengdu, dan ingin membuat dua IDC cloud di Shanghai dan Beijing yang perlu berkomunikasi dengan IDC lokal Anda. Dalam hal ini, kami merekomendasikan Anda menggunakan `10.2.0.0/16` dan `10.3.0.0/16` sebagai rentang IP VPC dari dua IDC cloud di Shanghai dan Beijing masing-masing, untuk menghindari kegagalan komunikasi yang disebabkan oleh rentang IP yang tumpang tindih. Anda dapat mengaktifkan komunikasi antara IDC lokal dan IDC cloud dan antara IDC cloud menggunakan dua metode berikut.
- **Method 1:** (Metode 1:) menambahkannya ke CCN untuk mengimplementasikan interkoneksi melalui jaringan publik dan pribadi.
![](https://main.qcloudimg.com/raw/05d61e7d26768a3e539858ba51d90f31.png)
- **Method 2:** (Metode 2:) menggunakan Direct Connect untuk menghubungkan IDC cloud di Shanghai dan Beijing ke IDC lokal di Chengdu, sehingga memungkinkan komunikasi antara IDC lokal dan IDC cloud. Untuk mengaktifkan komunikasi antara IDC cloud di Shanghai dan Beijing, gunakan peering connection untuk menghubungkan VPC yang sesuai.
![](https://main.qcloudimg.com/raw/cba1d5751f6e7f6fce991b9ed3877bf9.png)

**Suggestions for multi-VPC use cases:** (Saran untuk kasus penggunaan multi-VPC:)
- Coba rencanakan rentang IP yang berbeda untuk setiap VPC.
- Coba rencanakan rentang IP yang berbeda untuk subnet VPC jika setiap VPC tidak dapat memiliki rentang IP yang berbeda.
- Pastikan bahwa rentang IP subnet yang perlu berkomunikasi berbeda jika setiap subnet tidak dapat memiliki rentang IP yang berbeda.

## Dokumentasi
- Untuk informasi selengkapnya tentang cara cepat membangun Virtual Private Cloud (VPC) dengan blok CIDR IPv4, termasuk membuat VPC dan subnet, membeli CVM, dan mengikat EIP untuk mengaktifkan akses jaringan publik, lihat [Membangun VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
