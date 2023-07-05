## Skenario

Untuk memungkinkan Anda memberi nama instans CVM yang dibuat secara batch sesuai dengan aturan selama pembuatan, fitur berakhiran menaik secara otomatis dan menentukan string pola yang disediakan.

- Saat Anda perlu membeli n instans dan membuat nama instans dalam bentuk tertentu, seperti “CVM+Sequence number” (misalnya, CVM 1, CVM 2, dan CVM 3), Anda dapat menggunakan fitur [Secara Otomatis Menaikkan Nomor Berakhiran](#AutoAscending).
- Saat Anda perlu membuat instans **n** (n) dan memberi nama instans tertentu dengan nomor menaik mulai dari **x** (x), Anda dapat menggunakan fitur [Menentukan Satu String Pola](#SpecifySingleString).
- Saat Anda perlu membuat n instans dengan beberapa awalan dalam namanya, yang masing-masing berisi nomor seri tertentu, Anda dapat menggunakan fitur [Menentukan Beberapa String Pola](#SpecifyMultipleStrings).


## Langkah-Langkah

<span id="AutoAscending"></span>
### Secara Otomatis Menaikkan Angka Berakhiran

Fitur ini memungkinkan Anda memberi nama instans yang dibeli secara batch dengan awalan yang sama dan nomor berakhiran yang naik secara otomatis.
>Instans yang dibuat diberi akhiran dengan angka mulai dari 1 secara default. Nomor berakhiran awal adalah tetap.
>
Contoh berikut mengasumsikan bahwa Anda telah membeli tiga instans dan ingin memberi nama instans tersebut dalam bentuk “CVM+Nomor urut” (misalnya, CVM 1, CVM 2, dan CVM 3).

#### Operasi pada Halaman Pembelian

1. Beli tiga instans dengan merujuk ke [Buat Instans](http://intl.cloud.tencent.com/document/product/213/4855). Pada halaman tab **2. Security Group and CVM** (2. Grup Keamanan dan CVM), masukkan nama instans berupa **Prefix+Sequence number** (Awalan+Nomor urut). Dalam hal ini, masukkan `CVM` sebagai nama instans.
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. Ikuti petunjuk di halaman dan selesaikan pembayaran.
3. Kembali ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk melihat instans yang baru dibeli. Anda dapat melihat bahwa instans yang dibeli secara batch ini diberi nama dengan awalan yang sama dan nomor akhiran menaik.
![](https://main.qcloudimg.com/raw/27de624cd251910d47bea8e7732b284b.png)

#### Operasi API

Di [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API, atur bidang InstanceName ke `CVM`.

### Menentukan String Pola

Fitur ini memungkinkan Anda memberi nama instans yang dibeli secara batch dalam bentuk kompleks dengan nomor seri tertentu. Anda dapat menggunakan satu atau beberapa string pola dalam nama instans sesuai kebutuhan.

Nama instans dengan string pola yang ditentukan dalam bentuk **{R:x}** ({R:x}), di mana **x** (x) menunjukkan nomor awal dalam nama instans yang dihasilkan.

<span id="SpecifySingleString"></span>
#### Menentukan Satu String Pola

Contoh berikut mengasumsikan bahwa Anda ingin membuat tiga instans dan menamainya dengan nomor menaik mulai dari 3.

##### Operasi pada Halaman Pembelian

1. Beli tiga instans dengan merujuk ke [Buat Instans](http://intl.cloud.tencent.com/document/product/213/4855). Pada halaman tab **2. Set the CVM** (2. Atur CVM), masukkan nama instans berupa **Prefix+Specified pattern string {R:x}** (Prefix+Specified pattern string {R:x}). Dalam hal ini, masukkan `CVM{R:3}` sebagai nama instans.
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. Ikuti petunjuk di halaman dan selesaikan pembayaran.
3. Kembali ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk melihat instans yang baru dibeli. Anda dapat melihat bahwa instans yang dibeli secara batch ini diberi nama dengan awalan yang sama dan nomor berakhiran menaik mulai dari 3.
![](https://main.qcloudimg.com/raw/78dc40cf4baa707573ad95a77bed4e1d.png)

##### Operasi API

Di [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API, atur kolom InstanceName ke `CVM{R:3}`.

<span id="SpecifyMultipleStrings"></span>
#### Menentukan Beberapa String Pola

Contoh berikut mengasumsikan bahwa Anda ingin membuat tiga instans dan memberinya nama dengan awalan **cvm** (cvm), **Big** (Big), dan **test** (test), dengan **cvm** (cvm) dan **Big** (Big) masing-masing diikuti dengan nomor menaik mulai dari 13 dan 2. Misalnya, namanya masing-masing adalah cvm13-Big2-test, cvm14-Big3-test, dan cvm15-Big4-test.

##### Operasi pada Halaman Pembelian

1. Beli tiga instans dengan merujuk ke [Buat Instans](http://intl.cloud.tencent.com/document/product/213/4855). Pada halaman tab **2. Set the CVM** (2. Atur CVM), masukkan nama instans berupa **Prefix+Specified pattern string {R:x}-Prefix+Specified pattern string {R:x}-Prefix** (Prefix+Specified pattern string {R:x}-Prefix+Specified pattern string {R:x}-Prefix). Dalam hal ini, masukkan `cvm{R:13}-Big{R:2}-test` sebagai nama instans.
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. Ikuti petunjuk di halaman dan selesaikan pembayaran.
3. Kembali ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) untuk melihat instans yang baru dibeli. Anda dapat melihat bahwa instans yang dibeli secara batch ini diberi nama dengan awalan diikuti dengan nomor menaik mulai dari nomor yang ditentukan.
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

##### Operasi API

Di [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) API, atur bidang InstanceName ke `cvm{R:13}-Big{R:2}-test`.

