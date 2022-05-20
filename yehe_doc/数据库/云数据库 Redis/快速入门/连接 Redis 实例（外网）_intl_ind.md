## Ikhtisar
TencentDB for Redis tidak mendukung akses langsung melalui jaringan publik, tetapi Anda dapat menggunakan instans CVM dengan IP publik guna mengakses instans Redis melalui jaringan publik melalui penerusan port.
>?Penerusan port dengan iptables tidak stabil, karena itu kami tidak merekomendasikan solusi akses jaringan publik ini di lingkungan produksi.
>
![](https://main.qcloudimg.com/raw/bd7f9a09c2e01aac1adce409b949afe3.jpg)

## Petunjuk
1. Login ke [CVM](https://intl.cloud.tencent.com/document/product/213/5436) dan aktifkan fitur penerusan IP.
>?Instans CVM dan TencentDB harus berada di bawah akun yang sama dan di VPC yang sama di wilayah yang sama, atau keduanya di jaringan klasik.
>
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```
2. Konfigurasikan aturan penerusan. Kode contoh berikut adalah untuk meneruskan permintaan akses `26.xx.x.2:10001` (IP publik CVM dan port yang dapat disesuaikan) ke instans Redis yang IP dan port pribadinya adalah `10.0.0.5:6379`.
```
iptables -t nat -A PREROUTING -p tcp --dport 10001 -j DNAT --to-destination 10.0.0.5:6379
iptables -t nat -A POSTROUTING -d 10.0.0.5 -p tcp --dport 6379 -j MASQUERADE
```
3. Konfigurasikan [grup keamanan](https://intl.cloud.tencent.com/document/product/213/34272) untuk membuka port publik instans CVM. Kami menyarankan Anda mengonfigurasi aturan grup keamanan untuk mengizinkan hanya sumber yang perlu terhubung ke instans Redis.
4. Untuk terhubung ke instans Redis di jaringan pribadi menggunakan alamat jaringan publik (`26.xx.xx.2:10001` dalam kode contoh), Anda dapat menggunakan perintah yang sama dengan perintah koneksi jaringan pribadi. Untuk informasi selengkapnya, lihat [Menghubungkan ke Instans TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/9897).
5. Setelah terhubung ke instans Redis, jalankan perintah `info`. Jika informasi database ditampilkan, berarti koneksi berhasil.

