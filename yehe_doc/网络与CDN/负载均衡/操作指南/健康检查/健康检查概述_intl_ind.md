Instance CLB menentukan ketersediaan server asli melalui pemeriksaan kesehatan sehingga bisnis frontend tidak akan terkena dampak pengecualian server asli dan meningkatkan ketersediaan bisnis secara umum.
- Jika pemeriksaan kesehatan diaktifkan, instance CLB akan selalu melakukan pemeriksaan kesehatan di instance CVM backend berapa pun beratnya (termasuk 0).
- Jika instance CVM backend abnormal, instance CLB secara otomatis akan meneruskan permintaan baru ke instance CVM normal lainnya, dan bukan ke instance yang tidak sehat.
- Setelah instance CVM abnormal pulih, instance akan digunakan dalam layanan CLB kembali dan menerima permintaan baru.
- Jika semua server asli terdeteksi abnormal, permintaan akan diteruskan ke semua instance CVM backend.
- Jika pemeriksaan kesehatan dinonaktifkan, instance CLB akan meneruskan lalu lintas ke semua server asli termasuk abnormal.Oleh karena itu, sebaiknya Anda mengaktifkan pemeriksaan kesehatan pada instance CLB untuk memeriksa server asli secara otomatis dan menghapus yang abnormal.

## Status Pemeriksaan Kesehatan
Deskripsi status pemeriksaan kesehatan instance CVM backend yaitu sebagai berikut:

| Status | Deskripsi | Teruskan Lalu Lintas |
| ------- | ----------- | ---------------- |
| Mendeteksi | Status instance CVM backend baru selama interval periode pemeriksaan × batas sehat.Misalnya, anggap interval pemeriksaan 2 detik dan ambang batas sehat adalah 3 kali, instance CVM backend bertahan dalam status ini selama 6 detik.| Tidak. |
| Sehat | Kondisi server asli normal.| Ya. |
| Abnormal | Kondisi server asli abnormal. |  <li>Tidak.</li><li> Menurut aturan pendengar lapisan 4 atau URL lapisan 7, jika instance CLB mendeteksi bahwa kondisi semua server asli abnormal, permintaan akan diteruskan ke semua server asli.</li>|
| Dinonaktifkan | Pemeriksaan kesehatan dinonaktifkan.| Ya. |

## Pemeriksaan Kesehatan TCP
Untuk pendengar TCP lapisan 4, Anda dapat mengonfigurasi pemeriksaan kesehatan TCP untuk melihat status instance CVM backend melalui paket SYN, misalnya, handshake tiga arah TCP.Selain itu, untuk mengatasinya, Anda dapat menyesuaikan permintaan dan mengembalikan konten protokol.
![](https://main.qcloudimg.com/raw/5f30ebbb5e061affeff6eb031facaf28.png)
Mekanisme pemeriksaan kesehatan TCP yaitu sebagai berikut:
1.Instance CLB mengirimkan paket permintaan koneksi SYN ke (IP privat dan port pemeriksaan kesehatan dari) instance CVM backend.
2.Setelah menerima paket permintaan SYN, instance CVM backend akan mengembalikan paket respons SYN-ACK jika port mendengarkan secara normal.
3.Jika instance CLB menerima paket respons SYN-ACK yang dikembalikan dalam waktu habis respons, hal tersebut menunjukkan bahwa kondisi server asli normal dan hasil pemeriksaan kesehatan telah berhasil.Instance CLB akan mengirimkan paket TCP Reset (RST) ke instance CVM backend untuk memutus koneksi TCP.
4.Jika instance CLB tidak menerima paket respons SYN-ACK yang dikembalikan dalam waktu habis respons, hal tersebut menunjukkan bahwa kondisi server asli abnormal dan hasil pemeriksaan kesehatan gagal.Instance CLB akan mengirimkan paket TCP Reset (RST) ke instance CVM backend untuk memutus koneksi TCP.

## Pemeriksaan Kesehatan UDP
Untuk pendengar UDP lapisan 4, Anda dapat mengonfigurasi pemeriksaan kesehatan UDP untuk melihat status instance CVM backend dengan menjalankan perintah Ping dan mengirimkan paket deteksi UDP ke port pemeriksaan kesehatan.Selain itu, untuk mengatasinya, Anda dapat menyesuaikan permintaan dan mengembalikan konten protokol.
![](https://main.qcloudimg.com/raw/97127e438782907e02e183e9258e652c.png)
Mekanisme pemeriksaan kesehatan UDP yaitu sebagai berikut:
1.Instance CLB akan mengirimkan perintah Ping ke IP privat instance CVM backend.
2.Setelah itu, instance CLB akan mengirimkan paket deteksi UDP ke (IP privat dan port pemeriksaan kesehatan dari) instance CVM backend.
3.Jika perintah Ping berhasil dan instance CVM backend tidak mengembalikan kesalahan `port XX tidak dapat dijangkau` dalam waktu habis respons, hal tersebut menunjukkan bahwa kondisi server asli normal dan hasil pemeriksaan kesehatan berhasil.
4.Jika perintah Ping gagal dan instance CVM backend mengembalikan kesalahan `port XX tidak dapat dijangkau` dalam waktu habis respons, hal tersebut menunjukkan bahwa kondisi server asli abnormal dan hasil pemeriksaan kesehatan gagal.

>!
1.Pemeriksaan kesehatan UDP dilakukan berdasarkan ICMP sehingga instance CVM backend memerlukan izin agar dapat membalas paket ICMP (yaitu: perintah Ping didukung) dan paket "port tidak dapat dijangkau" ICMP (yaitu: port dapat dideteksi).
2.Jika server Linux digunakan sebagai instance CVM backend, kecepatan server untuk mengirimkan paket ICMP akan dibatasi selama konkurensi tinggi karena server Linux memiliki mekanisme pertahanan diri dari serangan ICMP.Dalam kasus ini, meskipun kondisi server asli abnormal, server tidak dapat mengembalikan kesalahan `port XX tidak dapat dijangkau` ke instance CLB.Kemudian, Instance CLB akan menentukan bahwa hasil pemeriksaan kesehatan berhasil sehingga status aktual server asli tidak dapat dikembalikan.
Solusi:Anda dapat mengonfigurasi pemeriksaan kesehatan UDP dengan input khusus dan string output.Dalam pemeriksaan kesehatan, string input khusus akan dikirimkan ke server asli, dan hasilnya akan ditetapkan sebagai berhasil hanya setelah instance CLB menerima string respons khusus.Metode ini dilakukan berdasarkan server asli, yang perlu memproses string input pemeriksaan kesehatan dan mengembalikan string output khusus.

## <span id="http"></span>Pemeriksaan Kesehatan HTTP
Untuk pendengar TCP lapisan 4 dan pendengar HTTP/HTTPS lapisan 7, Anda dapat mengonfigurasi pemeriksaan kesehatan HTTP untuk melihat status instance CVM backend dengan mengirimkan permintaan HTTP.
![](https://main.qcloudimg.com/raw/94d491d305eca2c6b891912fc1a62ffe.png)
Mekanisme pemeriksaan kesehatan HTTP yaitu sebagai berikut:
1.Menurut konfigurasi pemeriksaan kesehatan, instance CLB dapat mengirimkan permintaan HTTP (nama domain target telah ditentukan) ke (IP privat, port pemeriksaan kesehatan, dan jalur pemeriksaan dari) instance CVM backend.
2.Setelah menerima permintaan, instance CVM backend akan mengembalikan kode status HTTP yang sesuai.
3.Jika instance CLB menerima kode status HTTP yang dikembalikan dalam waktu habis respons dan kode status HTTP sesuai dengan yang ditetapkan, hal tersebut menunjukkan bawa hasil pemeriksaan kesehatan berhasil, jika tidak, artinya gagal.
4.Jika instance CLB tidak menerima paket respons dari instance CVM backend dalam waktu habis respons, hal tersebut menunjukkan bahwa hasil pemeriksaan kesehatan gagal.

>? Untuk pendengar HTTPS lapisan 7, jika HTTP dipilih sebagai protokol backend aturan penerusan pendengar HTTPS, pemeriksaan kesehatan HTTP akan dijalankan; jika HTTPS dipilih, pemeriksaan kesehatan HTTPS akan dijalankan.
Pemeriksaan kesehatan HTTPS pada dasarnya sama seperti <a href="#http">pemeriksaan kesehatan HTTP</a>.Perbedaannya yaitu dalam pemeriksaan kesehatan HTTPS, permintaan HTTPS dikirimkan dan status instance CVM backend ditentukan oleh kode status HTTPS yang dikembalikan.
## Periode Pemeriksaan Kesehatan
Mekanisme pemeriksaan kesehatan CLB meningkatkan ketersediaan bisnis, tetapi kegagalan pemeriksaan kesehatan yang berulang kali dapat menyebabkan penggantian server yang tidak diperlukan sehingga menurunkan ketersediaan sistem.Oleh karena itu, status pemeriksaan kesehatan hanya dapat diubah antara sehat dan abnormal jika diperoleh hasil yang sama dalam satu periode pemeriksaan kesehatan selama beberapa kali.Periode pemeriksaan kesehatan ditentukan berdasarkan faktor berikut:
<table>
<tr>
<th>Konfigurasi Pemeriksaan Kesehatan</th>
<th>Catatan</th>
<th>Nilai Default</th>
</tr>
<tr>
<td>Waktu Habis Respons</td>
<td><ul><li>Waktu habis respons maksimum pemeriksaan kesehatan.</li><li>Jika server asli tidak dapat merespons dalam waktu habis, server akan dianggap dalam kondisi abnormal.</li><li>Rentang nilai: 2-60 detik.</li></ul></td>
<td>2 detik</td>
</tr>
<tr>
<td>Interval pemeriksaan</td>
<td><ul><li>Interval antara dua pemeriksaan kesehatan.</li><li>Rentang nilai: 5-300 detik.</li></ul></td>
<td>5 detik</td>
</tr>
<tr>
<td>Ambang batas tidak sehat</td>
<td><ul><li>Jika hasil pemeriksaan kesehatan gagal sebanyak n (nilai dapat dikustomisasi) kali, instance CVM backend akan dianggap tidak sehat, dan konsol akan menampilkan status <b>Abnormal</b>.</li><li>Rentang nilai: 2-10 kali.</li></ul></td>
<td>3 kali</td>
</tr>
<tr>
<td>Ambang batas sehat</td>
<td><ul><li>Jika hasil pemeriksaan kesehatan berhasil sebanyak n (nilai dapat dikustomisasi) kali, instance CVM backend akan dianggap sehat, dan konsol akan menampilkan status <b>Sehat</b>.</li><li>Rentang nilai: 2-10 kali.</li></ul></td>
<td>3 kali</td>
</tr>
</table>

Penghitungan **lapisan 4 health check time window** (periode pemeriksaan kesehatan lapisan 4) yaitu sebagai berikut:
>?Pemeriksaan kesehatan lapisan 4, terutama pemeriksaan kesehatan TCP atau UDP, interval waktu antara kedua pemeriksaan merupakan nilai tetap, apa pun hasilnya atau meskipun waktu respons habis.
- Periode pemeriksaan kesehatan dengan hasil gagal = Interval pemeriksaan × (Ambang batas tidak sehat - 1)
Dalam contoh di bawah ini, waktu habis respons pemeriksaan kesehatan yaitu 2 detik, interval pemeriksaan 5 detik, dan ambang batas tidak sehat 3 kali sehingga periode pemeriksaan kesehatan dengan hasil gagal = 5 x (3-1) = 10 detik.
![](https://main.qcloudimg.com/raw/63ee9657f3bb44c31c8e271484a67729.png)
-Periode pemeriksaan kesehatan dengan hasil berhasil = Interval pemeriksaan × (Ambang batas sehat - 1)
Dalam contoh di bawah ini, periode respons pemeriksaan kesehatan yang berhasil yaitu 1 detik, interval pemeriksaan 5 detik, dan ambang batas sehat 3 kali sehingga periode pemeriksaan kesehatan dengan hasil yang berhasil = 5 x (3-1) = 10 detik.
![](https://main.qcloudimg.com/raw/9f147597b7eb8879c4460ec6eadea3cb.png)

Penghitungan **lapisan 7 health check time window** (periode pemeriksaan kesehatan lapisan 7) yaitu sebagai berikut:
- Periode pemeriksaan kesehatan dengan hasil gagal = Waktu habis respons × Ambang batas tidak sehat + Interval pemeriksaan × (Ambang batas tidak sehat - 1)
Dalam contoh di bawah ini, waktu habis respons pemeriksaan kesehatan yaitu 2 detik, interval pemeriksaan 5 detik, dan ambang batas tidak sehat 3 kali sehingga periode pemeriksaan kesehatan dengan hasil gagal = 2 x 3 + 5 x (3-1) = 16 detik.
![](https://main.qcloudimg.com/raw/8ddafd2348fd071942752dc24f5c5c2c.png)
- Periode pemeriksaan kesehatan dengan hasil berhasil = Periode respons pemeriksaan kesehatan berhasil × Ambang batas sehat + Interval pemeriksaan × (Ambang batas sehat -1)
Dalam contoh di bawah ini, periode respons pemeriksaan kesehatan yang berhasil yaitu 1 detik, interval pemeriksaan 5 detik, dan ambang batas sehat 3 kali sehingga periode pemeriksaan kesehatan dengan hasil yang berhasil = 1 x 3 + 5 x (3-1) = 13 detik.
![](https://main.qcloudimg.com/raw/a6afea17bf2767081c2fcd66913233d0.png)


## Pengidentifikasi Pemeriksaan Kesehatan
Setelah pemeriksaan kesehatan CLB dimulai, server asli akan menerima permintaan pemeriksaan kesehatan selain permintaan bisnis biasa.Permintaan pemeriksaan kesehatan mungkin memiliki properti berikut:
- IP sumber pemeriksaan kesehatan yaitu CLB VIP.
- Permintaan pemeriksaan kesehatan dari pendengar lapisan 4 (TCP, UDP, dan TCP SSL) akan ditandai dengan "HEALTH CHECK" (PEMERIKSAAN KESEHATAN).
- Untuk permintaan pemeriksaan kesehatan dari pendengar lapisan 7 (HTTP dan HTTPS), `user-agent` dalam header yaitu `clb-healthcheck`.
>?
>- Untuk permintaan pemeriksaan kesehatan dari instance CLB klasik jaringan privat, IP sumber pemeriksaan kesehatannya yaitu `169.254.128.0/17`.
>- Untuk permintaan pemeriksaan kesehatan dari instance CLB jaringan klasik, IP sumber pemeriksaan kesehatannya menggunakan IP fisik.

## Referensi
- [Mengonfigurasi Pemeriksaan Kesehatan](https://intl.cloud.tencent.com/document/product/214/39251)
- [Mengonfigurasi Log Pemeriksaan Kesehatan](https://cloud.tencent.com/document/product/214/55139)
