[](id:que1) 
### Como devo configurar o DNS?
- Se estiver usando o serviço de DNS da Tencent Cloud, faça login no [console da Tencent Cloud](https://console.cloud.tencent.com/cns) para configurar.
- Se estiver usando um serviço de DNS fornecido por outro provedor de serviços de domínio, poderá transferir seu domínio para a Tencent Cloud para resolução de DNS.
- Em outros casos, configure-o em seu provedor de serviços de domínio.


[](id:que2) 
### Por que a validação falharia depois de configurar o DNS conforme necessário?
 Normalmente, a sincronização do DNS leva 10 minutos. No entanto, pode haver um atraso dependendo do seu TTL. Use uma ferramenta para verificar se o DNS configurado está correto. Se não houver problema, aguarde.

[](id:que3) 
### Preciso obter o registro de ICP do meu domínio para usar o SES?
- Não é necessário se usar o domínio apenas para o envio de e-mails.
- Se o registro A do seu domínio apontar para um servidor na China Continental, você deverá concluir o registro de ICP para o domínio.

[](id:que4) 
### Posso usar um domínio de e-mail corporativo como o domínio de e-mail do SES?
Para evitar conflitos entre os registros SPF e MX, não use seu domínio de e-mail corporativo como o domínio de e-mail do SES.
Se for necessário usá-los juntos, precisará mesclar o registro SPF. Você também pode criar e usar um domínio de segundo nível no domínio do remetente existente.

[](id:que5) 
### Os subdomínios sob o mesmo domínio principal podem ser usados no SES?
Sim.

[](id:que6) 
### Há algum efeito se subdomínios diferentes usarem serviços de e-mail diferentes?
Não.
