
Dokumen ini menjelaskan operasi yang terkait dengan kebijakan perutean.

## Menambahkan Kebijakan Perutean
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan akses halaman **Route Table** (Tabel Rute).
2. Klik **ID/Name** (ID/Nama) dari tabel rute yang akan dimodifikasi untuk membuka halaman detailnya.
3. Klik **+New routing policies** (+Kebijakan perutean baru).
<img src="https://qcloudimg.tencent-cloud.cn/raw/38e0ec6462b9305afc0d3f7f0897fcde.png" width="80%">
4. Pada jendela pop-up, <span id="routeParam" />konfigurasikan kebijakan perutean.
>?Jika Anda telah men-deploy [layanan TKE](https://intl.cloud.tencent.com/document/product/457/6759) di VPC, tujuan yang Anda konfigurasikan dalam kebijakan perutean subnet VPC tidak boleh tumpang tindih dengan blok CIDR VPC atau rentang IP TKE. >Misalnya, jika blok CIDR VPC adalah `172.168.0.0/16` dan blok TKE CIDR adalah `192.168.0.0/16`, rentang IP tujuan tidak boleh berada dalam `172.168.0.0/16`, atau berisi `192.168 .0.0/16`.
>
><table><tbody>
><tr><th>Item Konfigurasi</th><th>Deskripsi</th></tr>
><tr><td>Tujuan</td><td>Menentukan rentang IP tujuan tempat Anda ingin meneruskan lalu lintas keluar subnet. Persyaratan untuk tujuan adalah sebagai berikut:
><ul><li>Masukkan rentang IP. Jika Anda ingin memasukkan satu IP, atur mask ke `32` (misalnya, `172.16.1.1/32`).</li>
><li>Tujuan tidak boleh berupa rentang IP VPC tempat tabel rute berada karena rute lokal telah mengizinkan interkoneksi jaringan pribadi di VPC ini.</li></ul>
>	</td></tr>
><tr><td>Jenis hop selanjutnya</td><td>Menunjukkan jalan keluar dari paket data untuk VPC. Jenis yang didukung:
>  <ul>
>     <li> NAT Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke NAT Gateway.</li>
>     <li>Peering Connections: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke pasangan VPC untuk peering connection.</li>
>     <li>Direct Connect Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke direct connect gateway.</li>
>    <li>IP Virtual Ketersediaan Tinggi: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke HAVIP.</li>
>    <li>VPN Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke VPN gateway.</li>
>    <li>IP publik CVM: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke IP publik (termasuk EIP) untuk instans CVM di VPC.</li>
>    <li>CVM: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke instans CVM di VPC.</li>
>    </ul>
> </td></tr>
><tr><td>Hop selanjutnya</td><td>Menentukan instans hop selanjutnya yang menjadi tujuan pengalihan lalu lintas, seperti gateway atau IP CVM.</td></tr>
><tr><td>Catatan</td><td>(Opsional) Anda dapat memasukkan deskripsi rute untuk pengelolaan sumber daya.</td></tr>
><tr><td>Tambahkan jalur</td><td>Anda dapat mengklik <b>+Tambahkan jalur</b> untuk mengonfigurasi beberapa kebijakan perutean, atau mengklik ikon penghapusan di kolom <b>Operasi</b> untuk menghapus kebijakan perutean yang tidak perlu.</td></tr>
></tbody> </table>
>
> <img src="https://qcloudimg.tencent-cloud.cn/raw/5d4e0dcde1c1a257298ea7fbdf15270a.png">
5. Klik **Create** (Buat).

## Mengedit Kebijakan Perutean
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan akses halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik **ID/Name** (ID/Nama) dari tabel rute target untuk membuka halaman detailnya.
3. Klik **Edit** (Edit) di kolom **Operation** (Operasi) dari kebijakan perutean untuk memodifikasinya.
![](https://main.qcloudimg.com/raw/6f817db7223a5f5f2ae146fc6a39d28b.png)
4. Setelah modifikasi, klik **OK** (OKE) untuk menyimpan atau **Cancel** (Batalkan) untuk menghapus hasil modifikasi.

## Memublikasikan/Menarik Kebijakan Perutean ke/dari CCN
Rute VPC yang dikaitkan dengan CCN dipublikasikan ke CCN secara default. Untuk kebijakan perutean kustom baru yang tidak dipublikasikan, Anda perlu memublikasikannya secara manual. Anda juga dapat menarik kebijakan perutean dari CCN.
Saat ini, hanya kebijakan perutean dengan **Next hop type** (Jenis hop selanjutnya) yang memiliki **High Availability Virtual IP** (IP Virtual Ketersediaan Tinggi) atau **CVM** (CVM) dalam tabel rute default atau kustom yang dapat dipublikasikan secara manual ke atau ditarik dari CCN.

### Prasyarat
VPC tempat HAVIP atau CVM berada dikaitkan dengan instans CCN.

### Petunjuk
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan akses halaman **Route Table** (Tabel Rute).
2. Klik **ID/Name** (ID/Nama) dari tabel rute yang akan dimodifikasi untuk membuka halaman detailnya.
3. Lakukan operasi berikut sesuai kebutuhan:
   + Klik **Publish to CCN** (Publikasikan ke CCN) untuk memublikasikan kebijakan perutean kustom secara manual ke CCN.
   + Klik **Withdraw from CCN** (Tarik dari CCN) untuk menarik kebijakan perutean kustom yang telah dipublikasikan ke CCN.
>!
>+ Kebijakan perutean yang dinonaktifkan tidak dapat dipublikasikan ke CCN.
>+ Kebijakan perutean tidak dapat dinonaktifkan setelah dipublikasikan ke CCN.


## Mengkueri dan Mengekspor Kebijakan Perutean
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan akses halaman **Route Table** (Tabel Rute).
2. Klik **ID/Name** (ID/Nama) dari tabel rute target untuk membuka halaman detailnya. Di halaman ini, Anda dapat melihat kebijakan perutean di tabel rute ini.
3. Pada kotak pencarian di kanan atas, Anda dapat mengkueri kebijakan perutean dengan memasukkan alamat tujuan.
![](https://qcloudimg.tencent-cloud.cn/raw/9be2e0939c90f89622a8e799e4b11ce6.png)
4. Klik **Export** (Ekspor) untuk menyimpan hasil pencarian dalam format .csv.

## Mengaktifkan/Menonaktifkan Kebijakan Perutean
Kebijakan perutean kustom dapat diaktifkan atau dinonaktifkan.
### Petunjuk
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=4), dan akses halaman **Route Table** (Tabel Rute).
2. Klik **ID/Name** (ID/Nama) dari tabel rute target untuk masuk ke halaman detailnya. Periksa status kebijakan perutean:
  + <img src="https://main.qcloudimg.com/raw/a142df25497e2ad5828a231dc17f5130.png" width="3%" />: diaktifkan
 + <img src="https://main.qcloudimg.com/raw/7c04cc17a33bd833f66627628aba31b7.png" width="3%" />: dinonaktifkan
3. Nonaktifkan kebijakan perutean: klik ikon <img src="https://main.qcloudimg.com/raw/a142df25497e2ad5828a231dc17f5130.png" width="3%" /> di samping kebijakan perutean untuk menonaktifkannya.
>!Menonaktifkan rute dapat mengakibatkan gangguan bisnis. Harap periksa kembali sebelum melanjutkan.
>
   <img src="https://qcloudimg.tencent-cloud.cn/raw/278ad06cfcdad1de0eb0aabd9b08bab8.png" width="50%" />
4. Aktifkan kebijakan perutean: klik ikon <img src="https://main.qcloudimg.com/raw/7c04cc17a33bd833f66627628aba31b7.png" width="3%" /> di samping kebijakan perutean untuk mengaktifkannya.
>! Setelah diaktifkan, rute dengan mask terpanjang akan digunakan. Hal ini dapat memengaruhi bisnis Anda saat ini. Harap periksa kembali sebelum melanjutkan.
>
 <img src="https://qcloudimg.tencent-cloud.cn/raw/c0fca3b5ddb0c6ba7e61e07470cd604a.png" width="50%" />
5. Aktifkan atau nonaktifkan beberapa kebijakan perutean: pilih kebijakan perutean target dan klik **Enable** (Aktifkan) atau **Disable** (Nonaktifkan) di atas daftar.
    ![](https://qcloudimg.tencent-cloud.cn/raw/1ea2f28cc53ed463f26edf7fdfd93640.png)

## Menghapus Kebijakan Perutean
Anda dapat menghapus kebijakan perutean yang tidak digunakan. Hanya kebijakan perutean kustom yang dapat dihapus.
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan akses halaman **Route Table** (Tabel Rute).
2. Klik **ID/Name** (ID/Nama) dari tabel rute yang akan dimodifikasi untuk membuka halaman detailnya.
3. Pilih kebijakan perutean yang akan dihapus, dan klik **Delete** (Hapus) di bawah kolom **Operation** (Operasi).
![](https://main.qcloudimg.com/raw/9ab1d9bcca75ba9f4cfdd4abfbddd58e.png)
4. Baca catatan dan klik **OK** (OKE).
<img src="https://qcloudimg.tencent-cloud.cn/raw/57035cab86a2e31d78477792548a7640.png" width="70%" />

