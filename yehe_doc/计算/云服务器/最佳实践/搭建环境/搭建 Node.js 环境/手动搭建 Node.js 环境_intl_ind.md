## Pengantar
Artikel ini menjelaskan cara men-deploy Node.js pada CVM dan membuat proyek sampel.

Untuk melakukan langkah ini, pahami perintah umum Linux seperti [Menginstal Perangkat Lunak melalui YUM di Lingkungan CentOS](https://intl.cloud.tencent.com/document/product/213/2046) dan pahami versi perangkat lunak yang diinstal.

## Perangkat Lunak
Menyiapkan Node.js menggunakan:
- CentOS: distribusi sistem operasi Linux. Kami menggunakan CentOS 7.6 dalam artikel ini.
- Node.js: lingkungan waktu proses JavaScript. Kami menggunakan Node.js 10.16.3 dan Node.js 6.9.5 dalam artikel ini.
- npm: pengelola paket untuk JavaScript. Kami menggunakan npm 6.9.0 dalam artikel ini untuk mengelola beberapa versi Node.js.

## Prasyarat
Untuk menyiapkan Node.js, Anda memerlukan CVM Linux. Jika Anda belum membelinya, lihat [Memulai CVM Linux](http://intl.cloud.tencent.com/document/product/213/2936).

## Petunjuk
### Langkah 1: Login ke instans Linux
[Login ke instans Linux menggunakan WebShell (direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang nyaman bagi Anda:
- [Login ke instans Linux menggunakan perangkat lunak login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502).
- [Login ke Instans Linux menggunakan SSH](https://intl.cloud.tencent.com/document/product/213/32501)


### Langkah 2: Menginstal Node.js
1. Jalankan perintah berikut untuk mengunduh paket penginstalan 64-bit Node.js untuk Linux.
```
wget https://nodejs.org/dist/v10.16.3/node-v10.16.3-linux-x64.tar.xz
```
>Buka [situs web resmi Node.js](https://nodejs.org/download/) untuk informasi selengkapnya.
>
2. Jalankan perintah berikut untuk mendekompresi paket penginstalan.
```
tar xvf node-v10.16.3-linux-x64.tar.xz
```
3. Jalankan perintah berikut untuk membuat tautan simbolik.
```
ln -s /root/node-v10.16.3-linux-x64/bin/node /usr/local/bin/node
```
```
ln -s /root/node-v10.16.3-linux-x64/bin/npm /usr/local/bin/npm
```
Setelah dibuat, Anda dapat menggunakan perintah node dan npm di direktori CVM mana pun.
4. Jalankan perintah berikut untuk melihat versi Node.js dan npm.
```
node -v
```
```
npm -v
```

### Langkah 3: Menginstal beberapa versi Node.js (opsional)
>Proses ini memungkinkan Anda menginstal beberapa versi Node.js. Developer dapat menggunakan ini untuk beralih antar versi dengan cepat.
>
1. Jalankan perintah berikut untuk menginstal git.
```
yum install -y git
```
2. Jalankan perintah berikut untuk mengunduh kode sumber NVM dan memeriksa versi terbaru.
```
git clone https://github.com/cnpm/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
```
3. Jalankan yang berikut ini untuk mengonfigurasi variabel lingkungan NVM.
```
echo ". ~/.nvm/nvm.sh" >> /etc/profile
```
4. Jalankan perintah berikut untuk membaca variabel lingkungan sistem.
```
source /etc/profile
```
5. Jalankan perintah berikut untuk melihat semua versi Node.js.
```
nvm list-remote
```
6. Jalankan perintah berikut untuk menginstal beberapa versi Node.js.
```
nvm install v6.9.5
```
```
nvm install v10.16.3
```
7. Jalankan perintah berikut untuk melihat semua versi Node.js yang terinstal.
```
nvm ls
```
Jika muncul hasil berikut, artinya penginstalan berhasil dan versi yang digunakan saat ini adalah Node.js 10.16.3.
![](https://main.qcloudimg.com/raw/a315fe51314357fb44ec725f20c101ed.png)
8. Jalankan tombol perintah berikut ke versi lain.
```
nvm use v6.9.5
```
Hasil berikut akan muncul:
![](https://main.qcloudimg.com/raw/817fd96fef77f818e65ce41a3723e5bc.png)

### Langkah 4: Membuat proyek sampel
1. Jalankan perintah berikut untuk membuat file bernama `index.js` pada bagian jalur root.
```
cd ~
```
```
vim index.js
```
2. Tekan **i** (i) untuk masuk ke mode edit dan masukkan konten berikut ini ke dalam file `index.js`:
```
const http = require('http');
const hostname = '0.0.0.0';
const port = 7500;
const server = http.createServer((req, res) => { 
    if (res.statusCode === 200) {
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World\n');
}); 
server.listen(port, hostname, () => { 
    console.log(`Server running at http://${hostname}:${port}/`);
});
```
>Artikel ini menggunakan port 7500 dalam file `index.js`. Anda dapat menggunakan port lain sesuai kebutuhan.
>
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file dan kembali.
4. Jalankan perintah berikut untuk menjalankan proyek Node.js yang baru saja dibuat.
```
node index.js
```
5. Buka jendela browser di mesin lokal Anda dan kunjungi URL berikut untuk memeriksa apakah proyek telah berhasil dijalankan.
```
http://CVM_Public_IP:Port
```
Jika hasil berikut muncul, artinya Node.js berhasil diinstal.
![](https://main.qcloudimg.com/raw/5b72798dc9e988eee8d8186055aa45e9.png)


## Pertanyaan Umum
Jika Anda mengalami masalah saat menggunakan CVM, lihat dokumen berikut untuk pemecahan masalah berdasarkan situasi aktual Anda.
- Untuk masalah terkait login CVM, lihat [Login Kata Sandi dan Login Kunci SSH](https://intl.cloud.tencent.com/document/product/213/18120) dan [Akses Login dan Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/17278).
- Untuk masalah terkait jaringan CVM, lihat [Alamat IP](https://intl.cloud.tencent.com/document/product/213/17285) dan [Grup Port dan Keamanan](https://intl.cloud.tencent.com/document/product/213/2502).
- Untuk masalah terkait disk CVM, lihat [Disk Sistem dan Data](https://intl.cloud.tencent.com/document/product/213/17351).

