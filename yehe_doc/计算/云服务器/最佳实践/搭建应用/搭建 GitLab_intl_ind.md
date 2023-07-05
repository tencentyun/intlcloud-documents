## Ikhtisar
GitLab adalah sistem manajemen versi sumber terbuka berbasis Ruby. Sistem ini menyediakan alat manajemen kode Git dan repositori Git yang dihosting secara mandiri untuk mendukung akses Web Anda ke proyek publik dan pribadi. Dokumen ini menjelaskan cara menginstal dan menggunakan GitLab di CVM Tencent Cloud.



## Perangkat Lunak
Instans CVM perlu dikonfigurasi dengan:
- vCPU: 2 core
- Memori: 4 GB
- Sistem operasi Linux: dokumen ini menggunakan CentOS 7.7 sebagai contoh

## Prasyarat
- CVM Linux diperlukan untuk menginstal GitLab. Jika Anda belum membeli CVM Linux, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
- Aturan grup keamanan untuk instans Linux telah dikonfigurasi. Buka port 80. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).

## Petunjuk
### Menginstal GitLab
1. Lihat [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
 - [Login ke Instans Linux melalui Fitur Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
2. Jalankan perintah berikut untuk menginstal dependensi.
```
yum install -y curl policycoreutils-python openssh-server
```
3. Jalankan perintah berikut secara berurutan untuk mengaktifkan autostart layanan SSH dan memulai layanan SSH.
```
systemctl enable sshd
```
```
systemctl start sshd
```
4. Jalankan perintah berikut untuk menginstal Postfix.
```
yum install -y postfix
```
5. Jalankan perintah berikut untuk mengaktifkan autostart layanan Postfix.
```
systemctl enable postfix
```
6. Jalankan perintah berikut untuk membuka file konfigurasi Postfix main.cf.
```
vim /etc/postfix/main.cf
```
7. Tekan **i** (i) untuk masuk ke mode pengeditan. Hapus `#` sebelum `inet_interfaces = all`, dan tambahkan `#` sebelum `inet_interfaces = localhost`, seperti yang ditunjukkan di bawah ini: 
![](https://main.qcloudimg.com/raw/57fa73bdcd05343b5dcee24e47b5f09a.png)
8. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
9. Jalankan perintah berikut untuk memulai Postfix.
```
systemctl start postfix
```
10. Jalankan perintah berikut untuk menambahkan repositori perangkat lunak GitLab.
```
 curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
11. Jalankan perintah berikut untuk menginstal GitLab.
```
sudo EXTERNAL_URL="Public IP address of the instance" yum install -y gitlab-ce
```
Untuk informasi selengkapnya tentang cara mendapatkan IP publik instans, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
12. Di browser lokal, kunjungi alamat IP publik yang Anda peroleh. Jika halaman berikut muncul, artinya GitLab telah berhasil diinstal.
>!Konfigurasikan kata sandi untuk akun GitLab Anda di sini.
>
![](https://main.qcloudimg.com/raw/791f5250c2bca059369a141c047f2c21.png)


### Membuat proyek
1. Di browser lokal, kunjungi alamat IP publik CVM Anda untuk mengakses halaman login GitLab. Masukkan akun `root` Anda dan kata sandi yang dikonfigurasi, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c0639741b40c1fa33d41434c0222c13b.png)
2. Buat proyek pribadi seperti yang diinstruksikan. Dokumen ini menggunakan `test` sebagai contoh pada gambar berikut:
![](https://main.qcloudimg.com/raw/912805dfffcba06558d3adbe8b33b4bc.png)
3. Setelah proyek dibuat, klik **Add SSH Key** (Tambahkan Kunci SSH) di bagian atas halaman.
4. Pada halaman **SSH Keys** (Kunci SSH), tambahkan kunci SSH dengan melakukan langkah-langkah berikut:
 1. [Dapatkan kunci](#getKey) untuk PC yang akan dikelola oleh proyek dan tempelkan di bidang `Key`.
 2. Masukkan nama kunci di bidang `Title`.
 3. Klik **Add key** (Tambahkan kunci) seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/c8d21821f0d6919a650cf36d43666f06.png)
Jika hasilnya mirip dengan gambar berikut, artinya kunci telah berhasil ditambahkan:
![](https://main.qcloudimg.com/raw/6908a9710bd01d57c01892b31247bc02.png)
5. <span id="Step5"></span>Di beranda proyek, klik **clone** (kloning) untuk mencatat alamat proyek, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/972726ec33e5a92c0a778a700ae9b4b0.png)


### Proyek kloning
1. Jalankan perintah berikut pada PC yang dikelola untuk mengonfigurasi nama pengguna repositori Git.
```
git config --global user.name "username" 
```
2. Jalankan perintah berikut untuk mengonfigurasi email untuk nama pengguna.
```
git config --global user.email "xxx@example.com" 
```
3. Jalankan perintah berikut untuk mengkloning proyek. Ganti alamat proyek dengan nilai aktual yang diperoleh di [Langkah 5](#Step5).
```
git clone “Project address”
```
Setelah proyek berhasil dikloning, direktori yang sama dan semua file proyek akan dibuat di komputer lokal Anda.

### Mengunggah file
1. Jalankan perintah berikut untuk mengakses direktori proyek.
```
cd test/
```
2. Jalankan perintah berikut untuk membuat file target yang akan diunggah ke GitLab. Dokumen ini menggunakan file test.sh sebagai contoh.
```
echo "test" > test.sh
```
3. Jalankan perintah berikut untuk menambahkan file test.sh ke indeks.
```
git add test.sh
```
4. Jalankan perintah berikut untuk mengirimkan test.sh ke repositori lokal.
```
git commit -m "test.sh"
```
5. Jalankan perintah berikut untuk menyinkronkan file test.sh dengan server GitLab.
```
git push -u origin master
```
Kembali ke halaman proyek pengujian. Anda sekarang dapat melihat file di halaman, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/e208c7a0f7399e4a42a1bb3d17a89c1c.png)

## Operasi yang Relevan
### Mendapatkan kunci<span id="getKey"></span>
1. Pada PC yang akan dikelola oleh proyek, jalankan perintah berikut untuk menginstal Git.
```
yum install -y git
```
2. Jalankan perintah berikut untuk menghasilkan file kunci “.ssh/id_rsa”. Selama proses pembuatan file kunci, tekan **Enter** (Enter) untuk mempertahankan konfigurasi default.
```
ssh-keygen
```
3. Jalankan perintah berikut untuk melihat dan mencatat informasi kunci.
```
cat .ssh/id_rsa.pub
```
