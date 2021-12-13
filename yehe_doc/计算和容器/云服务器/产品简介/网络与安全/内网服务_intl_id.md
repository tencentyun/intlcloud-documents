Layanan jaringan pribadi adalah layanan LAN, tempat layanan cloud dapat saling mengakses melalui tautan internal. Layanan Tencent Cloud dapat saling mengakses melalui [akses internet](https://intl.cloud.tencent.com/document/product/213/5224) atau jaringan pribadi Tencent Cloud. Pusat data Tencent Cloud saling terhubung dengan jaringan dasar megabyte/gigabyte. Pusat data tersebut memungkinkan komunikasi melalui jaringan pribadi dengan bandwidth besar dan latensi rendah, yang tidak dipungut biaya jika berada di wilayah yang sama untuk membantu Anda membangun arsitektur jaringan secara fleksibel.
## Alamat IP Pribadi
### Ringkasan
IP pribadi adalah alamat yang tidak dapat diakses melalui Internet, berdasarkan jaringan pribadi Tencent Cloud yang dibuat. Setiap instans memiliki antarmuka jaringan default (yaitu, eth0) untuk menetapkan IP pribadi. IP Pribadi dapat ditetapkan secara otomatis oleh Tencent Cloud, atau Anda dapat menyesuaikannya (hanya pada [VPC](https://intl.cloud.tencent.com/document/product/215/535)).
> Jika Anda mengubah IP pribadi dalam sistem operasi, jaringan pribadi dapat terganggu.
>

### Atribut
 - Jaringan pribadi peka terhadap pengguna, dan pengguna yang berbeda terisolasi satu sama lain. Secara default, layanan cloud pengguna lain tidak dapat diakses melalui jaringan pribadi.
 - Jaringan pribadi peka terhadap wilayah, dan wilayah yang berbeda terisolasi satu sama lain. Secara default, layanan cloud yang menggunakan akun yang sama di wilayah yang berbeda tidak dapat diakses melalui jaringan pribadi.

### Skenario Aplikasi
IP Pribadi dapat digunakan untuk komunikasi antara CLB dan instans CVM, dan antara instans CVM dan layanan Tencent Cloud lainnya (seperti TencentDB).

### Penetapan Alamat
Setiap instans CVM akan diberi alamat IP pribadi default saat dimulai. IP pribadi berbeda-beda berdasarkan [lingkungan jaringan](https://intl.cloud.tencent.com/document/product/213/5227):
 - Jaringan dasar: alamat IP pribadi ditetapkan secara otomatis oleh Tencent Cloud dan tidak dapat diubah.
 - VPC: Tencent Cloud VPC CIDR saat ini memungkinkan Anda menggunakan salah satu rentang IP berikut, serta mask maksimum dan minimumnya adalah /16 dan /28:
  - **10.0**.0.0 - **10.255**.255.255
  - **172.16**.0.0 - **172.31**.255.255
  - **192.168**.0.0 - **192.168**.255.255

## DNS Jaringan Pribadi 
### Alamat Server DNS
Layanan DNS jaringan pribadi digunakan untuk resolusi nama domain. Jika DNS dikonfigurasi dengan tidak benar, nama domain tidak dapat diakses.
Tencent Cloud menyediakan server DNS jaringan pribadi yang andal di berbagai wilayah. Konfigurasi tertentu ditunjukkan di bawah ini:
<table><tbody>
<tr><th>Lingkungan Jaringan</th><th>Wilayah</th><th>Server DNS Jaringan Pribadi</th></tr>
<tr><td rowspan="14">Jaringan Dasar</td><td rowspan="4">Guangzhou</td><td>Zona 1 Guangzhou: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Zona 2 Guangzhou: <br>10.112.65.31<br>10.112.65.32</td></tr>
<tr><td>Zona 3 Guangzhou: <br>10.59.218.193<br>10.59.218.194</td></tr>
<tr><td>Zona 4 Guangzhou: <br>100.121.190.140<br>100.121.190.141</td></tr>
<tr><td>Shanghai</td><td>10.236.158.114<br>10.236.158.106</td></tr>
<tr><td>Beijing</td><td>10.53.216.182<br>10.53.216.198</td></tr>
<tr><td>Amerika Utara</td><td>10.116.19.188<br>10.116.19.185</td></tr>
<tr><td>Hong Kong, Tiongkok</td><td>10.243.28.52<br>10.164.55.3</td></tr>
<tr><td>Singapura</td><td>100.78.90.19<br>100.78.90.8</td></tr>
<tr><td>Zona Terbuka Guangzhou</td><td>10.59.218.18<br>10.112.65.51</td></tr>
<tr><td>Chendu</td><td>100.88.222.14<br>100.88.222.16</td></tr>
<tr><td>Silicon Valley</td><td>100.102.22.21<br>100.102.22.30</td></tr>
<tr><td>Frankfurt</td><td>100.120.52.60<br>100.120.52.61</td></tr>
<tr><td>Seoul</td><td>10.165.180.53<br>10.165.180.62</td></tr>
<tr><td>VPC</td><td>Semua Wilayah</td><td>183.60.83.19<br>183.60.82.98</td></tr>
</tbody>
</table>

## Panduan Operasi
Anda dapat melihat atau mengubah alamat IP pribadi instans. Untuk mengetahui petunjuk mendetail, lihat:
- [Mendapatkan Alamat IP Pribadi dari Instans dan Pengaturan DNS Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/17941)
- [Mengubah Alamat IP Pribadi](https://intl.cloud.tencent.com/document/product/213/16561)
