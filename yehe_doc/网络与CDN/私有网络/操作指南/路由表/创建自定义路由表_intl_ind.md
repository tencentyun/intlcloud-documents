Tabel rute digunakan untuk mengontrol lalu lintas keluar dari subnet. Ini dapat berisi beberapa kebijakan perutean yakni, tabel rute default dan tabel rute kustom. Tabel rute default (rute lokal) memungkinkan interkoneksi jaringan pribadi di VPC, yang tidak dapat dihapus, tetapi dapat dikonfigurasi dengan kebijakan perutean dengan cara yang sama saat Anda mengonfigurasi tabel rute kustom. Dokumen ini menjelaskan cara membuat dan mengonfigurasi tabel rute kustom.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Klik **Route Tables** (Tabel Rute) di bilah sisi kiri untuk mengakses halaman pengelolaan.
3. Klik **+ New** (+ Baru).
4. Pada dialog pop-up, masukkan nama tabel rute, pilih VPC tempat tabel rute, dan konfigurasi kebijakan perutean.
    ![](https://main.qcloudimg.com/raw/8d001c82ce2c4ada7fba9a723a2b4e0c.png)
    
	>? Anda dapat mengonfigurasi kebijakan perutean saat membuat tabel rute. Atau, setelah tabel rute dibuat, Anda dapat mengeklik ID tabel rute untuk masuk ke halaman **Basic Information** (Informasi Dasar) dan klik **+ New routing policies** (+ Kebijakan perutean baru) untuk mengonfigurasi kebijakan perutean.
	>

	Mengonfigurasi kebijakan perutean [](id:routeParam):

<table><tbody>
<tr><th>Parameter</th><th>Deskripsi</th></tr>
<tr><td>Tujuan</td><td>Rentang IP tujuan tempat lalu lintas diteruskan. Konfigurasi harus memenuhi persyaratan berikut:
  <ul><li>Masukkan rentang IP. Jika Anda ingin memasukkan satu IP, atur mask ke 32 (misalnya, `172.16.1.1/32`).</li>
	<li>Tujuan tidak boleh berupa rentang IP VPC tempat tabel rute berada karena rute lokal telah mengizinkan interkoneksi jaringan pribadi di VPC ini.</li></ul>
	<p><b>Catatan:</b> Jika telah men-deploy <a href="https://intl.cloud.tencent.com/document/product/457/6759">Layanan TKE</a> di VPC, tujuan yang Anda konfigurasikan di kebijakan tabel rute subnet VPC tidak boleh berada dalam blok CIDR VPC atau berisi rentang IP TKE. Misalnya, jika blok CIDR VPC adalah `172.168.0.0/16` dan blok TKE CIDR adalah `192.168.0.0/16`, rentang IP tujuan tidak boleh berada dalam `172.168.0.0/16`, atau berisi `192.168 .0.0/16` saat Anda mengonfigurasi kebijakan perutean untuk subnet VPC.</note></td></tr>
<tr><td>Jenis hop selanjutnya</td><td>Jalur keluar dari paket data VPC. Berikut adalah jenis yang didukung:
 <ul>
<li> NAT Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke NAT Gateway.</li>
<li>Peering Connections: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke VPC di sisi lain koneksi peering.</li>
<li>Direct Connect Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke direct connect gateway.</li>
<li>IP Virtual Ketersediaan Tinggi: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke HAVIP.</li>
<li>VPN Gateway: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke VPN gateway.</li>
<li>IP publik CVM: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke IP publik (termasuk EIP) instans CVM di VPC.</li>
<li>CVM: lalu lintas yang diarahkan ke rentang IP tujuan diteruskan ke instans CVM di VPC.</li>
</ul>
</td></tr>
<tr><td>Hop selanjutnya</td><td>Menentukan instans hop selanjutnya yang menjadi tujuan pengalihan lalu lintas, seperti gateway atau IP CVM.</td></tr>
<tr><td>Catatan</td><td>Menjelaskan tujuan rute untuk pengelolaan sumber daya. Parameter ini bersifat opsional.</td></tr>
<tr><td>Tambahkan baris</td><td>: mengonfigurasi beberapa kebijakan perutean jika diperlukan. Anda dapat mengeklik ikon penghapusan di kolom **Operation** (Operasi) untuk menghapus kebijakan perutean yang tidak perlu. Tabel rute kustom setidaknya harus berisi satu kebijakan perutean.</td></tr>
</tbody> 
</table>

5. Setelah konfigurasi selesai, klik **Create** (Buat). Kemudian tabel rute akan ditampilkan dalam daftar.
![](https://main.qcloudimg.com/raw/c0e5611a3c21733e454ea0e7b8eb4430.png)

## Mengonfigurasi HAVIP
Saat ini, hanya kebijakan perutean dengan **Next hop type** (Jenis hop selanjutnya) yang memiliki **High Availability Virtual IP** (IP Virtual Ketersediaan Tinggi), **VPN Gateway**, atau **CVM** dalam tabel rute default atau kustom yang dapat dipublikasikan secara manual ke atau ditarik dari CCN.
1. Klik ID tabel rute untuk masuk ke halaman detail.
    ![](https://main.qcloudimg.com/raw/7f74257af9225a09dbbf3d2f2366c779.png)
2. Anda dapat melakukan operasi berikut sesuai kebutuhan:
    + Klik **Publish to CCN** (Publikasikan ke CCN) untuk memublikasikan kebijakan perutean yang diaktifkan ke CCN.
    + Klik **Withdraw from CCN** (Tarik dari CCN) untuk menarik kebijakan perutean kustom yang telah dipublikasikan ke CCN.
    + Klik **Edit** (Edit) untuk mengubah kebijakan perutean.
    + Klik **Delete** (Hapus) untuk menghapus kebijakan perutean yang dinonaktifkan.
