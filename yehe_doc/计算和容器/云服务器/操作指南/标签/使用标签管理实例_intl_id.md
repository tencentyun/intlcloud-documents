## Ikhtisar

**Tag** (Tag) adalah pasangan nilai kunci yang disediakan oleh Tencent Cloud untuk memudahkan identifikasi sumber daya. Anda dapat menggunakan tag untuk mengategorikan dan mengelola sumber daya CVM Anda.
Tencent Cloud tidak akan menggunakan tag Anda, tag tersebut hanya digunakan oleh Anda untuk mengelola sumber daya CVM Anda.

## Batasan Penggunaan
Perhatikan batasan berikut saat menggunakan tag:
- Batas kuantitas: setiap sumber daya Tencent Cloud memungkinkan hingga 50 tag.
- Batas kunci tag:
 - Kunci tag tidak dapat dimulai dengan `qcloud`, `tencent`, atau `project`.
 - Kunci tag dapat berisi hingga 255 karakter, termasuk angka, huruf, dan `+=.@-`.
- Batas nilai tag: nilai tag dapat berisi hingga 127 karakter, termasuk angka, huruf, dan `+=.@-`. Nilai ini bisa dibiarkan kosong jika perlu.

## Petunjuk dan Kasus

### Kasus penggunaan

Sebuah perusahaan telah membeli enam instans CVM, dengan grup bisnis, cakupan, dan pemiliknya adalah sebagai berikut:

| ID Instans | Grup Bisnis | Cakupan Bisnis | Pemilik |
|---------|---------|---------|--------|
| ins-abcdef1 | E-commerce | Kampanye pemasaran | John Smith |
| ins-abcdef2 | E-commerce | Kampanye pemasaran | Chris |
| ins-abcdef3 | Game | Game A | Jane Smith |
| ins-abcdef4 | Game | Game B | Chris |
| ins-abcdef5 | Hiburan | Pasca produksi | Chris |
| ins-abcdef6 | Hiburan | Pasca produksi | John Smith  |

Mengambil ins-abcdef1 sebagai contoh, kami dapat menambahkan 3 set tag berikut ke instans:
<table id="table02">
	<tr><th>Tag Key</th><th>Tag Value</th></tr>
	<tr><td>dept</td><td>ecommerce</td></tr>
	<tr><td>business</td><td>mkt</td></tr>
	<tr><td>owner</td><td>John Smith</td></tr>
</table>

Demikian pula, Anda dapat menambahkan pasangan nilai kunci tag ke instans lain berdasarkan grup bisnis, cakupan, dan pemilik.

### Mengatur tag di konsol CVM
Ambil kasus sebelumnya sebagai contoh. Setelah mendesain pasangan nilai kunci tag, Anda dapat masuk ke konsol CVM untuk menentukan tag.

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Pada halaman **Instance** (Instans), pilih instans target dan klik **More** (Lainnya) > **Instance Settings** (Pengaturan Instans) > **Edit Tags** (Edit Tag) di kolom **Operation** (Operasi).
2. Atur tag di bagian "1 sumber daya yang dipilih" dari jendela pop-up.
Misalnya, Anda dapat menambahkan [tiga pasangan nilai kunci tag](#table02) ke instans ins-abcdef1.
3. Klik **OK** (OKE). Sistem menampilkan pesan yang menunjukkan bahwa modifikasi berhasil.


### Memfilter instans berdasarkan tag

Untuk memfilter instans menurut tag, ikuti langkah-langkah di bawah ini:

1. Klik kotak pencarian dan pilih **Tag** (Tag) dari daftar drop-down.
2. Masukkan tag, dan klik <img src="https://main.qcloudimg.com/raw/3cca38f08eaa87087cdd1b81eaf08a0a.png" style="margin: 0;"> untuk menelusuri.
Anda dapat memfilter instans menggunakan tag. Misalnya, Anda dapat mencari instans yang terikat dengan tag `key1` atau `key2` dengan memasukkan `Tag: key1|key2` di kotak pencarian.
