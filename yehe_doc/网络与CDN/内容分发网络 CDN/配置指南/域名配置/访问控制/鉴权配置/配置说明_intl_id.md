
## Skenario Konfigurasi
Umumnya, konten yang dikirimkan melalui CDN adalah sumber daya publik secara default, yang dapat diakses oleh pengguna dengan URL.Untuk mencegah pengguna yang berniat buruk menautkan konten Anda untuk mencari keuntungan, Anda dapat mengonfigurasi autentikasi stempel waktu lanjutan selain kebijakan kontrol akses seperti daftar blokir/daftar izin referer, daftar blokir/daftar izin IP, dan batas frekuensi akses IP.

> !Setelah perlindungan hotlink stempel waktu dikonfigurasi, klien perlu menghitung tanda tangan yang dikonfigurasi dan membawanya ke server saat memulai permintaan.Simpul CDN akan mengautentikasi tanda tangan tersebut di server, yang hanya akan diteruskan setelah autentikasi berhasil.

## Panduan Konfigurasi
### Melihat konfigurasi
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, dan klik **Manage** (Kelola) di sebelah kanan nama domain untuk mengakses halaman konfigurasinya.Di bawah tab **Security Configuration** (Konfigurasi Keamanan), temukan konfigurasi autentikasi, yang dinonaktifkan secara default:
![](https://main.qcloudimg.com/raw/1efe407c5a9f2fc8f8837d5b1cdbb3d7.png)

### Memodifikasi konfigurasi
#### 1.Memodifikasi konfigurasi
CDN menyediakan empat model penghitungan tanda tangan autentikasi pilihan Anda.Anda dapat menggunakan **Authentication Calculator** (Kalkulator Autentikasi) yang disediakan untuk melihat model ini.Untuk informasi selengkapnya tentang efek konfigurasi dan algoritme, silakan lihat dokumen algoritme khusus untuk [TipeA](https://intl.cloud.tencent.com/document/product/228/35222), [TipeB](https://intl.cloud.tencent.com/document/product/228/35223), [TipeC](https://intl.cloud.tencent.com/document/product/228/35224), dan [TipeD](https://intl.cloud.tencent.com/document/product/228/35225):
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2.Menonaktifkan konfigurasi
Anda dapat mengalihkan switch konfigurasi autentikasi untuk menonaktifkan fitur ini.Saat switch dinonaktifkan, konfigurasi apa pun yang ada tidak akan diterapkan di lingkungan produksi.Jika Anda mengaktifkan switch, sebuah pesan akan ditampilkan yang meminta konfirmasi Anda sebelum konfigurasi diterapkan di seluruh jaringan.
![](https://main.qcloudimg.com/raw/f892392e86acae153ef7821944888155.png)

#### 3.Menambahkan konfigurasi khusus wilayah
Jika nama domain akselerasi Anda dikonfigurasi untuk akselerasi global dan Anda ingin akselerasi di dalam dan di luar Tiongkok Daratan memiliki konfigurasi autentikasi yang berbeda, Anda dapat mengeklik **Add Special Configuration** (Tambahkan Konfigurasi Khusus) di bawah konfigurasi.
![](https://main.qcloudimg.com/raw/8e6e0e08ef230322f4366a4fa92288e0.png)

> !Saat ini, item konfigurasi khusus wilayah yang ditambahkan tidak dapat dihapus, tetapi item tersebut hanya dapat dinonaktifkan.

## Sampel Konfigurasi
Misalkan nama domain `cloud.tencent.com` dikonfigurasi untuk akselerasi global dan konfigurasi autentikasi adalah sebagai berikut:
![](https://main.qcloudimg.com/raw/1d82f89f383aa35f5d7ae679f19669fb.png)
Efek aktualnya adalah sebagai berikut:

1.Seorang pengguna di Tiongkok Daratan dapat mengakses sumber daya `http://cloud.tencent.com/1.jpg` dengan memulai permintaan secara langsung.
2.Pengguna di luar Tiongkok Daratan dapat mengakses sumber daya `http://cloud.tencent.com/1.jpg` dengan memulai permintaan dengan URL dalam format `http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg`.


## Kode sampel

Berikut ini adalah metode penghitungan autentikasi dengan Demo for Python sebagai contoh:

```
import requests
import json
import sys
import time
import hashlib

def generate_url(category, ts=None):
url = 'http://www.test.com'              # Nama domain pengujian
path = '/1.txt'                                     # Jalur akses
suffix = '?a=1&b=2'                                 # Parameter URL
key = 'abc123456789'                                # Kunci autentikasi
now = int(time.mktime(time.strptime(ts, "%Y%m%d%H%M%S")) if ts else time.time())                # Jika `ts` dimasukkan, `ts` tersebut akan digunakan; jika tidak, `ts` saat ini akan digunakan
sign_key = 'key'                                    # Bidang tanda tangan URL
time_key = 't'                                      # Bidang waktu URL
ttl_format = 10                                     # Format waktu.Nilai valid:10, 16.Ini hanya didukung untuk tipe D
if category == 'A':# Tipe A
ts = now
rand_str = '123abc'
sign = hashlib.md5('%s-%s-%s-%s-%s' % (path, ts, rand_str, 0, key)).hexdigest()
request_url = '%s%s?%s=%s' % (url, path, sign_key, '%s-%s-%s-%s' % (ts, rand_str, 0, sign))
print(request_url)
elif category == 'B':# Tipe B
ts = time.strftime('%Y%m%d%H%M', time.localtime(now))
sign = hashlib.md5('%s%s%s' % (key, ts, path)).hexdigest()
request_url = '%s/%s/%s%s%s' % (url, ts, sign, path, suffix)
print(request_url)
elif category == 'C':# Tipe C
ts = hex(now)[2:]
sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
request_url = '%s/%s/%s%s%s' % (url, sign, ts, path, suffix)
print(request_url)
elif category == 'D':# Tipe D
ts = now if ttl_format == 10 else hex(now)[2:]
sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
request_url = '%s%s?%s=%s&%s=%s' % (url, path, sign_key, sign, time_key, ts)
print(request_url)


if __name__ == '__main__':
if len(sys.argv) == 1:
print('usage: python generate_url.py A 20200501000000')
args = sys.argv[1:]
generate_url(*args)
```
