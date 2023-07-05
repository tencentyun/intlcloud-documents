## Introdução
As contas e as senhas do CVM podem ser usadas como credenciais para as instâncias do CVM. Este artigo descreve como usar e gerenciar as senhas ao fazer login em uma instância do CVM.

## Requisitos de senha

Uma senha deve atender a estes requisitos:
- Senha da instância do Linux: a senha deve conter de 8 a 30 caracteres. Recomendamos que você use uma senha de pelo menos 12 caracteres. A senha não pode começar com `/` e deve conter pelo menos três dos seguintes: (`a-z`, `A-Z`, `0-9` e símbolos especiais ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```).
- Senha da instância do Windows: a senha deve conter de 12 a 30 caracteres. A senha não pode começar com `/` e deve conter pelo menos três dos seguintes: (`a-z`, `A-Z`, `0-9` e símbolos especiais ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```) e não pode conter o nome de usuário.

## Instruções

### Definição de uma senha inicial
Existem duas maneiras de definir a senha inicial, dependendo de como você configurou sua instância do CVM ao adquiri-la:
 - Se você usou a opção [**Quick Configuration (Configuração rápida)**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR), a senha inicial é enviada para você por e-mail e mensagem para o [Centro de mensagens](https://console.cloud.tencent.com/message) do console.
 - Se você usou a opção [**Custom Configuration (Configuração personalizada)**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR&bandwidth=1), a senha inicial é definida das seguintes maneiras, dependendo de como você escolhe fazer o login:
<table>
	<tr><th>Método de login</th><th>Descrição</th></tr>
	<tr><td>Geração automática de senha</td><td>A senha inicial é enviada a você por e-mail e pelo <a href="https://console.cloud.tencent.com/message">Centro de mensagens</a> do console.</td></tr>
	<tr><td>Associar chaves agora</td><td><b>Desativado por padrão</b>. Você faz o login usando o nome de usuário e a senha, mas a senha inicial é enviada a você por e-mail e pelo <a href="https://console.cloud.tencent.com/message">Centro de mensagens</a> do console.</td></tr>
	<tr><td>Definir uma senha</td><td>Você define a senha inicial.</td></tr>
</table>


### Visualização da senha

A senha de login é enviada a você por e-mail e pelo [Centro de mensagens](https://console.cloud.tencent.com/message) do console. Veja como verificar as mensagens no centro de mensagens.
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Clique em <img src="https://main.qcloudimg.com/raw/f5d915ab4297418f3eae30fd28f41122.png" style="margin: 0;"></img> no canto superior direito e selecione a mensagem do produto correspondente, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/e3c624a805d2f5776807df44bd373b59.png)
Visualize a senha na página de mensagens.
![](https://main.qcloudimg.com/raw/73bef8b11ded3d0cee5441d3d3218e25.png)

### Redefinição de senha

Para obter instruções sobre como redefinir a senha, consulte [Redefinição da senha de uma instância](http://intl.cloud.tencent.com/document/product/213/16566).
