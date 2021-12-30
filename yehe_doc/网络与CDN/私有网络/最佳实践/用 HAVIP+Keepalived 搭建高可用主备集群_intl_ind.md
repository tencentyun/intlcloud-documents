Dokumen ini menjelaskan cara menggunakan Keepalived dengan [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) untuk membangun kluster utama/sekunder ketersediaan tinggi di Tencent Cloud VPC.
>? HAVIP saat ini dalam periode pengujian beta. Beralih antara server utama/sekunder mungkin memerlukan waktu 10 detik. Untuk mencobanya, harap ajukan permohonan untuk menjadi pengguna beta.

## Prinsip Dasar
Biasanya, kluster utama/sekunder ketersediaan tinggi terdiri dari dua server: server utama aktif dan server sekunder siaga. Kedua server berbagi VIP (IP virtual) yang sama hanya berlaku untuk server utama. Ketika server utama gagal, server sekunder akan mengambil alih VIP untuk terus menyediakan layanan. Mode ini banyak digunakan di switch sumber/replika MySQL dan akses web Ngnix.

Keepalived adalah perangkat lunak ketersediaan tinggi berbasis VRRP yang dapat digunakan untuk membangun kluster utama/sekunder ketersediaan tinggi di antara CVM berbasis VPC. Untuk menggunakan Keepalived, pertama selesaikan konfigurasinya di file `keepalived.conf`.
![](https://main.qcloudimg.com/raw/28815d732550f9eebb66e8d81cea22fd.png)
- Dalam jaringan fisik tradisional, status utama/sekunder dapat dinegosiasikan dengan protokol VRRP Keepalived. Perangkat utama mengirimkan pesan ARP gratis secara berkala untuk membersihkan tabel MAC atau tabel ARP terminal dari pertukaran uplink untuk memicu migrasi VIP ke perangkat utama.
- Di Tencent Cloud VPC, kluster utama/sekunder dengan ketersediaan tinggi juga dapat diimplementasikan dengan men-deploy Keepalived pada CVM, dengan perbedaan berikut:
   - VIP harus berupa [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) yang diajukan dari Tencent Cloud.
   - HAVIP sensitif terhadap subnet dan hanya dapat diikat ke server di bawah subnet yang sama melalui pengumuman.

## Catatan
+ Kami merekomendasikan komunikasi VRRP dalam mode unicast.
+ Kami merekomendasikan Anda menggunakan Keepalived **1.2.24 or later versions** (1.2.24 atau versi yang lebih baru).
+ Pastikan parameter `garp` telah dikonfigurasi. Karena Keepalived bergantung pada pesan ARP untuk memperbarui alamat IP, konfigurasi ini memastikan bahwa perangkat utama selalu mengirim pesan ARP untuk komunikasi.
	```plaintext
	garp_master_delay 1
	garp_master_refresh 5
	```
+ Konfigurasikan ID router VRRP unik untuk setiap kluster utama/sekunder di VPC.
+ Jangan gunakan mode ketat. Pastikan konfigurasi “vrrp_strict” telah dihapus.
+ Kontrol jumlah HAVIP yang terikat pada satu ENI tidak lebih dari 5. Jika Anda perlu menggunakan beberapa VIP, tambahkan atau modifikasi `vrrp_garp_master_repeat 1` di bagian “global_defs” pada file konfigurasi Keepalived.
+ Tentukan parameter `adver_int` dengan benar untuk menyeimbangkan jitter anti-jaringan dan kecepatan pemulihan bencana. Jika parameter `advert_int` diatur terlalu kecil, peralihan yang sering dan **active-active (split brain)** (aktif-aktif (split brain)) sementara dapat terjadi jika terjadi gangguan jaringan. Jika parameter `advert_int` diatur terlalu besar, diperlukan waktu lama untuk peralihan utama-sekunder terjadi setelah server utama gagal, yang menyebabkan gangguan layanan yang lama. **Please fully assess the impact of the active-active (split brain) status on your businesses.** (Harap menilai sepenuhnya dampak status aktif-aktif (split brain) pada bisnis Anda.)
+ Atur parameter `interval` dalam item eksekusi spesifik skrip `track_script` (seperti `checkhaproxy`) ke nilai yang lebih besar, menghindari status `FAULT` yang disebabkan oleh waktu tunggu eksekusi skrip.
+ Opsional: waspadai peningkatan penggunaan disk karena pencetakan log. Ini dapat diselesaikan dengan menggunakan logrotate atau alat lain.


## Petunjuk
>!Dokumen ini menggunakan lingkungan berikut sebagai contoh. Silakan ganti dengan konfigurasi aktual Anda.
>+ CVM Utama: HAVIP-01, 172.16.16.5
>+ CVM Sekunder: HAVIP-02, 172.16.16.6
>+ HAVIP: 172.16.16.12
>+ EIP: 81.71.14.118
>+ Citra: CentOS 7.6 64-bit
### Langkah 1: ajukan VIP[](id:langkah1)
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc/).
2. Pilih **IP and ENI** (IP dan ENI) > **HAVIP** (HAVIP) di bilah sisi kiri untuk masuk ke halaman manajemen HAVIP. 
3. Pilih wilayah yang relevan di halaman manajemen HAVIP dan klik **Apply** (Terapkan).
4. Pada kotak dialog pop-up, masukkan nama, pilih VPC dan subnet untuk HAVIP, dan klik **OK** (Oke).
>?Alamat IP HAVIP dapat ditetapkan secara otomatis atau ditentukan secara manual. Jika Anda memilih untuk memasukkan alamat IP, pastikan alamat IP pribadi yang dimasukkan berada dalam rentang IP subnet dan bukan merupakan alamat IP yang dicadangkan dari sistem. Misalnya, jika rentang IP subnet adalah `10.0.0.0/24`, alamat IP pribadi yang dimasukkan harus berada dalam `10.0.0.2 - 10.0.0.254`.
>
![](https://main.qcloudimg.com/raw/fc0224eda94238588f0dfc0178d08b77.png)
Kemudian Anda dapat melihat HAVIP yang Anda ajukan permohonannya.
![](https://main.qcloudimg.com/raw/3cdee897dc6a5b69ff45ad47725444d9.png)

### Langkah 2: instal Keepalived (versi 1.2.24 atau lebih baru) pada CVM utama dan sekunder
Dokumen ini menggunakan CentOS 7.6 sebagai contoh untuk menginstal Keepalived.
1. Jalankan perintah berikut untuk memverifikasi apakah versi Keepalived memenuhi persyaratan.
 ```plaintext
 daftar yum keepalived
 ```
 + Jika ya, lanjutkan ke [langkah 2](#sublangkah2)
 + Jika tidak, lanjutkan ke [langkah 3](#sublangkah3)
2. <span id="substep2">Instal paket perangkat lunak menggunakan perintah `yum`.
```plaintext
instal yum -y keepalived
```
3. Instal paket perangkat lunak menggunakan kode sumber.[](id:substep3)
```plaintext
tar zxvf keepalived-1.2.24.tar.gz
cd keepalived-1.2.24
./configure --prefix=/
make; make install
chmod +x /etc/init.d/keepalived // Mencegah terjadinya env: /etc/init.d/keepalived: Izin ditolak
```

### Langkah 3: konfigurasikan Keepalived, dan ikat HAVIP ke CVM utama dan sekunder.
1. Login ke CVM HAVIP-01 utama dan jalankan `vim /etc/keepalived/keepalived.conf` untuk mengubah konfigurasinya.
<dx-alert infotype="explain" title="">
Dalam contoh ini, HAVIP-01 dan HAVIP-02 dikonfigurasi dengan bobot yang sama. Keduanya dalam status **BACKUP** (CADANGAN), dengan prioritas 100. Ini akan mengurangi jumlah peralihan yang disebabkan oleh jitter jaringan.
</dx-alert>
 ```plaintext
   ! File Konfigurasi untuk keepaliveD
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1   
      smtp_connect_timeout 30
      router_id LVS_DEVEL
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
   vrrp_script checkhaproxy
   {
        script "/etc/keepalived/do_sth.sh" # Periksa apakah proses layanan berjalan normal. Ganti “do_sth.sh” dengan nama skrip aktual Anda. Jalankan sesuai kebutuhan.
        interval 5
   }
   vrrp_instance VI_1 {
   # Pilih parameter yang tepat untuk CVM utama dan sekunder.
   state CADANGAN              # Atur status awal ke `Backup`
       interface eth0          # ENI seperti `eth0` digunakan untuk mengikat VIP  
       virtual_router_id 51        # Nilai `virtual_router_id` untuk kluster
       nopreempt                   # Mode Non-preempt
       # preempt_delay 10      # Efektif hanya jika `state` adalah `MASTER`    
       priority 100            # Konfigurasikan bobot yang sama untuk kedua perangkat
       advert_int 5        
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.5 # Alamat IP pribadi perangkat lokal
       unicast_peer {
           172.16.16.6                # Alamat IP perangkat pasangan
       }
       virtual_ipaddress {
           172.16.16.12              # HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # Berapa lama waktu yang dibutuhkan sebelum cache ARP dapat diperbarui setelah CVM beralih ke status utama
       garp_master_refresh 5   # Interval waktu antara node utama mengirim pesan ARP

       track_interface {
                   eth0               # ENI yang terikat dengan VIP, seperti `eth0`
           }
       track_script {
          checkhaproxy 
       }
   }
 ```
2. Tekan **Esc** dan masukkan **:wq** untuk menyimpan file dan keluar dari vi.
3. Login ke CVM HAVIP-02 sekunder dan jalankan `vim /etc/keepalived/keepalived.conf` untuk mengubah konfigurasinya.
   ```plaintext
   ! File Konfigurasi untuk keepaliveD
   global_defs {
      notification_email {
        acassen@firewall.loc
        failover@firewall.loc
        sysadmin@firewall.loc
      }
      notification_email_from Alexandre.Cassen@firewall.loc
      smtp_server 192.168.200.1
      smtp_connect_timeout 30
      router_id LVS_DEVEL
      vrrp_skip_check_adv_addr
      vrrp_garp_interval 0
      vrrp_gna_interval 0
   }
   vrrp_script checkhaproxy
   {
       script "/etc/keepalived/do_sth.sh"
        interval 5
   }
   vrrp_instance VI_1 {
   # Pilih parameter yang tepat untuk CVM utama dan sekunder.
   state BACKUP            #Atur status awal ke `Backup`
       interface eth0          #ENI seperti `eth0` digunakan untuk mengikat VIP  
       virtual_router_id 51        #Nilai untuk kluster `virtual_router_id`
       nopreempt                   #Mode Non-preempt
       # preempt_delay 10      #Efektif hanya saat "status MASTER"    
       priority 100            # Konfigurasikan bobot yang sama untuk kedua perangkat
       advert_int 5       
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.6   #IP pribadi perangkat lokal
       unicast_peer {
           172.16.16.5                #Alamat IP perangkat pasangan
       }
       virtual_ipaddress {
           172.16.16.12              #HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # Berapa lama waktu yang dibutuhkan sebelum cache ARP dapat diperbarui setelah CVM beralih ke status utama
       garp_master_refresh 5   #Interval waktu antara node utama mengirim pesan ARP
       track_interface {
                   eth0               # ENI seperti `eth0` yang mengikat VIP
           }
       track_script {
          checkhaproxy 
       }
   }
   ```
4. Tekan **Esc** dan masukkan **:wq** untuk menyimpan file dan keluar dari vi.
5. Mulai ulang Keepalived agar konfigurasi menampakkan hasil.
 ```plaintext
 mulai systemctl keepalived
 ```
6. Periksa status utama/sekunder dari kedua CVM, dan konfirmasikan bahwa keduanya memiliki HAVIP yang terikat dengan benar.
>?Dalam contoh ini, HAVIP-01 memulai Keepalived terlebih dahulu dan biasanya akan berfungsi sebagai node utama.
>
Login ke konsol [HAVIP](https://console.cloud.tencent.com/vpc/havip). Anda akan melihat bahwa HAVIP terikat ke CVM HAVIP-01 utama, seperti yang ditampilkan di bawah ini.
![](https://main.qcloudimg.com/raw/1104e6a7305dec04ce1ea242db0c2c8c.png)


### Langkah 4: **bind an EIP to HAVIP (optional)** (ikat EIP ke HAVIP (opsional))  
1. Login ke konsol [HAVIP](https://console.cloud.tencent.com/vpc/havip), temukan HAVIP yang telah Anda ajukan di [Langkah 1](#langkah1), dan klik **Bind** (Ikat).
![](https://main.qcloudimg.com/raw/129cd10051b4d07e1d420b1bec710614.png)
2. Pada kotak dialog pop-up, pilih EIP yang akan diikat dan klik **OK** (Oke). Jika tidak ada EIP yang tersedia, terlebih dahulu buka konsol [EIP](https://console.cloud.tencent.com/cvm/eip?rid=46) untuk mendaftar.
![](https://main.qcloudimg.com/raw/8ca21593889529f42af52c5b68ec2f78.png)

### Langkah 5: gunakan notify_action.sh untuk pencatatan sederhana (opsional)
Log utama Keepalived masih disimpan di “/var/log/message”, dan Anda dapat menambahkan skrip “notify” untuk pencatatan sederhana.
1. Login ke CVM dan jalankan perintah `vim /etc/keepalived/notify_action.sh` untuk menambahkan skrip “notify_action.sh” berikut.
   ```plaintext
   #!/bin/bash
   #/etc/keepalived/notify_action.sh
   log_file=/var/log/keepalived.log
   log_write()
   {
       echo "[`date '+%Y-%m-%d %T'`] $1" >> $log_file
   }
   [ ! -d /var/keepalived/ ] && mkdir -p /var/keepalived/
   
   case "$1" in
       "MASTER" )
           echo -n "$1" > /var/keepalived/state
           log_write " notify_master"
           echo -n "0" /var/keepalived/vip_check_failed_count
           ;;
       "BACKUP" )
           echo -n "$1" > /var/keepalived/state
           log_write " notify_backup"
           ;;
       "FAULT" )
           echo -n "$1" > /var/keepalived/state
           log_write " notify_fault"
           ;;
       "STOP" )
           echo -n "$1" > /var/keepalived/state
           log_write " notify_stop"
           ;;
       *)
           log_write "notify_action.sh: STATE ERROR!!!"
           ;;
   esac
   ```
2. Jalankan perintah `chmod a+x /etc/keepalived/notify_action.sh` untuk mengubah izin skrip.

### Langkah 6: verifikasi apakah VIP dan IP publik dialihkan secara normal selama peralihan utama/sekunder
Simulasikan kegagalan CVM dengan memulai ulang proses Keepalived atau memulai ulang CVM untuk memeriksa apakah VIP dapat dimigrasikan.
- Jika peralihan utama/sekunder berhasil, CVM sekunder akan menjadi server yang terikat dengan HAVIP di konsol.
- Anda juga dapat melakukan ping ke VIP dari dalam VPC untuk memeriksa selang waktu dari gangguan jaringan hingga pemulihan. Setiap peralihan dapat menyebabkan gangguan selama sekitar 4 detik. Jika Anda melakukan ping EIP yang terikat ke HAVIP melalui jaringan publik, hasilnya akan sama.
- Jalankan perintah `ip addr show` untuk memeriksa apakah HAVIP terikat ke ENI utama.
