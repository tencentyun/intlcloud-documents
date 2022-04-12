Tutorial ini akan menjelaskan cara cepat membuat Virtual Private Cloud (VPC) dengan blok CIDR IPv4.
## Ikhtisar
Dokumen ini akan memandu seluruh proses penyiapan VPC berbasis IPv4. 
![](https://qcloudimg.tencent-cloud.cn/raw/926843feffd998e8dbf151b63178b366.png)

## Prasyarat
Pastikan Anda telah [mendaftar akun Tencent Cloud](https://intl.cloud.tencent.com/register) dan menyelesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629) jika Anda perlu membeli sumber daya apa pun di daratan Tiongkok.

## Petunjuk
### Langkah 1: buat VPC dan subnet
>? Setelah membuat VPC dan subnet, Anda tidak dapat mengubah blok CIDR-nya. Dengan demikian, selesaikan [perencanaan jaringan](https://intl.cloud.tencent.com/document/product/215/31795) terlebih dahulu.
>
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas dan klik **+New** (+Baru).
3. Di jendela pop-up **Create VPC** (Buat VPC), konfigurasikan informasi VPC dan subnet seperti yang diinstruksikan di bawah ini.
![](https://qcloudimg.tencent-cloud.cn/raw/ba0387f51ed8112ab819d5cb9c5113b5.png)
 - **VPC Information** (Informasi VPC)
    - Nama: nama VPC.
    - Blok CIDR IPV4: Anda dapat memilih salah satu dari rentang IP **10.0**.0.0 - **10.255**.255.255, **172.16**.0.0 - **172.31**.255.255, dan 
    **192.168**.0.0 - **192.168**.255.255 sebagai rentang IP VPC. Rentang mask harus 16 hingga 28, seperti `10.0.0.0/16`.
     - Opsi Lanjutan: Anda dapat menambahkan tag secara opsional untuk membantu Anda mengelola izin sumber daya sub-pengguna dan kolaborator dengan lebih baik.
  - **Subnet information** (Informasi subnet)
    -  Blok CIDR IPv4:
		- Anda dapat memilih rentang IP di dalam atau sama dengan rentang IP VPC. Misalnya, jika rentang IP VPC adalah 10.0.0.0/16, Anda dapat memilih rentang IP antara 10.0.0.0/16 dan 10.0.255.255/28 sebagai rentang IP subnet.
		- Jika VPC tempat subnet berada perlu berkomunikasi dengan VPC atau IDC lain, pastikan rentang IP subnet tidak tumpang tindih dengan rentang pasangan IP. Jika tidak, interkoneksi melalui jaringan pribadi mungkin gagal.
    - Zona Ketersediaan: pilih zona ketersediaan tempat subnet berada. VPC memungkinkan subnet di zona ketersediaan yang berbeda, dan subnet ini dapat berkomunikasi satu sama lain melalui jaringan pribadi secara default.
    - Opsi Lanjutan: Anda dapat menambahkan tag secara opsional untuk membantu Anda mengelola izin sumber daya sub-pengguna dan kolaborator dengan lebih baik.

### Langkah 2: beli instans CVM
1. Masuk ke [Konsol CVM](https://console.cloud.tencent.com/cvm) untuk membuat instans CVM di VPC yang dibuat pada langkah sebelumnya.
2. Klik **Create** (Buat) di sudut kiri atas halaman daftar untuk mengakses halaman pembelian CVM.
<img src="" width="80%">
3. Pada halaman konfigurasi kustom, konfigurasikan instans CVM lalu klik **Buy Now** (Beli Sekarang). Konfigurasi jaringan CVM adalah sebagai berikut:
 - Jaringan: pilih VPC dan subnet yang dibuat.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec59dbff60a37870ef4f9cdaf2aff70.png)
 - Bandwidth jaringan publik: jangan centang <img src="https://main.qcloudimg.com/raw/50eef42428eb34dc35cf40995c9b7736.png" style="margin:-3px 0">.
![](https://qcloudimg.tencent-cloud.cn/raw/f59fd4da95bd18e3f8585a1541d7547b.png)
 - Grup Keamanan: pilih **New security group** (Grup keamanan baru) dan konfigurasikan seperti yang diinstruksikan di [Mengonfigurasi Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/15377).
![](https://qcloudimg.tencent-cloud.cn/raw/72584971b62015e38c9ad22da7ddd3d4.png)

### Langkah 3: terapkan untuk EIP dan ikat ke instans CVM
IP Elastis (EIP) adalah alamat IP publik yang dapat diterapkan dan dibeli secara mandiri. Anda dapat mengikatnya ke instans CVM untuk mengaktifkan akses jaringan publik.
1. Login ke [Konsol EIP](https://console.cloud.tencent.com/cvm/eip).
2. Pada halaman **EIP** (EIP), pilih wilayah tempat CVM berada. Klik **Apply** (Terapkan) di sudut kiri atas.
3. Di jendela **Apply for EIP** (Terapkan untuk EIP), konfigurasikan parameter yang relevan dan klik **OK** (Oke).
4. Pada halaman **EIP** (EIP), cari EIP yang Anda terapkan, dan klik **More** (Lainnya) > **Bind** (Ikat) di bawah kolom **Operation**  (Operasi).
5. Di jendela **Bind resources** (Ikat sumber daya), pilih **CVM Instances** (Instans CVM) sebagai jenis sumber daya yang akan diikat, pilih instans CVM, dan klik **OK** (Oke).
![]()
6. Di jendela konfirmasi pop-up, klik **OK** (Oke).


### Langkah 4: uji konektivitas jaringan publik
Selesaikan operasi berikut untuk menguji konektivitas jaringan publik instans CVM.
>?Sebelum melakukan pengujian, pastikan grup keamanan mengizinkan akses ke alamat IP dan port yang sesuai. Misalnya, protokol ICMP dibuka, dan server dapat di-ping melalui jaringan publik. Untuk informasi selengkapnya, lihat [Melihat Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35514).
>
1. Login ke instans CVM dengan EIP terikat. Untuk petunjuk mendetail, lihat [Login dan Akses Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
2. Jalankan perintah `ping <public IP address>`, seperti `ping www.qq.com` untuk menguji konektivitas jaringan publik.
![](https://main.qcloudimg.com/raw/e19b0921e6d0471ca0e9b78923ccdd06.png)

