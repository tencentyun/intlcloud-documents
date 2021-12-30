Setiap VPC dapat memiliki satu blok CIDR utama, yang tidak dapat diubah setelah pembuatan VPC. Saat IP di blok CIDR utama tidak dapat memenuhi kebutuhan Anda, Anda dapat membuat beberapa blok CIDR sekunder untuk menambahkan rentang IP.
Anda dapat mengalokasikan subnet dengan rentang IP dari blok CIDR primer atau sekunder. Semua subnet dari VPC yang sama saling terhubung secara default, terlepas dari apakah mereka termasuk dalam blok CIDR primer atau sekunder.

## Batasan Penggunaan
+ CVM berbasis jaringan klasik tidak dapat terhubung dengan sumber informasi cloud di blok CIDR sekunder.
+ Peering connection tidak mendukung blok CIDR sekunder.
+ Cloud Connect Network, VPN gateway, dan standard direct connect gateway mendukung blok CIDR sekunder. Perhatikan batasan berikut untuk direct connect gateway:
  - Fitur ini tidak tersedia di wilayah Finance Cloud.
  - Hingga 10 blok CIDR sekunder dapat disebarkan.
  - Fitur ini tidak tersedia untuk NAT direct connect gateway.



## Membuat Blok CIDR Sekunder[](id:21)
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC**.
3. Di daftar VPC, temukan VPC dan pilih **More** > **Edit IPv4 CIDR block** (Lainnya > Edit blok CIDR IPv4) di bawah kolom **Operation** (Operasi).
4. Di kotak dialog pop-up, klik **Add** (Tambahkan) untuk memasukkan blok CIDR sekunder.
>!Blok CIDR sekunder dapat tumpang tindih dengan rentang IP tujuan dari rute kustom. Perhatikan bahwa blok CIDR sekunder menggunakan rute lokal, yang memiliki prioritas lebih tinggi daripada rute subnet kustom.
>
5. Klik **OK** (Oke).

## Menghapus Blok CIDR Sekunder[](id:32)
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC**.
3. Di daftar VPC, temukan VPC tempat blok CIDR sekunder akan dihapus, dan pilih **More** > **Edit IPv4 CIDR block** (Lainnya > Edit blok CIDR IPv4) di bawah kolom **Operation** (Operasi).
4. Di kotak dialog pop-up, klik **Delete** (Hapus) di sebelah blok CIDR sekunder.

5. Klik **OK** (Oke).
