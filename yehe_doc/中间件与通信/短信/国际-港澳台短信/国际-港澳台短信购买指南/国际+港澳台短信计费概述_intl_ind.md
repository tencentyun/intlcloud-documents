<span id="size"></span>
## Aturan Perhitungan Panjang SMS
Panjang SMS = jumlah karakter dalam tanda tangan SMS + jumlah karakter dalam isi SMS. Satu pesan SMS dapat berisi hingga 500 karakter.
>Tanda tangan bersifat opsional untuk SMS Global.

### SMS yang hanya berisi karakter bahasa Inggris

 - Karakter GSM standar dihitung sebagai **1 karakter**, sedangkan karakter GSM panjang dihitung sebagai **2 karakter**.
  <table>
     <tr>
         <th width="20%">Kategori</th>  
         <th nowrap="nowrap">Daftar Karakter</th>  
     </tr>
	 <tr>      
         <td>Karakter standar</td>   
	     <td>! " # $ % ' ( ) * + , - . / : ; < = > ? @ _ ¡ £ ¥ § ¿ & ¤<br>
0 1 2 3 4 5 6 7 8 9<br>
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z<br>
a b c d e f g h i j k l m n o p q r s t u v w x y z<br>
Ä Å Æ Ç É Ñ Ø ø Ü ß Ö à ä å æ è é ì ñ ò ö ù ü Δ Φ Γ Λ Ω Π Ψ Σ Θ Ξ</td>     
     </tr> 
	 <tr> 
	     <td>Karakter panjang</td>   
	     <td>| ^ € { } [ ] ~ \</td>
     </tr> 
</table>
 - Jika berisi maksimum 160 karakter, pesan SMS akan dikenai tagihan sebagai satu pesan. Jika berisi lebih dari 160 karakter, pesan SMS akan dikenai tagihan sebagai beberapa pesan berdasarkan standar 153 karakter per pesan.
  Misalnya, pesan SMS yang berisi 320 karakter akan dikenai tagihan sebagai 3 pesan (153 + 153 + 14 karakter).

### SMS yang berisi karakter non-Inggris
- Satu karakter, huruf, angka, tanda baca bahasa Mandarin (baik bentuk fullwidth maupun halfwidth), atau spasi akan dihitung sebagai **1 karakter**.
- Jika berisi maksimum 70 karakter, pesan SMS akan dikenai tagihan sebagai satu pesan. Jika berisi lebih dari 70 karakter, pesan SMS akan dikenai tagihan sebagai beberapa pesan berdasarkan standar 67 karakter per pesan.
 Misalnya, pesan SMS yang berisi 150 karakter akan dikenai tagihan sebagai 3 pesan (67 + 67 + 16 karakter).



## Mode Penagihan
Pembayaran SMS Global dilakukan sesuai dengan pemakaian harian berdasarkan panjang per pesan. **Voucher umum tidak berlaku.** Pembayaran untuk satu hari tertentu akan dipotong pada pukul 8.00 hari berikutnya sebagaimana dijelaskan dalam tagihan. SMS Global tersedia di lebih dari 200 negara dan wilayah dengan harga yang berbeda-beda. Untuk informasi selengkapnya, lihat [Ikhtisar Penetapan Harga SMS Global](https://intl.cloud.tencent.com/document/product/382/8414).

## Detail Penagihan
Sebelum tanggal 3 setiap bulan, Tencent Cloud akan mengirim detail tagihan SMS global untuk bulan sebelumnya kepada Anda. Anda dapat mengeklik **Details** (Detail) untuk layanan SMS di Konsol Tencent Cloud > **Billing Center** > **[Transactions] (Pusat Penagihan > [Transaksi])(https://console.cloud.tencent.com/expense/transactions)** untuk melihat detail penagihan. Anda juga dapat mengekspor laporan untuk pelaporan keuangan dan pembukuan.

## Keterlambatan Pembayaran
Pembayaran SMS Global dilakukan berdasarkan pemakaian harian. Pembayaran untuk satu hari tertentu dipotong pada pukul 8.00 hari berikutnya. Jika pembayaran gagal karena saldo tidak cukup, Anda akan menerima pemberitahuan keterlambatan pembayaran melalui SMS. Jika Anda tidak membayar tagihan yang telah jatuh tempo dalam waktu 12 jam, layanan akan ditangguhkan.
Layanan akan kembali tersedia setelah saldo di akun Tencent Cloud Anda cukup. Konsekuensi yang terjadi akibat penangguhan layanan karena keterlambatan pembayaran ditanggung sepenuhnya oleh Anda.
