## Cenário de configuração
Quando o CDN do Tencent Cloud encaminha uma solicitação para o servidor de origem, o período limite padrão para a conexão TCP é de 5 segundos e o período limite padrão para o carregamento de dados durante o pull de origem é de 10 segundos. Se a duração do pull de origem exceder os limites de tempo mencionados acima, muitas vezes ocorrerão falhas.

É possível ajustar os períodos limites para a conexão TCP de pull de origem e o carregamento de dados conforme as condições de processamento de dados do servidor de origem e do ambiente de rede, de modo a garantir um pull de origem normal.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique no nome de domínio para acessar sua página de configuração. Você encontrará a configuração de tempo limite de pull de origem na guia **Origin Configuration (Configuração de origem)**. Por padrão:
- O tempo limite da conexão TCP é de 5 segundos.
- O período limite de carregamento de pull de origem é de 10 segundos.

![](https://main.qcloudimg.com/raw/061fef4060d6aae5d16b3522b23fbbea.png)

### Modificação da configuração
Você pode clicar em **Edit (Editar)** à direita para modificar o período limite correspondente, conforme necessário:
- O período limite da conexão TCP pode ser definido para 5 a 60 segundos.
![](https://main.qcloudimg.com/raw/f70013c886612ef4dc33c353d8612336.png)
- O período limite de carregamento de pull de origem pode ser definido para 5 a 60 segundos.
![](https://main.qcloudimg.com/raw/e9c2cf6344275d477272ab2ba8c7e3b0.png)

>Se o seu nome de domínio de aceleração estiver configurado para a aceleração global, o período limite de pull de origem configurado terá efeito global. Essa configuração não distingue entre solicitações da China Continental e de fora da China Continental.

