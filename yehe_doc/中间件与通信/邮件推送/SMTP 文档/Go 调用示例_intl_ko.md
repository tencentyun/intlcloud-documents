다음은 SMTP를 사용하여 Go 언어(v1.16)로 이메일을 보내는 예시 코드입니다.
```
package main

import (
	"crypto/tls"
	"fmt"
	"log"
	"net"
	"net/smtp"
)

// Test465  for port 465
func Test465() error {
	host := "smtp.qcloudmail.com"
	port := 465
    //콘솔에서 생성된 발신자 주소
	email := "abc@cd.com" 
    //콘솔에 설정된 SMTP 비밀번호
	password := "****"
	toEmail := "test@test123.com"
	header := make(map[string]string)
	header["From"] = "test " + "<" + email + ">"
	header["To"] = toEmail
	header["Subject"] = "test subject"
	//html 이메일
	header["Content-Type"] = "text/html; charset=UTF-8"
	body := "<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
		"<h1>내 첫 번째 제목</h1>\n    <p>내 첫 번째 단락.</p>\n</body>\n</html>"
	//일반 텍스트 이메일
	//header["Content-Type"] = "text/plain; charset=UTF-8"
	//body := "test body"
	message := ""
	for k, v := range header {
		message += fmt.Sprintf("%s: %s\r\n", k, v)
	}
	message += "\r\n" + body
	auth := smtp.PlainAuth(
		"",
		email,
		password,
		host,
	)
	err := SendMailWithTLS(
		fmt.Sprintf("%s:%d", host, port),
		auth,
		email,
		[]string{toEmail},
		[]byte(message),
	)
	if err != nil {
		fmt.Println("Send email error:", err)
	} else {
		fmt.Println("Send mail success!")
	}
	return err
}

// Dial return a smtp client
func Dial(addr string) (*smtp.Client, error) {
	conn, err := tls.Dial("tcp", addr, nil)
	if err != nil {
		log.Println("tls.Dial Error:", err)
		return nil, err
	}

	host, _, _ := net.SplitHostPort(addr)
	return smtp.NewClient(conn, host)
}

// SendMailWithTLS send email with tls
func SendMailWithTLS(addr string, auth smtp.Auth, from string,
	to []string, msg []byte) (err error) {
	//create smtp client
	c, err := Dial(addr)
	if err != nil {
		log.Println("Create smtp client error:", err)
		return err
	}
	defer c.Close()
	if auth != nil {
		if ok, _ := c.Extension("AUTH"); ok {
			if err = c.Auth(auth); err != nil {
				log.Println("Error during AUTH", err)
				return err
			}
		}
	}
	if err = c.Mail(from); err != nil {
		return err
	}
	for _, addr := range to {
		if err = c.Rcpt(addr); err != nil {
			return err
		}
	}
	w, err := c.Data()
	if err != nil {
		return err
	}
	_, err = w.Write(msg)
	if err != nil {
		return err
	}
	err = w.Close()
	if err != nil {
		return err
	}
	return c.Quit()
}

func main() {
	Test465()
}
```
