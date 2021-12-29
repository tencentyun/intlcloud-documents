## Mendapatkan IP Klien Nyata Melalui TOA
Ketika koneksi akselerasi meneruskan paket data, SNAT dan DNAT akan dijalankan pada paket; yaitu, alamat sumber dan tujuan paket data akan dimodifikasi. Alamat sumber paket yang dilihat oleh server asal akan menjadi alamat IP penerusan dari koneksi akselerasi, bukan IP klien yang nyata. Untuk meneruskan IP klien ke server, koneksi akselerasi akan menyertakan IP klien dan port di kolom `tcp option` khusus saat meneruskan paket, seperti yang ditunjukkan di bawah ini:
```
#tentukan TCPOPT_ADDR  200    
#tentukan TCPOLEN_ADDR 8 /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * masukkan ip klien di opsi tcp, sekarang hanya mendukung IPV4,
 * harus selaras dengan 4 byte.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

## Mendapatkan IP Klien Nyata Melalui Proxy Protocol
Proxy Protocol memfasilitasi transmisi informasi klien (seperti tumpukan protokol, IP sumber, IP tujuan, port sumber, dan port tujuan, dll.) dengan menambahkan header ke TCP yang ideal untuk kasus saat kondisi jaringan kompleks dan klien IP diperlukan. Selama proses ini, proksi memasukkan paket data yang berisi informasi empat kali lipat koneksi asal ke dalam koneksi setelah handshake tiga arah.

Untuk mendapatkan IP klien menggunakan metode Proxy Protocol, Anda harus mengonfigurasinya di konsol terlebih dahulu. Itu hanya dapat dikonfigurasi untuk pendengar dengan TCP. Setelah layanan akselerasi terhubung dengan server asal, teks Proxy Protocol akan disisipkan ke dalam paket `payload` yang pertama kali ditransmisikan.

Saat ini, Nginx dan HAProxy mendukung Proxy Protocol. Untuk konfigurasi Proxy Protocol di Nginx, Anda hanya perlu menambahkan `proxy_protocol` setelah perintah `listen` di chunk `server`.
```
http {
    #...
    server {
        listen 80   proxy_protocol;
        listen 443  ssl proxy_protocol;
        #...
    }
}
```

 Untuk program yang tidak mendukung Proxy Protocol, setelah koneksi TCP disiapkan, Anda perlu menguraikan string teks Proxy Protocol sebagai berikut untuk mendapatkan IP klien:
 ```
 PROXY TCP4 1.1.1.2 2.2.2.2 12345 80\r\n
 ```
