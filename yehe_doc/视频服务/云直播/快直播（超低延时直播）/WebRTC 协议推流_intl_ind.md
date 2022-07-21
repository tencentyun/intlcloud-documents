SDK TXLivePusher digunakan untuk melakukan push pada streaming untuk LEB (streaming dengan latensi ultra-rendah). SDK TXLivePusher dapat melakukan push pada audio dan video yang diambil browser dari file kamera, layar, atau media lokal ke server streaming langsung melalui WebRTC.
>! Dengan WebRTC, setiap nama domain push dapat digunakan untuk maksimum **100 streaming bersamaan** secara default. Jika Anda ingin melakukan push pada lebih banyak streaming, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category).

## Penjelasan Dasar

Berikut adalah beberapa informasi dasar yang perlu Anda ketahui sebelum melakukan integrasi SDK.

### Menyambungkan URL push

Untuk menggunakan layanan streaming langsung Tencent Cloud, Anda perlu menyambungkan URL push dalam format yang diminta oleh Tencent Cloud, yang terdiri dari empat bagian.

![](https://main.qcloudimg.com/raw/55879651fe2ca61a3699ab4ed9de41d4.jpg)

Tidak diperlukan kunci autentikasi. Anda dapat mengaktifkan autentikasi push jika memerlukan perlindungan hotlink. Untuk informasi selengkapnya, pelajari [Splicing Live Streaming URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393).

### Dukungan browser

Push untuk LEB bergantung pada WebRTC sehingga hanya dapat digunakan di OS dan browser yang mendukung WebRTC.

Fitur pengambilan audio/video tidak didukung dengan baik di browser seluler. Misalnya, browser seluler tidak mendukung perekaman layar, serta hanya iOS 14.3 dan versi yang lebih baru yang mengizinkan permintaan akses kamera. Oleh karena itu, SDK push sebagian besar digunakan di browser desktop. Versi terbaru Chrome, Firefox, dan Safari semuanya mendukung push untuk LEB.

Untuk melakukan push pada streaming melalui browser seluler, gunakan [SDK MLVB](https://intl.cloud.tencent.com/document/product/1071/38157).

## Integrasi SDK

### Langkah 1. Siapkan halaman

Tambahkan skrip inisialisasi ke halaman (desktop) tempat push akan dilakukan pada streaming.

```html
<script src="https://imgcache.qq.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```
>? Skrip perlu diimpor ke bagian `body` kode HTML. Jika skrip diimpor ke bagian `head`, akan ada laporan kesalahan.

Jika bisnis Anda berada di wilayah yang dibatasi domain, Anda dapat mengimpor tautan berikut:

```html
<script src="https://cloudcache.tencent-cloud.com/open/qcloud/live/webrtc/js/TXLivePusher-1.0.2.min.js" charset="utf-8"></script>
```

### Langkah 2. Tambahkan kontainer ke halaman HTML

Tambahkan kontainer pemutar ke bagian halaman tempat video lokal akan diputar. Untuk melakukannya, tambahkan div dan beri nama, misalnya `id_local_video`. Video lokal akan di-render dalam kontainer. Untuk menyesuaikan ukuran kontainer, atur gaya div menggunakan CSS.

```html
<div id="id_local_video" style="width:100%;height:500px;display:flex;align-items:center;justify-content:center;"></div>
```

### Langkah 3. Push streaming
1. **Buat instans SDK push:**
Buat instans objek global `TXLivePusher`. Semua operasi selanjutnya akan dilakukan melalui instans tersebut.
```javascript
var livePusher = new TXLivePusher();
```
2. **Tentukan kontainer pemutar video lokal:**
Tentukan div untuk kontainer pemutar video lokal, yaitu tempat audio dan video yang diambil oleh browser akan di-render.
```javascript
livePusher.setRenderView('id_local_video');
```
>?Elemen video yang dibuat melalui `setRenderView` diaktifkan suaranya secara default. Untuk menonaktifkan suara video, dapatkan elemen video menggunakan kode di bawah ini.
>```javascript
document.getElementById('id_local_video').getElementsByTagName('video')[0].muted = true;
```
3. **Atur kualitas audio/video:**
Kualitas audio/video harus diatur sebelum perekaman dimulai. Anda dapat menentukan parameter kualitas jika pengaturan default tidak memenuhi kebutuhan Anda.
```javascript
// Mengatur kualitas video
livePusher.setVideoQuality('720p');
// Mengatur kualitas audio
livePusher.setAudioQuality('standard');
// Mengatur frame rate
livePusher.setProperty('setVideoFPS', 25);
```
4. **Tangkap streaming:**
Anda dapat menangkap streaming dari file kamera, mikrofon, layar, dan media lokal. Jika penangkapan berhasil, kontainer pemutar akan mulai memutar audio/video yang ditangkap.
```javascript
// Mengaktifkan kamera
livePusher.startCamera();
// Mengaktifkan mikrofon
livePusher.startMicrophone();
```
5. **Push streaming:**
Teruskan URL push LEB untuk mulai melakukan push pada streaming. Untuk format URL push, lihat [Splicing Live Streaming URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393). Anda perlu mengganti awalan `rtmp://` dengan `webrtc://`.
```javascript
livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
```
>?Sebelum Anda melakukan push, pastikan bahwa streaming audio/video berhasil ditangkap, jika tidak, Anda akan gagal memanggil API push. Anda dapat menggunakan kode di bawah ini untuk melakukan push pada streaming secara otomatis setelah audio/video ditangkap, yaitu setelah panggilan balik untuk menangkap frame audio atau video pertama diterima. Jika audio dan video ditangkap, push hanya akan dimulai setelah panggilan balik untuk menangkap frame audio pertama dan panggilan balik untuk menangkap frame video pertama diterima.
```javascript
var hasVideo = false;
var hasAudio = false;
var isPush = false;
livePusher.setObserver({
    onCaptureFirstAudioFrame: function() {
      hasAudio = true;
      if (hasVideo && !isPush) {
        isPush = true;
        livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
      }
    },
    onCaptureFirstVideoFrame: function() {
      hasVideo = true;
      if (hasAudio && !isPush) {
        isPush = true;
        livePusher.startPush('webrtc://domain/AppName/StreamName?txSecret=xxx&txTime=xxx');
      }
    }
});
```
</dx-codeblock>
6. **Stop push** (Hentikan push):
```javascript
livePusher.stopPush();
```
7. **Stop capturing audio and video** (Berhenti menangkap audio dan video):
```javascript
// Menonaktifkan kamera
livePusher.stopCamera();
// Menonaktifkan mikrofon
livePusher.stopMicrophone();
```

## Fitur Tingkat Lanjut
### Kompatibilitas
SDK menyediakan metode statis untuk mengetahui suatu browser mendukung WebRTC atau tidak.

<dx-codeblock>
::: javascript javascript
TXLivePusher.checkSupport().then(function(data) {  
  // Apakah WebRTC didukung  
  if (data.isWebRTCSupported) {    
    console.log('WebRTC Support');  
  } else {    
    console.log('WebRTC Not Support');  
  }  
  // Apakah H.264 didukung  
  if (data.isH264EncodeSupported) {    
    console.log('H264 Encode Support');  
  } else {    
    console.log('H264 Encode Not Support');  
  }
});
:::
</dx-codeblock>

### Panggilan balik peristiwa
SDK mendukung pemberitahuan panggilan balik peristiwa. Anda dapat mengatur pengamat untuk menerima panggilan balik status SDK dan statistik terkait WebRTC. Untuk informasi selengkapnya, lihat [TXLivePusherObserver](https://intl.cloud.tencent.com/document/product/1071/42709).
<dx-codeblock>
::: javascript javascript
livePusher.setObserver({
  // Peringatan untuk push
  onWarning: function(code, msg) {
    console.log(code, msg);
  },
  // Status push
  onPushStatusUpdate: function(status, msg) {
    console.log(status, msg);
  },
  // Statistik push
  onStatisticsUpdate: function(data) {
    console.log('video fps is ' + data.video.framesPerSecond);
  }
});
:::
</dx-codeblock>

### Manajemen perangkat

Anda dapat menggunakan instans manajemen perangkat untuk mendapatkan daftar perangkat, beralih perangkat, dan melakukan operasi terkait perangkat lainnya.
<dx-codeblock>
::: javascript javascript
var deviceManager = livePusher.getDeviceManager();
// Mendapatkan daftar perangkat
deviceManager.getDevicesList().then(function(data) {
  data.forEach(function(device) {
      console.log(device.deviceId, device.deviceName);  
  });
});
// Beralih kamera
deviceManager.switchCamera('camera_device_id');
:::
</dx-codeblock>



