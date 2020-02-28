Tencent Cloud has adjusted the calculation rule for global SMS message length, which will take effect on March 2, 2020. The calculation rule after adjustment is as follows:

### SMS containing only English characters

 - A standard GSM character is calculated as **1 character**, while an extended GSM character is calculated as **2 characters**.
  <table>
     <tr>
         <th width="20%">Category</th>  
         <th nowrap="nowrap">Character List</th>  
     </tr>
	 <tr>      
         <td>Standard characters</td>   
	     <td>! " # $ % ' ( ) * + , - . / : ; < = > ? @ _ ¡ £ ¥ § ¿ & ¤<br>
0 1 2 3 4 5 6 7 8 9<br>
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z<br>
a b c d e f g h i j k l m n o p q r s t u v w x y z<br>
Ä Å Æ Ç É Ñ Ø ø Ü ß Ö à ä å æ è é ì ñ ò ö ù ü Δ Φ Γ Λ Ω Π Ψ Σ Θ Ξ</td>     
     </tr> 
	 <tr> 
	     <td>Extended characters</td>   
	     <td>| ^ € { } [ ] ~ \</td>
     </tr> 
</table>
 - If an SMS message contains less than 160 characters, it will be billed as one message; otherwise, it will be billed as multiple messages based on the standard of 153 characters per message.
  For example, if an SMS message contains 320 characters, it will be billed as 3 messages (153 + 153 + 14 characters).

### SMS containing non-English characters
- One Chinese character, letter, digit, punctuation mark (both fullwidth and halfwidth forms), or space will be calculated as **1 character**.
- If an SMS message contains less than 70 characters, it will be billed as one message; otherwise, it will be billed as multiple messages based on the standard of 67 characters per message.
 For example, if an SMS message contains 150 characters, it will be billed as 3 messages (67 + 67 + 16 characters).
