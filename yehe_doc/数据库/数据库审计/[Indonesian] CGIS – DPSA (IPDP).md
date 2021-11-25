
## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan (“**Fitur**”) Audit Basis Data. Modul ini dimasukkan ke dalam Perjanjian Privasi dan Keamanan Data yang berada di https://intl.cloud.tencent.com/document/product/301/17347 ("**DPSA**”). Istilah-istilah yang digunakan namun tidak didefinisikan dalam Modul ini memiliki arti yang ditentukan oleh DPSA untuk istilah tersebut. Jika terjadi pertentangan antara DPSA dan Modul ini, maka Modul inilah yang akan berlaku bahkan jika sampai terjadi inkonsistensi. 

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Tujuan Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Konfigurasi**  (kebijakan audit yang Anda tetapkan, nama kebijakan audit, ID sumber daya, nama sumber daya  , wilayah, detail konfigurasi sumber daya, Layanan Elasticsearch Anda  kata sandi basis data) | Kami  hanya memproses data ini untuk menyediakan Fitur kepada Anda  sesuai dengan konfigurasi spesifik Anda.  Harap perhatikan bahwa data ini terintegrasi dengan fitur TencentDB untuk MySQL,  TencentDB untuk MongoDB, TDSQL-C kami, dan disimpan dalam  fitur Layanan Elasticsearch kami. |
| **Data Log Audit**  (termasuk waktu eksekusi pernyataan SQL, ID utas, detail baris, detail  waktu pemrosesan, kode kesalahan pernyataan SQL yang gagal, nomor aturan audit,  IP klien, nama instans, ID instans, nama pengguna (baik yang dibuat oleh Anda atau  acak), nama basis data, nama kebijakan audit, pernyataan SQL dan  jenis pernyataan SQL) | Kami  hanya memproses data ini untuk menyediakan Fitur kepada Anda, agar  dapat merekam operasi basis data.  Mohon  perhatikan bahwa data ini diterima dari fitur basis data target, dan  (selain ID instans) disimpan dalam fitur Layanan Elasticsearch kami. |


## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PEMROSESAN

Sebagaimana ditentukan dalam DPSA.

## 5\. RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi  Pribadi**                                    | **Kebijakan Penyimpanan**                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Data Konfigurasi  Data Log Audit (selain ID instans,  yang tidak disimpan) | Kami menyimpan data tersebut selama batas waktu retensi data  yang Anda pilih.  Jika Anda tidak  memilih batas waktu retensi data, kami akan secara otomatis menghapus data tersebut 30  hari setelah penyimpanan.   Jika Anda meminta agar data tersebut dihapus sebelum batas waktu retensi data Anda  berakhir, data tersebut akan dihapus dalam waktu 3  hari setelah permintaan penghapusan dibuat.  Jika Fitur ini dimatikan, data tersebut akan disimpan selama 3 hari sebelum  dihapus.   Jika Anda tidak memperbarui layanan setelah layanan berakhir, data tersebut  akan dihapus secara otomatis 3 hari setelah layanan tersebut berakhir. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum di mana seseorang dapat menyetujui pemrosesan data pribadi. Persyaratan ini mungkin berbeda-beda, bergantung dari wilayah yurisdiksi tempat pengguna akhir berada.