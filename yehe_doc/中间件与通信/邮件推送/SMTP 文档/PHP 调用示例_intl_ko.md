## 주의 사항
1. PHPMailer 패키지 사용을 권장합니다:
 - 만약 새로운 프로젝트이고 composer를 사용한다면 composer.json에 `"phpmailer/phpmailer": "^6.5"` 를 추가하거나 `composer require phpmailer/phpmailer` 를 실행한 후 아래 코드를 사용하십시오.
 - 오래된 프로젝트이고 composer를 사용하지 않는 경우 [PHPMailer](https://github.com/PHPMailer/PHPMailer)를 수동으로 가져와야 합니다.
2. 서비스 주소 및 포트는 [SMTP 서비스 주소](https://intl.cloud.tencent.com/document/product/1084/44457)를 참고하십시오.

다음은 코드 예시입니다:

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
