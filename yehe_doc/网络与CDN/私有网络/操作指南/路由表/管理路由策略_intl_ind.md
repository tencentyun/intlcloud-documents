Kebijakan perutean dalam tabel rute dapat dioperasikan secara real-time. Beberapa tindakan kebijakan perutean yang tersedia adalah menambahkan, menghapus, membuat kueri, mengekspor, atau memublikasikan dan menarik ke/dari CCN. Dokumen ini menjelaskan semua operasi yang disebutkan di atas dari kebijakan perutean.

## Menambahkan Kebijakan Perutean
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan pilih **[Route Tables] (Tabel Rute)(https://console.cloud.tencent.com/vpc/route?rid=1)** di bilah sisi kiri untuk membuka halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik ID tabel rute yang akan diubah untuk menuju halaman detail.
3. Klik **+New routing policies** (+Kebijakan perutean baru).
4. Pada jendela pop-up, <span id="routeParam" />konfigurasi kebijakan perutean.
 >? Jika telah men-deploy <a href="https://int/product/457/6759">Layanan TKE</a> di VPC, saat Anda mengonfigurasi kebijakan perutean tabel rute untuk subnet VPC, tujuan tidak boleh berada dalam rentang blok CIDR dari VPC, juga tidak dapat berisi rentang IP kontainer. Misalnya, jika blok CIDR VPC adalah 172.168.0.0/16 dan blok CIDR jaringan kontainer adalah 192.168.0.0/16, saat Anda mengonfigurasi kebijakan perutean untuk subnet VPC, rentang IP tujuan tidak boleh berada di kisaran 172.168. 0.0/16, dan tidak boleh berisi 192.168.0.0/16.
 >
  <table><tbody>
   <tr><th>Item Konfigurasi</th><th>Deskripsi</th></tr>
   <tr><td>Tujuan</td><td>Rentang IP tujuan yang Anda inginkan untuk meneruskan lalu lintas keluar subnet. Persyaratannya adalah sebagai berikut:
    <ul><li>Rentang IP tujuan hanya boleh dalam format rentang IP. Jika ingin tujuan berupa IP tunggal, atur mask ke 32 (misalnya, 172.16.1.1/32).</li>
	  <li>Tujuan tidak boleh berupa rentang IP di VPC tempat tabel perutean karena perutean lokal telah mengindikasikan bahwa jaringan pribadi terhubung di VPC ini secara default.</li></ul>
    	</td></tr>
    <tr><td>Jenis hop selanjutnya</td><td>Jalur keluar dari paket data VPC. Berikut adalah jenis yang didukung:
        <ul>
           <li> NAT Gateway: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke NAT Gateway.</li>
           <li>Peering Connections: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke VPC di ujung koneksi peering lainnya.</li>
           <li>Direct Connect Gateway: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke direct connect gateway.</li>
          <li>IP Virtual Ketersediaan Tinggi: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke IP virtual ketersediaan tinggi.</li>
          <li>VPN Gateway: lalu lintas yang ditujukan untuk rentang IP tujuan diteruskan ke VPN Gateway.</li>
          <li>IP publik CVM: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke IP publik dari instans CVM di VPC (termasuk IP publik dan IP elastis).</li>
          <li>CVM: lalu lintas yang ditetapkan untuk rentang IP tujuan diteruskan ke instans CVM di VPC.</li>
          </ul>
       </td></tr>
   <tr><td>Hop selanjutnya</td><td>Menentukan instans hop selanjutnya yang akan dialihkan, seperti gateway atau IP CVM.</td></tr>
    <tr><td>Catatan</td><td>Anda dapat menyesuaikan deskripsi rute untuk pengelolaan sumber daya.</td></tr>
    <tr><td>Tambahkan jalur</td><td>Anda dapat mengeklik <b>+Tambahkan jalur</b> untuk mengonfigurasi beberapa kebijakan perutean, atau mengeklik ikon penghapusan di kolom <b>Operasi</b> untuk menghapus kebijakan perutean yang tidak perlu.</td></tr>
     </tbody> </table>
5. Klik **Complete** (Selesai) untuk menyelesaikan pembuatan.

## Memublikasikan Kebijakan Perutean ke CCN/Menarik Kebijakan Perutean dari CCN
Untuk instans VPC atau VPN yang terhubung dengan CCN, rute dipublikasikan ke CCN secara default. Untuk kebijakan perutean kustom baru yang tidak dipublikasikan ke CCN secara default, Anda harus memublikasikannya secara manual. Kebijakan perutean yang dipublikasikan secara manual atau dipublikasikan secara default dapat ditarik dari CCN.
Saat ini, hanya kebijakan perutean dengan **Next hop type** (Jenis hop selanjutnya) yang **High Availability Virtual IP** (IP Virtual Ketersediaan Tinggi), **VPN Gateway**, atau **CVM** di tabel rute (termasuk tabel rute default dan tabel rute kustom) dapat dipublikasikan secara manual ke CCN/ditarik dari CCN.

### Prasyarat
VPC tempat IP virtual dengan ketersediaan tinggi, VPN gateway, dan CVM telah dihubungkan ke CCN.

### Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan pilih **[Route Tables] (Tabel Rute)(https://console.cloud.tencent.com/vpc/route?rid=1)** di bilah sisi kiri untuk membuka halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik ID tabel rute yang akan diubah untuk menuju halaman detail.
   ![](https://main.qcloudimg.com/raw/351e5dec96293642293015fcebdc3ba5.png)
3. Anda dapat melakukan operasi berikut sesuai kebutuhan:
   + Untuk kebijakan perutean kustom, Anda dapat mengeklik **Publish to CCN** (Publikasikan ke CCN) untuk memublikasikan kebijakan perutean ini secara manual ke CCN.
   + Untuk kebijakan perutean kustom yang telah dipublikasikan ke CCN, Anda dapat mengeklik **Withdrawn from CCN** (Ditarik dari CCN) untuk mengklaim kembali kebijakan tersebut.
   + Klik **Edit** (Edit) untuk mengubah kebijakan perutean.
 >?
 >> Saat kebijakan perutean dinonaktifkan, kebijakan tersebut tidak dapat dipublikasikan ke CCN.
 >> Kebijakan perutean tidak dapat dinonaktifkan setelah dipublikasikan ke CCN.

## Mengedit Kebijakan Perutean
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan pilih **[Route Tables] (Tabel Rute)(https://console.cloud.tencent.com/vpc/route?rid=1)** di bilah sisi kiri untuk membuka halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik ID tabel rute untuk membuka halaman detail.
3. Klik **Edit** di sebelah kanan kebijakan perutean untuk memodifikasinya.
![](https://main.qcloudimg.com/raw/6f817db7223a5f5f2ae146fc6a39d28b.png)
4. Klik **OK** untuk menyelesaikan modifikasi, atau klik **Cancel** (Batal) untuk membatalkan modifikasi.

## Mengkueri dan Mengekspor Kebijakan Perutean
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan pilih **[Route Tables] (Tabel Rute)(https://console.cloud.tencent.com/vpc/route?rid=1)** di bilah sisi kiri untuk membuka halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik ID tabel rute untuk membuka halaman detail. Anda dapat menemukan kebijakan perutean di tabel rute ini.
3. Pada kotak pencarian di kanan atas, Anda dapat mengkueri kebijakan perutean dengan memasukkan alamat tujuan.
![](https://main.qcloudimg.com/raw/0fb54a38484b8525e5cdd9fdc904a183.png)
4. Klik **Export** (Ekspor) untuk mengekspor kebijakan perutean dalam daftar, dan menyimpannya dalam format .csv.

## Menghapus Kebijakan Perutean
Anda dapat menghapus kebijakan perutean yang tidak perlu. Hanya kebijakan perutean kustom yang dapat dihapus.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/route?rid=1), dan pilih **[Route Tables] (Tabel Rute)(https://console.cloud.tencent.com/vpc/route?rid=1)** di bilah sisi kiri untuk membuka halaman **Route Table** (Tabel Rute).
2. Dalam daftar, klik ID tabel rute yang akan diubah untuk menuju halaman detail.
3. Klik **Delete** (Hapus) di sebelah kanan kebijakan perutean yang ingin Anda hapus.
![](https://main.qcloudimg.com/raw/9ab1d9bcca75ba9f4cfdd4abfbddd58e.png)
4. Harap pastikan bahwa Anda mengetahui kemungkinan dampak penghapusan kebijakan perutean, lalu klik **OK** (OKE).
