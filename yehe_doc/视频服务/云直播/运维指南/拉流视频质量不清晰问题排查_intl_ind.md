Video host direkam menggunakan kamera lokal, dikodekan dan di-push menggunakan SDK untuk klien, lalu didistribusikan kepada pemirsa dengan CDN Tencent Cloud. Jika Anda memberikan alamat multi-bitrate, streaming video juga akan dikodekan ulang di Tencent Cloud. Kualitas video output umumnya ditentukan oleh kualitas video input yang direkam oleh kamera, serta frame rate, interval keyframe, resolusi, dan bitrate yang dikonfigurasikan untuk pengodean. Dengan mempertimbangkan pengaruh terhadap jeda dan bitrate video, kami merekomendasikan Anda untuk mengatur interval keyframe ke 2‒3 detik.

Dokumen ini menjelaskan cara memecahkan masalah ketika video yang ditarik ke **dua** alamat pemutaran ulang berikut berubah menjadi piksel dan cara mengoptimalkan kualitas video.

## Alamat Pemutaran Ulang Streaming Video Input
Jika video yang ditarik ke **alamat pemutaran ulang streaming video input** (tanpa watermark dan tidak dicampur) berubah menjadi piksel, kami merekomendasikan Anda untuk mencari masalah di proses push:
1. Pecahkan masalah kamera. Misalnya, pastikan bahwa tidak ada debu, atau pastikan bahwa kamera telah difokuskan atau dapat mengambil gambar dengan benar.
2. Pastikan bahwa frame rate dan bitrate streaming yang di-push sudah sesuai dengan yang diinginkan.
<table>
<thead><tr><th>Resolusi</th><th>Frame Rate</th><th>Bitrate yang Diinginkan</th></tr></thead>
<tbody><tr>
<td>640 × 368</td>
<td>15 fps</td>
<td>800 Kbps</td>
</tr><tr>
<td>960 × 544</td>
<td>15 fps</td>
<td>1.000 Kbps</td>
</tr><tr>
<td>1280 × 720</td>
<td>15 fps</td>
<td>1.500 Kbps</td>
</tr><tr>
<td>1920 × 1080</td>
<td>15 fps</td>
<td>2.500 Kbps</td>
</tr>
</tbody></table>

#### Pengoptimalan
- Jika Anda menggunakan SDK pihak ketiga, silakan gunakan bitrate yang direkomendasikan di atas untuk menyesuaikan dan mengontrol kualitas video, atau hubungi pembuat SDK pihak ketiga untuk mengatasi masalah.
- Jika video di jendela pratinjau memiliki kualitas bagus, tetapi video yang ditarik berubah menjadi piksel, mungkin kualitas video di jendela pratinjau tidak konsisten dengan kualitas video yang dikodekan dan di-push. Silakan pelajari rekomendasi pengaturan di atas untuk menyesuaikan kualitas video yang dikodekan dan di-push.

 

## Alamat Pemutaran Ulang Streaming Video dengan Bitrate dan Resolusi Rendah
Jika video yang ditarik ke **alamat pemutaran ulang streaming video dengan bitrate rendah dan resolusi rendah** diubah menjadi piksel, Anda perlu memeriksa kualitas video di alamat pemutaran ulang streaming video input. Jika video input memiliki kualitas bagus, video yang di-push oleh klien juga akan memiliki kualitas bagus. Dalam kasus ini, kami merekomendasikan Anda untuk memodifikasi parameter transcoding di Tencent Cloud. Misalnya, Anda dapat meningkatkan bitrate output ke nilai yang direkomendasikan di templat transcoding.
<table>
<thead><tr><th>Resolusi</th><th>Frame Rate</th><th>Bitrate yang Diinginkan</th></tr></thead>
<tbody><tr>
<td>640 × 368</td>
<td>15 fps</td>
<td>800 Kbps</td>
</tr><tr>
<td>960 × 544</td>
<td>15 fps</td>
<td>1.000 Kbps</td>
</tr><tr>
<td>1280 × 720</td>
<td>15 fps</td>
<td>1.500 Kbps</td>
</tr><tr>
<td>1920 × 1080</td>
<td>15 fps</td>
<td>2.500 Kbps</td>
</tr>
</tbody></table>

Misalnya, jika video memiliki resolusi 640 × 368 dan frame rate templat 30 fps, kami merekomendasikan Anda untuk meningkatkan bitrate output menjadi 1,5 kali nilai aslinya sehingga perhitungan bitrate yang direkomendasikan menjadi 800 Kbps × 1,5=1.200 Kbps.


>! Jika masalah tetap terjadi setelah semua langkah-langkah di atas dilakukan, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=39&source=0&data_title=%E4%BA%91%E7%9B%B4%E6%92%AD%20%20CSS&step=1).



