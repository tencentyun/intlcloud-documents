## Ikhtisar
Dokumen ini menjelaskan cara membuat dan menggunakan Docker pada instans CVM Tencent Cloud, dan dirancang untuk developer CVM baru yang memahami sistem operasi Linux.

## Perangkat Lunak

Dokumen ini menggunakan perangkat lunak berikut untuk membangun lingkungan Docker:
- Sistem operasi: Sistem operasi Linux. Dokumen ini menggunakan CentOS 7.6 sebagai contoh.
>? Docker harus dibangun pada sistem operasi 64-bit dengan versi kernel 3.10 atau yang lebih baru.
>

## Prasyarat
CVM Linux diperlukan untuk menyiapkan lingkungan Docker. Jika Anda belum membeli CVM Linux, lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).
>? Docker harus dibangun pada sistem operasi 64-bit dengan versi kernel 3.10 atau yang lebih baru.
>

## Petunjuk

### Menginstal Docker

1. Lihat [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436). Anda juga dapat menggunakan metode login lain yang lebih nyaman bagi Anda:
 - [Login ke Instans Linux melalui Fitur Login Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Login ke Instans Linux melalui Kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501)
2. Jalankan perintah berikut secara berurutan untuk menambahkan repositori yum.
```
yum update
```
```
yum install epel-release -y
```
```
yum clean all
```
```
yum list
```
3. Jalankan perintah berikut untuk menginstal Docker.
```
yum install docker-io -y
```
4. Jalankan perintah berikut untuk menjalankan Docker.
```
systemctl start docker
```
5. Jalankan perintah berikut untuk memeriksa hasil penginstalan.
```
docker info
```
Jika Anda melihat perintah berikut, hal ini menunjukkan bahwa Docker telah berhasil diinstal.
![](https://main.qcloudimg.com/raw/a848737e9d011f528f66dc54fca61c08.png)


### Menggunakan Docker
Anda dapat menggunakan Docker dengan perintah berikut:
- Kelola daemon Docker.
 - Jalankan daemon Docker.
```
systemctl start docker
```
 - Hentikan daemon Docker.
```
systemctl stop docker
```
 - Mulai ulang daemon Docker.
```
systemctl restart docker
```
- Kelola citra. Dokumen ini menggunakan citra Nginx dari Docker Hub sebagai contoh.
```
docker pull nginx 
```
 - Ubah tag citra untuk membantu Anda mengidentifikasi citra.
```
docker tag docker.io/nginx:latest tencentyun/nginx:v1
```
 - Lakukan kueri pada citra yang sudah ada.
```
docker images
```
 - Hapus citra secara paksa.
```
docker rmi -f tencentyun/nginx:v1
```
- Kelola kontainer.
 - Masukkan kontainer.
```
docker run -it ImageId /bin/bash
```
Jalankan perintah `docker images` untuk mendapatkan nilai `ImageId`.
 - Keluar dari kontainer. Jalankan perintah `exit` untuk keluar dari kontainer.
 - Masukkan kontainer yang berjalan di latar belakang.
```
docker exec -it container ID /bin/bash
```
 - Buat citra dari kontainer.
```
docker commit <container ID or container name> [<repository name>[:<tag>]]
```
Misalnya:
```
docker commit 1c23456cd7**** tencentyun/nginx:v2
```

### Membuat citra

1. Jalankan perintah berikut untuk membuka file "Dockerfile".
```
vim Dockerfile
```
2. Tekan **i** (i) untuk beralih ke mode edit dan masukkan konten berikut:
```
FROM tencentyun/nginx:v2  #Deklarasikan citra dasar.
MAINTAINER DTSTACK #Deklarasikan pemilik citra.
RUN mkdir /dtstact #Tambahkan perintah yang perlu dijalankan sebelum kontainer dimulai setelah perintah RUN. Karena file Dockerfile hanya dapat berisi maksimal 127 baris, sebaiknya Anda menulis dan menjalankan perintah dalam skrip.
ENTRYPOINT ping https://cloud.tencent.com/ #Perintah yang dijalankan saat startup. Perintah terakhir harus berupa perintah frontend yang berjalan terus-menerus. Jika tidak, kontainer akan keluar setelah menjalankan semua perintah.
```
3. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file.
4. Jalankan perintah berikut untuk membuat citra.
```
docker build -t nginxos:v1 .  #Titik tunggal (.) menentukan jalur Dockerfile dan harus disertakan.
```
5. Jalankan perintah berikut untuk memeriksa apakah citra telah dibuat.
```
docker images
```
6. Jalankan perintah berikut secara berurutan untuk menjalankan dan memeriksa kontainer.
```
docker run -d nginxos:v1 #Jalankan kontainer di latar belakang.
docker ps                        #Periksa kontainer yang sedang berjalan.
docker ps -a                     #Periksa semua kontainer termasuk yang tidak berjalan.
docker logs CONTAINER ID/IMAGE   #Periksa log startup untuk memecahkan masalah berdasarkan ID kontainer atau nama jika Anda tidak melihat kontainer dalam hasil yang ditampilkan
```
7. Jalankan perintah berikut secara berurutan untuk membuat citra.
```
docker commit fb2844b6**** nginxweb:v2 #Tambahkan ID kontainer serta nama dan versi citra baru. setelah perintah penerapan.
docker images                    #Daftar citra lokal yang telah diunduh dan dibuat.
```
8. Jalankan perintah berikut untuk mendorong citra ke repositori jarak jauh.
Citra didorong ke Docker Hub secara default. Untuk mendorong citra, login ke Docker, beri tag, dan beri nama citra dalam format berikut: `Docker username/image name: tag`.
```
docker login #Masukkan nama pengguna dan kata sandi registri citra setelah menjalankan perintah
docker tag [image name]:[tag] [username]:[tag]
docker push [username]:[tag]
```
Setelah citra didorong, Anda dapat login ke Docker Hub untuk melihat citra.



