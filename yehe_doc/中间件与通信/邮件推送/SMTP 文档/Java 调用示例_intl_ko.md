다음은 JDK 1.8 Demo 예시 코드입니다.
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
        // 이메일 전송을 위한 환경 속성 구성
        final Properties props = new Properties();
        // 인증이 필요한 이메일을 보내는 데 SMTP가 사용됨을 표시
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // ssl을 사용하는 경우 포트 25를 사용하는 구성을 제거 후 다음 설정 진행,
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // 발신자 계정. xxx@xxx.com과 같이 콘솔에 구성된 발신자 주소 입력
        props.put("mail.user", "xxx@xxx.com");
        // SMTP 서비스 접속 시 입력해야 하는 비밀번호(콘솔에서 발신자 주소를 선택하여 구성)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // SMTP 인증을 위한 권한 정보 빌드
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // 사용자 이름과 비밀번호
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // 환경 속성 및 권한 부여 정보를 사용하여 이메일 세션 생성
        Session mailSession = Session.getInstance(props, authenticator);
//        mailSession.setDebug(true);
        //UUID uuid = UUID.randomUUID();
        //final String messageIDValue = "<" + uuid.toString() + ">";
        // 이메일 메시지 생성
        MimeMessage message = new MimeMessage(mailSession) {
            //@Override
            //protected void updateMessageID() throws MessagingException {
            //사용자 정의 Message-ID 값 설정
            //setHeader("Message-ID", messageIDValue);
            //}
        };
        try {
            // 발신자 이메일 주소와 이름 설정. 여기에 xxx@xxx.com과 같이 콘솔에서 구성한 발신자 주소(상기 mail.user와 동일해야 함) 입력. 이름은 사용자 정의 가능.
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            //옵션. 회신 주소 설정
//            Address[] a = new Address[1];
//            a[0] = new InternetAddress("***");
//            message.setReplyTo(a);
            // 수신자의 이메일 주소 설정(예시: yyy@yyy.com)
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            //이메일을 동시에 여러 수신자에게 보낼 경우 상기 두 줄을 다음으로 대체(일부 이메일 시스템의 제한으로 인해 한 번에 한 수신자에게 이메일을 보내도록 권장합니다. 또한 이메일은 한 번에 최대 50명의 수신자에게 보낼 수 있습니다):
            //InternetAddress[] adds = new InternetAddress[2];
            //adds[0] = new InternetAddress("xxx@xxx.com");
            //adds[1] = new InternetAddress("xxx@xxx.com");
            //message.setRecipients(Message.RecipientType.TO, adds);

            // 이메일 제목 설정
            message.setSubject("이메일 테스트");
            message.setHeader("Content-Transfer-Encoding", "base64");
            // 이메일 본문 설정 type: text/plain(일반 텍스트) 또는 text/html(HTML 문서)
            message.setContent("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>내 첫 번째 제목</h1>\n    <p>내 첫 번째 단락.</p>\n</body>\n</html>", "text/html;charset=UTF-8");
            //이메일 전송
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }

}
```

## 첨부 파일 전송
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
        // 이메일 전송을 위한 환경 속성 구성
        final Properties props = new Properties();
        // 인증이 필요한 이메일을 보내는 데 SMTP가 사용됨 표시
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // ssl을 사용하는 경우 포트 25를 사용하는 구성을 제거 후 다음 설정 진행,
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // 발신자 계정. xxx@xxx.com과 같이 콘솔에 구성된 발신자 주소 입력
        props.put("mail.user", "xxx@xxx.com");
        // SMTP 서비스 접속 시 입력해야 하는 비밀번호(콘솔에서 발신자 주소를 선택하여 구성)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // SMTP 인증을 위한 권한 정보 빌드
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // 사용자 이름과 비밀번호
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // 환경 속성 및 권한 부여 정보를 사용하여 이메일 세션 생성
        Session mailSession = Session.getInstance(props, authenticator);

        UUID uuid = UUID.randomUUID();
        final String messageIDValue = "<" + uuid.toString() + ">";
        //이메일 메시지 생성
        MimeMessage message = new MimeMessage(mailSession) {
            @Override
            protected void updateMessageID() throws MessagingException {
                //사용자 정의 Message-ID 값 설정
                setHeader("Message-ID", messageIDValue);
            }
        };
        try {
            // 발신자 이메일 주소와 이름을 설정합니다. 여기에 콘솔에서 구성한 발신자 주소를 입력합니다(상기 mail.user와 동일해야 함). 이름은 test와 같이 사용자 정의할 수 있습니다.
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            //옵션. 회신 주소 설정
            Address[] a = new Address[1];
            a[0] = new InternetAddress("xxx@xxx.com");
            message.setReplyTo(a);
            //수신자의 이메일 주소 설정(예시: yyy@yyy.com)
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            //이메일을 동시에 여러 수신자에게 보낼 경우 상기 두 줄을 다음으로 대체(일부 이메일 시스템의 제한으로 인해 한 번에 한 수신자에게 이메일을 보내도록 권장합니다. 또한 이메일은 한 번에 최대 50명의 수신자에게 보낼 수 있습니다):
            /*InternetAddress[] adds = new InternetAddress[2];
            adds[0] = new InternetAddress("xxx@xxx.com");
            adds[1] = new InternetAddress("xxx@xxx.com");
            message.setRecipients(Message.RecipientType.TO, adds);*/

            // 이메일 제목 설정
            message.setSubject("이메일 테스트");
            //첨부 파일 전송, 총 메시지 크기는 10M 이하, 메시지 부분 생성
            BodyPart messageBodyPart = new MimeBodyPart();
            //메시지 본문: text/plain(일반 텍스트) 또는 text/html(HTML 문서)
            messageBodyPart.setText("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>내 첫 번째 제목</h1>\n    <p>내 첫 번째 단락.</p>\n</body>\n</html>");
            messageBodyPart.setHeader("Content-Type", "text/plain;charset=utf-8");
            //멀티파트 메시지 생성
            Multipart multipart = new MimeMultipart();
            //문자 메시지 부분 설정
            multipart.addBodyPart(messageBodyPart);
            //첨부 부분
            messageBodyPart = new MimeBodyPart();
            //첨부파일 경로 설정
            String filename = "/Users/aaa/bbb/a.txt";
            FileDataSource source = new FileDataSource(filename);
            messageBodyPart.setDataHandler(new DataHandler(source));
            //중국어로 된 첨부 파일 이름의 깨진 글자 문제 처리(첨부 파일 경로)
            String filenameEncode = MimeUtility.encodeText(filename, "UTF-8", "base64");
            messageBodyPart.setFileName(filenameEncode);
            messageBodyPart.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart.setHeader("Content-Disposition", "attachment");
            messageBodyPart.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode + "\"");
            multipart.addBodyPart(messageBodyPart);

            //첨부 부분. 여러 첨부 파일은 여러 part로 분할
            BodyPart messageBodyPart1 = new MimeBodyPart();
            //첨부파일 경로 설정
            String filename1 = "/Users/aaa/bbb/b.txt";
            FileDataSource source1 = new FileDataSource(filename1);
            messageBodyPart1.setDataHandler(new DataHandler(source1));
            //중국어로 된 첨부 파일 이름의 깨진 글자 문제 처리(첨부 파일 경로)
            String filenameEncode1 = MimeUtility.encodeText(filename1, "UTF-8", "base64");
            messageBodyPart1.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart1.setHeader("Content-Disposition", "attachment");
            messageBodyPart1.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode1 + "\"");
            multipart.addBodyPart(messageBodyPart1);

            //첨부 파일과 함께 전체 메시지 전송
            message.setContent(multipart);
            //첨부 파일을 보내기 위한 코드(end)
            //이메일 전송
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }
}
```
## FAQ
### “No appropriate protocol (protocol is disabled or cipher suites are inappropriate)” 오류를 수정하려면 어떻게 해야 합니까?
`jdk/jre/lib/security/java.security` 파일을 찾아 수정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d05f0478d608849a10f61290777a2689.png)
