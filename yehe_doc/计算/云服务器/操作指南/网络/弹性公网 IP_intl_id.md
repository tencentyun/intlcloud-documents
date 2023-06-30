## Skenario
Elastic IP, atau ElP, adalah IP statis yang dirancang untuk komputasi cloud dinamis dan IP publik tetap di wilayah tertentu. Dengan EIP, Anda dapat memetakan ulang dengan cepat alamat ke instans lain di akun Anda atau instans gateway NAT untuk menghindari kegagalan instans. Dokumen ini menjelaskan cara menggunakan EIP.

## Prasyarat

Anda telah login ke [Konsol CVM](https://console.cloud.tencent.com/cvm).

## Petunjuk

### Mengajukan EIP 

1. Di bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk masuk ke halaman pengelolaan EIP.
2. Klik **Apply** (Ajukan) di halaman pengelolaan EIP.
3. Di jendela pop-up “Apply for EIP” (Ajukan EIP), pilih wilayah, jenis alamat IP, metode penagihan, dan batas bandwidth, lalu masukkan jumlah EIP yang ingin Anda ajukan.
4. Klik **OK** (OKE) untuk menyelesaikan aplikasi EIP.
Setelah aplikasi selesai, Anda dapat melihat di daftar EIP yang Anda ajukan, yang dalam status tidak terikat.

<span id = "jump2">  </span>
### Mengikat EIP ke produk cloud

1. Di bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk masuk ke halaman pengelolaan EIP.
2. Di halaman pengelolaan EIP, pilih EIP yang ingin Anda ikat ke produk cloud dan klik **More** (Lainnya) > **Bind** (Ikat).
> Jika EIP telah terikat pada instans, harap lepaskan terlebih dahulu.
>
3. Di jendela pop-up “Bind resources” (Ikat sumber daya), pilih sumber daya yang akan diikat ke EIP dan klik **OK** (OKE).
4. Di jendela pop-up, klik **OK** (OKE) untuk menyelesaikan pengikatan EIP ke produk cloud.


### Melepaskan EIP dari produk cloud

1. Di bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk masuk ke halaman pengelolaan EIP.
2. Di halaman pengelolaan EIP, pilih EIP yang ingin Anda lepaskan dari produk cloud dan klik **More** (Lainnya) > **Unbind** (Lepaskan).
3. Di jendela pop-up “Unbind EIP” (Lepaskan EIP), konfirmasikan informasi pelepasan dan klik **OK** (OKE).
4. Di jendela pop-up, klik **OK** (OKE) untuk menyelesaikan pelepasan EIP dari produk cloud.
> Setelah pelepasan, instans produk cloud dapat menerima IP publik baru, yang mungkin berbeda dari IP sebelum pengikatan.
>

<span id = "jump">  </span>
### Merilis EIP

1. Di bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk masuk ke halaman pengelolaan EIP.
2. Di halaman pengelolaan EIP, pilih EIP yang ingin Anda rilis dari produk cloud dan klik **More** (Lainnya) > **Release** (Rilis).
3. Di jendela pop-up “Are you sure you want to release the selected EIPs?” (Anda yakin ingin merilis EIP yang dipilih?) , pilih **Release the above EIPs** (Rilis EIP di atas) dan klik **Release** (Rilis).

### Menyesuaikan Bandwidth
1. Di bilah sisi kiri, klik **[EIP](https://console.cloud.tencent.com/cvm/eip)** ([EIP]) untuk masuk ke halaman pengelolaan EIP.
2. Pilih EIP yang bandwidth-nya perlu disesuaikan dan klik **Adjust Bandwidth** (Sesuaikan Bandwidth)
3. Di jendela pop-up “Adjust Bandwidth” (Sesuaikan Bandwidth), konfigurasikan nilai bandwidth dan klik **OK** (OKE) untuk menyelesaikan penyesuaian.

### Mengonversi IP publik menjadi EIP
IP publik yang dibeli bersama dengan instans CVM tidak elastis dan tidak dapat dipasang atau dilepas. Tencent Cloud memungkinkan Anda mengonversi IP publik ke EIP dengan langkah-langkah berikut:
1. Di bilah sisi kiri, klik **[Instances](https://console.cloud.tencent.com/cvm/index)** (Instans) untuk masuk ke halaman pengelolaan instans.
2. Pilih instans yang IP publiknya perlu dikonversi ke EIP, lalu klik <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/53b608b2bb0840920703e7f50957611a.jpg)
3. Di jendela pop-up “Convert to EIP” (Konversikan ke EIP), klik **OK** (OKE).
![](https://main.qcloudimg.com/raw/3d20c058c66975f847e68e42ae944d6f.png)

## Memecahkan Masalah Pengecualian
Tidak dapat diaksesnya jaringan dapat terjadi dengan EIP karena alasan berikut: 
- EIP tidak terikat dengan produk cloud apa pun. Untuk informasi selengkapnya tentang cara mengikat EIP ke produk cloud, harap lihat [Mengikat EIP ke produk cloud](#jump2).
- Kebijakan keamanan tidak valid. Periksa apakah ada kebijakan keamanan yang valid (grup keamanan atau ACL jaringan). Jika produk cloud terikat memiliki kebijakan grup keamanan, seperti akses ke port 8080 ditolak, port 8080 EIP juga tidak dapat diakses.
