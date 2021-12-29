## Skenario Operasi
Grup keamanan digunakan untuk menentukan apakah akan mengizinkan permintaan akses dari internet atau jaringan pribadi. Untuk pertimbangan keamanan, penolakan akses digunakan di arah masuk dalam banyak kasus. Jika Anda memilih templat "Buka semua port ke internet" atau "Buka port 22, 80, 443, dan 3389 dan protokol ICMP ke internet" saat membuat grup keamanan, sistem akan secara otomatis menambahkan aturan grup keamanan untuk beberapa port komunikasi berdasarkan templat yang dipilih. 

Dokumen ini menjelaskan cara menambahkan aturan grup keamanan guna mengizinkan atau melarang CVM dalam grup keamanan untuk mengakses internet atau instans VPC.

## Catatan

- Aturan grup keamanan dibagi menjadi aturan grup keamanan IPv4 dan IPv6.
- **Open all ports** (Buka semua port) berlaku untuk aturan grup keamanan IPv4 dan IPv6.

## Prasyarat
- Anda telah membuat grup keamanan. 
- Anda mengetahui permintaan akses internet atau jaringan pribadi yang perlu diizinkan atau ditolak untuk instans CVM Anda. - Untuk kasus penggunaan lainnya dari pengaturan aturan grup keamanan, lihat [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35519).

## Langkah
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di bilah sisi kiri, klik **[Security Group] (https://console.cloud.tencent.com/cvm/securitygroup)** (Grup Keamanan) untuk masuk ke halaman manajemen grup keamanan.
3. Pada halaman manajemen grup keamanan, pilih **Region** (Wilayah), dan temukan baris grup keamanan yang ingin Anda tetapkan aturannya.
4. Di kolom operasi, klik **Modify Rules** (Modifikasi Aturan).
5. <span id="step05">Pada halaman aturan grup keamanan, klik **Inbound rules** (Aturan masuk), dan pilih salah satu mode berikut berdasarkan kebutuhan aktual Anda untuk menyelesaikan operasi.</span>
> Contoh operasi berikut menggunakan mode 2 (aturan penambahan).
>
 - Mode 1 (buka semua port): berlaku untuk skenario dengan aturan protokol ICMP yang tidak perlu diatur dan operasi yang dapat dilakukan melalui port 22, 3389, 80, 443, 20, dan 21, serta protokol ICMP .
 - Mode 2 (aturan penambahan): berlaku untuk skenario dengan beberapa protokol komunikasi, seperti ICMP yang perlu diatur.
6. Pada jendela **Add Inbound Rules** (Tambahkan Aturan Masuk) yang muncul, tetapkan aturan.
Parameter utama yang diperlukan untuk menambahkan aturan adalah sebagai berikut:
 - Ketik: nilai default adalah "Custom" (Kustom). Anda juga dapat memilih templat aturan sistem lain, seperti "Login Windows", "Login Linux", "Ping", "HTTP (80)", atau "HTTPS (443)".
 - Sumber/Tujuan: sumber (aturan masuk) atau tujuan (aturan keluar) lalu lintas. Pilih salah satu opsi berikut:
<table>
	<tr><th>Sumber/Tujuan Tertentu</th><th>Deskripsi</th></tr>
	<tr><td>Alamat IPv4 atau rentang alamat IPv4</td><td>Tentukan dalam notasi CIDR (misalnya, <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, atau <code>0.0.0.0/0</code>, di mana <code>0.0.0.0/0</code> menunjukkan bahwa semua alamat IPv4 akan dicocokkan).</td></tr>
	<tr><td>Alamat IPv6 atau rentang alamat IPv6</td><td>Tentukan dalam notasi CIDR (misalnya, <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, di mana <code>::/0</code> atau <code>0::0/0</code> menunjukkan bahwa semua alamat IPv6 akan dicocokkan).</td></tr>
	<tr><td>Impor ID grup keamanan: Anda dapat mengimpor ID grup keamanan berikut:<ul  style="margin: 0;"><li>ID grup keamanan</li><li>Grup keamanan lain</li></ul>
</td><td><ul  style="margin: 0;"><li>Grup keamanan saat ini mengacu pada CVM yang terhubung ke grup keamanan.</li><li>Grup keamanan lain mengacu pada ID grup keamanan lain di proyek yang sama di wilayah yang sama.</li></ul>
</td></tr>
	<tr><td>Impor objek alamat IP atau objek grup alamat IP di <a href="https://intl.cloud.tencent.com/document/product/215/31867">templat parameter</a>.</td><td>-</td></tr>
</table>
 - Port protokol: masukkan jenis protokol dan rentang port, atau impor port protokol atau grup port protokol di [templat parameter](https://intl.cloud.tencent.com/document/product/215/31867).
 - Kebijakan: nilai defaultnya adalah "Permit" (Izinkan).
    - Permit (Izinkan): mengizinkan permintaan akses melalui port.
    - Reject (Tolak): menghapus paket data secara langsung tanpa mengembalikan respons apa pun.
 - Remarks (Keterangan): menjelaskan secara singkat aturan untuk memfasilitasi pengelolaan di masa mendatang.
7. <span id="step07">Klik **Finish** (Selesai). Aturan masuk ditambahkan ke grup keamanan.</span>
8. Pada halaman aturan grup keamanan, klik **Outbound Rules** (Aturan Keluar), dan tambahkan aturan keluar ke grup keamanan dengan merujuk ke [Langkah 5](#step05) ke [Langkah 7](#step07).
