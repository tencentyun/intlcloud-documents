Setelah instance CLB dibuat, Anda bisa mengonfigurasi satu grup keamanan CLB untuk mengisolasi lalu lintas jaringan publik.Dokumen ini menjelaskan cara mengonfigurasikan grup keamanan CLB di mode-mode berbeda.
## Batasan Penggunaan
- Satu instance CLB bisa diikat ke maksimum lima grup keamanan.
- Hingga 512 aturan diizinkan untuk grup keamanan.
- Grup keamanan tidak bisa diikat ke instance CLB pribadi berbasis jaringan klasik dan instance CLB pribadi klasik.Jika satu instance CLB terikat ke [Anycast EIP](https://intl.cloud.tencent.com/document/product/214/32426), grup keamanan yang terikat ke instance tersebut tidak akan aktif.
- **Allow by Default** (Izinkan secara Default) tidak tersedia untuk CLB pribadi klasik dan CLB berbasis jaringan klasik.

## Latar belakang
Grup keamanan adalah firewall virtual yang bisa memfilter paket data stateful dan mengendalikan lalu lintas keluar dan masuk pada level instance.Untuk informasi selengkapnya, lihat [Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/12452).

Grup keamanan CLB terikat dengan instance CLB, sementara grup keamanan CVM terikat dengan instance CVM.Target mereka adalah objek yang berbeda.Untuk grup keamanan CLB, Anda bisa memilih untuk:
- [Mengaktifkan **Allow by Default** (Izinkan secara Default)](#open-security-group)
- [Menonaktifkan **Allow by Default** (Izinkan secara Default)](#close-security-group)

>?
>- Untuk grup keamanan CLB IPv4, **Allow by Default** (Izinkan secara Default) dinonaktifkan secara default, Anda bisa mengaktifkannya di konsol.
>- Untuk grup keamanan CLB IPv6, **Allow by Default** (Izinkan secara Default) diaktifkan secara default, Anda tidak bisa menonaktifkannya.


### Mengaktifkan **Allow by Default** (Izinkan secara Default)[](id:open-security-group)
![](https://main.qcloudimg.com/raw/0d2b50ca557d805ce5790fcdd3974b40.jpg)
Saat **Allow by Default** (Izinkan secara Default) diaktifkan:
<ul ><li>Jika Anda ingin memberi izin akses dari IP klien tertentu saja, Anda <strong>harus mengizinkannya</strong> dan port pendengaran di grup keamanan CLB, tetapi Anda <strong>tidak perlu mengizinkan</strong> IP klien dan port layanan di grup keamanan CVM backend.Lalu lintas akses dari CLB hanya melewati grup keamanan CLB, karena server asli mengizinkan lalu lintas dari CLB secara default.</li>
<li>Lalu lintas dari IP publik (termasuk IP dan EIP publik umum) masih harus melewati grup keamanan CVM.</li>
<li>Jika satu instance CLB belum mengonfigurasi grup keamanan, semua lalu lintas akan diizinkan, dan hanya port yang dikonfigurasikan dengan pendengar di VIP instance CLB yang bisa diakses; oleh karena itu, port pendengaran akan mengizinkan lalu lintas dari semua IP.</li>
<li>Untuk menolak lalu lintas dari IP klien tertentu, Anda harus mengonfigurasi di grup keamanan CLB.Menolak IP klien di grup keamanan CVM hanya berlaku untuk lalu lintas dari IP publik (termasuk IP dan EIP publik umum) tetapi <strong>tidak</strong> untuk lalu lintas dari CLB.</li></ul>


### Menonaktifkan **Allow by Default** (Izinkan secara Default)[](id:close-security-group)
![](https://main.qcloudimg.com/raw/9357f8d81a0027110bd6a977cda4aafc.jpg)
Jika **Allow by Default** (Izinkan secara Default) dinonaktifkan:</p>
<ul ><li>Jika Anda hanya ingin mengizinkan akses dari IP klien tertentu, Anda <strong>harus mengizinkan</strong> IP klien dan port pendengaran di grup keamanan CLB dan <strong>juga mengizinkan</strong> IP klien dan port layanan di grup keamanan CVM; oleh karena itu, lalu lintas bisnis yang melewati CLB akan diperiksa dua kali oleh baik grup keamanan CLB dan grup keamanan CVM.</li>
<li>Lalu lintas dari IP publik (termasuk IP dan EIP publik umum) masih harus melewati grup keamanan CVM.</li>
<li>Jika instance CLB belum mengonfigurasi grup keamanan, hanya lalu lintas yang melewati grup keamanan CVM yang diizinkan.</li>
<li>Anda bisa menolak akses baik untuk grup keamanan CLB maupun grup keamanan CVM untuk menolak lalu lintas dari IP klien tertentu.</li></ul>

<p >Jika <b>Izinkan secara Default</b> dinonaktifkan, grup keamanan CVM harus dikonfigurasikan seperti berikut ini untuk memastikan pemeriksaan kesehatan yang efektif:</p>
<ol ><li>Konfigurasikan CLB jaringan publik<br>Anda harus mengizinkan VIP CLB di grup keamanan CVM backend, agar CLB bisa menggunakan VIP untuk mendeteksi status kesehatan CVM backend.</li>
<li>Konfigurasikan CLB jaringan pribadi<ul><li>Untuk CLB jaringan pribadi (sebelumnya “CLB aplikasi pribadi”), jika instance CLB Anda dalam VPC, VIP CLB perlu diizinkan di grup keamanan CVM backend untuk pemeriksaan kesehatan; jika instance CLB Anda dalam jaringan klasik, konfigurasi tambahan tidak diperlukan karena IP pemeriksaan kesehatan sudah diizinkan secara default.</li><li>Untuk CLB klasik jaringan pribadi, jika instance CLB Anda dibuat sebelum 5 Desember 2016 dan ada di VPC, VIP CLB perlu diizinkan (untuk pemeriksaan kesehatan) di grup keamanan CVM backend; jika tidak, konfigurasi tambahan tidak diperlukan karena IP pemeriksaan kesehatan sudah diizinkan secara default.</li></ul></li></ol>

## Petunjuk
Pada contoh berikut ini, grup keamanan dikonfigurasikan agar hanya mengizinkan lalu lintas masuk ke CLB dari port 80, dan layanan tersedia melalui CVM port 8080.Tidak ada batasan pada IP klien.
> ! Untuk instance CLB jaringan publik yang digunakan pada contoh ini, VIP CLB perlu diizinkan di grup keamanan CVM backend untuk pemeriksaan kesehatan.IP saat ini diatur ke `0.0.0.0/0`, yang artinya semua IP diizinkan.

### Langkah 1.Buat satu instance dan pendengar CLB, dan ikat mereka ke CVM

Untuk informasi selengkapnya, silakan lihat [Memulai CLB](https://intl.cloud.tencent.com/document/product/214/8975).Satu pendengar HTTP:80 dibuat dan diikat ke instance CVM backend dengan port layanan 8080 pada contoh ini.
<img alt="" src="https://main.qcloudimg.com/raw/9ec487d62b6092e6f5b14c1791ef5f4e.png" >

### Langkah 2.Konfigurasikan grup keamanan CLB
1.Konfigurasikan aturan grup keamanan CLB<br>Masuk ke <a rel="nofollow" href="https://console.cloud.tencent.com/cvm/securitygroup">Konsol Grup Keamanan</a> untuk mengonfigurasikan aturan grup keamanan.Di aturan masuk, izinkan permintaan dari port 80 dari semua IP (misalnya, `0.0.0.0/0`) dan tolak lalu lintas dari port lainnya.
> ?
> - Aturan grup keamanan disaring agar berlaku dari atas ke bawah.Jika aturan yang baru diberlakukan, aturan lainnya akan ditolak secara default; oleh karena itu, perhatikan urutannya.Untuk informasi selengkapnya, lihat<a rel="nofollow" href="https://intl.cloud.tencent.com/document/product/215/38750">Ikhtisar Grup Keamanan</a>.
> - Satu grup keamanan memiliki aturan masuk dan keluar.Konfigurasi di atas dimaksudkan untuk membatasi lalu lintas masuk dan karenanya merupakan <strong>aturan masuk</strong>, sementara aturan keluar tidak perlu dikonfigurasi secara khusus.
>
![](https://main.qcloudimg.com/raw/65b035098c49c77f4a82eed799353bc4.png)

2.Ikat grup keamanan ke instance CLB
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman “Manajemen Instance”, klik ID instance CLB target.
3.Di halaman detail instance, klik tab **Security Group** (Grup Keamanan) dan klik **Bind** (Ikat) pada modul **Bound Security Groups** (Grup Keamanan Terikat).
4.Di jendela **Configure Security Group** (Konfigurasi Grup Keamanan) yang muncul, pilih grup keamanan yang terikat ke instance CLB dan klik **OK**.
![](https://main.qcloudimg.com/raw/8a9701e700a94ba55a9a650eb87b4456.png)
Konfigurasi grup keamanan CLB sudah selesai, yang hanya mengizinkan akses pada CLB dari port 80.
<img alt="" src="https://main.qcloudimg.com/raw/a32cd86653185a5138006757aab38075.png" >

### Langkah 3.Konfigurasikan **Allow by Default** (Izinkan secara Default)
Anda bisa memilih untuk mengaktifkan atau menonaktifkan **Allow by Default** (Izinkan secara Default) dengan konfigurasi berbeda seperti berikut ini:
- Metode 1.Aktifkan **Allow by Default** (Izinkan secara Default), agar server asli tidak perlu mengizinkan port.
>?Fitur ini tidak didukung untuk CLB jaringan privat klasik dan CLB di jaringan klasik.
- Metode 2.Nonaktifkan **Allow by Default** (Izinkan secara Default), dan Anda juga perlu mengizinkan IP klien (0.0.0.0/0 pada contoh ini) di grup keamanan CVM.

#### Metode 1.Aktifkan **Allow by Default** (Izinkan secara Default)
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman **Instance Management** (Manajemen Instance), klik ID instance CLB target.
3.Di halaman detail instance, klik tab **Security Group** (Grup Keamanan).
2.Pada tab **Security Group** (Grup Keamanan), klik <img style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png"> untuk mengaktifkan **Allow by Default** (Izinkan secara Default).
3.Jika **Allow by Default** (Izinkan secara Default) diaktifkan, hanya aturan grup keamanan di <strong>ikhtisar aturan</strong> seperti yang ditunjukkan di bawah ini yang perlu diverifikasi.
![](https://main.qcloudimg.com/raw/6caa47138ecb97cc3c60cb38971792fd.png)

#### Metode 2.Nonaktifkan **Allow by Default** (Izinkan secara Default)
Jika **Allow by Default** (Izinkan secara Default) dinonaktifkan, Anda perlu mengizinkan IP klien di grup keamanan CVM.Lalu lintas bisnis hanya diizinkan mengakses CVM dari port 80 CLB dan menggunakan layanan yang disediakan melalui port 8080 CVM.
>?Untuk mengizinkan lalu lintas dari IP klien tertentu, Anda perlu mengizinkan IP tersebut di grup keamanan CLB dan grup keamanan CVM.Jika CLB tidak memiliki grup keamanan, silakan izinkan IP di grup keamanan CVM.
>
1.Konfigurasikan aturan grup keamanan CVM
Grup keamanan CVM bisa dikonfigurasi agar hanya mengizinkan akses dari port layanan untuk lalu lintas yang mengakses instance CVM backend.<br>Buka [Konsol Grup Keamanan](https://console.cloud.tencent.com/cvm/securitygroup) untuk mengonfigurasikan kebijakan grup keamanan.Di aturan masuk, semua port 8080 dari semua IP.Untuk memastikan kelancaran layanan masuk dan ping CVM jarak jauh, buka 22, 3389, dan layanan ICMP di grup keamanan.
![](https://console.cloud.tencent.com/cvm/instance/index?rid=1)
2.Ikat grup keamanan ke instance CVM
1.Di [Konsol CVM](https://console.intl.cloud.tencent.com/cvm/instance/index?rid=1), klik ID instance CVM yang terikat ke instance CLB untuk masuk ke halaman detail.
2.Pilih tab **Security Group** (Grup Keamanan) dan klik **Bind** (Ikat) di modul **Bound Security Groups** (Grup Keamanan Terikat).
3.Pada jendela **Configure Security Group** (Konfigurasi Grup Keamanan) yang muncul, pilih grup keamanan yang terikat ke instance CVM dan klik **OK**.      <img alt="" src="https://main.qcloudimg.com/raw/6e0e1c2f834bb7425ef3ca010114165a.png" title="Click to view the original image">

