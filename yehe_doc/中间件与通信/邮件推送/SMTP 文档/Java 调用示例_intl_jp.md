以下のコード例は、JDK1.8を使用したDemoです。
```
package org.example;

import javax.mail.*;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import java.io.UnsupportedEncodingException;
import java.nio.charset.StandardCharsets;
import java.util.Properties;

public class SampleMail {
    private static final String SMTP_HOST = "smtp.qcloudmail.com";
    private static final String SMTP_PORT = "465";

    public static void main(String[] args) {
        // メール送信のための環境属性を設定します
        final Properties props = new Properties();
        // SMTPによるメール送信を示し、ID認証が必要です
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // sslを使用する場合は、25番ポートを使用する設定を削除し、次のように設定してください
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // 送信者のアカウントには、コンソールで設定した送信元アドレス（例：xxx@xxx.com）を入力します
        props.put("mail.user", "xxx@xxx.com");
        // SMTPサービスにアクセスするときに提供する必要のあるパスワード（コンソールで送信元アドレスを選択して設定します）
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // SMTPのID認証用の権限承認情報を作成します
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // ユーザー名、パスワード
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // 環境属性と権限承認情報を使用してメールセッションを作成します
        Session mailSession = Session.getInstance(props, authenticator);
//        mailSession.setDebug(true);
        //UUID uuid = UUID.randomUUID();
        //final String messageIDValue = "<" + uuid.toString() + ">";
        // メールメッセージを作成します
        MimeMessage message = new MimeMessage(mailSession) {
            //@Override
            //protected void updateMessageID() throws MessagingException {
            //カスタムMessage-IDの値を設定します
            //setHeader("Message-ID", messageIDValue);
            //}
        };
        try {
            // 送信者のメールアドレスと名前を設定します。xxx@xxx.comなど、コンソールで設定した送信元アドレスを入力します。上記のmail.userと同じにします。ユーザーは名前をカスタマイズして入力できます。
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            //オプションです。リターンアドレスを設定します
//            Address[] a = new Address[1];
//            a[0] = new InternetAddress("***");
//            message.setReplyTo(a);
            // yyy@yyy.comを例として、受信者のメールアドレスを設定します
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            //同時に複数人に送信する場合は、上の2行を次のように書き換えます（一部の受信システムでは制限があるため、可能な限り1回につき1人に配信するようにしてください。また、1回で送信できる人数は50人までです）。
            //InternetAddress[] adds = new InternetAddress[2];
            //adds[0] = new InternetAddress("xxx@xxx.com");
            //adds[1] = new InternetAddress("xxx@xxx.com");
            //message.setRecipients(Message.RecipientType.TO, adds);

            // メール件名を設定します
            message.setSubject("テストメール");
            message.setHeader("Content-Transfer-Encoding", "base64");
            // メールのコンテンツ本文を設定します。type: text/plain（プレーンテキスト）text/html（HTMLドキュメント）
            message.setContent("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>私の最初の件名</h1>\n    <p>私の最初の段落。</p>\n</body>\n</html>", "text/html;charset=UTF-8");
            //メールを送信します
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }

}
```

## 添付ファイルを送信します
```
package org.example;

import javax.activation.DataHandler;
import javax.activation.FileDataSource;
import javax.mail.*;
import javax.mail.internet.*;
import java.io.UnsupportedEncodingException;
import java.nio.charset.StandardCharsets;
import java.util.Properties;
import java.util.UUID;

public class SampleMailAttach {
    private static final String SMTP_HOST = "smtp.qcloudmail.com";
    private static final String SMTP_PORT = "465";

    public static void main(String[] args) {
        // メール送信のための環境属性を設定します
        final Properties props = new Properties();
        // SMTPによるメール送信を示し、ID認証が必要です
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // sslを使用する場合は、25番ポートを使用する設定を削除し、次のように設定してください
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // 送信者のアカウントには、コンソールで設定した送信元アドレス（例：xxx@xxx.com）を入力します
        props.put("mail.user", "xxx@xxx.com");
        // SMTPサービスにアクセスするときに提供する必要のあるパスワード（コンソールで送信元アドレスを選択して設定します）
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // SMTPのID認証用の権限承認情報を作成します
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // ユーザー名、パスワード
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // 環境属性と権限承認情報を使用してメールセッションを作成します
        Session mailSession = Session.getInstance(props, authenticator);

        UUID uuid = UUID.randomUUID();
        final String messageIDValue = "<" + uuid.toString() + ">";
        //メールメッセージを作成します
        MimeMessage message = new MimeMessage(mailSession) {
            @Override
            protected void updateMessageID() throws MessagingException {
                //カスタムMessage-IDの値を設定します
                setHeader("Message-ID", messageIDValue);
            }
        };
        try {
            // 送信者のメールアドレスと名前を設定します。コンソールで設定した送信元アドレスを入力します。mail.userと同じにします。送信エイリアスはtestなど、カスタマイズが可能です。
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            //オプションです。リターンアドレスを設定します
            Address[] a = new Address[1];
            a[0] = new InternetAddress("xxx@xxx.com");
            message.setReplyTo(a);
            //yyy@yyy.comを例として、受信者のメールアドレスを設定します
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            //同時に複数人に送信する場合は、上の2行を次のように書き換えます（一部の受信システムでは制限があるため、可能な限り1回につき1人に配信するようにしてください。また、1回で送信できる人数は50人までです）。
            /*InternetAddress[] adds = new InternetAddress[2];
            adds[0] = new InternetAddress("xxx@xxx.com");
            adds[1] = new InternetAddress("xxx@xxx.com");
            message.setRecipients(Message.RecipientType.TO, adds);*/

            // メール件名を設定します
            message.setSubject("テストメール");
            //添付ファイルを送信します。メールの合計サイズは10Mを超えないようにし、メッセージパートを作成します
            BodyPart messageBodyPart = new MimeBodyPart();
            // メッセージ type: text/plain（プレーンテキスト）text/html（HTMLドキュメント）
            messageBodyPart.setText("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>私の最初の件名</h1>\n    <p>私の最初の段落。</p>\n</body>\n</html>");
            messageBodyPart.setHeader("Content-Type", "text/plain;charset=utf-8");
            //複数のメッセージを作成します
            Multipart multipart = new MimeMultipart();
            //テキストメッセージパートを設定します
            multipart.addBodyPart(messageBodyPart);
            //添付ファイルパート
            messageBodyPart = new MimeBodyPart();
            //添付ファイルを送信する際のファイルパスを設定します
            String filename = "/Users/aaa/bbb/a.txt";
            FileDataSource source = new FileDataSource(filename);
            messageBodyPart.setDataHandler(new DataHandler(source));
            //添付ファイル名の中国語（添付ファイルパス）の文字化けの問題に対応します
            String filenameEncode = MimeUtility.encodeText(filename, "UTF-8", "base64");
            messageBodyPart.setFileName(filenameEncode);
            messageBodyPart.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart.setHeader("Content-Disposition", "attachment");
            messageBodyPart.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode + "\"");
            multipart.addBodyPart(messageBodyPart);

            //添付ファイルパート、複数の添付ファイル、複数のpartに分割します
            BodyPart messageBodyPart1 = new MimeBodyPart();
            //添付ファイルを送信する際のファイルパスを設定します
            String filename1 = "/Users/aaa/bbb/b.txt";
            FileDataSource source1 = new FileDataSource(filename1);
            messageBodyPart1.setDataHandler(new DataHandler(source1));
            //添付ファイル名の中国語（添付ファイルパス）の文字化けの問題に対応します
            String filenameEncode1 = MimeUtility.encodeText(filename1, "UTF-8", "base64");
            messageBodyPart1.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart1.setHeader("Content-Disposition", "attachment");
            messageBodyPart1.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode1 + "\"");
            multipart.addBodyPart(messageBodyPart1);

            //添付ファイル付きの完全なメッセージを送信します
            message.setContent(multipart);
            //添付ファイルコードを送信し、終了します
            //メールを送信します
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }
}
```
## よくあるご質問
### 「No appropriate protocol (protocol is disabled or cipher suites are inappropriate)」というエラーが発生しました。どうすればよいですか。
`jdk/jre/lib/security/java.security`ファイルを見つけて、次のように変更します。
![](https://qcloudimg.tencent-cloud.cn/raw/d05f0478d608849a10f61290777a2689.png)
