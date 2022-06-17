O código de exemplo abaixo é uma demonstração no JDK 1.8:
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
    private static final String SMTP_HOST = "465";

    public static void main(String[] args) {
        // Configure os atributos de ambiente para envio de e-mail
        final Properties props = new Properties();
        // Indique que o SMTP é usado para enviar o e-mail, o que requer autenticação
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // Se o SSL for usado, remova a configuração de uso da porta 25 e execute a seguinte configuração:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Conta do remetente. Digite o endereço do remetente configurado no console, como xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // A senha que precisa ser fornecida quando o serviço SMTP for acessado (selecione o endereço do remetente no console para configurar)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Crie as informações de autorização para autenticação do SMTP
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Usuário e senha
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Crie a sessão de e-mail com os atributos de ambiente e informações de autorização
        Session mailSession = Session.getInstance(props, authenticator);
//        mailSession.setDebug(true);
        //UUID uuid = UUID.randomUUID();
        //final String messageIDValue = "<" + uuid.toString() + ">";
        // Crie a mensagem de e-mail
        MimeMessage message = new MimeMessage(mailSession) {
            //@Override
            //protected void updateMessageID() throws MessagingException {
            // Defina o valor personalizado de `Message-ID`
            //setHeader("Message-ID", messageIDValue);
            //}
        };
        try {
            // Defina o endereço de e-mail e o nome do remetente. Aqui, digite o endereço do remetente configurado no console (que deve ser o mesmo do `mail.user` acima), como xxx@xxx.com. O nome pode ser personalizado
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Opcional) Defina o endereço de resposta
//            Address[] a = new Address[1];
//            a[0] = new InternetAddress("***");
//            message.setReplyTo(a);
            // Defina o endereço de e-mail do destinatário, como yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // Se o e-mail for enviado para vários destinatários ao mesmo tempo, substitua as duas linhas acima pelo seguinte (devido às restrições de alguns sistemas de e-mail, recomendamos que você tente enviar o e-mail para um destinatário de cada vez; além disso, o e-mail pode ser enviado para até 50 destinatários por vez):
            //InternetAddress[] adds = new InternetAddress[2];
            //adds[0] = new InternetAddress("xxx@xxx.com");
            //adds[1] = new InternetAddress("xxx@xxx.com");
            //message.setRecipients(Message.RecipientType.TO, adds);

            // Defina o assunto do e-mail
            message.setSubject("Test email");
            message.setHeader("Content-Transfer-Encoding", "base64");
            // Defina o tipo de corpo do e-mail: `text/plain` (plain text) or `text/html` (HTML document)
            message.setContent("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>", "text/html;charset=UTF-8");
            // Envie o e-mail
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }

}
```

## Envio de anexo
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
    private static final String SMTP_HOST = "465";

    public static void main(String[] args) {
        // Configure os atributos de ambiente para envio de e-mail
        final Properties props = new Properties();
        // Indique que o SMTP é usado para enviar o e-mail, o que requer autenticação
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // Se SSL for usado, remova a configuração de uso da porta 25 e execute a seguinte configuração:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Conta do remetente. Digite o endereço do remetente configurado no console, como xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // A senha que precisa ser fornecida quando o serviço SMTP for acessado (selecione o endereço do remetente no console para configurar)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Crie as informações de autorização para autenticação SMTP
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Usuário e senha
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Crie a sessão de e-mail com os atributos de ambiente e informações de autorização
        Session mailSession = Session.getInstance(props, authenticator);

        UUID uuid = UUID.randomUUID();
        final String messageIDValue = "<" + uuid.toString() + ">";
        // Crie a mensagem de e-mail
        MimeMessage message = new MimeMessage(mailSession) {
            @Override
            protected void updateMessageID() throws MessagingException {
                // Defina o valor personalizado de `Message-ID`
                setHeader("Message-ID", messageIDValue);
            }
        };
        try {
            // Defina o endereço de e-mail e o nome do remetente. Aqui, digite o endereço do remetente configurado no console (que deve ser o mesmo do `mail.user` acima). O nome pode ser personalizado, como test
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Opcional) Defina o endereço de resposta
            Address[] a = new Address[1];
            a[0] = new InternetAddress("xxx@xxx.com");
            message.setReplyTo(a);
            // Defina o endereço de e-mail do destinatário, como yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // Se o e-mail for enviado para vários destinatários ao mesmo tempo, substitua as duas linhas acima pelo seguinte (devido às restrições de alguns sistemas de e-mail, recomendamos que você tente enviar o e-mail para um destinatário de cada vez; além disso, o e-mail pode ser enviado para até 50 destinatários por vez):
            /*InternetAddress[] adds = new InternetAddress[2];
            adds[0] = new InternetAddress("xxx@xxx.com");
            adds[1] = new InternetAddress("xxx@xxx.com");
            message.setRecipients(Message.RecipientType.TO, adds);*/

            // Defina o assunto do e-mail
            message.setSubject("Test email");
            // Envie o anexo. O tamanho total da mensagem não excede 10M, crie uma parte da mensagem
            BodyPart messageBodyPart = new MimeBodyPart();
            // Corpo da mensagem: `text/plain` (plain text) or `text/html` (HTML document)
            messageBodyPart.setText("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>");
            messageBodyPart.setHeader("Content-Type", "text/plain;charset=utf-8");
            // Crie a mensagem de várias partes
            Multipart multipart = new MimeMultipart();
            // Defina a parte da mensagem de texto
            multipart.addBodyPart(messageBodyPart);
            // Parte do anexo
            messageBodyPart = new MimeBodyPart();
            // Defina o caminho do arquivo anexo
            String filename = "/Users/aaa/bbb/a.txt";
            FileDataSource source = new FileDataSource(filename);
            messageBodyPart.setDataHandler(new DataHandler(source));
            // Resolva o problema de texto ilegível do nome do anexo em chinês (caminho do arquivo anexado)
            String filenameEncode = MimeUtility.encodeText(filename, "UTF-8", "base64");
            messageBodyPart.setFileName(filenameEncode);
            messageBodyPart.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart.setHeader("Content-Disposition", "attachment");
            messageBodyPart.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode + "\"");
            multipart.addBodyPart(messageBodyPart);

            // Parte do anexo. Vários anexos devem ser divididos em várias partes
            BodyPart messageBodyPart1 = new MimeBodyPart();
            // Defina o caminho do arquivo anexo
            String filename1 = "/Users/aaa/bbb/b.txt";
            FileDataSource source1 = new FileDataSource(filename1);
            messageBodyPart1.setDataHandler(new DataHandler(source1));
            // Resolva o problema de texto ilegível do nome do anexo em chinês (caminho do arquivo anexado)
            String filenameEncode1 = MimeUtility.encodeText(filename1, "UTF-8", "base64");
            messageBodyPart1.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart1.setHeader("Content-Disposition", "attachment");
            messageBodyPart1.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode1 + "\"");
            multipart.addBodyPart(messageBodyPart1);

            // Envie a mensagem completa com anexos
            message.setContent(multipart);
            // Código para envio de anexos (fim)
            // Envie o e-mail
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }
}
```
## Perguntas frequentes
### Como corrigir o erro “No appropriate protocol (protocol is disabled or cipher suites are inappropriate)”?
Localize o arquivo `jdk/jre/lib/security/java.security` e modifique-o:
![](https://qcloudimg.tencent-cloud.cn/raw/d05f0478d608849a10f61290777a2689.png)
