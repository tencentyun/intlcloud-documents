Tabel rute terdiri dari beberapa kebijakan perutean yang mengontrol arah lalu lintas keluar subnet di VPC. Setiap subnet hanya dapat dihubungkan dengan satu tabel rute, sedangkan setiap tabel rute dapat dihubungkan dengan beberapa subnet. Anda dapat membuat beberapa tabel rute untuk subnet dengan rute lalu lintas yang berbeda.

## Jenis
Ada dua jenis tabel rute: default dan kustom. 
- **Default route table** (Tabel rute default): saat Anda membuat VPC, sistem secara otomatis membuat tabel rute default yang akan dihubungkan ke subnet yang dibuat nanti jika tidak ada tabel rute kustom yang dipilih. Anda tidak dapat menghapus tabel rute default, tetapi dapat menambahkan, menghapus, dan mengubah kebijakan perutean di dalamnya.
- **Custom route table** (Tabel rute kustom): Anda dapat membuat atau menghapus tabel rute kustom di VPC. Tabel rute kustom ini dapat dihubungkan ke semua subnet untuk menerapkan kebijakan perutean yang sama.
>?Anda dapat menghubungkan tabel rute saat [membuat subnet](https://intl.cloud.tencent.com/document/product/215/31806), atau [mengubah tabel rute](https://intl.cloud.tencent.com/document/product/215/40090) setelah subnet dibuat.

## Kebijakan Perutean
Tabel rute mengontrol rute lalu lintas dengan menggunakan kebijakan perutean. Kebijakan perutean terdiri dari tujuan, jenis hop selanjutnya, dan hop selanjutnya.
- **Destination** (Tujuan) : menentukan rentang IP tujuan yang Anda inginkan untuk meneruskan lalu lintas. Kebijakan harus berupa rentang IP. Jika Anda ingin memasukkan satu alamat IP, atur mask ke `32` (misalnya, `172.16.1.1/32`). Tujuan tidak boleh berupa rentang IP VPC tempat tabel rute, karena rute lokal telah mengizinkan interkoneksi jaringan pribadi di VPC ini.
>?Jika Anda telah men-deploy [Layanan TKE](https://intl.cloud.tencent.com/document/product/457/6759) di VPC, tujuan yang Anda konfigurasikan dalam kebijakan perutean subnet VPC tidak boleh berada dalam blok CIDR VPC atau berisi rentang IP TKE.
>Misalnya, jika blok CIDR VPC adalah `172.168.0.0/16` dan blok TKE CIDR adalah `192.168.0.0/16`, rentang IP tujuan tidak boleh berada dalam `172.168.0.0/16`, atau berisi `192.168 .0.0/16` saat Anda mengonfigurasi kebijakan perutean untuk subnet VPC.
- **Next-hop type** (Jenis hop selanjutnya): menunjukkan jalan keluar paket data untuk VPC. Jenis VPC hop selanjutnya mendukung **NAT Gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, dan lainnya.
- **Next hop** (Hop selanjutnya) : menentukan instans hop selanjutnya (diidentifikasi dengan ID hop selanjutnya) yang menjadi tujuan penerusan lalu lintas, seperti Gateway NAT di VPC.


### Prioritas kebijakan perutean
Ketika ada beberapa aturan perutean dalam tabel perutean, prioritas perutean berikut berlaku:
- Lalu lintas dalam VPC: lalu lintas dalam VPC dicocokkan terlebih dahulu.
- Perutean tepat (pencocokan awalan terpanjang): ketika ada beberapa rute di tabel rute yang dapat cocok dengan IP tujuan, rute dengan mask terpanjang (tepat) dicocokkan untuk menentukan hop selanjutnya.
- IP Publik: jika tidak ada kebijakan perutean yang cocok, instans CVM dapat mengakses internet melalui alamat IP publiknya.

**Use case:** (Kasus Penggunaan)
Ketika subnet dihubungkan ke NAT Gateway, dan CVM di subnet memiliki IP publik (atau EIP), CVM mengakses internet melalui NAT Gateway secara default (karena prioritas rute pencocokan tepat lebih tinggi dari prioritas IP publik). Namun, Anda dapat menetapkan kebijakan perutean untuk mengizinkan CVM mengakses internet menggunakan alamat IP publiknya. Untuk detailnya, lihat [Menyesuaikan Prioritas NAT Gateway dan EIP](https://intl.cloud.tencent.com/document/product/1015/32734).


