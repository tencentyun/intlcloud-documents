Setelah nama domain Anda terhubung ke CDN, Anda akan menerima nama domain CNAME berakhiran `.cdn.dnsv1.com`, yang dapat dilihat di [Pengelolaan Domain](https://console.cloud.tencent.com/cdn/domains) page in the CDN console.Agar nama domain CNAME dapat diakses, Anda harus menyelesaikan konfigurasi CNAME di penyedia layanan nama domain terlebih dahulu.Ketika konfigurasi aktif, Anda dapat menggunakan layanan akselerasi CDN.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Petunjuk Konfigurasi

Dokumen ini memberikan petunjuk konfigurasi CNAME di Tencent Cloud dan Alibaba Cloud:

- [Pengaturan di Tencent Cloud](#m1)
- [Pengaturan di Alibaba Cloud](#m2)

[](id:m1)
### Pengaturan di Tencent Cloud

> !Rekaman yang berlainan jenis memiliki prioritas berbeda-beda.Untuk host yang sama, beberapa jenis rekaman tidak bisa hadir bersamaan.Jenis CNAME bertentangan dengan jenis rekaman lainnya.Anda harus menghapus rekaman jenis lain agar dapat menambahkan rekaman CNAME.


1.Masuk ke [DNSpod](https://www.dnspod.com/Products/dns/list), klik nama domain yang diinginkan di tab **My Domains** (Domain Saya).
 
2.Klik **Add Records** (Tambahkan Rekaman), lalu konfigurasikan sesuai petunjuk berikut:
![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	
- **Host** (Host):Masukkan nama subdomain.Misalnya, jika Anda ingin menambahkan resolusi untuk `www.dnspod.com`, pilih **www** sebagai rekaman host.Jika Anda ingin menambahkan resolusi untuk `dnspod.com`, pilih **@**.
- **Type** (Jenis):Pilih **CNAME**.
- **Split Zone** (Zona Terpisah):PIlih **Default** (Default).DNSPod menawarkan berbagai opsi bagi zona untuk menetapkan rekaman ke pengguna tertentu.Untuk informasi selengkapnya, silakan baca [Deskripsi Zona Terpisah](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).
- **Value** (Nilai):Masukkan nama domain target (biasanya CNAME, misalnya, `xxx.xxx.com.cdn.dnsv1.com`).Setelah rekaman dihasilkan, biasanya tanda `.` akan otomatis ditambahkan ke nama domain.
- **Weight** (Bobot):Nilai rekaman yang berbeda di zona terpisah yang sama dari sebuah rekaman host dapat diatur dengan berbagai bobot sehingga resolusinya akan dikembalikan sesuai rasio bobotnya.
Masukkan integer antara 0 hingga 100.
- **MX**:Prioritas rekaman MX.Anda boleh membiarkannya kosong.
- **TTL**:TTL (Time to Live, Waktu untuk Tayang) menentukan lamanya meng-cache kueri atau konten.Semakin kecil nilainya, semakin singkat waktu untuk merekam perubahan agar aktif secara global.Nilai default adalah 600 detik.
3.Klik **Confirm** (Konfirmasikan) untuk menyelesaikan konfigurasi.

   

####  Pengaturan tambahan
- Untuk mengaktifkan layanan akselerasi bagi seluruh situs web, Anda dapat mengatur **Split Zone** (Zona Terpisah) dari rekaman host sebagai **Default** (Default).
Misalnya, jika Anda ingin mengarahkan semua pengguna ke `1.com`, Anda dapat mengonfigurasi rekaman CNAME dengan **Default** (Default) sebagai zona terpisah dan `1.com` sebagai nilai.
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)

- Anda juga dapat mengaktifkan layanan akselerasi untuk zona terpisah tertentu.
Misalnya, jika Anda ingin mengarahkan pengguna CMCC ke `1.com` dan pengguna CUCC ke `2.com`, Anda dapat mengonfigurasi dua rekaman CNAME: satu dengan **CMCC** sebagai zona terpisah dan `1.com` sebagai nilai, satunya lagi dengan **CUCC** sebagai zona terpisah dan `2.com` sebagai nilai.
![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

>?Untuk informasi selengkapnya tentang konfigurasi zona terpisah, silakan baca [Deskripsi Zona Terpisah](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).


[](id:m2)
### Pengaturan di Alibaba Cloud

Jika penyedia layanan DNS Anda adalah Alibaba Cloud, Anda dapat menambahkan rekaman CNAME sebagai berikut.

1.Masuk ke konsol Alibaba Cloud DNS.
2.Klik nama domain yang hendak diresolusi agar dapat masuk ke halaman rekaman resolusi.
3.Klik **Add Record** (Tambahkan Rekaman).
4.Untuk mengatur rekaman resolusi CNAME, pilih **CNAME** sebagai jenis rekaman.Masukkan rekaman host sesuai kebutuhan (misalnya, `www`), yang merupakan awalan nama domain.Masukkan nama domain yang ditunjukkan oleh nama domain saat ini sebagai nilai rekaman.Pertahankan pengaturan default untuk ISP Line dan TTL.
![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5.Terakhir, klik **Confirm** (Konfirmasikan).



## Memverifikasi Rekaman CNAME

Waktu yang dibutuhkan agar rekaman CNAME aktif berbeda-beda sesuai dengan penyedia layanan DNS.Biasanya berlangsung dalam 30 menit.Anda juga dapat memeriksa apakah rekaman CNAME sudah aktif dengan menjalankan `nslookup` atau `dig`.Jika tanggapan rekaman CNAME berupa CNAME terkonfigurasi, hal ini menunjukkan bahwa konfigurasinya berhasil dan akselerasinya aktif.

- `nslookup -qt=cname <acceleration domain name>`
![img](https://main.qcloudimg.com/raw/89faaf228a2b88e23b82d0a839367c76.png)
- `dig <acceleration domain name>`
![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
