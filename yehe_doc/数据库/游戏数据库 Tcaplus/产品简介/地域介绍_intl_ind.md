Pusat data TencentDB dihosting di beberapa lokasi di seluruh dunia. Lokasi ini dikenal sebagai wilayah. Setiap wilayah merupakan area geografis yang berdiri sendiri.
Nama wilayah dapat secara langsung menunjukkan cakupan pusat data. Konvensi penamaan berikut digunakan demi kenyamanan Anda:
Nama wilayah terdiri dari **region + city** (wilayah + kota). `region` menunjukkan wilayah geografis yang dicakup oleh pusat data, sedangkan `city` mewakili kota di dalam atau di dekat pusat data tersebut.


>?TcaplusDB tidak membagi instans berdasarkan urutan AZ.

## Cara Memilih Wilayah
Wilayah Tencent Cloud benar-benar terisolasi. Hal ini menjamin stabilitas lintas wilayah maksimum dan toleransi kesalahan. Saat membeli layanan Tencent Cloud, sebaiknya pilih wilayah yang paling dekat dengan pengguna akhir Anda untuk meminimalkan latensi akses dan meningkatkan kecepatan unduhan. Operasi seperti meluncurkan atau melihat instans dilakukan di tingkat wilayah.
Catatan tentang komunikasi jaringan pribadi:
- Sumber daya Tencent Cloud di wilayah yang sama (di bawah akun yang sama dan di VPC yang sama) dapat berkomunikasi satu sama lain melalui jaringan pribadi. Sumber daya ini juga dapat diakses melalui [IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225).
- Jaringan dari wilayah yang berbeda sepenuhnya terisolasi satu sama lain, dan layanan Tencent Cloud di wilayah yang berbeda tidak dapat berkomunikasi satu sama lain melalui jaringan pribadi secara default.
- Layanan Tencent Cloud di berbagai wilayah dapat berkomunikasi satu sama lain dengan mengakses internet melalui [IP publik](https://intl.cloud.tencent.com/document/product/213/5224). Layanan Tencent Cloud di VPC yang berbeda dapat berkomunikasi satu sama lain melalui [CCN](https://intl.cloud.tencent.com/document/product/1003), yang lebih cepat dan stabil.


## Daftar Wilayah
TcaplusDB membagi instans hanya berdasarkan wilayah dan tersedia di wilayah berikut:

## Tiongkok
| Wilayah | Pengidentifikasi | 
|---------|---------|
| Tiongkok Timur (Shanghai) | ap-shanghai | 
| Hong Kong/Makau/Taiwan (Hong Kong, Tiongkok) | ap-hongkong |

### Negara/wilayah lain
| Wilayah | Pengidentifikasi | 
|---------|---------|
| Asia Tenggara Pasifik (Singapura) | ap-singapore | 
| Asia Pasifik Timur Laut (Seoul) | ap-seoul |
| Asia Timur Laut Pasifik (Tokyo) | ap-tokyo |
| AS Barat (Silicon Valley) | na-siliconvalley |
| AS Timur (Virginia) | na-ashburn |
| Eropa (Frankfurt) | eu-frankfurt |


