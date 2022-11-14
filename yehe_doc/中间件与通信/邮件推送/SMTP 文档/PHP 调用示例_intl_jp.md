## 注意事項
1. ユーザーにはPHPMailerパッケージの使用を推奨します。
 - 新規プロジェクトで、なおかつcomposerを使用している場合は、composer.jsonに`"phpmailer/phpmailer": "^6.5"`を追加するか、または`composer require phpmailer/phpmailer`を実行し、次のコードを使用します。
 - 既存のプロジェクトで、なおかつcomposerを使用していない場合は、[PHPMailer](https://github.com/PHPMailer/PHPMailer)を手動でインポートする必要があります。
2. サービスアドレスおよびポートについては、[SMTPサービスアドレス](https://intl.cloud.tencent.com/document/product/1084/44457)をご参照ください。

コードは次のとおりです。

```php
<?php

use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;
require './PHPMailer/src/Exception.php';
require './PHPMailer/src/PHPMailer.php';
require './PHPMailer/src/SMTP.php';

$mail = new PHPMailer(true);

try {
    //Server settings
    $mail->SMTPDebug  = SMTP::DEBUG_SERVER;                     //Enable verbose debug output
    $mail->SMTPAuth   = true;                                   //Enable SMTP authentication
    //$mail->AuthType   = 'LOGIN';                
    $mail->isSMTP();                                            //Send using SMTP
    $mail->Host       = 'smtp.qcloudmail.com';                  //Set the SMTP server to send through
    $mail->Username   = 'abc@qq.aa.com';          //SMTP username
    $mail->Password   = '123456';                  //SMTP password

    $mail->SMTPSecure = PHPMailer::ENCRYPTION_SMTPS;            //Enable implicit TLS encryption
    $mail->CharSet 	  = PHPMailer::CHARSET_UTF8;
    $mail->CharSet 	  = 'UTF-8';
    $mail->ContentType = 'text/plain; charset=UTF-8';
    $mail->Encoding   = PHPMailer::ENCODING_BASE64;
    //$mail->Encoding   = '8bit';
    $mail->Port       = 465;                                    //TCP port to connect to; use 587 if you have set `SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS`

    //Recipients
    $mail->setFrom('abc@qq.aa.com', 'fromName');
    $mail->addAddress('test@test.com', 'toName');    //Add a recipient
    //$mail->addAddress('ellen@example.com');                   //Name is optional
    //$mail->addReplyTo('info@example.com', 'Information');
    //$mail->addCC('cc@example.com');
    //$mail->addBCC('bcc@example.com');

    //Attachments
    $mail->addAttachment('./tmp.txt');         	                //Add attachments
    //$mail->addAttachment('/tmp/image.jpg', 'new.jpg');    	//Optional name

    //Content
    //$mail->isHTML(true);                                        //Set email format to HTML
    $mail->Subject = 'Here is the subject';
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    //$mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

    $mail->send();
    echo 'Message has been sent';
} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}

```
