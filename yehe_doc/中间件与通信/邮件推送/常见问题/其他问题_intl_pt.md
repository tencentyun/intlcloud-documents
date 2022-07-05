[](id:que1) 
### No SES, é permitido o envio de e-mails para endereços de e-mail fora da China Continental?
Sim. O SES da Tencent Cloud está disponível em mais de 200 países/regiões, ajudando você a entregar e-mails de forma instantânea para endereços de e-mail em todo o mundo. Ele possui uma capacidade de entrega de 97% (exceto para endereços de e-mail inválidos e e-mails corporativos restritos) e aceita os principais provedores de serviços de e-mail, como Gmail, Yahoo, Hotmail, 163.com e QQmail. Em geral, o SES possui alta estabilidade de serviço e capacidade de entrega de e-mail.


[](id:que2) 
### A documentação da API diz que `Region` aceita apenas Hong Kong (China). Posso enviar e-mails para outras regiões?
**Sim.** `Region` indica apenas a localização do servidor e não afeta as regiões para onde os e-mails são enviados.

[](id:que3) 
### No SES, é permitido o envio de e-mails para vários destinatários ao mesmo tempo como cópia oculta?
Não.

[](id:que4) 
### Existe um limite de versão do SES?
As versões gerais podem atender às necessidades dos usuários. No entanto, se a versão do seu ambiente estiver muito desatualizada, você precisará atualizar o SDK conforme as instruções.

[](id:que5) 
### Como posso consultar os registros de envio de e-mail?
Você pode consultar registros de envio de e-mail por meio de chamadas de API. Para obter mais informações, consulte [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502).
 
 [](id:que6) 
### Quais métodos de envio são aceitos pelo SES?
O SES aceita três métodos de envio, são eles: envio pelo console, por API e por SMTP.


[](id:que7) 
### Por que meu e-mail está na caixa de entrada, mas a taxa de abertura é 0?
- Para e-mails em HTML, a Tencent Cloud consegue capturar os eventos de abertura e calcular as taxas de abertura.
- Para e-mails de texto sem formatação, a Tencent Cloud não consegue calcular a taxa de abertura.
