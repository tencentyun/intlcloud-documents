Após seu nome de domínio conectar ao CDN, você receberá um nome de domínio do CNAME com o sufixo `.cdn.dnsv1.com`, que pode ser visualizado na página [Gerenciamento de domínio](https://console.cloud.tencent.com/cdn/domains) no console do CDN. Para tornar o nome de domínio do CNAME acessível, primeiro é necessário concluir a configuração do CNAME em seu provedor de serviços de nomes de domínio. Quando a configuração entrar em vigor, você pode usar o serviço de aceleração do CDN.
![img](https://main.qcloudimg.com/raw/073b948565743f7947aae8503eef995d.png)

## Instruções de configuração

Este documento fornece instruções de configuração do CNAME no Tencent Cloud e no Alibaba Cloud:

- [Configurações no Tencent Cloud](#m1)
- [Configurações no Alibaba Cloud](#m2)

[](id:m1)
### Configurações no Tencent Cloud

> !Registros de tipos diferentes possuem prioridades diferentes. Para o mesmo host, alguns tipos de registro não podem existir ao mesmo tempo. O tipo CNAME entra em conflito com todos os outros tipos de registro. É necessário excluir os registros de outros tipos para adicionar registros CNAME.


1. Faça login no [DNSpod](https://www.dnspod.com/Products/dns/list), clique no nome de domínio desejado na guia **My Domains (Meus domínios)**.
 
2. Clique em **Add Records (Adicionar registros)** e configure-o conforme as instruções abaixo:
   ![img](https://main.qcloudimg.com/raw/36f84a0d21b51bc56d79544943f0f752.png)
	
	- **Host**: insira o nome do subdomínio. Por exemplo, se você deseja adicionar a resolução para `www.dnspod.com`, selecione **www** como o registro do host. Se você deseja adicionar a resolução para `dnspod.com`, selecione **@**.
	- **Type (Tipo)**: selecione **CNAME**.
	- **Split Zone (Zona dividida)**: selecione **Default (Padrão)**. O DNSPod oferece várias opções de zonas divididas para você especificar registros para usuários específicos. Para obter mais informações, consulte [Descrição de zonas divididas](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).
	- **Value (Valor)**: insira o nome do domínio de destino (geralmente o CNAME, por exemplo, `xxx.xxx.com.cdn.dnsv1.com`). Depois que o registro for gerado, um `.` será adicionado automaticamente após o nome de domínio, o que é normal.
	- **Weight (Peso)**: valores de registro diferentes na mesma zona dividida de um registro de host podem ser configurados com pesos diferentes, de forma que a resolução seja retornada de acordo com suas proporções de peso.
		Insira um número inteiro entre 0 e 100.
	- **MX**: prioridade do registro MX. Você pode deixar em branco.
	- **TTL**: a vida útil (TTL, na sigla em inglês) determina por quanto tempo armazenar uma consulta ou conteúdo em cache. Quanto menor for o valor, menor será o custo de tempo para que as alterações de registro tenham efeito global. O valor padrão é 600 segundos.
3. Clique em **Confirm (Confirmar)** para finalizar a configuração.

   

####  Configurações adicionais
- Para habilitar o serviço de aceleração para todo o site, é possível definir a **Split Zone (Zona dividida)** de um registro de host como **Default (Padrão)**.
Por exemplo, se você deseja direcionar todos os usuários para `1.com`, é possível configurar um registro CNAME com **Default (Padrão)** como a zona dividida e `1.com` como o valor.
![img](https://main.qcloudimg.com/raw/0c146a23008acc3c0e4884aa1c4d3a3c.png)

- Também é possível ativar o serviço de aceleração para uma zona dividida especificada.
Por exemplo, se você deseja direcionar os usuários do CMCC para `1.com` e os usuários do CUCC para `2.com`, é possível configurar dois registros CNAME: um com **CMCC** como a zona dividida e `1.com` como o valor, outro com **CUCC** como a zona dividida e `2.com` como o valor.
 ![](https://main.qcloudimg.com/raw/ecf4d1ad94eaf897473647459b923209.png)

>?Para obter mais informações sobre as configurações de zonas divididas, consulte [Descrição de zonas divididas](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/).


[](id:m2)
### Configurações no Alibaba Cloud

Se o seu provedor de serviços de DNS for o Alibaba Cloud, é possível adicionar um registro CNAME da seguinte forma.

1. Faça login no console do DNS do Alibaba Cloud.
2. Clique no nome de domínio a ser resolvido para entrar na página de registro de resolução.
3. Clique em **Add record (Adicionar registro)**.
4. Para definir um registro de resolução CNAME, selecione **CNAME** como o tipo de registro. Insira o registro do host conforme necessário (por exemplo, `www`), que é o prefixo do nome de domínio. Insira o nome de domínio direcionado pelo nome de domínio atual como o valor de registro. Mantenha as configurações padrão para ISP Line (Linha de ISP) e TTL.
![img](https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png)
5. Por fim, clique em **Confirm (Confirmar)**.



## Verificação de um registro CNAME

O tempo que um registro CNAME leva para entrar em vigor varia de acordo com o provedor de serviços de DNS. Normalmente, leva 30 minutos. Também é possível verificar se o registro CNAME está em vigor executando `nslookup` ou `dig`. Se a resposta do registro CNAME for o CNAME configurado, isso indica que a configuração obteve êxito e a aceleração está habilitada.

- `nslookup -qt=cname <acceleration domain name>`
  ![img](https://main.qcloudimg.com/raw/89faaf228a2b88e23b82d0a839367c76.png)
- `dig <acceleration domain name>`
  ![img](https://main.qcloudimg.com/raw/2ba5ec76f1671c3b8ee345cef896de10.png)
