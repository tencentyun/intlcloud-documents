## Deskripsi Masalah
Pengguna mengalami latensi tinggi saat login ke CVM yang berlokasi di Amerika Utara.

## Analisis Masalah
Karena terbatasnya jumlah router egress internasional dalam negara tersebut, konkurensi yang tinggi dapat menyebabkan kemacetan tautan dan akses yang tidak stabil. Tencent Cloud telah melaporkan masalah ini ke ISP.
Jika Anda perlu mengelola CVM di dalam negara yang berlokasi di Amerika Utara, Anda dapat membeli CVM yang berlokasi di Hong Kong (Tiongkok) dan menggunakannya sebagai titik transfer untuk login ke CVM yang berlokasi di Amerika Utara.

## Solusi
1. Beli CVM Windows yang berlokasi di Hong Kong (Tiongkok) sebagai **jump server** (server lompat).
> 
> - Pada halaman “1. Select a model” (1. Pilih model) dari halaman “Custom Configuration” (Konfigurasi Kustom), pilih **Hong Kong, China** (Hong Kong, Tiongkok).
> [Klik di sini untuk membeli >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1®ionId=5&zoneId=0&instanceType=S2ne.SMALL2&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=BANDWIDTH_PREPAID&loginSet=SET_PASSWORD)
> - Sistem operasi Windows mendukung login ke CVM Windows dan Linux yang berlokasi di Amerika Utara, yang direkomendasikan untuk dibeli.
> - **When purchasing the Windows CVM located in Hong Kong (China), you need to buy at least 1 Mbps bandwidth. Otherwise, you cannot log in to the jump server.** (Saat membeli CVM Windows yang berlokasi di Hong Kong (Tiongkok), Anda harus membeli setidaknya 1 Mbps bandwidth. Jika tidak, Anda tidak dapat login ke server lompat.)
>
2. Setelah pembelian selesai, login ke CVM Windows yang berlokasi di Hong Kong (Tiongkok) sesuai kebutuhan Anda:
 - [Login ke instans Windows menggunakan file RDP](https://intl.cloud.tencent.com/document/product/213/5435)
 - [Login ke instans Windows melalui desktop jarak jauh](https://intl.cloud.tencent.com/document/product/213/32498)
 - [Login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496)
3. Login ke CVM Anda yang berlokasi di Amerika Utara dari CVM Windows yang berlokasi di Hong Kong (Tiongkok) sesuai kebutuhan Anda:
 - Login ke CVM Linux yang berlokasi di Amerika Utara
    - [Login ke instans Linux menggunakan metode login standar](https://intl.cloud.tencent.com/document/product/213/5436)
    - [Login ke instans Linux melalui alat login jarak jauh](https://intl.cloud.tencent.com/document/product/213/32502)
    - [Login ke instans Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
 - Login ke CVM Windows yang berlokasi di Amerika Utara 
    - [Login ke instans Windows menggunakan file RDP](https://intl.cloud.tencent.com/document/product/213/5435)
    - [Login ke instans Windows melalui desktop jarak jauh](https://intl.cloud.tencent.com/document/product/213/32498)
    - [Login ke instans Windows melalui VNC](https://intl.cloud.tencent.com/document/product/213/32496).
