## Batas Akun untuk Membeli Instans CVM

- Anda harus mendaftar untuk akun Tencent Cloud. Untuk informasi selengkapnya, lihat [Mendaftar untuk Akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985).
- Jika Anda membuat CVM bayar sesuai pemakaian, sistem akan menangguhkan biaya penggunaan CVM selama satu jam. Pastikan bahwa akun Anda memiliki saldo yang cukup untuk melakukan pemesanan.

## Batas Penggunaan Instans CVM

- Perangkat lunak virtual tidak dapat diinstal atau divirtualisasi ulang (seperti menginstal VMware atau Hyper-V).
- Anda tidak dapat menggunakan kartu suara atau memasang perangkat keras eksternal (seperti flash drive USB, disk eksternal, dan tombol U).
- CVM gateway publik hanya tersedia di sistem operasi Linux.

## Batas Pembelian Instans CVM

- Untuk setiap pengguna, **quota** (kuota) instans CVM bayar sesuai pemakaian di setiap zona ketersediaan adalah 30.
Untuk informasi selengkapnya, lihat [Batas Pembelian](https://intl.cloud.tencent.com/document/product/213/2664).


## Batas Citra

- Citra publik: tidak ada batasan penggunaan.
- Citra kustom: setiap wilayah mendukung maksimal 10 citra kustom.
- Citra yang dibagikan: setiap citra kustom dapat dibagikan kepada maksimal 50 pengguna Tencent Cloud. Citra kustom hanya dapat dibagikan dengan akun di wilayah yang sama dengan akun sumber.
- Untuk informasi selengkapnya, lihat [Jenis Citra](https://intl.cloud.tencent.com/document/product/213/4941).

## Batas EIP

#### Batas Kuota

| Sumber Daya | Batas |
|---------|:---------:|
| Jumlah EIP untuk setiap akun Tencent Cloud di setiap wilayah | 20 |
| Jumlah aplikasi pembelian harian untuk setiap akun Tencent Cloud di setiap wilayah | Kuota * 2 |
| Frekuensi alamat IP publik dapat dipindahkan ke setiap akun secara gratis per hari saat EIP tidak terikat | 10 |

#### Batasan pada IP publik yang terikat ke CVM

Mulai tanggal 18 September 2019, jumlah maksimum IP publik yang dapat diikat ke satu CVM telah diubah berdasarkan konfigurasi CPU. Kuota ditampilkan seperti di bawah ini:
>? Batasan ini tidak berlaku untuk instans CVM yang dibeli sebelum pukul 00.00, 18 September 2019. Untuk instans ini, jumlah IP publik yang dapat diikat ke setiap instans sama dengan [jumlah IP pribadi](https://intl.cloud.tencent.com/document/product/576/18527) yang didukung oleh server Anda.
>

| Jumlah CPU pada CVM | Jumlah maksimum IP publik yang dapat diikat (termasuk IP publik dan elastis) |
|---------|---------|
| 1-5 | 2 |
| 6-11 | 3 |
| 12-17 | 4 |
| 18-23 | 5 |
| 24-29 | 6 |
| 30-35 | 7 |
| 36-41 | 8 |
| 42-47 | 9 |
| ≥ 48 | 10 |

## Batas ENI

Berdasarkan konfigurasi CPU dan memori, jumlah ENI yang terikat ke CVM berbeda dengan jumlah IP pribadi yang terikat ke ENI. Kuota tersebut seperti yang ditunjukkan di bawah ini:
>! Jumlah alamat IP yang terikat pada satu ENI menunjukkan jumlah maksimum yang diizinkan. Kuota EIP tidak diberikan berdasarkan batas atas ini tetapi berdasarkan EIP [batas penggunaan](https://intl.cloud.tencent.com/document/product/213/5733).

<dx-tabs>
::: Number\sof\sENIs\sbound\sto\sa\sCVM\sinstance
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Model</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Jenis Instans</th>
    <th width="86%" colspan="10" style = "text-align:center;">Jumlah ENI</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 core</th>
    <th style = "text-align:center;">CPU: 2 core</th>
    <th style = "text-align:center;">CPU: 4 core</th>
    <th style = "text-align:center;">CPU: 6 core</th>
    <th style = "text-align:center;">CPU: 8 core</th>
    <th style = "text-align:center;">CPU: 10 core</th>
    <th style = "text-align:center;">CPU: 12 core</th>
    <th style = "text-align:center;">CPU: 14 core</th>
    <th style = "text-align:center;">CPU: 16 core</th>
    <th style = "text-align:center;">CPU: &gt;16 core</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Standar</th>
    <th style="text-align:center">S5 Standar</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S5se yang Dioptimalkan Penyimpanan Standar</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">SA2 Standar</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S4 Standar</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">SN3ne yang Dioptimalkan Jaringan Standar</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S3 Standar</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">SA1 Standar</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S2 Standar</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S1 Standar</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">IO tinggi</th>
    <th style = "text-align:center;">IO IT5 tinggi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">IO IT3 tinggi</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">MEM Dioptimalkan</th>
    <th  style = "text-align:center;">M5 yang Dioptimalkan Memori</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">M4 yang Dioptimalkan Memori</th>
    <td >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M3 yang Dioptimalkan Memori</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M2 yang Dioptimalkan Memori</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M1 yang Dioptimalkan Memori</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Komputasi</th>
    <th  style = "text-align:center;">C4 yang Dioptimalkan Komputasi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">CN3 yang dioptimalkan untuk Jaringan Komputasi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Komputasi C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Komputasi C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">Berbasis GPU</th>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">Komputasi GPU GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Komputasi GPU GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">Komputasi GPU GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big Data</th>
    <th  style = "text-align:center;">Big Data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td>8</td>
    <td>8</td>
   </tr>
  </table>
:::
::: Number\sof\sprivate\sIPs\sbound\sto\sa\ssingle\sENI\son\sCVM\sinstances
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Model</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Jenis Instans</th>
    <th width="86%" colspan="10" style = "text-align:center;">Jumlah IP pribadi yang terikat pada satu ENI</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 core</th>
    <th style = "text-align:center;">CPU: 2 core</th>
    <th style = "text-align:center;">CPU: 4 core</th>
    <th style = "text-align:center;">CPU: 6 core</th>
    <th style = "text-align:center;">CPU: 8 core</th>
    <th style = "text-align:center;">CPU: 10 core</th>
    <th style = "text-align:center;">CPU: 12 core</th>
    <th style = "text-align:center;">CPU: 14 core</th>
    <th style = "text-align:center;">CPU: 16 core</th>
    <th style = "text-align:center;">CPU: &gt;16 core</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Standar</th>
    <th style="text-align:center">S5 Standar</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S5se yang Dioptimalkan Penyimpanan Standar</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">SA2 Standar</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S4 Standar</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">SN3ne yang Dioptimalkan Jaringan Standar</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S3 Standar</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">SA1 Standar</th>
    <td >Memori 1 GB: Memori 2<br/>&gt;1 GB: 6</td>
    <td >10</td>
    <td >Memori 8 GB: Memori 10<br/>16 GB: 20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S2 Standar</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">S1 Standar</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">IO tinggi</th>
    <th style = "text-align:center;">IO IT5 tinggi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">IO IT3 tinggi</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">MEM Dioptimalkan</th>
    <th  style = "text-align:center;">M5 yang Dioptimalkan Memori</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">M4 yang Dioptimalkan Memori</th>
    <td >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M3 yang Dioptimalkan Memori</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M2 yang Dioptimalkan Memori</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">M1 yang Dioptimalkan Memori</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Komputasi</th>
    <th  style = "text-align:center;">C4 yang Dioptimalkan Komputasi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">CN3 yang dioptimalkan untuk Jaringan Komputasi</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Komputasi C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Komputasi C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">Berbasis GPU</th>
    <th  style = "text-align:center;">Komputasi GPU GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">Komputasi GPU GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Komputasi GPU GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">Komputasi GPU GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Komputasi GPU GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Berbasis FPGA</th>
    <th style = "text-align:center;">FPGA Accelerated FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big Data</th>
    <th  style = "text-align:center;">Big Data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big Data D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">Mesin Fisik Cloud 2.0</th>
    <td colspan="10" style = "text-align:center;">Tidak didukung</td>
   </tr>
  </table>
:::
</dx-tabs>


## Batas Bandwidth

- Bandwidth keluar maksimum (bandwidth hilir)
 - Aturan berikut berlaku untuk instans yang dibuat sebelum pukul 00:00, 24 Februari 2020: 
<table>
<tr><th rowspan="2">Metode Penagihan Jaringan</th><th colspan="2">Instans</th><th rowspan="2">Rentang Bandwidth Maksimum (Mbps)</th></tr>
<tr><th>Metode Penagihan Instans</th><th>Konfigurasi Instans</th></tr>
<tr><td>Tagihan per lalu lintas</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Tagihan per bandwidth</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Paket Bandwidth</td><td colspan="2">Semua</td><td>0-2000</td></tr>
</table>

 - Aturan berikut berlaku untuk instans yang dibuat setelah pukul 00.00, 24 Februari 2020:
<table>
<tr><th rowspan="2">Metode Penagihan Jaringan</th><th colspan="2">Instans</th><th rowspan="2">Rentang Bandwidth Maksimum (Mbps)</th></tr>
<tr><th style="width: 18.5607%;">Metode Penagihan Instans</th><th style="width: 24.5814%;">Konfigurasi Instans</th></tr>
<tr><td>Tagihan per lalu lintas</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Tagihan per bandwidth</td><td>Instans berbasis pembayaran sesuai pemakaian</td><td>Semua</td><td>0-100</td></tr>
<tr><td>Paket Bandwidth</td><td colspan="2">Semua</td><td>0-2000</td></tr>
</table>

- Bandwidth masuk maksimum (bandwidth hulu)
	- Jika bandwidth tetap yang Anda beli lebih besar dari 10 Mbps, Tencent Cloud akan menetapkan bandwidth masuk jaringan publik sama dengan bandwidth yang dibeli.
	- Jika bandwidth tetap yang Anda beli kurang dari 10 Mbps, Tencent Cloud akan menetapkan bandwidth masuk jaringan publik 10-Mbps.

## Batas Disk

<table>
	<tr><th>Batasan</th><th>Deskripsi</th></tr>
	<tr><td>Kemampuan disk cloud elastis</td><td>Mulai dari Mei 2018, semua disk data yang dibeli dengan CVM adalah disk cloud elastis, yang dapat dilepas dari dan dipasang kembali ke CVM. Fitur ini didukung di semua <a href="https://intl.cloud.tencent.com/document/product/213/35071">zona ketersediaan</a>.</td></tr>
	<tr><td>Performa disk cloud elastis</td><td>Spesifikasi I/O berlaku untuk performa input dan output secara bersamaan.<br/>Misalnya, jika SSD 1 TB memiliki IOPS acak maksimum 26.000, artinya performa baca dan tulisnya dapat mencapai nilai ini. Karena batasan performa, jika ukuran blok dalam contoh ini adalah 4 KB atau 8 KB, IOPS maksimum dapat dicapai. Jika ukuran blok 16 KB, IOPS maksimum tidak dapat dicapai (throughput telah mencapai batas 260 MB/dtk.)</td></tr>
	<tr><td>Jumlah disk cloud elastis yang dipasang ke CVM</td><td>Maksimum 20</td></tr>
	<tr><td>Jumlah snapshot dalam satu wilayah</td><td>64 + Jumlah disk cloud di wilayah tersebut x 64</td></tr>
	<tr><td>Disk cloud yang dipasang ke CVM</td><td>CVM dan disk cloud harus berada di zona ketersediaan yang sama.</td></tr>
	<tr><td>Pengembalian snapshot</td><td>Data snapshot hanya dapat dikembalikan ke disk cloud tempat snapshot dibuat.</td></tr>
	<tr><td>Jenis disk cloud dapat dibuat menggunakan snapshot</td><td>Hanya snapshot dari disk data yang dapat digunakan untuk membuat disk cloud elastis baru.</td></tr>
	<tr><td>Ukuran disk cloud yang dibuat menggunakan snapshot</td><td>Ukuran disk cloud yang dibuat menggunakan snapshot harus lebih besar atau sama dengan disk cloud sumber.</td></tr>
</table>


## Batas Grup Keamanan

- Grup keamanan bersifat khusus wilayah. CVM hanya dapat diikat ke grup keamanan di wilayah yang sama.
- Grup keamanan berlaku untuk instans CVM di [lingkungan jaringan](https://intl.cloud.tencent.com/document/product/213/5227) mana pun.
- Setiap pengguna dapat mengonfigurasi maksimum 50 grup keamanan untuk setiap proyek di suatu wilayah.
- Maksimal 100 aturan masuk atau keluar dapat dikonfigurasi untuk grup keamanan.
- Satu CVM dapat dikaitkan dengan beberapa grup keamanan, dan grup keamanan dapat dikaitkan dengan beberapa instans CVM.
- Grup keamanan yang terkait dengan CVM di **classic network** (jaringan klasik) tidak dapat memfilter paket dari atau ke database TencentDB (MySQL, MariaDB, SQL Server, atau PostgreSQL) dan NoSQL (Redis atau Memcached). Sebagai gantinya, Anda dapat menggunakan iptables untuk memfilter lalu lintas untuk instans tersebut.
- Kuota tersebut ditunjukkan seperti di bawah ini:
<table>
<tr><th>Item</th><th>Batas</th></tr>
<tr><td>Jumlah grup keamanan</td><td>50 per wilayah</td></tr>
<tr><td>Jumlah aturan dalam grup keamanan</td><td>100 untuk aturan masuk dan 100 untuk aturan keluar</td></tr>
<tr><td>Jumlah instans CVM yang terkait dengan grup keamanan</td><td>2.000</td></tr>
<tr><td>Jumlah grup keamanan yang terkait dengan instans CVM</td><td>5</td></tr>
<tr><td>Jumlah grup keamanan yang dapat dirujuk oleh grup keamanan</td><td>10</td></tr>
</table>

## Batas VPC

| Sumber Daya | Batas |
|---------|---------|
| Jumlah VPC per wilayah untuk setiap akun | 20 |
| Jumlah subnet per VPC | 100 |
| Jumlah CVM berbasis jaringan klasik dapat dikaitkan dengan setiap instans VPC | 100 |
| Jumlah tabel rute per VPC | 10 |
| Jumlah tabel rute yang terkait dengan setiap subnet | 1 |
| Jumlah kebijakan perutean per tabel rute | 50 |
| Jumlah HAVIP default per VPC | 10 |

