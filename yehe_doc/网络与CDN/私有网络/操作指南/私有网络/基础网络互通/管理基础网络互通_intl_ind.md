## Membuat Classiclink
Classiclink menghubungkan CVM berbasis jaringan klasik dengan VPC untuk mengaktifkan interkoneksi antara VPC dan jaringan klasik. Hal ini memungkinkan CVM berbasis jaringan klasik berkomunikasi dengan sumber daya VPC.
>?
>- IP pribadi dari CVM berbasis jaringan klasik terkait akan secara otomatis ditambahkan ke kebijakan lokal untuk tabel rute VPC. Hal ini memungkinkan interkoneksi tanpa perlu memodifikasi kebijakan perutean VPC secara manual.
>- Setelah CVM berbasis jaringan klasik dihubungkan dengan VPC, pengaturan ACL firewall dan jaringannya akan tetap efektif.


### Petunjuk
1.  Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2.  Pilih wilayah, dan klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3.  Klik tab **Classiclink** (Classiclink), lalu klik **+Associate with CVM** (+Hubungkan dengan CVM). 
![](https://main.qcloudimg.com/raw/ad9b76faac017dbc093b3710f0d5070b.png)
4.  Pada jendela pop-up, pilih CVM di jaringan klasik untuk dihubungkan dengan VPC dan klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/b99329129fc8de27dddfbe7897d59218.png)

## Melihat Classiclink
Anda dapat melihat daftar CVM berbasis jaringan klasik yang terhubung dengan VPC.
### Petunjuk
1.  Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2.  Pilih wilayah, dan klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3.  Klik tab **Classiclink** (Classiclink) untuk melihat daftar CVM berbasis jaringan klasik yang terhubung dengan VPC.
![](https://main.qcloudimg.com/raw/3b4e1ad2a860c35f89b42315e709d11f.png)
4.  Masukkan IP pribadi pada kotak pencarian di sudut kanan atas untuk menemukan CVM dengan cepat.

## Menghapus Classiclink[](id:release)
Tindakan ini akan memutuskan koneksi CVM berbasis jaringan klasik dari VPC dan menghentikan interkoneksinya.

### Petunjuk
1.  Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik ID VPC yang memerlukan Classiclink untuk mengakses halaman detail.
3.  Klik tab **Classiclink** (Classiclink), pilih CVM yang akan dibatalkan hubungannya dari daftar CVM berbasis jaringan klasik, lalu klik **Disassociate** (Batalkan Hubungan) di kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/156dd9a80b6923a96bb52e2d76b55993.png)
4.  Periksa kembali catatan, lalu klik **OK** (OKE).
5.  Untuk membatalkan hubungan beberapa CVM, Anda dapat memilih CVM ini untuk dibatalkan hubungannya dan klik **Disassociate** (Batalkan Hubungan) di atas daftar.
