Anda dapat melihat sumber informasi semua subnet di VPC di konsol VPC, misalnya, sumber informasi cloud yang di-deploy di subnet, tabel rute yang terhubung dengan subnet, dan aturan ACL yang terikat ke subnet.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Subnet** di bilah sisi kiri untuk membuka halaman pengelolaan subnet.
3. Di bagian atas halaman **Subnet**, pilih wilayah dan VPC tempat subnet tersebut berada. Jika Anda mempertahankan nilai default, yaitu **All VPCs** (Semua VPC), Anda dapat melihat semua subnet dari semua VPC di wilayah ini, seperti yang ditampilkan di bawah ini:
![](https://main.qcloudimg.com/raw/56e17047ec183ee28d6ffcd5784ffcb3.png)
Arti dari daftar kolom yang ditampilkan di antarmuka adalah sebagai berikut:
 + ID/Nama: menampilkan ID dan nama subnet. Setiap subnet diberi ID saat dibuat, dan nama subnet dapat diubah secara real-time.
 + Jaringan: VPC tempat subnet berada.
 + CIDR: rentang IP blok CIDR dari subnet. Blok CIDR subnet tidak dapat diubah.
 + Zona Ketersediaan: menampilkan zona ketersediaan tempat subnet berada.
 + Tabel Rute yang Terhubung: tabel rute yang terhubung dengan subnet.
 + CVM: menampilkan jumlah CVM yang di-deploy di subnet.
 + IP yang Tersedia: jumlah alamat IP yang tersedia dalam rentang blok CIDR dari subnet.
 + Subnet Default: untuk subnet yang dibuat oleh pengguna di halaman **Subnet** di konsol VPC, yang bukan merupakan subnet default, kolom nilai akan menampilkan **No** (Tidak). Jika Anda memilih VPC default dan subnet yang dibuat secara otomatis oleh Tencent Cloud di halaman pembelian CVM, di sini akan muncul **Yes** (Ya). Hanya ada satu VPC dan subnet default di wilayah tertentu.
 + Waktu Pembuatan: waktu pembuatan subnet.
 + Operasi: operasi yang dapat dieksekusi untuk subnet. Anda dapat menghapus subnet tanpa sumber informasi, atau Anda dapat mengeklik **More** > **Change Route Table** (Lainnya > Ubah Tabel Rute) untuk mengganti tabel rute yang terhubung dengan subnet.
4. Klik ID subnet untuk melihat detail sumber informasi subnet. Ganti tab untuk melihat aturan perutean dan aturan ACL.
![](https://main.qcloudimg.com/raw/308eaf31ea4d3a1f92fbc868fa7ce699.png)
5. Klik ID VPC jaringan tempat subnet tersebut berada, atau ID tabel rute dari tabel rute yang terhubung untuk melihat informasi mendetail tentang sumber informasi terkait.
6. Klik jumlah CVM untuk membuka halaman instans CVM. Jika jumlahnya 0, klik ikon CVM untuk membuka halaman pembelian CVM.
7. Di bagian atas halaman, klik **Filter** untuk melihat daftar subnet di zona ketersediaan yang ditentukan.
8. Klik kotak pencarian di kanan atas halaman untuk membuat kueri dengan cepat berdasarkan **subnet ID**, **Subnet Name**, **Tag**, dan **IPv4 CIDR Block** (ID subnet, Nama Subnet, Tag, dan Blok CIDR IPv4).
9. Klik ikon Pengaturan di kanan atas untuk menyesuaikan kolom yang ditampilkan.

