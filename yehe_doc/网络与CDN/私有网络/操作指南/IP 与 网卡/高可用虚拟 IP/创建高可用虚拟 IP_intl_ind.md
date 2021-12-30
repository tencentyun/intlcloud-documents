Dokumen ini menjelaskan cara membuat HAVIP di konsol dan mengonfigurasinya di perangkat lunak pihak ketiga.

## Petunjuk
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/) dan pilih **IP and Interface** (IP dan Antarmuka) > **HAVIP** di bilah sisi kiri. 
2. Pilih wilayah target di halaman pengelolaan HAVIP dan klik **Apply** (Terapkan).
3. Pada kotak dialog pop-up, konfigurasikan parameter HAVIP.
 + **Name** (Nama): masukkan nama untuk HAVIP.
 + **Virtual Private Cloud**: pilih VPC tempat HAVIP yang akan dibuat.
 + **Subnet**: pilih subnet untuk HAVIP yang spesifik untuk subnet.
 + **IP address** (Alamat IP): alamat IP HAVIP dapat ditetapkan secara otomatis atau ditentukan secara manual. Jika Anda memilih **Automatic Assignment** (Penetapan Otomatis), alamat IP subnet akan ditetapkan secara otomatis. Jika Anda memilih **Enter manually** (Masukkan secara manual), pastikan alamat IP yang dimasukkan berada dalam rentang IP subnet dan bukan alamat IP yang dicadangkan dari sistem. Misalnya, jika rentang IP subnet adalah `10.0.0.0/24`, alamat IP pribadi yang dimasukkan harus berada dalam `10.0.0.2-10.0.0.254`.
4. Klik **OK** (OKE). Setelah berhasil dibuat, HAVIP akan ditampilkan dalam daftar, dan statusnya adalah **Not bound with CVM yet** (Belum diikatkan dengan CVM).

## Mengonfigurasi HAVIP
HAVIP dirancang untuk digunakan bersama dengan perangkat lunak HA pihak ketiga yang harus dikonfigurasi dalam perangkat lunak HA pihak ketiga. HAVIP hanya merupakan objek operasi dan alamat IP pribadi yang dapat diikatkan melalui pengumuman. Dengan demikian, pengikatan dan pemutusan ikatan HAVIP ke CVM tidak dilakukan di konsol Tencent Cloud. Sebagai gantinya, Anda hanya perlu menentukan HAVIP sebagai alamat IP virtual floating (VIP) di perangkat lunak HA pihak ketiga yang kemudian menentukan ENI untuk dikaitkan ke HAVIP melalui ARP. Berikut ini adalah cara mengikat atau memutuskan ikatan HAVIP:
![](https://main.qcloudimg.com/raw/1007a3d550fda9bf404673be571bf2dc.png)
Dalam lingkungan perangkat fisik tradisional, semua alamat IP pribadi diikat ke ENI melalui ARP secara default dan dapat ditentukan sebagai alamat IP floating dalam perangkat lunak HA. Di lingkungan cloud publik, IP pribadi tidak dapat menggunakan ARP, atau ditetapkan sebagai alamat IP floating di perangkat lunak HA. Dengan demikian, Anda harus mengikuti langkah yang sama dengan perangkat lunak pihak ketiga untuk menentukan HAVIP sebagai alamat IP floating.

>?Program perangkat lunak HA umum meliputi: Linux HeartBeat, Keepalived, Pacemaker, dan Windows MSCS.
>
Saat menentukan VIP di file konfigurasi perangkat lunak HA, Anda hanya perlu memasukkan HAVIP yang Anda buat:

```	
vrrp_instanceVI_1 {
# Pilih parameter yang tepat untuk CVM utama dan sekunder.
    state MASTER               #Atur status awal ke `Pencadangan`.
    interface eth0              #ENI seperti `eth0` digunakan untuk mengikat VIP
    virtual_router_id 51        #Nilai untuk kluster `virtual_router_id`
		nopreempt                   #Mode Non-preempt
		preempt_delay 10           #Atur penundaan ke 10 menit
    priority 100               #Prioritas. Semakin besar nilai, semakin tinggi prioritas
    advert_int 1               #Periksa interval. Nilai default adalah 1 detik
    authentication {           #Autentikasi
        auth_type PASS          #Metode autentikasi
        auth_pass 1111          #Kata sandi autentikasi
    }
		unicast_src_ip 172.16.16.5 #Alamat IP pribadi perangkat lokal
		unicast_peer{
		172.16.16.6                #alamat IP perangkat pasangan
		}
    virtual_ipaddress {     
		172.16.16.12               #HAVIP
    }
	}
```

Setelah konfigurasi selesai di perangkat lunak HA CVM, status HAVIP akan berubah menjadi **Bound with CVM** (Terikat ke CVM) di konsol.

Lihat kasus berikut untuk konfigurasi Anda:
> + [Membangun Kluster Utama/Sekunder HA Menggunakan HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) 
> + [Membuat Database HA Menggunakan HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) 

## Dokumentasi
Mirip dengan IP pribadi, HAVIP juga dapat diikat dengan atau diputuskan ikatannya dari EIP di konsol. Jika Anda memerlukan komunikasi jaringan publik, lihat [Mengikat atau Memutuskan Ikatan EIP](https://intl.cloud.tencent.com/zh/document/product/215/40083).


