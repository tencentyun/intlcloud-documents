Tencent Cloud telah menyesuaikan aturan penghitungan untuk panjang pesan SMS global, yang mulai berlaku pada 2 Maret 2020. Aturan penghitungan setelah penyesuaian adalah sebagai berikut:

### SMS yang hanya berisi karakter bahasa Inggris

 - Karakter GSM standar dihitung sebagai **1 karakter**, sedangkan karakter GSM yang diperluas dihitung sebagai **2 karakter**.
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
	     <td>Karakter yang diperluas</td>   
	     <td>| ^ € { } [ ] ~ \</td>
     </tr> 
</table>
 - Jika pesan SMS berisi 160 karakter atau kurang, pesan akan ditagih sebagai satu pesan; jika lebih dari itu, pesan akan ditagih sebagai beberapa pesan berdasarkan standar 153 karakter per pesan.
  Misalnya, jika pesan SMS berisi 320 karakter, pesan akan ditagih sebagai 3 pesan (153 + 153 + 14 karakter).

### SMS yang berisi karakter non-bahasa Inggris
- Satu karakter, huruf, angka, tanda baca di bahasa Mandarin (baik bentuk fullwidth maupun halfwidth), atau spasi akan dihitung sebagai **1 karakter**.
- Jika pesan SMS berisi 70 karakter atau kurang, pesan akan ditagih sebagai satu pesan; jika lebih dari itu, pesan akan ditagih sebagai beberapa pesan berdasarkan standar 67 karakter per pesan.
 Misalnya, jika pesan SMS berisi 150 karakter, pesan akan ditagih sebagai 3 pesan (67 + 67 + 16 karakter).
