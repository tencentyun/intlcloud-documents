## 1.CLB Capability Description (Deskripsi Kemampuan CLB)

Dengan mengoptimalkan tumpukan protokol dan server secara mendalam, Tencent Cloud CLB mencapai peningkatan yang besar dalam kinerja HTTPS.Sementara itu, Tencent Cloud sangat menghemat biaya sertifikat melalui kerja sama dengan otoritas sertifikat internasional.CLB dapat menghadirkan manfaat besar bagi bisnis Anda dalam aspek-aspek berikut:

1.Penggunaan HTTPS tidak memengaruhi kecepatan akses klien.
2.Kinerja enkripsi dan dekripsi SSL dari satu server dalam sebuah kluster dapat mempertahankan handshake penuh hingga 65.000 koneksi per detik (CPS), yang sekurang-kurangnya 3,5 kali lebih tinggi daripada CPU berkinerja tinggi.Keunggulan ini mengurangi biaya server, sangat meningkatkan kemampuan layanan selama periode puncak bisnis dan lonjakan lalu lintas, serta memperkuat kemampuan tangkal serangan berbasis komputasi.
3.Offloading dan konversi beberapa protokol didukung, yang mengurangi tekanan bisnis dalam beradaptasi dengan beragam protokol klien.Backend bisnis hanya perlu mendukung HTTP/1.1 untuk menggunakan berbagai macam protokol, seperti HTTP/2, SPDY, SSL 3.0, dan TLS 1.2.
4.Layanan permohonan, pemantauan, dan penggantian sertifikat SSL satu atap disediakan.Tencent Cloud bekerja sama dengan Comodo dan SecureSite, dua otoritas sertifikat internasional, untuk menyederhanakan proses permohonan sertifikat dan mengurangi biaya permohonan tersebut.
5.Tersedia Fitur Anti-CC dan WAF untuk menghadang serangan lapisan-aplikasi, seperti serangan HTTP lambat, serangan dengan target frekuensi tinggi, injeksi SQL, dan trojan situs web.

## 2.HTTP and HTTPS Header Identifiers (Pengidentifikasi Header HTTP dan HTTPS)

CLB bertindak sebagai proksi untuk HTTPS.Baik permintaan HTTP maupun HTTPS akan menjadi permintaan HTTP ketika diteruskan ke instance CVM backend oleh CLB.Dengan demikian, Anda tidak dapat membedakan mana permintaan frontend yang dalam HTTP atau HTTPS.

CLB menanamkan `X-Client-Proto` ke dalam header saat meneruskan permintaan ke server asli:

X-Client-Proto: http (permintaan HTTP di frontend)
X-Client-Proto: https (permintaan HTTPS di frontend)

## 3.Memulai


Anggaplah bahwa Anda perlu mengonfigurasi situs web `https://example.com`, agar pengguna akhir dapat mengunjunginya secara aman melalui HTTPS ketika pengguna tersebut memasukkan `www.example.com` langsung di peramban.

Dalam hal ini, permintaan untuk mengakses `www.example.com` yang dimasukkan oleh pengguna akhir akan diteruskan seperti di bawah ini:

1.Permintaan ditransfer melalui HTTP dan mengakses port 80 pendengar CLB melalui VIP.Setelah itu, permintaan diteruskan ke port 8080 server asli.

2.Dengan konfigurasi penulisan ulang di Nginx di server asli, permintaan melewati port 8080 dan ditulis ulang di halaman `https://example.com`.

3.Setelah itu, peramban akan mengirimkan kembali permintaan `https://example.com` ke situs HTTPS yang sesuai.Permintaan tersebut mengakses port 443 pendengar CLB melalui VIP, kemudian diteruskan ke port 80 server asli.

Dengan demikian, proses penerusan permintaan telah selesai.

Operasi ini menuliskan ulang permintaan HTTP pengguna peramban menjadi permintaan HTTPS yang lebih aman dan tidak terlihat oleh pengguna.Untuk menerapkan operasi penerusan permintaan di atas, Anda dapat mengonfigurasi server asli sebagai berikut:

```
server {

listen 8080;
server_name example.qcloud.com;

location / {

#! customized_conf_begin;
client_max_body_size 200m;
rewrite ^/.(.*) https://$host/$1 redirect;

} 
}
```

Atau, dalam versi baru Nginx, alihkan halaman HTTP Nginx ke halaman HTTPS menggunakan metode pengalihan 301 yang direkomendasikan:

```
server {
listen  80;
server_name    example.qcloud.com;
return  301 https://$server_name$request_uri;
}

server {
listen  443 ssl;
server_name    example.qcloud.com;
	[....]
}
```
