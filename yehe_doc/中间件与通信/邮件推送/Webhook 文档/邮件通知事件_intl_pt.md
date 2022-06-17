A Tencent Cloud notificará o endereço de retorno sobre entrega bem-sucedida, falha na entrega, devolução de e-mail, abertura de e-mail, clique no link, cancelamento de assinatura e outros eventos. O formato do protocolo de push de eventos é o seguinte:
## Solicitação de exemplo
```json
{
  "event": "delivered",
  "email": "example@example.com",
  "bulkId": "qcloud-ses-4F001945B2D9BXXXXXX",
  "timestamp": 1587953211,
  "reason": "the reason when email failed to delivered",
  "bounceType": ""
}
```

Campo | Tipo | Descrição
--|--|--
event | string | Tipo de evento. Para obter detalhes, consulte [Tipos de eventos](#Event_Type).
email | string | Endereço de e-mail do destinatário
link | string | URL, no e-mail, em que o destinatário clica. Este campo só terá efeito quando o valor de `event` for `click`.
bulkId | string | `MessageId` retornado pela API `SendEmail`
timestamp | int | Carimbo de data e hora quando o evento é gerado
reason | string | Motivo pelo qual o e-mail não foi entregue
bounceType | string | Tipo de rejeição quando o e-mail é rejeitado pelo provedor de serviços de e-mail (ESP) do destinatário. Valores válidos: soft, hard. Este campo só terá efeito quando o valor de `event` for `bounce`.

## Tipos de eventos[](id:Event_Type)
Valor | Descrição
--|--
processed | Em entrega. Esse é um estado intermediário e não pode ser retornado.
deferred | A entrega do e-mail foi atrasada pelo ESP do destinatário e está sendo repetida.
delivered | A entrega foi bem-sucedida. O ESP do destinatário recebe o e-mail.
dropped | O e-mail não pode ser entregue e é descartado por alguns motivos.
open | O destinatário abre o e-mail.
click | O destinatário clica no URL no e-mail.
bounce | O ESP do destinatário rejeita o e-mail (normalmente porque o endereço de e-mail está incorreto).
spamreport | O destinatário denuncia o e-mail.
unsubscribe | O destinatário clica no botão de cancelamento de assinatura. O URL de cancelamento de assinatura deve conter a palavra-chave “unsubscribe (cancelar assinatura)”.
