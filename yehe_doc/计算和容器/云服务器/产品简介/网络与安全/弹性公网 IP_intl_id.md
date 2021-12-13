## Ikhtisar

Elastic Public IP, atau ElP, adalah IP statis yang dirancang untuk komputasi cloud dinamis dan IP publik tetap di wilayah tertentu. Dengan EIP, Anda dapat memetakan alamat ke instans lain dengan cepat (atau instans gateway NAT) di akun Anda agar instans tidak mengalami kegagalan.

Anda dapat menyimpan EIP di akun Anda hingga dirilis. Sementara IP publik hanya dapat dirilis dengan CVM, EIP dapat dipisahkan dari siklus pemakaian CVM dan beroperasi secara independen sebagai sumber daya cloud. Misalnya, jika Anda perlu mempertahankan IP publik yang sangat terkait dengan bisnis, Anda dapat mengubahnya menjadi EIP dan menyimpannya di akun Anda.

## Aturan dan Batasan

### Aturan Penggunaan

- Alamat EIP diterapkan secara bersamaan ke instans di jaringan dasar dan VPC, serta instans [gateway NAT](https://intl.cloud.tencent.com/document/product/1015) di VPC.
- Saat EIP terikat ke instans CVM, IP publik saat ini dari instans akan dirilis.
- Saat instans gateway CVM/NAT dihentikan, maka tidak akan dikaitkan dari EIP-nya.
- Untuk detail tentang aturan penagihan EIP, lihat [Penagihan untuk Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/17156).
- Untuk pengoperasian EIP langkah demi langkah, lihat [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/16586).
 
### Batasan Kuota

| Sumber Daya            | Batas         |
|---------|:---------:|
| Kuota EIP untuk setiap akun Tencent Cloud di setiap wilayah | 20 |
| Jumlah aplikasi pembelian harian setiap akun Tencent Cloud di setiap wilayah | Kuota \* 2 kali |
| Berapa kali IP publik dapat dialihkan ke setiap akun secara gratis per hari saat EIP tidak terikat | 10 kali |

> Penyesuaian kuota EIP tidak didukung secara default. Anda dapat melakukan konvergensi IP melalui [Gateway NAT](https://intl.cloud.tencent.com/product/nat) dan [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
> - Jika Anda harus menyesuaikan kuota EIP, akun Anda harus memiliki jumlah sumber daya CVM yang sesuai agar dapat digunakan dengan baik.
> - Jika diperlukan kuota yang lebih tinggi, mungkin akan dikenakan biaya.
> - Jika Anda sering mengubah IP atau melanggar hukum yang berlaku setelah penyesuaian, Tencent Cloud berhak mencabut kuota.
>


### Batasan IP publik yang terikat ke CVM

Sejak 18 September 2019 (inklusif), jumlah maksimum IP publik yang dapat diikat ke satu CVM telah diubah berdasarkan konfigurasi CPU.
> Batasan ini tidak berlaku untuk CVM yang dibeli sebelum pukul 00.00 pada tanggal 18 September 2019.
>
| Jumlah CPU CVM | Jumlah maksimum IP publik yang dapat diikat ke CVM (termasuk IP publik dan EIP) |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



