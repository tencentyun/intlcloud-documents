## Visão geral das configurações

Na seção **Origin Server Configuration (Configuração do servidor de origem)**, é possível modificar as informações básicas do servidor de origem do nome de domínio, o protocolo de pull de origem, o domínio de origem e outras informações.


## Guia de configuração

### Configuração do servidor de origem principal

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Basic Configuration (Configurações básicas)** para ver a seção **Origin Server Information (Informações do servidor de origem)**.
![img](https://main.qcloudimg.com/raw/524f3c9aa2f9f2017d53409ee610bb5b.png)
**Tipo do servidor de origem**
Servidor de origem externa: selecione essa opção se você já tiver seu próprio servidor empresarial (ou seja, servidor de origem) e insira a lista de endereços IP correspondente ou um nome de domínio como o endereço do servidor de origem.
[Origem do COS](https://intl.cloud.tencent.com/product/cos): se os seus recursos forem armazenados no COS, o bucket pode ser selecionado como o servidor de origem.

**Protocolo de pull de origem**
O protocolo usado quando um nó de cache do CDN encaminha solicitações ao servidor de origem para pull de origem. É possível selecionar HTTP ou HTTPS.

Você pode configurar o protocolo de pull de origem para o nome de domínio como HTTP, HTTPS ou seguir o protocolo na configuração do servidor de origem:

- **HTTP**: o pull de origem de HTTP é usado para solicitações de acesso em HTTP e HTTPS.
- **HTTPS**: o pull de origem de HTTPS é usado para solicitações de acesso em HTTP e HTTPS.
- **Seguir o protocolo**: as solicitações HTTP usam pull de origem de HTTP, já as solicitações HTTPS usam pull de origem de HTTPS.

> !
> - Se você selecionar pull de origem de HTTPS, certifique-se de que o servidor de origem aceita o acesso HTTPS, caso contrário, o pull de origem falhará.
> - Atualmente, você ainda pode modificar esse item de configuração na página de gerenciamento de certificados. No entanto, ele será migrado no futuro.



**Endereço do servidor de origem**
<table>
<thead>
<tr>
<td style="width:80px">Origem externa</td>
<td style="padding-bottom:0px;padding-top:15px"><ul><li>Você pode inserir um nome de domínio ou vários IPs (uma entrada por linha) como o servidor de origem:
  <br><strong>Pull de origem de verificação de vários IPs: </strong>vários IPs (uma entrada por linha) podem ser configurados como o servidor de origem e são verificados durante o pull de origem. Por padrão, o CDN verifica o servidor de origem. Se um IP falhar por alguns momentos durante o pull de origem, ele será bloqueado automaticamente por um período e retomado mais tarde, durante esse período nenhuma solicitação de pull de origem será enviada para lá.<br>Se você for aceito como um usuário beta do servidor de origem IPv6 e habilitá-lo ao adicionar o nome de domínio, poderá inserir um servidor de origem IPv6.<br><strong>Pull de origem do nome de domínio: </strong>um único nome de domínio pode ser configurado como o servidor de origem, que deve ser diferente do nome de domínio de aceleração empresarial (o nome de domínio IPv6 não pode ser usado aqui).<br><li>A porta e o peso podem ser configurados: intervalo de portas: 0 a 65535; peso: 1 a 100; formato: servidor de origem:porta:peso (a porta pode ser omitida, formato: servidor de origem::peso)<br><strong>Observação: </strong>Se "HTTPS" ou "Seguir protocolo" for selecionado como o protocolo de pull de origem, a porta deve ser 443 ou deixada em branco.<br><li>Até 511 caracteres podem ser inseridos na caixa de entrada do servidor de origem.</td></ul>
</tr>
</thead>
<tbody><tr>
<td>Origem do COS</td>
<td>É possível selecionar um bucket do COS como o servidor de origem. O acesso ao bucket privado pode ser habilitado.</td>
</tr>
</tbody></table>




**Domínio de origem**
Um domínio de origem refere-se ao nome de domínio do site acessado no endereço IP do servidor de origem por um nó do CDN durante o pull de origem. O padrão é o nome de domínio de aceleração atual ou um nome de domínio curinga se um curinga estiver conectado, e o domínio de origem real é o nome de domínio de acesso. É possível modificá-lo conforme necessário, exceto no caso em que o COS é usado como servidor de origem. Para obter mais informações, consulte [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289).

> ?As diferenças entre um endereço de servidor de origem e um domínio de origem são as seguintes:
> - O endereço do servidor de origem especifica o endereço IP para o qual uma solicitação de pull de origem é enviada.
> - O domínio de origem especifica o site correspondente ao endereço IP para o qual uma solicitação de pull de origem é enviada.

### Configuração do servidor de origem de backup dinâmico

É possível adicionar um servidor de origem de backup dinâmico para seu servidor de origem principal. Todas as solicitações de pull de origem serão encaminhadas primeiro ao servidor de origem principal. Se um código de erro 4XX ou 5XX for retornado ou uma exceção como tempo limite de conexão ou incompatibilidade de protocolo ocorrer, as solicitações serão encaminhadas ao servidor de origem de backup dinâmico para efetuar pull de recursos, garantindo a alta disponibilidade de pull de origem.

O servidor de origem de backup dinâmico pode ser configurado com seu próprio endereço de servidor de origem e domínio de origem.
![img](https://main.qcloudimg.com/raw/4d2ba172412182eb87ba40149775689f.png)

>!Se um servidor de origem IPv6 for usado como o servidor de origem principal, ele não poderá ser configurado com um servidor de origem de backup dinâmico.

### Configuração específica da região

Se o seu nome de domínio de aceleração estiver configurado para a aceleração global e você quiser evitar o tráfego entre fronteiras, pode clicar em **Add Special Configuration (Adicionar configuração especial)** para configurar servidores de origem diferentes para regiões de serviço diferentes do nome de domínio de aceleração:
![img](https://main.qcloudimg.com/raw/d4a7a61ed28daa2c3eb0febf02ca931c.png)
Selecione as regiões que precisam de políticas de pull de origem diferentes e insira as informações do servidor de origem correspondente.

>!
> - Depois que a configuração específica da região for adicionada, ela não poderá ser excluída diretamente.
> - Se a configuração específica da região for exatamente igual à configuração básica, elas serão mescladas automaticamente. É possível configurá-las igualmente para excluir a configuração específica da região.

## Exemplos de configuração
[](id:exp)
### Configuração do domínio de origem

Se o servidor de origem do CDN e o nome de domínio de aceleração `www.test.com` forem configurados conforme abaixo:
![img](https://main.qcloudimg.com/raw/ec2e007bb32723f7dd12aac17524c8af.png)
A rota de acesso para o usuário será:
Quando um usuário acessa o recurso `http://www.test.com/test.txt`, que não é armazenado em cache no nó do CDN, o nó resolverá o nome de domínio `www.abc.com` para obter o endereço do servidor de origem `1.1.1.1`. Em seguida, o nó do CDN acessará o servidor `1.1.1.1`, encontrará o arquivo `test.txt` no caminho do site `www.def.com` e retornará o arquivo ao usuário.

### Configuração específica da região

Se o servidor de origem do CDN e o nome de domínio de aceleração `www.test.com` forem configurados conforme abaixo:
![img](https://main.qcloudimg.com/raw/e9104ca2b0e38c62bdffb022a933b2b9.png)
O processo de pull de origem real será:

1. Quando um usuário na China Continental acessa o arquivo `http://www.test.com/test.txt` e o nó na China Continental não tem esse recurso em cache, ele encaminhará a solicitação para o servidor `1.1.1.1` e tentará encontrar o arquivo `test.txt` no caminho do site `1.test.com`. Se o recurso existir, o nó retornará o arquivo diretamente ao usuário. Caso contrário, ele vai para a Etapa 2.
2. Como o nó do CDN na China Continental falhou em encaminhar a solicitação para o servidor de origem principal e não conseguiu encontrar o recurso, ele encaminha a solicitação para o servidor `2.2.2.2`, encontra o arquivo `test.txt` no caminho do site `1.test.com` e, em seguida, armazena em cache e o devolve ao usuário.
3. Neste momento, um usuário fora da China Continental acessa o arquivo `http://www.test.com/test.txt`. Como o nó fora da China Continental não armazenou esse recurso em cache, ele encaminha a solicitação ao servidor `3.3.3.3` e tentará encontrar o arquivo `test.txt` no caminho do site `3.test.com`. Se o recurso existir, o nó retornará o arquivo diretamente ao usuário. Caso contrário, ele vai para a etapa 4.
4. Como o nó do CDN fora da China Continental falhou em encaminhar a solicitação para o servidor de origem principal fora da China Continental e não conseguiu encontrar o recurso, ele encaminha a solicitação para o servidor `4.4.4.4`, encontra o arquivo `test.txt` no caminho do site `4.test.com` e, em seguida, armazena em cache e o devolve ao usuário fora da China Continental.
