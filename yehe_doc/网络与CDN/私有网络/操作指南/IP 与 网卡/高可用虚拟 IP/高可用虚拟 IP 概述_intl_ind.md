IP virtual ketersediaan tinggi (HAVIP) adalah alamat IP pribadi yang ditetapkan dari blok CIDR dari subnet VPC. Alamat ini biasanya digunakan bersama perangkat lunak dengan ketersediaan tinggi, seperti Keepalived dan Windows Server Failover Cluster, untuk membangun kluster utama/sekunder dengan ketersediaan tinggi.
>?
>- HAVIP saat ini dalam versi beta, dan peralihan antara server utama/sekunder mungkin memerlukan waktu 10 detik. Untuk mencobanya, harap ajukan permohonan untuk menjadi pengguna beta.
>- Untuk menjamin ketersediaan tinggi CVM di kluster utama/sekunder, Anda sebaiknya menetapkan CVM ke host yang berbeda menggunakan [grup penempatan](https://intl.cloud.tencent.com/document/product/213/15486). Untuk informasi selengkapnya tentang grup penempatan, lihat [Grup Penempatan](https://intl.cloud.tencent.com/document/product/213/15486).
>- Perangkat lunak ketersediaan tinggi harus mendukung pengiriman pesan ARP.

## Fitur
- Anda dapat mengajukan beberapa alamat HAVIP di konsol untuk setiap VPC.
- Anda harus mengikat HAVIP di file konfigurasi CVM.


## Arsitektur dan Prinsip
Biasanya, kluster utama/sekunder ketersediaan tinggi terdiri dari dua server: server utama aktif dan server sekunder siaga. Kedua server memiliki VIP (IP virtual) yang sama. VIP hanya dapat bekerja di satu server utama pada saat bersamaan. Ketika server utama gagal, server sekunder akan mengambil alih VIP untuk terus menyediakan layanan.
+ Dalam jaringan fisik tradisional, status utama/sekunder dapat dinegosiasikan dengan protokol VRRP Keepalived. Perangkat utama mengirimkan pesan ARP gratis secara berkala untuk membersihkan tabel MAC atau tabel ARP terminal dari pertukaran uplink, sehingga memicu migrasi VIP ke perangkat utama.
+ Dalam VPC, kluster utama/sekunder ketersediaan tinggi juga dapat diimplementasikan dengan men-deploy Keepalived di CVM. Namun, instans CVM biasanya tidak dapat memperoleh IP pribadi melalui pengumuman ARP karena alasan keamanan seperti spoofing ARP. VIP harus HAVIP yang diterapkan dari Tencent Cloud yang berbasis subnet. Dengan demikian, HAVIP hanya dapat diikat ke server di subnet yang sama melalui pengumuman.
>?Keepalived adalah perangkat lunak ketersediaan tinggi berbasis VRRP. Untuk menggunakan Keepalived, pertama selesaikan konfigurasinya di file `Keepalived.conf`.

Gambar berikut menunjukkan arsitektur HAVIP.
![](https://main.qcloudimg.com/raw/e8d0e60cbd3221089256087c5686588f.png)
Menurut gambar contoh, CVM1 dan CVM2 dapat dibangun ke dalam kluster utama/sekunder ketersediaan tinggi dengan langkah-langkah berikut:

1. Instal Keepalived di CVM1 dan CVM2, konfigurasikan HAVIP sebagai VRRP VIP, dan tetapkan prioritas server utama dan sekunder. Nilai yang lebih besar merepresentasikan prioritas yang lebih tinggi.
2. Keepalived menggunakan protokol VRRP untuk membandingkan prioritas awal CVM1 dan CVM2 dan menentukan CVM1 sebagai server utama karena prioritasnya yang lebih tinggi.
3. Server utama mengirimkan pesan ARP, mengumumkan VIP (HAVIP), dan memperbarui pemetaan VIP ke mac. Dalam hal ini, CVM1 adalah server utama dan menyediakan layanan dengan menggunakan IP pribadi (HAVIP) untuk komunikasi. Anda dapat melihat HAVIP terikat ke server utama CVM1 di konsol HAVIP.   
4. (Opsional) Ikat EIP ke HAVIP di konsol untuk menerapkan komunikasi melalui jaringan publik.
5. Server utama mengirimkan pesan VRRP ke server sekunder secara berkala. Jika server utama gagal mengirim pesan VRRP dalam jangka waktu tertentu, server sekunder akan ditetapkan sebagai utama dan mengirimkan pesan pembaruan ARP yang membawa alamat MAC-nya. Dalam hal ini, CVM2 menjadi server utama untuk menyediakan layanan komunikasi dan menangani permintaan akses eksternal. Anda akan melihat bahwa CVM yang diikatkan ke HAVIP berubah menjadi CVM2 pada konsol HAVIP.

## Kasus Penggunaan Umum
- **Cloud load balancer HA**
  Untuk men-deploy Cloud Load Balancers (CLB), Anda biasanya akan menggunakan HA antar instans CLB dan mengonfigurasi server nyata sebagai kluster. Dengan demikian, Anda harus men-deploy dan menggunakan HAVIP sebagai IP virtual antara dua server CLB.
- **Database relasional utama/sekunder**
  Jika Keepalived atau Windows Server Failover Cluster digunakan di antara dua database untuk membangun kluster utama/sekunder dengan ketersediaan tinggi, gunakan HAVIP sebagai IP virtual. Untuk informasi selengkapnya, lihat [Membangun Kluster Utama/Sekunder Ketersediaan Tinggi Menggunakan HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) dan [Membuat Database Ketersediaan Tinggi dengan Menggunakan HAVIP + Kluster Failover Server Windows](https://intl.cloud.tencent.com/document/product/215/31878) pada Praktik Terbaik.


## Pertanyaan Umum

### Mengapa saya harus menggunakan HAVIP bersama Keepalive di VPC?
Beberapa vendor cloud publik tidak mendukung pengikatan IP pribadi ke CVM melalui pengumuman ARP karena alasan keamanan seperti spoofing ARP. Jika Anda langsung menggunakan IP pribadi sebagai IP virtual di file “Keepalived.conf”, Keepalived tidak akan dapat memperbarui pemetaan IP ke MAC selama peralihan IP virtual server utama/sekunder. Dalam hal ini, Anda harus memanggil API untuk mengganti IP.
Menggunakan konfigurasi Keepalived sebagai contoh, konfigurasi IP adalah sebagai berikut:
```plaintext
vrrp_instance VI_1 {
    state BACKUP           #Perangkat sekunder
    interface eth0          #nama ENI 
    virtual_router_id 51
    nopreempt                   #Mode Non-preempt
    #preempt_delay 10
    priority 80
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    unicast_src_ip 172.17.16.7 #IP pribadi perangkat lokal
    unicast_peer {
        172.17.16.13           #Alamat IP dari perangkat pasangan, misalnya: 10.0.0.1
    }

    virtual_ipaddress {

        172.17.16.3 #Masukkan alamat HAVIP yang telah diterapkan di konsol.

    }

    garp_master_delay 1
    garp_master_refresh 5

    track_interface {
        eth0              
    }

    track_script {
        checkhaproxy
    }
}
```
Jika tidak ada HAVIP, bagian berikut dari file konfigurasi akan tidak valid.
```plaintext
virtual_ipaddress {
   172.17.16.3 #Masukkan alamat HAVIP yang telah diterapkan di konsol.
}
```

## Referensi
- Untuk informasi selengkapnya tentang batas HAVIP, lihat [Batas](https://intl.cloud.tencent.com/document/product/215/31818).
- Untuk informasi selengkapnya tentang panduan pengoperasian HAVIP, lihat [Mengelola HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
