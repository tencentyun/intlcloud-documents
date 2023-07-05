## Ikhtisar
Dokumen ini menjelaskan operasi umum yang terkait dengan penggunaan pasangan kunci SSH untuk masuk ke instans. Misalnya, Anda dapat membuat, mengikat, melepas ikatan, memodifikasi, atau menghapus pasangan kunci SSH.
>!Untuk mengikat kunci SSH ke atau melepas ikatan dari sebuah instans, harap matikan instans terlebih dahulu. Lihat [Mematikan Instans](https://intl.cloud.tencent.com/document/product/213/4929).
>

## Petunjuk

<span id="creatSSH"></span>
### Membuat kunci SSH
 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Klik **[SSh Key](https://console.cloud.tencent.com/cvm/sshkey)** (Kunci SSH) di bilah sisi kiri.
 3. Klik **New** (Baru) di halaman **SSH key** (Kunci SSH).
>! Setelah mengklik **OK** (OKE), kunci pribadi akan diunduh secara otomatis. Tencent Cloud tidak akan menyimpan kunci pribadi Anda. Pastikan untuk menyimpannya dengan aman.
 > 
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
  - Jika Anda memilih **Create a new key pair** (Buat pasangan kunci baru), masukkan nama kunci.
  - Jika Anda memilih **Use an existing public key** (Gunakan kunci publik yang ada), masukkan nama kunci dan informasi kunci publik asli.


<span id="bindingSSH"></span>
### Mengikat kunci ke instans
 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Klik **[SSh Key](https://console.cloud.tencent.com/cvm/sshkey)** (Kunci SSH) di bilah sisi kiri.
 3. Pada halaman pengelolaan kunci SSH, pilih kunci SSH target, lalu klik **Bind with instances** (Ikat dengan instans).
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
 4. Di jendela pop-up, pilih wilayah target dan instans, lalu klik **Bind** (Ikat).


### Melepas kunci dari instans
 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Klik **[SSh Key](https://console.cloud.tencent.com/cvm/sshkey)** (Kunci SSH) di bilah sisi kiri.
 3. Pada halaman pengelolaan kunci SSH, pilih kunci SSH target, lalu klik **Unbind from instances** (Lepaskan dari instans).
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
 4. Di jendela pop-up, pilih wilayah dan instans yang akan dilepas dari kunci, lalu klik **Unbind** (Lepaskan ikatan).


### Memodifikasi nama atau deskripsi kunci SSH
 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Klik **[SSh Key](https://console.cloud.tencent.com/cvm/sshkey)** (Kunci SSH) di bilah sisi kiri.
 3. Pada halaman pengelolaan kunci SSH, pilih kunci yang akan dimodifikasi dan klik <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/> di sebelah nama kunci, seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
 4. Di jendela pop-up, masukkan nama atau deskripsi kunci baru, dan klik **OK** (OKE).

### Menghapus kunci SSH
>! Kunci SSH tidak dapat dihapus ketika terikat dengan instans CVM atau citra kustom, tidak dapat dihapus.
>
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Klik **[SSh Key](https://console.cloud.tencent.com/cvm/sshkey)** (Kunci SSH) di bilah sisi kiri. Anda dapat menghapus satu atau beberapa kunci SSH sesuai kebutuhan.
 - **Deleting a single key** (Menghapus satu kunci)
    1. Pada halaman pengelolaan kunci SSH, pilih kunci SSH yang akan dihapus, lalu klik **Delete** (Hapus) di bawah kolom **Operation** (Operasi), seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. Di jendela pop-up, klik **OK** (OKE).
 - **Batch deleting keys** (Kunci penghapusan batch)
    1. Pada halaman pengelolaan kunci SSH, pilih kunci SSH yang akan dihapus, lalu klik **Delete** (Hapus) di atas daftar untuk menghapusnya per batch.
    2. Di jendela pop-up, klik **OK** (OKE), seperti yang ditunjukkan di bawah ini.
    Hanya kunci yang dapat dihapus dari pasangan kunci yang dipilih yang akan dihapus.
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)


### Menggunakan kunci SSH untuk login ke CVM Linux

1. [Buat kunci SSH](#createSSH).
2. [Ikat kunci SSH ke instans CVM](#bindingSSH).
3. [Masuk ke instans Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
