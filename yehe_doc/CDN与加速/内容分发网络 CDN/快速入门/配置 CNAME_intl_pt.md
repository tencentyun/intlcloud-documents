![](https://main.qcloudimg.com/raw/705a1315248316e32c25a8093fd9f799.png)

## Preparações

### Adição de nome de domínio
Antes de configurar um registro CNAME, você precisa [adicionar um nome de domínio](https://intl.cloud.tencent.com/document/product/228/5734) primeiro. Se você já adicionou um, prossiga.


## Instruções

### Etapas de configuração

Você precisa concluir a configuração no provedor de serviços de DNS do seu nome de domínio. Este documento descreve as etapas de configuração na Tencent Cloud e na Alibaba Cloud:

- [Configurações na Tencent Cloud](#m1)
- [Configurações na Alibaba Cloud](#m2)

[](id:m1)
### Tencent Cloud

## Configuração rápida

Se o seu provedor de serviços de domínio for a Tencent Cloud, recomendamos que você use o recurso de configuração rápida de registro CNAME. Para obter mais informações, consulte [Configuração de CNAME via DNSPod](https://intl.cloud.tencent.com/document/product/228/42353).



#### Configuração manual

1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e copie o endereço CNAME.
   Antes que seu nome de domínio seja resolvido com sucesso, um ícone de aviso é exibido ao lado do registro CNAME. Copie o valor do registro CNAME.

2. Faça login no [console do DNSPod](https://console.cloud.tencent.com/cns) e clique em **Record (Registrar)**.

3. Adicione um registro CNAME e clique em **OK**.

4. Aguarde a configuração entrar em vigor.

**Descrição da configuração:**

| Configuração | Descrição                                                     |
| :------- | :----------------------------------------------------------- |
| Host | É o prefixo do nome de domínio. <br><br>**Exemplo:** para adicionar um registro para `dnspod.com`, selecione **@** para **Host**. Para adicionar um registro para `www.dnspod.com`, selecione **www** para **Host**. |
Tipo de registro | Selecione **CNAME**.                                               |
| Zona Dividida | Selecione **Padrão**. O DNSPod oferece várias opções de zonas divididas para você especificar registros para usuários específicos. Para obter mais informações, consulte [Descrição da zona dividida](https://docs.dnspod.cn/dns/5f4775898ae73e11c5b01afc/). |
| Valor | Digite o nome de domínio apontado pelo CNAME, por exemplo, `xxx.xxx.com.cdn.dnsv1.com`. Depois que o registro for gerado, um `.` será adicionado automaticamente após o nome de domínio. |
| Peso     | Valores de registro diferentes na mesma zona dividida de um registro de host podem ser configurados com pesos diferentes, de forma que a resolução seja retornada de acordo com suas proporções de peso.| Faixa de valores: 1 a 100. |
| MX       | Refere-se à prioridade. Quanto menor o valor, maior a prioridade. Recomendamos que você o deixe vazio.       |
| TTL      | Refere-se à vida útil. Quanto menor for o valor, menor será o custo de tempo para que as alterações de registro tenham efeito global. O valor padrão é 600 segundos.  |

[](id:m2)
### Alibaba Cloud

Se o seu provedor de serviços de DNS for a Alibaba Cloud, é possível adicionar um registro CNAME da seguinte forma.

1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e copie o endereço CNAME.
   Antes que seu nome de domínio seja resolvido com sucesso, um ícone de aviso é exibido ao lado do registro CNAME. Copie o valor do registro CNAME.

2. Faça login no console do DNS da Alibaba Cloud.
3. Clique no nome de domínio a ser resolvido para entrar na página de registro de resolução.
4. Clique em **Add record (Adicionar registro)**.
5. Selecione ***CNAME** como o tipo de registro. Insira o registro do host conforme necessário (como `www`), que é o prefixo do nome de domínio. Insira o registro CNAME copiado na etapa 1 como o valor do registro. Mantenha as configurações padrão da zona dividida e TTL.
<img src="https://main.qcloudimg.com/raw/6b8bb9ce4f998b8d17ca27fd10512dc6.png" width="80%">
6. Por fim, clique em **Confirm (Confirmar)**.

## Operações subsequentes

### Verificação de CNAME

O tempo que um registro CNAME leva para entrar em vigor varia de acordo com o provedor de serviços de DNS. Geralmente é dentro de meia hora. Também é possível verificar se o registro CNAME está em vigor executando `nslookup` ou `dig`. Se a resposta do registro CNAME for o CNAME configurado, isso indica que a configuração obteve êxito e a aceleração está habilitada.

- nslookup -qt=cname <acceleration domain name>
<img src="https://main.qcloudimg.com/raw/1f94ea7e3ee46fc761e8e839ce68a86d.png" width="70%">
- dig <acceleration domain name></br>
<img src="https://main.qcloudimg.com/raw/fe9b8f9a1a26d3a7df5db614762caeaf.png" width="70%">

### Instruções

Você concluiu a configuração básica do serviço CDN. Para mais configurações de CDN, consulte o documento correspondente em [Guia de configuração](https://intl.cloud.tencent.com/document/product/228/15417).

