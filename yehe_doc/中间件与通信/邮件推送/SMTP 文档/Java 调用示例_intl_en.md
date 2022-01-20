The following sample code is a demo on JDK 1.8:
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
        // Configure the environment attributes for email sending
        final Properties props = new Properties();
        // Indicate that SMTP is used to send the email, which requires authentication
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // If SSL is used, remove the configuration of using port 25 and perform the following configuration:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Sender account. Enter the sender address configured in the console, such as xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // The password that needs to be provided when the SMTP service is accessed (select the sender address in the console to configure)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Build the authorization information for SMTP authentication
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Username and password
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Create the email session with the environment attributes and authorization information
        Session mailSession = Session.getInstance(props, authenticator);
//        mailSession.setDebug(true);
        //UUID uuid = UUID.randomUUID();
        //final String messageIDValue = "<" + uuid.toString() + ">";
        // Create the email message
        MimeMessage message = new MimeMessage(mailSession) {
            //@Override
            //protected void updateMessageID() throws MessagingException {
            // Set the custom `Message-ID` value
            //setHeader("Message-ID", messageIDValue);
            //}
        };
        try {
            // Set the sender email address and name. Here, enter the sender address configured in the console (which must be the same as the `mail.user` above), such as xxx@xxx.com. The name can be customized
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Optional) Set the reply-to address
//            Address[] a = new Address[1];
//            a[0] = new InternetAddress("***");
//            message.setReplyTo(a);
            // Set the recipient's email address, such as yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // If the email is to be sent to multiple recipients at the same time, replace the above two lines with the following (due to the restrictions of some emailing systems, we recommend you try to send the email to one recipient at a time; plus, the email can be sent to up to 50 recipients at a time):
            //InternetAddress[] adds = new InternetAddress[2];
            //adds[0] = new InternetAddress("xxx@xxx.com");
            //adds[1] = new InternetAddress("xxx@xxx.com");
            //message.setRecipients(Message.RecipientType.TO, adds);

            // Set the email subject
            message.setSubject("Test email");
            message.setHeader("Content-Transfer-Encoding", "base64");
            // Set the email body type: `text/plain` (plain text) or `text/html` (HTML document)
            message.setContent("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>", "text/html;charset=UTF-8");
            // Send the email
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }

}
```

## Sending Attachment
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
        // Configure the environment attributes for email sending
        final Properties props = new Properties();
        // Indicate that SMTP is used to send the email, which requires authentication
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // If SSL is used, remove the configuration of using port 25 and perform the following configuration:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Sender account. Enter the sender address configured in the console, such as xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // The password that needs to be provided when the SMTP service is accessed (select the sender address in the console to configure)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Build the authorization information for SMTP authentication
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Username and password
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Create the email session with the environment attributes and authorization information
        Session mailSession = Session.getInstance(props, authenticator);

        UUID uuid = UUID.randomUUID();
        final String messageIDValue = "<" + uuid.toString() + ">";
        // Create the email message
        MimeMessage message = new MimeMessage(mailSession) {
            @Override
            protected void updateMessageID() throws MessagingException {
                // Set the custom `Message-ID` value
                setHeader("Message-ID", messageIDValue);
            }
        };
        try {
            // Set the sender email address and name. Here, enter the sender address configured in the console (which must be the same as the `mail.user` above). The name can be customized, such as test
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Optional) Set the reply-to address
            Address[] a = new Address[1];
            a[0] = new InternetAddress("xxx@xxx.com");
            message.setReplyTo(a);
            // Set the recipient's email address, such as yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // If the email is to be sent to multiple recipients at the same time, replace the above two lines with the following (due to the restrictions of some emailing systems, we recommend you try to send the email to one recipient at a time; plus, the email can be sent to up to 50 recipients at a time):
            /*InternetAddress[] adds = new InternetAddress[2];
            adds[0] = new InternetAddress("xxx@xxx.com");
            adds[1] = new InternetAddress("xxx@xxx.com");
            message.setRecipients(Message.RecipientType.TO, adds);*/

            // Set the email subject
            message.setSubject("Test email");
            // Send the attachment. The total message size does not exceed 10M, create a message part
            BodyPart messageBodyPart = new MimeBodyPart();
            // Message body: `text/plain` (plain text) or `text/html` (HTML document)
            messageBodyPart.setText("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>");
            messageBodyPart.setHeader("Content-Type", "text/plain;charset=utf-8");
            // Create the multipart message
            Multipart multipart = new MimeMultipart();
            // Set the text message part
            multipart.addBodyPart(messageBodyPart);
            // Attachment part
            messageBodyPart = new MimeBodyPart();
            // Set the path of the attachment file
            String filename = "/Users/aaa/bbb/a.txt";
            FileDataSource source = new FileDataSource(filename);
            messageBodyPart.setDataHandler(new DataHandler(source));
            // Handle the garbled text problem of the attachment name in Chinese (attached file path)
            String filenameEncode = MimeUtility.encodeText(filename, "UTF-8", "base64");
            messageBodyPart.setFileName(filenameEncode);
            messageBodyPart.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart.setHeader("Content-Disposition", "attachment");
            messageBodyPart.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode + "\"");
            multipart.addBodyPart(messageBodyPart);

            // Attachment part. Multiple attachments should be divided into multiple parts
            BodyPart messageBodyPart1 = new MimeBodyPart();
            // Set the path of the attachment file
            String filename1 = "/Users/aaa/bbb/b.txt";
            FileDataSource source1 = new FileDataSource(filename1);
            messageBodyPart1.setDataHandler(new DataHandler(source1));
            // Handle the garbled text problem of the attachment name in Chinese (attached file path)
            String filenameEncode1 = MimeUtility.encodeText(filename1, "UTF-8", "base64");
            messageBodyPart1.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart1.setHeader("Content-Disposition", "attachment");
            messageBodyPart1.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode1 + "\"");
            multipart.addBodyPart(messageBodyPart1);

            // Send the complete message with attachments
            message.setContent(multipart);
            // Code for sending attachments (end)
            // Send the email
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }
}
```
## FAQs
### How do I fix the error "No appropriate protocol (protocol is disabled or cipher suites are inappropriate)"?
Find the `jdk/jre/lib/security/java.security` file and modify it:
![](https://qcloudimg.tencent-cloud.cn/raw/d05f0478d608849a10f61290777a2689.png)
