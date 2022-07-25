TS melalui SRT mengirimkan langsung streaming TS yang berisi data audio/video menggunakan **SRT protocol** (protokol SRT). Sistem streaming langsung yang ada saat ini digunakan untuk pemutaran ulang. TS melalui SRT digunakan sebagai format push standar untuk perangkat keras Haivision dan OBS.
Dalam mode ini, server SRT mengurai streaming TS, melakukan remuxing pada streaming RTMP, dan meneruskan ke server RTMP backend.
![](https://main.qcloudimg.com/raw/0124f28a30572bb0b0f1b0f6fbcb8d86.png)

>! Penggunaan SRT untuk push tidak menyebabkan peningkatan biaya.

## Perbandingan Tingkat Lag Upstream
Penggunaan SRT untuk melakukan push pada streaming akan mengurangi lag, seperti yang ditampilkan di gambar berikut:
![](https://main.qcloudimg.com/raw/c0bc00e4f081c142ed3c01ed8427d862.png)


## Perbandingan Tingkat Kehilangan Paket
Penggunaan SRT untuk melakukan push pada streaming akan mengoptimalkan performa upstream sehingga menghasilkan pemutaran ulang yang lebih lancar. Tabel berikut menunjukkan perbandingan performa untuk aplikasi Douyu.
- Android: data pengujian performa push melalui SRT (perangkat pengujian — Mi 9):
![](https://main.qcloudimg.com/raw/6c174b5529010ba188b9b120c1f4d04f.png)
- iOS : data pengujian performa push melalui SRT (perangkat pengujian — iPhone XR):
![](https://main.qcloudimg.com/raw/3126fb6c2f2aa65b6be4e9692fad0c44.png)



## Perbandingan Pencegahan Kehilangan Paket
Dibandingkan dengan QUIC, SRT mampu mengurangi kehilangan paket di lapisan aplikasi dengan tingkat kehilangan paket yang sama berkat kontrol transmisi ulang dan mekanisme pemacuannya yang lebih cepat dan lebih presisi untuk skenario streaming langsung. Ketika tingkat kehilangan paket sebesar 50%, SRT masih dapat menjamin transmisi yang stabil.

Dengan tautan dan file streaming langsung yang sama di sisi push, tingkat kehilangan paket berkurang sebesar 5% setiap lima menit ketika SRT digunakan. Gambar berikut menunjukkan bahwa frame rate push SRT lebih stabil.

## Push Langsung
### Metode akses
Push langsung mendukung penggunaan **port 9000** untuk melakukan push pada streaming melalui SRT. Anda dapat [membuat alamat push](https://intl.cloud.tencent.com/document/product/267/31084) lewat [Address Generator (Pembuat Alamat)](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)] di konsol CSS dan menyambungkan alamat dengan mengikuti aturan berikut.

Alamat push SRT Tencent Cloud:
```
srt://${rtmp-push-domain}:9000?streamid=#!::h=${rtmp-push-domain},r=${app}/${stream},txSecret=${txSecret},txTime=${txTime}
```

>! `$ {app}` adalah sebuah variabel dan harus diganti dengan nilai aktual. Ingat bahwa bagian `$`, `{`, dan `}` tidak diperlukan.

### Metode implementasi
Server SRT melakukan remuxing pada streaming TS ke streaming RTMP dan meneruskannya ke domain `${rtmp-push-domain}`.
Sampel kode streaming langsung OBS:

>! Jika Anda ingin melakukan push pada streaming melalui SRT, jangan gunakan OBS dengan versi di bawah v25.0.


## Pull Langsung
Ikuti proses pull dan pemutaran ulang yang umum. Informasi selengkapnya dapat dilihat di [Pemutaran Ulang CSS](https://intl.cloud.tencent.com/document/product/267/31559).



