 ## Kesalahan
Kesalahan `InvalidParameter.OtherError` terjadi ketika pencampuran streaming dimulai.

## Kemungkinan Penyebab
- Lebar atau tinggi citra streaming input melebihi 2.000 px.
- Saluran bersamaan suatu streaming melebihi 20.
- Akun “Channel Mode” (Mode Saluran) menggunakan API `CreateCommonMixStream`.

## Solusi
Bagian berikut menjelaskan berbagai metode pemecahan masalah umum untuk kode subkesalahan.

[](id:error1)
#### Kesalahan 1: `"Message":"InnerErrCode : [ -10021 ],IrnerErrMsg: [ Params Error ]"`
Backend pencampuran streaming hanya mendukung streaming dengan lebar dan tinggi citra kurang dari 2.000 px. Kesalahan `-10021` akan terjadi jika lebar atau tinggi citra streaming input melebihi 2.000 px.

1. Gunakan FFplay untuk memutar ulang streaming langsung dan melihat resolusinya. Resolusi berikut adalah `1920 x 1080`, yang tidak akan menimbulkan kesalahan.
   Perintah: `ffplay -i "playback URL"`.
   ![](https://main.qcloudimg.com/raw/cf074af38048408dc5b35c6db451770c.png)  
2. [Gunakan VLC](https://intl.cloud.tencent.com/document/product/267/32483) untuk memutar ulang streaming langsung:
   - Aktifkan VLC, klik **Media** > **Open Network Stream** > **Network** (Media > Buka Streaming Jaringan > Jaringan), lalu masukkan URL. Setelah konfirmasi, Anda dapat menarik streaming langsung.
   - Anda dapat melihat resolusi streaming langsung di **Tools** > **Media Information** > **Codec** (Alat > Informasi Media > Codec).
     

[](id:error2)
#### Kesalahan 2: `"Message":"InnerErrCode:[ -41 ],InnerErrMsg: [ ]"`

Backend pencampuran streaming hanya mendukung 20 saluran bersamaan untuk satu streaming. Umumnya, Anda perlu menggunakan streaming yang sama sebagai input ke beberapa sesi pencampuran streaming hanya jika beberapa host menyiarkan penjualan langsung.

Misalnya, sebuah host membuat sesi pencampuran streaming, kemudian keluar dari sesi tersebut tanpa membatalkannya. Nama streaming yang sama akan digunakan oleh beberapa sesi pencampuran streaming jika host tersebut masuk ke sesi lain sehingga akan memicu kesalahan ini.

Ketika sesi pencampuran streaming mengalami interupsi, layar pencampuran streaming akan berhenti di frame terakhir jika streaming latar belakang tidak mengalami interupsi. Anda dapat memanggil API `CancelCommonMixStream` agar frame terakhir tidak ditampilkan terus di layar. Jika streaming latar belakang diinterupsi, seluruh layar akan macet.
- Jika semua streaming input berhasil didorong dengan nama streaming yang sama dalam waktu 15 menit, sesi pencampuran streaming akan dipulihkan.
- Jika semua streaming input diinterupsi, sesi pencampuran streaming akan dibatalkan secara otomatis setelah 15 menit.


[](id:error3)
#### Kesalahan 3: `"Message":"InnerErrCode:[ -4 ],InnerErrMsg: [ get liveconfig failed! ]"` (`"Pesan":"InnerErrCode:[ -4 ],InnerErrMsg: [ gagal mendapatkan liveconfig! ]"`)

Kesalahan ini akan terjadi jika Anda menggunakan akun dengan konsol lama (mode saluran) untuk memanggil API v3.0 [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997).

Anda dapat [meningkatkan konsol CSS](https://intl.cloud.tencent.com/zh/document/product/267) ke versi terbaru (mode kode streaming langsung) untuk mengatasi kesalahan ini.

[](id:error4)
#### Kesalahan 4: `"Message":"input stream num is not match the template id!"` (`"Pesan":"nomor streaming input tidak sesuai dengan templat id!"`)

Kesalahan ini akan terjadi jika Anda menggunakan templat pencampuran streaming default yang disediakan oleh Tencent Cloud, tetapi streaming output tidak memenuhi persyaratan templat tersebut.
Misalnya, jika menggunakan templat 10, Anda harus memiliki dua streaming input; jika menggunakan templat 390, Anda harus memiliki tiga streaming input, yang dapat berupa dua streaming audio/video dan satu streaming latar belakang.

Detail tentang parameter dan petunjuk terkait dapat dilihat di [CreateCommonMixStream API > MixStreamTemplateId](https://intl.cloud.tencent.com/document/product/267/35997).




[](id:error5)
#### Kesalahan 5: `"Message":"InnerErrCode:[ -300 ],InnerErrMsg: [ outputstreamid not avaliable, outputstreamid alread use as background in other sessionid ]"` (`"Pesan":"InnerErrCode:[ -300 ],InnerErrMsg: [ outputstreamid tidak tersedia, outputstreamid sudah digunakan sebagai latar belakang di sessionid lain ]"`)

Kesalahan ini terjadi jika nama streaming A digunakan sebagai nama streaming latar belakang dan streaming output sesi A, dan sesi B yang dimulai beberapa saat kemudian juga menggunakan nama streaming output yang sama.

Untuk mengatasi kesalahan ini, Anda dapat mengatur **`OutputStreamName` yang berbeda** untuk sesi B.



[](id:error6)
#### Kesalahan 6: `"Message": "InnerErrCode:[ -2 ],InnerErrMsg: [ small picture out of the background ]"` (`"Pesan":"InnerErrCode:[ -2 ],InnerErrMsg: [ gambar kecil di luar latar belakang ]"`)
Kesalahan ini akan terjadi jika bagian citra berukuran kecil berada di luar citra latar belakang. Misalnya, citra latar belakang dan citra berukuran kecil masing-masing memiliki resolusi `1920*1080` dan `1280*720`. Jika `LocationX` (offset sumbu X citra input di citra output) + 1280 > 1920` atau `LocationY` (offset sumbu Y citra input di citra output) + 720 > 1080`, kesalahan ini akan terjadi.
- Cara mengatur `LocationX` dapat dipelajari di [CommonMixLayoutParams > LocationX](https://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams).
- Cara mengatur `LocationY` dapat dipelajari di [CommonMixLayoutParams > LocationX](https://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams).
- Contoh lain terkait penggunaan templat pencampuran streaming dapat ditemukan di [Live Stream Mixing (Pencampuran Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/37665).


[](id:error7)
#### Kesalahan 7: `"Message": "InnerErrCode:[ -111 ],InnerErrMsg: [ output_stream_type is [0],but output_stream_id xxxxx is not in input stream list ]"` (`"Pesan":"InnerErrCode:[ -111 ],InnerErrMsg: [ output_stream_type bukan [0], tetapi output_stream_id xxxxx tidak ada dalam daftar streaming input ]"`)
Kesalahan ini akan terjadi jika [OutputStreamType](https://cloud.tencent.com/document/api/267/20474#CommonMixOutputParams) diatur ke nilai default `0` (menggunakan salah satu nama streaming input sebagai nama streaming output), tetapi nama streaming output aktualnya tidak tercantum dalam daftar streaming input.
Catatan:
- Jika `OutputStreamType` diatur ke `0` atau dikosongkan, Anda perlu mengatur `OutputStreamName` ke salah satu nama streaming input.
- Jika Anda ingin menggunakan `OutputStreamName` baru, atur `OutputStreamType` ke `1`.
- Jika `OutputStreamType` diatur ke `1`, Anda tidak dapat mengatur `OutputStreamName` ke nama streaming mana pun dalam `InputStreamList` dan backend streaming langsung.

