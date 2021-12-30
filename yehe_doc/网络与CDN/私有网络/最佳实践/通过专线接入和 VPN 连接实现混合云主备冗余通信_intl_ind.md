Jika bisnis Anda di-deploy di IDC lokal dan Tencent Cloud VPC, Anda dapat menghubungkannya melalui Direct Connect atau VPN. Untuk meningkatkan ketersediaan bisnis, Anda mengatur koneksi DC dan VPN dan mengonfigurasinya sebagai tautan primer dan sekunder untuk komunikasi yang berlebihan. Dokumen ini memandu Anda melalui cara mengonfigurasi koneksi DC dan VPN sebagai tautan primer/sekunder untuk menghubungkan IDC Anda ke cloud.
>?
>+ Fitur prioritas rute saat ini dalam uji beta. Untuk mencobanya, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).
>+ Jenis hop selanjutnya menentukan prioritas rute di tabel rute VPC. Secara default, prioritas rute dari tinggi ke rendah adalah CCN, direct connect gateway, VPN gateway, dan lainnya.
>+ Saat ini, Anda tidak dapat menyesuaikan prioritas rute di konsol. Jika diperlukan, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).



## Skenario
Anda telah men-deploy bisnis di Tencent Cloud VPC dan IDC. Untuk menghubungkannya, Anda perlu mengonfigurasi layanan koneksi jaringan untuk komunikasi ketersediaan tinggi sebagai berikut:
+ Direct Connect (utama): menghubungkan IDC lokal ke direct connect gateway berbasis VPC melalui koneksi. Saat hubungan koneksi normal, semua lalu lintas data antara IDC dan VPC diteruskan melalui koneksi.
+ VPN connection (sekunder): membuat tunnel VPN IPsec untuk menghubungkan IDC lokal dan Tencent Cloud VPC. Saat tautan koneksi gagal, lalu lintas akan diteruskan menggunakan tautan ini untuk memastikan ketersediaan bisnis.
![](https://main.qcloudimg.com/raw/c50965f32412860aec344f2cd0dabd6d.png)

## Prasyarat
+ Perangkat IDC gateway lokal Anda harus mendukung fitur IPsec VPN dan dapat bertindak sebagai gateway pelanggan untuk membuat tunnel VPN dengan VPN gateway.
+ Perangkat IDC gateway telah dikonfigurasi dengan alamat IP statis.
+ Contoh data dan konfigurasi:
  <table>
  <th colspan="3">Item konfigurasi</th>
   <th>Nilai sampel</th>
  <tr>
  <td rowspan="4">Jaringan</td>
  <td rowspan="2">Informasi VPC</td>
  <td>Blok CIDR subnet</td>
  <td>192.168.1.0/24 </td>
  </tr>
  <tr>
  <td>IP publik dari VPN gateway</td>
  <td>203.xx.xx.82</td>
  </tr>
  <tr>
  <td rowspan="2">Informasi IDC</td>
  <td>Blok CIDR subnet</td>
  <td>10.0.1.0/24</td>
  </tr>
	<tr>
	<td>IP publik dari gateway</td>
	<td>202.xx.xx.5</td>
	</tr>
	</table>
	

## Langkah
<dx-steps>
- [Hubungkan IDC ke VPC melalui Direct Connect](#langkah1)
- [Hubungkan IDC ke VPC melalui VPN connection](#langkah2)
- [Konfigurasikan probe jaringan](#langkah3)
- [Konfigurasikan kebijakan alarm](#langkah4)
- [Beralih antara rute primer dan sekunder](#langkah5)
  </dx-steps>

## Petunjuk

### [](id:step1)Langkah 1: sambungkan IDC ke VPC melalui Direct Connect
1. Login ke konsol Direct Connect dan buka [Tunnel Kustom](https://console.cloud.tencent.com/dc/dc) dan klik **Connections** (Koneksi) di bilah sisi kiri untuk membuat koneksi.
2. Login ke [Konsol VPC](https://console.intl.cloud.tencent.com/vpc/vpc?rid=4) dan klik **Direct Connect Gateway** (Direct Connect Gateway) di bilah sisi kiri. Klik **+New** (+Baru) untuk membuat direct connect gateway standar dengan **Associate Network** (Hubungkan Jaringan) **VPC**. Jika rentang IP IDC bertentangan dengan rentang IP VPC, pilih **NAT Type** (Jenis NAT).
3. Buka halaman **Dedicated Tunnels** (Tunnel Kustom) dan klik **+New** (+Baru) untuk membuat tunnel kustom. Masukkan nama tunnel, pilih jenis koneksi dan instans direct connect gateway yang baru saja dibuat. Konfigurasikan alamat IP di kedua sisi Tencent Cloud dan IDC, pilih rute statis, dan masukkan rentang IP CPE. Setelah konfigurasi selesai, klik **Download configuration guide** (Unduh panduan konfigurasi) dan selesaikan konfigurasi perangkat IDC seperti yang diinstruksikan dalam panduan.
4. Di tabel rute yang terhubung dengan subnet VPC untuk komunikasi, konfigurasikan kebijakan perutean dengan direct connect gateway sebagai hop selanjutnya dan rentang IP IDC sebagai tujuan.
>?Untuk konfigurasi detail, lihat [Memulai](https://intl.cloud.tencent.com/document/product/216/7557).


###  [](id:step2)Langkah 2: sambungkan IDC ke VPC melalui VPN connection
1. Login ke [Konsol VPN Gateway](https://console.cloud.tencent.com/vpc/vpnGw?rid=1) dan klik **+New** (+Baru) untuk membuat VPN gateway dengan **Associate Network** (Hubungkan Jaringan) sebagai **Virtual Private Cloud**.
2. Klik **Customer Gateway** (Gateway Pelanggan) di bilah sisi kiri dan klik **+New** (+Baru) untuk mengonfigurasi gateway pelanggan (objek logis dari VPN gateway di sisi IDC). Masukkan alamat IP publik gateway VPN di sisi IDC, seperti `202.xx.xx.5`.
3. Klik **VPN Tunnel** (Tunnel VPN) di bilah sisi kiri dan klik **+New** (+Baru) untuk menyelesaikan konfigurasi seperti kebijakan SPD, IKE, dan IPsec.
4. Konfigurasikan tunnel VPN yang sama dengan langkah 3 pada perangkat gateway lokal IDC untuk memastikan koneksi normal.
5. Di tabel rute yang terhubung dengan subnet VPC untuk komunikasi, konfigurasikan kebijakan perutean dengan VPN gateway sebagai hop selanjutnya dan rentang IP IDC sebagai tujuan.
>?Untuk petunjuk detail, lihat [Menghubungkan VPC ke IDC (Tabel Rute)](https://intl.cloud.tencent.com/document/product/1037/39675).
>

###  [](id:step3)Langkah 3: konfigurasikan probe jaringan
>?Setelah dua langkah pertama, ada dua rute VPC ke IDC. Artinya, direct connect gateway dan VPN gateway bertindak sebagai hop selanjutnya. Secara default, rute direct connect gateway memiliki prioritas lebih tinggi, menjadikannya jalur utama dan VPN gateway sebagai jalur sekunder.

Untuk tetap berada di atas kualitas koneksi primer/sekunder, konfigurasikan dua probe jaringan secara terpisah untuk memantau metrik utama seperti latensi dan tingkat kehilangan paket serta memeriksa ketersediaan rute primer/sekunder.
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/detection?rid=1).
2. Klik **+New** (+Baru) untuk membuat probe jaringan. Masukkan nama dan IP tujuan, pilih VPC dan subnet, dan atur **Source Next Hop** (Sumber Hop Selanjutnya) ke direct connect gateway.
3. Ulangi [langkah 2](#langkah2) dan atur **Source Next Hop** (Sumber Hop Selanjutnya) ke VPN gateway. Setelah konfigurasi selesai, Anda dapat memeriksa latensi jaringan probe dan tingkat kehilangan paket dari direct connect gateway dan VPN connection.
>? Untuk konfigurasi mendetail, lihat [Probe Jaringan](https://intl.cloud.tencent.com/document/product/215/35522).
>

### [](id:step4)Langkah 4: konfigurasikan kebijakan alarm
Anda dapat mengonfigurasi kebijakan alarm untuk tautan. Saat tautan memiliki pengecualian, Anda akan dikirim notifikasi alarm secara otomatis melalui email dan pesan SMS, memperingatkan Anda tentang risiko sebelumnya.
1. Login ke konsol CM dan buka halaman [**Alarm Policy** (Kebijakan Alarm)](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Klik **Create** (Buat). Masukkan nama kebijakan, pilih VPC/Network Probe untuk jenis kebijakan, tentukan instans probe jaringan sebagai objek alarm, dan konfigurasikan kondisi pemicu, notifikasi alarm, dan informasi lainnya. Kemudian klik **Complete** (Selesai).

### [](id:step5)Langkah 5: beralih antara rute primer dan sekunder
Setelah menerima alarm pengecualian tentang direct connect gateway, Anda harus menonaktifkan rute utama secara manual, dan meneruskan lalu lintas ke VPN gateway rute sekunder.
1. Login ke konsol VPC dan buka halaman [**Route Tables**(Tabel Rute)](https://console.cloud.tencent.com/vpc/route?rid=1).
2. Cari tabel rute yang terhubung dengan subnet VPC untuk komunikasi, klik **ID/Name** (ID/Nama) untuk masuk ke halaman detailnya. Klik <img src="https://main.qcloudimg.com/raw/af79ad3ab5488ea94ead43a8fba3486f.png" width="3%" /> untuk menonaktifkan rute utama dengan CCN sebagai hop selanjutnya. Kemudian lalu lintas VPC yang ditujukan ke IDC akan diteruskan ke VPN gateway, bukan ke direct connect gateway.
