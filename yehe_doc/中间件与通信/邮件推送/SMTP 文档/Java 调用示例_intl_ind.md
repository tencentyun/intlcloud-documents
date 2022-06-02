Contoh kode berikut adalah demo di JDK 1.8:
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
        // Konfigurasikan atribut lingkungan untuk pengiriman email
        final Properties props = new Properties();
        // Tunjukkan bahwa SMTP digunakan untuk mengirim email, yang memerlukan autentikasi
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // Jika SSL digunakan, hapus konfigurasi menggunakan port 25 dan lakukan konfigurasi berikut:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Akun pengirim. Masukkan alamat pengirim yang dikonfigurasi di konsol, seperti xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // Kata sandi yang perlu diberikan saat layanan SMTP diakses (pilih alamat pengirim di konsol untuk dikonfigurasi)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Buat informasi otorisasi untuk autentikasi SMTP
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Nama pengguna dan kata sandi
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Buat sesi email dengan atribut lingkungan dan informasi otorisasi
        Session mailSession = Session.getInstance(props, authenticator);
//        mailSession.setDebug(true);
        //UUID uuid = UUID.randomUUID();
        //final String messageIDValue = "<" + uuid.toString() + ">";
        // Buat pesan email
        MimeMessage message = new MimeMessage(mailSession) {
            //@Override
            //protected void updateMessageID() throws MessagingException {
            // Tetapkan nilai `Message-ID` kustom
            //setHeader("Message-ID", messageIDValue);
            //}
        };
        try {
            // Tetapkan alamat dan nama email pengirim. Di sini, masukkan alamat pengirim yang dikonfigurasi di konsol (yang harus sama dengan `mail.user` di atas), seperti xxx@xxx.com. Nama dapat disesuaikan
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Opsional) Tetapkan alamat balas-ke
//            Address[] a = new Address[1];
//            a[0] = new InternetAddress("***");
//            message.setReplyTo(a);
            // Tetapkan alamat email penerima, seperti yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // Jika email akan dikirim ke beberapa penerima sekaligus, ganti dua baris di atas dengan yang berikut (karena pembatasan beberapa sistem email, kami sarankan Anda mencoba mengirim email ke satu penerima dalam satu waktu; selain itu, email dapat dikirim ke hingga 50 penerima sekaligus):
            //InternetAddress[] adds = new InternetAddress[2];
            //adds[0] = new InternetAddress("xxx@xxx.com");
            //adds[1] = new InternetAddress("xxx@xxx.com");
            //message.setRecipients(Message.RecipientType.TO, adds);

            // Tetapkan subjek email
            message.setSubject("Test email");
            message.setHeader("Content-Transfer-Encoding", "base64");
            // Tetapkan jenis badan email: `text/plain` (plain text) or `text/html` (HTML document)
            message.setContent("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>", "text/html;charset=UTF-8");
            // Kirim email
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }

}
```

## Mengirim Lampiran
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
        // Konfigurasikan atribut lingkungan untuk pengiriman email
        final Properties props = new Properties();
        // Tunjukkan bahwa SMTP digunakan untuk mengirim email, yang memerlukan autentikasi
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.host", SMTP_HOST);
        // Jika SSL digunakan, hapus konfigurasi menggunakan port 25 dan lakukan konfigurasi berikut:
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.port", SMTP_PORT);
        props.put("mail.smtp.port", SMTP_PORT);
        // Akun pengirim. Masukkan alamat pengirim yang dikonfigurasi di konsol, seperti xxx@xxx.com
        props.put("mail.user", "xxx@xxx.com");
        // Kata sandi yang perlu diberikan saat layanan SMTP diakses (pilih alamat pengirim di konsol untuk dikonfigurasi)
        props.put("mail.password", "XXXX");
        props.setProperty("mail.smtp.socketFactory.fallback", "false");
        props.put("mail.smtp.ssl.enable", "true");
        //props.put("mail.smtp.starttls.enable","true");
        // Buat informasi otorisasi untuk autentikasi SMTP
        Authenticator authenticator = new Authenticator() {
            @Override
            protected PasswordAuthentication getPasswordAuthentication() {
                // Nama pengguna dan kata sandi
                String userName = props.getProperty("mail.user");
                String password = props.getProperty("mail.password");
                return new PasswordAuthentication(userName, password);
            }
        };
        // Buat sesi email dengan atribut lingkungan dan informasi otorisasi
        Session mailSession = Session.getInstance(props, authenticator);

        UUID uuid = UUID.randomUUID();
        final String messageIDValue = "<" + uuid.toString() + ">";
        // Buat pesan email
        MimeMessage message = new MimeMessage(mailSession) {
            @Override
            protected void updateMessageID() throws MessagingException {
                // Tetapkan nilai `Message-ID` kustom
                setHeader("Message-ID", messageIDValue);
            }
        };
        try {
            // Tetapkan alamat dan nama email pengirim. Di sini, masukkan alamat pengirim yang dikonfigurasi di konsol (yang harus sama dengan `mail.user` di atas). Nama dapat disesuaikan, seperti uji
            InternetAddress from = new InternetAddress("xxx@xxx.com", "test");
            message.setFrom(from);
            // (Opsional) Tetapkan alamat balas-ke
            Address[] a = new Address[1];
            a[0] = new InternetAddress("xxx@xxx.com");
            message.setReplyTo(a);
            // Tetapkan lamat email penerima, seperti yyy@yyy.com
            InternetAddress to = new InternetAddress("xxx@xxx.com");
            message.setRecipient(MimeMessage.RecipientType.TO, to);
            // Jika email akan dikirim ke beberapa penerima sekaligus, ganti dua baris di atas dengan yang berikut (karena pembatasan beberapa sistem email, kami sarankan Anda mencoba mengirim email ke satu penerima dalam satu waktu; selain itu, email dapat dikirim ke hingga 50 penerima sekaligus):
            /*InternetAddress[] adds = new InternetAddress[2];
            adds[0] = new InternetAddress("xxx@xxx.com");
            adds[1] = new InternetAddress("xxx@xxx.com");
            message.setRecipients(Message.RecipientType.TO, adds);*/

            // Tetapkan subjek email
            message.setSubject("Test email");
            // Kirim lampiran Ukuran total pesan tidak boleh melebihi 10M, buat bagian pesan
            BodyPart messageBodyPart = new MimeBodyPart();
            // Badan pesan: `text/plain` (plain text) or `text/html` (HTML document)
            messageBodyPart.setText("<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
                    "<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>");
            messageBodyPart.setHeader("Content-Type", "text/plain;charset=utf-8");
            // Buat pesan multi-bagian
            Multipart multipart = new MimeMultipart();
            // Tetapkan bagian pesan teks
            multipart.addBodyPart(messageBodyPart);
            // Bagian lampiran
            messageBodyPart = new MimeBodyPart();
            // Tetapkan jalur file lampiran
            String filename = "/Users/aaa/bbb/a.txt";
            FileDataSource source = new FileDataSource(filename);
            messageBodyPart.setDataHandler(new DataHandler(source));
            // Menangani masalah teks yang kacau dari nama lampiran dalam bahasa Mandarin (jalur file terlampir)
            String filenameEncode = MimeUtility.encodeText(filename, "UTF-8", "base64");
            messageBodyPart.setFileName(filenameEncode);
            messageBodyPart.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart.setHeader("Content-Disposition", "attachment");
            messageBodyPart.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode + "\"");
            multipart.addBodyPart(messageBodyPart);

            // Bagian lampiran. Beberapa lampiran harus dibagi menjadi beberapa bagian
            BodyPart messageBodyPart1 = new MimeBodyPart();
            // Tetapkan jalur file lampiran
            String filename1 = "/Users/aaa/bbb/b.txt";
            FileDataSource source1 = new FileDataSource(filename1);
            messageBodyPart1.setDataHandler(new DataHandler(source1));
            // Menangani masalah teks yang kacau dari nama lampiran dalam bahasa Mandarin (jalur file terlampir)
            String filenameEncode1 = MimeUtility.encodeText(filename1, "UTF-8", "base64");
            messageBodyPart1.setHeader("Content-Transfer-Encoding", "base64");
            messageBodyPart1.setHeader("Content-Disposition", "attachment");
            messageBodyPart1.setHeader("Content-Type", "application/octet-stream;name=\"" + filenameEncode1 + "\"");
            multipart.addBodyPart(messageBodyPart1);

            // Kirim pesan lengkap dengan lampiran
            message.setContent(multipart);
            // Kode untuk mengirim lampiran (akhir)
            // Kirim email
            Transport.send(message);
        } catch (MessagingException | UnsupportedEncodingException e) {
            String err = e.getMessage();
            err = new String(err.getBytes(StandardCharsets.ISO_8859_1), StandardCharsets.UTF_8);
            System.out.println(err);
        }
    }
}
```
## Pertanyaan Umum
### Bagaimana cara memperbaiki kesalahan "Tidak ada protokol yang sesuai (protokol dinonaktifkan atau rangkaian sandi tidak sesuai)"?
Temukan file `jdk/jre/lib/security/java.security` dan ubahlah:
![](https://qcloudimg.tencent-cloud.cn/raw/d05f0478d608849a10f61290777a2689.png)
