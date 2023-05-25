

## 1\. Latar Belakang

Modul ini berlaku jika Anda menggunakan Cloud Log Service (“**Fitur**”). Modul ini dimasukkan ke dalam Perjanjian Pemrosesan dan Keamanan Data yang terletak di [ (“**DPSA**”)](https://intl.cloud.tencent.com/document/product/301/17347). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditetapkan dalam DPSA. Jika terdapat perbedaan antara DPSA dengan Modul ini, Modul inilah yang akan berlaku apabila terjadi ketidaksesuaian.

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Bisnis,** yaitu log cloud Anda yang Anda unggah ke Fitur melalui alat pengumpul log khusus "loglistener". | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap perhatikan bahwa data ini disimpan, dicadangkan, dan dikelola di Cloud Object Storage, Ckafka /ES, dan CK yang terletak di wilayah layanan Fitur yang Anda pilih. |
| **Data konfigurasi,** termasuk dalam kaitannya dengan:<li>pengumpulan log (yaitu alamat IP komputer virtual cloud, direktori log, waktu log, dan kebijakan filter;</li><li>dasbor dan indeks: bidang yang ditentukan pengguna yang digunakan untuk membangun Indeks dan Dasbor; dan</li><li> peringatan (yaitu kebijakan dan periode peringatan). </li> | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap perhatikan bahwa data ini disimpan dan dicadangkan di COS/Ckafka/ES, yang terletak di wilayah layanan Fitur yang Anda pilih. |



## 3\. wilayah layanan

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-Prosesor

Sebagaimana ditentukan dalam DPSA.

## 5\. penyimpanan data

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi** | **Kebijakan Penyimpanan**                                         |
| ------------------------ | ------------------------------------------------------------ |
| Data Bisnis            | Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Jika tidak, kami akan menghapus data tersebut dalam waktu 7 hari setelah Anda berhenti menggunakan Fitur ini atau menghapus akun Anda. |
| Data Konfigurasi       | Kami menyimpan data tersebut setelah periode penyimpanan data yang ditentukan pengguna (1 hingga 366 hari). Setelah periode yang ditentukan berakhir, data akan dihapus secara otomatis. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.