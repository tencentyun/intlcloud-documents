## Ikhtisar
Grup keamanan digunakan untuk mengatur lalu lintas ke dan dari jaringan publik dan pribadi. Demi keamanan, sebagian besar lalu lintas masuk ditolak secara default. Jika Anda memilih **Open all ports** (Buka semua port) atau **Open ports 22, 80, 443, 3389 and ICMP protocol** (Buka port 22, 80, 443, 3389, dan protokol ICMP) sebagai templat saat membuat grup keamanan, aturan akan otomatis dibuat dan ditambahkan ke grup keamanan untuk mengizinkan lalu lintas di port tersebut. Untuk informasi selengkapnya, harap lihat [Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

Dokumen ini menjelaskan cara menambahkan aturan grup keamanan untuk mengizinkan atau menolak lalu lintas ke dan dari jaringan publik atau pribadi.

## Catatan

- Aturan grup keamanan mendukung aturan IPv4 dan IPv6.
- **Open all ports** (Buka semua port) mengizinkan lalu lintas IPv4 dan IPv6.

## Prasyarat
- Anda harus memiliki grup keamanan yang ada. Jika tidak, lihat [Membuat Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34271) untuk detailnya.
- Anda harus mengetahui lalu lintas mana yang diizinkan atau ditolak untuk instans CVM Anda. Untuk informasi selengkapnya tentang aturan grup keamanan dan kasus penggunaannya, harap lihat [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/32369).

### Petunjuk
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Pilih [**Security Group**] (Grup Keamanan)(https://console.cloud.tencent.com/cvm/securitygroup) di bilah sisi kiri untuk mengakses halaman pengelolaan grup keamanan.
3. Pilih wilayah, dan temukan grup keamanan yang ingin Anda tetapkan aturannya.
4. Klik **Modify Rules** (Modifikasi Aturan) di kolom **Operation** (Operasi).
5. <span id="step05">Klik **Inbound rules** (Aturan masuk) dan pilih salah satu metode berikut untuk menambahkan aturan.</span>
![](https://main.qcloudimg.com/raw/e4c1f93fe75de51aa8de068da60a2206.png)
>? Petunjuk berikut menggunakan **Add a Rule** (Tambahkan aturan) sebagai contoh.
>
 - **Open all ports** (Buka semua port): metode ini ideal jika Anda tidak memerlukan aturan ICMP kustom dan semua lalu lintas melewati port 20, 21, 22, 80, 443, dan 3389 dan protokol ICMP.
 - **Add a Rule** (Tambahkan Aturan): metode ini ideal jika Anda perlu menggunakan beberapa protokol dan port selain yang disebutkan di atas.
6. Di jendela pop-up, tetapkan aturan.
![](https://main.qcloudimg.com/raw/0114aa46ffabc46dd9d6921095f6e8fa.png)
Konfigurasikan parameter berikut:
 - **Type** (Jenis): **Custom** (Kustom) dipilih secara default. Anda juga dapat memilih templat aturan sistem lain termasuk **Login Windows CVMs (3389)** (CVM Login Windows (3389)), **Login Linux CVMs (22)** (CVM Login Linux (22)), **Ping** (Ping), **HTTP (80)** (HTTP (80)), **HTTPS (443)** (HTTPS (443)), **MySQL (3306)** (MySQL (3306)), dan **SQL Server (1433)** (SQL Server (1433)).
 - **Source** (Sumber) atau **Destination** (Tujuan): sumber lalu lintas (aturan masuk) atau tujuan (aturan keluar). Anda perlu menentukan salah satu opsi berikut:
<table>
	<tr><th>Sumber atau Tujuan</th><th>Deskripsi</th></tr>
	<tr><td>Satu alamat IPv4 atau rentang IPv4</td><td>Dalam notasi CIDR, seperti <code>203.0.113.0</code>, <code>203.0.113.0/24</code> atau <code>0.0.0.0/0</code>, dimana <code>0.0.0.0/0</code> menunjukkan semua alamat IPv4 akan cocok.</td></tr>
	<tr><td>Satu alamat IPv6 atau rentang IPv6</td><td>Dalam notasi CIDR, seperti <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> atau <code>0::0/0</code>, dimana <code>::/0</code> atau <code>0::0/0</code> menunjukkan semua alamat IPv6 akan dicocokkan.</td></tr>
	<tr><td>ID grup keamanan yang dirujuk. Anda dapat merujuk ID dari:<ul  style="margin: 0;"><li>Grup keamanan saat ini</li><li>Grup keamanan lainnya</li></ul>
</td><td><ul  style="margin: 0;"><li>Untuk merujuk grup keamanan saat ini, masukkan ID grup keamanan yang terkait dengan CVM.</li><li>Anda juga dapat merujuk grup keamanan lain di wilayah yang sama dan milik ke proyek yang sama dengan memasukkan ID grup keamanan.</li></ul>
<blockquote class="d-mod-explain"><div class="d-mod-title d-explain-title"><i class="d-icon-explain"></i>Catatan:</div>
<p></p><ul>
<li>Grup keamanan yang dirujuk tersedia untuk Anda sebagai fitur lanjutan. Aturan grup keamanan yang dirujuk tidak ditambahkan ke grup keamanan saat ini.</li>
<li>Jika Anda memasukkan ID grup keamanan di **Source** (Sumber)/**Destination** (Tujuan) saat mengonfigurasi aturan grup keamanan, alamat IP pribadi instans CVM dan ENI yang terkait dengan ID grup keamanan ini akan digunakan sebagai sumber/tujuan. Hal ini tidak termasuk alamat IP publik.</li>
</ul>
</blockquote>
</td></tr>
	<tr><td>Merujuk objek alamat IP atau objek grup alamat IP dalam <a href="https://intl.cloud.tencent.com/document/product/215/31867">templat parameter</a>.</td><td>-</td></tr>
</table>
 - **Protocol port** (Port protokol): masukkan jenis protokol dan rentang port atau rujukan protokol/port atau grup protokol/port dalam [templat parameter](https://intl.cloud.tencent.com/document/product/215/31867). Jenis protokol yang didukung termasuk TCP, UDP, ICMP, ICMPv6 dan GRE dalam format berikut.
    - Port tunggal: seperti `TCP:80`.
    - Beberapa port: seperti `TCP:80,443`.
    - Jangkauan port: seperti `TCP:3306-20000`.
    - Semua port: seperti `TCP:ALL`.
 - **Policy** (Kebijakan): **Allow** (Izinkan) atau **Refuse** (Tolak). **Allow** (Izinkan) dipilih secara default.
    - Izinkan: lalu lintas ke port ini diizinkan.
    - Tolak: paket data akan dibuang tanpa respons apa pun.
 - **Notes** (Catatan): deskripsi singkat tentang aturan untuk pengelolaan yang lebih mudah.
7. <span id="step07">Klik **Complete** (Selesai) untuk menyelesaikan penambahan aturan.</span>
8. Untuk menambahkan aturan keluar, klik **Outbound rule** (Aturan keluar) dan lihat [Langkah 5](#step05) ke [Langkah 7](#step07).
