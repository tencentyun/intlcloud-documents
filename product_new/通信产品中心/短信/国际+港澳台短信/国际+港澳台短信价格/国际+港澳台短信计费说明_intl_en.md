<span id="size"></span>
## SMS Length Calculation Rule
SMS length = number of characters in the signature + number of characters in the body. A single SMS message can contain up to 500 characters.
>?Signature is optional for global SMS.

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
 - If an SMS message contains 160 characters or less, it will be billed as one message; otherwise, it will be billed as multiple messages based on the standard of 153 characters per message.
  For example, if an SMS message contains 320 characters, it will be billed as 3 messages (153 + 153 + 14 characters).

### SMS containing non-English characters
- One Chinese character, letter, digit, punctuation mark (both fullwidth and halfwidth forms), or space will be calculated as **1 character**.
- If an SMS message contains 70 characters or less, it will be billed as one message; otherwise, it will be billed as multiple messages based on the standard of 67 characters per message.
 For example, if an SMS message contains 150 characters, it will be billed as 3 messages (67 + 67 + 16 characters).



## Billing Mode
Global SMS is daily pay-as-you-go by message length on a per message basis. **General vouchers do not apply.** The payment for a day is deducted at 8:00 am the next day as detailed in the bill. Global SMS is available in over 200 countries and regions by which the prices vary. For more information, please see [Global SMS Pricing Overview](https://cloud.tencent.com/document/product/382/18051).

## Billing Details
Before the 3rd day of each month, Tencent Cloud will provide you with a detailed global SMS bill for last month. You can click **Details** for the SMS service in Tencent Cloud Console > **Billing Center** > **[Transactions](https://console.cloud.tencent.com/expense/transactions)** to view the billing details. You can also export reports for financial reporting and bookkeeping.

## Arrears
Global SMS is daily pay-as-you-go. The payment for a day is deducted at 8:00 am the next day. If payment fails due to insufficient balance, you will receive an arrears notification via SMS. If you fail to top up your account within 12 hours, the service will be suspended.
The service will resume when you have sufficient balance in your Tencent Cloud account. You shall be responsible for any consequences caused by service suspension due to arrears.
