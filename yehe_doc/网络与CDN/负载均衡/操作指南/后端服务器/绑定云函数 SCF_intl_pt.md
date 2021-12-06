É possível implementar serviços da web de back-end escrevendo funções do SCF e vinculando-as a instâncias do CLB para fornecer serviços.
>? Atualmente, a vinculação de instâncias do CLB com funções do SCF está em teste beta. Se desejar usá-la, entre em contato com seu representante de vendas.
>

## Informações gerais
O [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583) do Tencent Cloud é um ambiente de execução sem servidor que permite criar e executar aplicativos sem ter que adquirir e gerenciar servidores. Após a criação de uma função, você pode criar um gatilho do CLB para vincular a função e o evento. O gatilho do CLB passará o conteúdo da solicitação como parâmetros para a função e retornará o resultado da função ao solicitante como resposta.

## Casos de uso
<dx-accordion>
::: \sHTTP/HTTPS\sgeneral\saccess
Aplicável a aplicativos de comércio eletrônico, mídias sociais e outros serviços, e aplicações da web para blogs pessoais, páginas de eventos e muito mais. O fluxo de trabalho é conforme abaixo: 
1. As solicitações HTTP/HTTPS iniciadas por aplicativos, navegadores, páginas H5 ou miniprogramas acessam a função do SCF por meio da instância do CLB.
2. Depois que a instância do CLB conclui a desinstalação do certificado, o SCF só precisa fornecer serviços HTTP.
3. A solicitação é então transferida para a função do SCF para processamento posterior, como gravação no banco de dados em nuvem e chamada de outras APIs.
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: Switching\sbetween\sCVM\sand\sSCF
Aplicável à migração de serviços HTTP/HTTPS do CVM para o SCF, especialmente em caso de failover. O fluxo de trabalho é conforme abaixo:
1. O aplicativo, navegador, H5 ou miniprogramas do Wechat inicia uma solicitação HTTP/HTTPS.
2. A solicitação é então resolvida para VIPs de duas instâncias do CLB pelo DNS.
3. Uma instância do CLB encaminha a solicitação ao CVM e a outra ao SCF.
4. A mudança do CVM para o SCF no back-end é concluída sem afetar o cliente.
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\sbusiness\sdiversion
Aplicável ao uso do SCF para lidar com serviços altamente elásticos e ao uso do CVM para lidar com negócios diários em cenários como vendas rápidas e compra instantânea.
1. Por meio da resolução de DNS, o nome de domínio A é resolvido para o VIP de uma instância do CLB e o nome de domínio B é resolvido para o VIP da outra instância do CLB.
2. Uma instância do CLB encaminha a solicitação ao CVM e a outra ao SCF.
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## Restrições
- A vinculação com o SCF está disponível apenas em Guangzhou, Xangai, Pequim, Chengdu, Hong Kong (China), Singapura, Mumbai, Tóquio e Vale do Silício.
- As funções do SCF só podem ser vinculadas a instâncias do CLB de contas de faturamento por IP, mas não de contas de faturamento por CVM. Se você estiver usando uma conta de faturamento por CVM, recomendamos atualizá-la para uma conta de faturamento por IP. Para obter mais informações, consulte [Verificação do tipo de conta](https://intl.cloud.tencent.com/document/product/684/15246). 
- As funções do SCF não podem ser associadas a instâncias clássicas do CLB.
- As funções do SCF não podem ser associadas a instâncias do CLB da rede clássica.
- As funções do SCF só podem ser vinculadas entre VPCs, mas não entre regiões.
- Atualmente, as funções do SCF só podem ser associadas a instâncias do CLB IPv4 e IPv6 NAT64, mas não a instâncias do CLB IPv6.
- As funções do SCF só podem ser associadas a listeners HTTP e HTTPS da camada 7, mas não a listeners QUIC da camada 7 ou listeners (TCP, UDP e TCP SSL) da camada 4.


## Pré-requisitos
1. Você criou uma [instância do CLB](https://intl.cloud.tencent.com/document/product/214/6149).
2. Você configurou um listener [HTTP](https://intl.cloud.tencent.com/document/product/214/32515) ou [HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Instruções
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### Etapa 1. Crie uma função
1. Faça login no [Console do SCF](https://console.cloud.tencent.com/scf) e clique em **Function Service (Serviço de funções)** na barra lateral esquerda.
2. Na página **Function Service (Serviço de funções)**, clique em **Create (Criar)**.
3. Na página **Create (Criar)**, selecione **Custom (Personalizado)** para o modo de criação e insira um nome de função. Em seguida, selecione a mesma região que você selecionou para sua instância do CLB e **Python3.6** para o ambiente de tempo de execução, insira o seguinte código na caixa de entrada (Hello CLB é usado para ilustração) e clique em **Complete (Concluir)**.
>!Ao vincular sua instância do CLB à função do SCF, o conteúdo precisa ser retornado no formato de integração de resposta específico. Para obter mais informações, consulte [Gatilho do CLB](https://intl.cloud.tencent.com/document/product/583/39849).
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

    return {
        "isBase64Encoded": False,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### Etapa 2. Implante a função
1. Na página da lista "Functions (Funções)", clique no nome da função criada.
2. Na página **Function Management (Gerenciamento de funções)**, selecione a guia **Function Codes (Códigos de função)** e clique em **Deploy (Implantar)** na parte inferior.

### Etapa 3. Vincule a função
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb) e clique em **Instance Management (Gerenciamento de instâncias)** na barra lateral esquerda.
2. Na página **Instance Management (Gerenciamento de instâncias)**, clique em **Configure Listener (Configurar listener)** à direita de uma instância.
3. Na seção **HTTP/HTTPS Listener (Listener HTTP/HTTPS)**, selecione o listener a ser vinculado a uma função do SCF. Clique no ícone **+** à esquerda do listener e no nome de domínio abaixo dele, selecione o caminho do URL exibido e clique em **Bind (Vincular)**.
4. Na janela pop-up, selecione SCF como o tipo de destino, defina os itens de configuração e clique em **Confirm (Confirmar)**.
5. Na guia **Listener Management (Gerenciamento de listener)**, você deve ver a função vinculada à instância do CLB na seção **Forwarding Rules (Regras de encaminhamento)**, indicando que o gatilho do CLB foi criado.
>? Você também pode criar um gatilho do CLB no console do SCF para vincular a instância do CLB a uma função do SCF. Para obter mais informações, consulte [Criação de gatilhos](https://intl.cloud.tencent.com/document/product/583/31441).

## Validação do resultado
1. Faça login no [Console do SCF](https://console.cloud.tencent.com/scf) e clique em **Function Service (Serviço de funções)** na barra lateral esquerda.
2. Na página **Function Service (Serviço de funções)**, clique na função recém-criada.
3. Clique em **Trigger Management (Gerenciamento de gatilhos)** à esquerda.
4. Na página **Trigger Management (Gerenciamento de gatilhos)**, clique em **Access Path (Caminho de acesso)**.
5. Abra o caminho de acesso em um navegador. Se "Hello CLB" for exibido, a função foi implantada com sucesso.


## Referência
[Criação de funções usando o console](https://intl.cloud.tencent.com/document/product/583/32742)
