## Ikhtisar
Dokumen ini menjelaskan cara menguji performa jaringan CVM dengan alat, yang membantu Anda tetap berada dalam performa jaringan CVM berdasarkan hasil pengujian.


## Metrik Uji Performa Jaringan

<table>
<tr><th style="width: 25%;">Metrik</th><th>Deskripsi</th></tr>
<tr><td><b>Bandwidth (Mbits/dtk)</b></td><td>Jumlah maksimum data (bit) yang ditransfer per satuan waktu (1 detik)</td></tr>
<tr><td><b>TCP-RR (kali/dtk)</b></td><td>Efisiensi respons bila beberapa komunikasi permintaan/tanggapan dibuat selama satu koneksi persisten TCP. TCP-RR banyak digunakan dalam tautan akses database</td></tr>
<tr><td><b>UDP-STREAM (paket/dtk)</b></td><td>Troughput data UDP selama transfer data batch, yang mencerminkan kapasitas penerusan maksimum dari ENI</td></tr>
<tr><td><b>TCP-STREAM (Mbits/sec)</b></td><td>Throughput data berbasis TCP selama transfer data batch</td></tr>
</table>

## Informasi Alat

| Metrik | Deskripsi |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM | Netperf |
| Bandwidth | iperf |
| melihat PPS | sar |
| melihat antrean ENI | ethtool |


## Petunjuk
### Membangun lingkungan pengujian

#### Mempersiapkan server pengujian

- Citra: CentOS 7.4 64-bit
- Spesifikasi: S3.2XLARGE16
- Kuantitas: 1

Asumsikan bahwa alamat IP server pengujian adalah 10.0.0.1.

#### Mempersiapkan server pelatihan pendamping

* Citra: CentOS 7.4 64-bit
* Spesifikasi: S3.2XLARGE16
* Kuantitas: 8

Asumsikan bahwa alamat IP dari server pelatihan pendamping adalah 10.0.0.2 hingga 10.0.0.9.

#### Men-deploy alat pengujian

>! Saat membuat lingkungan pengujian dan melakukan pengujian di lingkungan tersebut, pastikan Anda memiliki izin pengguna root.
>
1. Jalankan perintah berikut untuk menginstal lingkungan kompilasi dan alat deteksi status sistem:
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. Jalankan perintah berikut untuk mengunduh paket kompresi Netperf:
Anda juga dapat mengunduh Netperf versi terbaru dari GitHub: [Netperf](https://github.com/HewlettPackard/netperf).
```
wget -O netperf-2.5.0.tar.gz -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. Jalankan perintah berikut untuk mendekompresi paket kompresi Netperf:
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. Jalankan perintah berikut untuk mengompilasi dan menginstal Netperf:
```
./configure && make && make install
```
5. Jalankan perintah berikut untuk memverifikasi apakah penginstalan berhasil:
```
netperf -h
netserver -h
```
Jika “Help” (Bantuan) muncul, penginstalan berhasil.
6. Jalankan perintah berikut berdasarkan jenis OS untuk menginstal iperf:
```
yum install iperf         #Untuk CentOS. Pastikan Anda memiliki izin root.
apt-get install iperf #Untuk Ubuntu atau Debian. Pastikan Anda memiliki izin root.
```
7. Jalankan perintah berikut untuk memverifikasi apakah penginstalan berhasil:
```
iperf -h
```
Jika “Help” (Bantuan) muncul, penginstalan berhasil.

### Pengujian bandwidth

Sebaiknya Anda menggunakan dua CVM dengan konfigurasi yang sama untuk pengujian untuk mencegah penyimpangan dalam hasil pengujian performa. Satu CVM digunakan sebagai server pengujian sedangkan CVM lainnya digunakan sebagai server pelatihan pendamping. Dalam contoh ini, 10.0.0.1 dan 10.0.0.2 ditentukan untuk pengujian.

#### Server pengujian
Jalankan perintah berikut:
```
iperf -s
```

#### Server pelatihan pendamping

Jalankan perintah berikut:
```
iperf -c ${<Server IP address>} -b 2048M -t 300 -P ${<Number of ENI queues>}
```
Misalnya, jika alamat IP server pengujian adalah 10.0.0.1 dan jumlah antrean ENI adalah 8, jalankan perintah berikut di server pelatihan pendamping:
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

### Pengujian UDP-STREAM

Sebaiknya Anda menggunakan satu server pengujian dan delapan server pelatihan pendamping untuk pengujian. 10.0.0.1 adalah server pengujian, dan 10.0.0.2 hingga 10.0.0.9 adalah server pelatihan pendamping.

#### Server pengujian
Jalankan perintah berikut untuk melihat nilai PPS jaringan:
```
netserver
sar -n DEV 2
```

#### Server pelatihan pendamping

Jalankan perintah berikut:
```
./netperf -H <Private IP address of the test server> -l 300 -t UDP_STREAM -- -m 1 &
```
Pada server pelatihan pendamping, luncurkan beberapa instans Netperf. Berdasarkan pengalaman, meluncurkan satu instans sudah cukup. Jika performa sistem tidak stabil, tambahkan lebih banyak instans Netperf untuk mencapai batas UDP_STREAM.
Misalnya, jika alamat IP pribadi server pengujian adalah 10.0.0.1, jalankan perintah berikut:
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

### Pengujian TCP-RR

Sebaiknya Anda menggunakan satu server pengujian dan delapan server pelatihan pendamping untuk pengujian. 10.0.0.1 adalah server pengujian, dan 10.0.0.2 hingga 10.0.0.9 adalah server pelatihan pendamping.

#### Server pengujian
Jalankan perintah berikut untuk melihat nilai PPS jaringan:
```
netserver
sar -n DEV 2
```

#### Server pelatihan pendamping

Jalankan perintah berikut:
```
./netperf -H <Private IP address of the test server> -l 300 -t TCP_RR -- -r 1,1 &
```
Di server pelatihan pendamping, luncurkan beberapa instans Netperf. Berdasarkan pengalaman, setidaknya 300 instans Netperf harus diluncurkan untuk mencapai batas TCP-RR.
Misalnya, jika alamat IP pribadi server pengujian adalah 10.0.0.1, jalankan perintah berikut:
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## Analisis Data Pengujian

### Analisis performa alat sar

#### Data analisis sampel

```
14:41:03     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
14:41:04      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
14:41:04        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

14:41:04     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
14:41:05      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
14:41:05        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

14:41:05     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
14:41:06      eth0 1646689.00      1.00  69148.10      0.40      0.00      0.00      0.00
14:41:06        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

14:41:06     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
14:41:07      eth0 1605957.00      1.00  67437.67      0.40      0.00      0.00      0.00
14:41:07        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

#### Deskripsi bidang

| Bidang | Deskripsi |
| ------- | ---------------------- |
| rxpck/s | Jumlah paket yang diterima per detik; yaitu, PPS penerimaan |
| txpck/s | Jumlah paket yang dikirim per detik; yaitu, PPS pengiriman |
| rxkB/s | Bandwidth penerimaan |
| txkB/s | Bandwidth pengiriman |

### Analisis performa alat iperf

#### Sampel data analisis

```
	[ ID] Interval           Transfer     Bandwidth
	[  5]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[  5]   0,00-300,03 dtk  6,88 GByte   197 Mbit/dtk                  penerima
	[  7]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[  7]   0,00-300,03 dtk  6,45 GByte   185 Mbit/dtk                  penerima
	[  9]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[  9]   0,00-300,03 dtk  6,40 GByte   183 Mbit/dtk                  penerima
	[ 11]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[ 11]   0,00-300,03 dtk  6,19 GByte   177 Mbit/dtk                  penerima
	[ 13]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[ 13]   0,00-300,03 dtk  6,82 GByte   195 Mbit/dtk                  penerima
	[ 15]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[ 15]   0,00-300,03 dtk  6,70 GByte   192 Mbit/dtk                  penerima
	[ 17]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[ 17]   0,00-300,03 dtk  7,04 GByte   202 Mbit/dtk                  penerima
	[ 19]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[ 19]   0,00-300,03 dtk  7,02 GByte   201 Mbit/dtk                  penerima
	[SUM]   0,00-300,03 dtk  0,00 Byte  0,00 bit/dtk                  pengirim
	[SUM]   0,00-300,03 dtk  53,5 GByte  1,53 Gbit/dtk                  penerima
```

#### Deskripsi bidang

Dalam baris SUM, pengirim mewakili volume data yang dikirim dan penerima mewakili volume data yang diterima.

| Bidang | Deskripsi |
| --------- | ------------------------------------------------ |
| Interval | Durasi pengujian |
| Transfer | Volume transfer data, termasuk volume data yang dikirim dan diterima |
| Bandwidth | Bandwidth, termasuk bandwidth pengiriman dan penerimaan |

## Operasi yang Relevan
### Skrip untuk meluncurkan beberapa instans Netperf

Di TCP-RR dan UDP-STREAM, beberapa instans Netperf perlu diluncurkan. Jumlah instans yang perlu diluncurkan bergantung pada konfigurasi server. Dokumen ini menyediakan templat skrip untuk meluncurkan beberapa instans Netperf guna menyederhanakan proses pengujian. Misalnya, skrip untuk TCP_RR adalah sebagai berikut:
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # Masukkan alamat IP server setelah -H.
     # Masukkan durasi pengujian setelah -l. Atur durasi ke 10000 untuk mencegah Netperf berakhir sebelum waktunya.
     # Masukkan metode pengujian (TCP_RR atau TCP_CRR) setelah -t.
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
