
## Ikhtisar Penagihan

Tencent Cloud menyediakan jaringan BGP multi-jalur berkualitas tinggi untuk memastikan pengalaman jaringan yang optimal.
Tencent Cloud saat ini menyediakan dua paket penagihan: tagihan per lalu lintas dan tagihan per bandwidth.
>! 
> - Biaya jaringan publik ditagih berdasarkan bandwidth/lalu lintas keluar. Bandwidth keluar mengacu pada bandwidth dari CVM ke jaringan publik. Misalnya, pengguna menggunakan klien untuk mengunduh sumber daya instans CVM.
> - Untuk menghindari biaya tak terduga akibat lonjakan lalu lintas, Anda dapat menetapkan batas bandwidth. Setiap lalu lintas di atas batas akan dibatalkan dan tidak akan dikenakan biaya apa pun.
> 


## Paket Penagihan


Tabel berikut membandingkan metode pembayaran, siklus penagihan, dan kasus penggunaan dari dua paket penagihan yang berbeda:

- Menghitung penggunaan berdasarkan lalu lintas (GB):

 <table class="comparison-table">
                     <tbody><tr>
                        <th>Paket Penagihan</th>
                        <th>Metode Pembayaran</th>
                                    <th>Siklus Penagihan</th>
<th>Kasus Penggunaan</th>
                     </tr>
                     <tr>
                        <td>Per lalu lintas</td>
                        <td>Pascabayar</td> 
                                    <td>Per Jam</td>
                                    <td>Cocok untuk skenario di mana lalu lintas bisnis puncak sangat fluktuatif pada waktu yang bervariasi.</td></tr></tbody></table>

- Menghitung penggunaan berdasarkan bandwidth (Mbps):


 <table class="comparison-table">
                     <tbody><tr>
                        <th>Paket Penagihan</th>
                        <th>Metode Pembayaran</th>
                                    <th>Siklus Penagihan</th>
<th>Kasus Penggunaan</th>
                     </tr>
                        <td>Paket bandwidth</td>
                        <td>Pascabayar</td> 
                                    <td>Bulanan</td>
                                    <td>Cocok untuk bisnis skala besar di mana lalu lintas dapat diatur antar sejumlah instans yang berbeda menggunakan jaringan publik.</td>
</tr></tbody></table>


- Bandwidth puncak dari paket penagihan tagihan per lalu lintas dan paket tagihan per bandwidth berbeda. Lihat tabel di bawah untuk detailnya.
<table>
       <tbody><tr>
            <th>Tagihan per lalu lintas</th>
            <th>Tagihan per bandwidth</th>
       </tr>
       <tr>          
            <td>Bandwidth puncak hanya dianggap sebagai <strong>bandwidth puncak maksimum</strong>, bukan sebagai bandwidth tetap. Jika terjadi konflik sumber daya, bandwidth puncak mungkin dibatasi.</td> 
            <td>Bandwidth puncak dianggap sebagai bandwidth tetap. Jika terjadi konflik sumber daya, bandwidth puncak akan dijamin dan tidak akan dibatasi.</td>
            </tr> 
</tbody></table>

## Dokumentasi
[Biaya Jaringan Publik](https://intl.cloud.tencent.com/zh/document/product/213/39743)



