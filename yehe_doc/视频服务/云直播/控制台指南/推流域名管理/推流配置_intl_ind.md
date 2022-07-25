Untuk melindungi konten streaming langsung Anda, autentikasi push diaktifkan untuk domain push secara default. Anda dapat menggunakan pembuat alamat di halaman detail domain push untuk membuat URL push, yang dapat Anda gunakan untuk melakukan push pada streaming (mengunggah video langsung) ke platform CSS.

## Catatan

- CSS menyediakan nama domain pengujian `xxxx.tlivepush.com`. Anda dapat menggunakannya untuk menguji push langsung, tetapi Anda tidak disarankan untuk menggunakannya sebagai nama domain push untuk tujuan bisnis. 
- URL push dapat digunakan sebelum waktu kedaluwarsa yang Anda tentukan. Setelah URL push kedaluwarsa, Anda perlu membuat URL baru.

## Prasyarat

Anda telah mengaktifkan layanan CSS.

## Konfigurasi Autentikasi
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), klik **push domain name** (nama domain push) target atau klik **Manage** (Kelola) untuk membuka halaman detail domain. 
2. Klik **Push Configuration** (Konfigurasi Push) dan, di area **Authentication Configuration** (Konfigurasi Autentikasi), klik **Edit**.
	![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3. Di jendela pop-up, aktifkan **Push Authentication** (Autentikasi Push).
4. Masukkan kunci utama dan kunci cadangan, lalu klik **Save** (Simpan).
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? Kunci utama harus dimasukkan, tetapi memasukkan kunci cadangan bersifat opsional. Jika memasukkan keduanya, Anda dapat beralih ke kunci lain ketika salah satu kunci telah diketahui orang lain.

## Pembuat Alamat Push

### Petunjuk
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), klik nama domain target atau klik **Manage** (Kelola) di sebelah kanan untuk membuka halaman detail.
2. Pilih **Push Configuration** (Konfigurasi Push) dan, di **Push Address Generator** (Pembuat Alamat Push), selesaikan pengaturan berikut:
   1. Pilih waktu kedaluwarsa, misalnya `2021-06-30 19:26:02`.
   2. Masukkan `StreamName` kustom, misalnya `liveteststream`.
   3. Klik **Generate Push Address** (Buat Alamat Push) untuk membuat URL push RTMP yang berisi `StreamName`.
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. Jika belum mengaktifkan autentikasi untuk domain push, Anda dapat menemukan URL RTMP dan UDP di bagian **Push URL** (URL Push). Ganti `StreamName` dengan nama streaming Anda agar Anda dapat menggunakan URL pemutaran ulang terkait untuk memutar streaming. 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)



### Format URL push

URL push RTMP tampak seperti berikut:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
URL push RTMP terdiri dari bidang-bidang berikut:
- `domain`: Nama domain push
- `AppName`: Nama aplikasi streaming langsung, yang secara default diberi nama `live`, dan nama ini dapat diubah
- `StreamName`: Nama streaming kustom yang digunakan untuk mengidentifikasi streaming langsung
- `txSecret`: String autentikasi yang dibuat setelah autentikasi push diaktifkan
- `txTime`: Stempel waktu kedaluwarsa yang ditetapkan untuk URL push di konsol

>!
>- Jika Anda telah mengaktifkan autentikasi, waktu kedaluwarsa aktual URL adalah `txTime` ditambah masa berlaku kunci.
>- Demi kenyamanan, waktu yang Anda atur di konsol adalah waktu kedaluwarsa aktual. **Jika Anda mengaktifkan autentikasi, sistem akan menghitung `txTime` saat membuat URL push.**
>- Push atau pemutaran ulang dapat tetap dilanjutkan bahkan setelah URL kedaluwarsa asalkan Anda memulai push atau pemutaran ulang sebelum waktu kedaluwarsa dan streaming tidak terputus.



## Kode Sampel URL Push

Kami menawarkan kode sampel dalam PHP dan Java untuk membuat URL push. Untuk melihat kode, ikuti langkah-langkah di bawah ini:

1. Login ke konsol CSS dan klik **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain).
2. Klik nama domain push atau klik **Manage** (Kelola) di sebelah kanan untuk masuk ke halaman detail.
3. Pilih **Push Configuration** (Konfigurasi Push) dan gulir ke bawah untuk menemukan **Push Address Sample Code** (Kode Sampel Alamat Push).
4. Klik tab untuk melihat kode sampel untuk PHP atau Java.
<dx-codeblock>
::: PHP php
```
/**
    * Dapatkan URL push
    * Jika Anda tidak memasukkan kunci autentikasi dan waktu kedaluwarsa URL, URL tanpa perlindungan hotlink akan ditampilkan.
    * @param domain: Nama domain push Anda
    *        streamName: Nama streaming unik untuk mengidentifikasi URL push
    *        key: Kunci autentikasi
    *        time: Waktu kedaluwarsa (akurat sampai dengan detik). Contoh: 2016-11-12 12:00:00
    * @return String url

function getPushUrl($domain, $streamName, $key = null, $time = null){
   if($key && $time){
      $txTime = strtoupper(base_convert(strtotime($time),10,16));
      //txSecret = MD5( KEY + streamName + txTime )
      $txSecret = md5($key.$streamName.$txTime);
      $ext_str = "?".http_build_query(array(
                "txSecret"=> $txSecret,
                "txTime"=> $txTime
      ));
    }
   return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}
echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
```
:::
::: Java java
```
package com.test;
import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
public class Test {
    public static void main(String[] args) {
        System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
    }
    private static final char[] DIGITS_LOWER =
        {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
    /*
    * KEY+ streamName + txTime
    */
    private static String getSafeUrl(String key, String streamName, long txTime) {
        String input = new StringBuilder().
                            append(key).
                            append(streamName).
                            append(Long.toHexString(txTime).toUpperCase()).toString();
        String txSecret = null;
        try {
            MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            txSecret  = byteArrayToHexString(
                        messageDigest.digest(input.getBytes("UTF-8")));
        } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
        } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
        }
        return txSecret == null ? "" :
                           new StringBuilder().
                           append("txSecret=").
                           append(txSecret).
                           append("&").
                           append("txTime=").
                           append(Long.toHexString(txTime).toUpperCase()).
                           toString();
        }
    private static String byteArrayToHexString(byte[] data) {
        char[] out = new char[data.length << 1];
        for (int i = 0, j = 0; i < data.length; i++) {
                out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                out[j++] = DIGITS_LOWER[0x0F & data[i]];
        }
        return new String(out);
    }
}
```
:::
</dx-codeblock>



## Operasi Berikutnya
Anda dapat mulai melakukan push pada streaming setelah URL push dibuat. Informasi lebih lanjut dapat dipelajari di [Live Push (Push Langsung)](https://intl.cloud.tencent.com/document/product/267/31558).

