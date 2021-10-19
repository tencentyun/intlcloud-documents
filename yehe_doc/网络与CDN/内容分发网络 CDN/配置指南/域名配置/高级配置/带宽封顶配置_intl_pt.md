
## Visão geral das configurações

O CDN do Tencent Cloud é um serviço com pagamento conforme o uso. Se você estiver preocupado com o uso excessivo de largura de banda e aumentos de taxas devido a hotlinking por usuários mal-intencionados, defina um limite de largura de banda para controlar o uso. Essa funcionalidade é aplicável apenas a usuários de faturamento por largura de banda.

A configuração do limite de largura de banda pode detectar a largura de banda gerada em um período estatístico (em uma granularidade de 5 minutos). Além disso, pode executar um pull de origem forçado de acordo com a configuração ou desativar o serviço do CDN (um erro 404 será retornado para todas as solicitações) se o limite for ultrapassado. Isso evitará gerar taxas adicionais de aceleração do CDN.

>! A configuração do limite de largura de banda leva cerca de dez minutos para entrar em vigor, durante os quais o consumo gerado é cobrado.

## Guia de configuração
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Advanced Configuration (Configurações avançadas)** para exibir a seção **Bandwidth Cap Configuration (Configuração do limite de largura de banda)**. Por padrão, ela fica desativada:
![](https://main.qcloudimg.com/raw/2dc4d64a3c1f4054471a31681c19765e.png)
### Modificação da configuração
#### 1. Modificar a configuração
Você pode ativar o botão de alternância para configurar o limite de largura de banda:
- Para nomes de domínio com o COS como servidor de origem, retornar um erro 404 é a única opção quando o limite é atingido.
- Se a largura de banda do nome de domínio detectada exceder o limite, o pull de origem ou o retorno do erro 404 para acesso precisa ser implementado em toda a rede, nó por nó; portanto, pode haver um certo atraso para que a configuração entre em vigor.

![](https://main.qcloudimg.com/raw/7520963775f790d2adaf588b9418bd7c.png)

#### 2. Desativar a configuração
Você pode desativar o botão de alternância dessa funcionalidade diretamente. Quando estiver desativado, a configuração não terá efeito no ambiente de produção. Se você ativar o botão de alternância, a configuração entrará em vigor em toda a rede após a confirmação da ação.
![](https://main.qcloudimg.com/raw/1a18d747e269347c90aa17f116601509.png)

#### 3. Adicionar a configuração específica da região
Se o seu nome de domínio de aceleração estiver configurado para a aceleração global e você quiser configurar a aceleração dentro e fora da China Continental com configurações diferentes de limite de largura de banda, você pode clicar em **Add Special Configuration (Adicionar configuração especial)**.
![](https://main.qcloudimg.com/raw/ee63c14e4bcbd38899e8d9c063499db9.png)

>!
>
>- Atualmente, os itens de configuração específicos da região não podem ser excluídos depois de adicionados, mas podem ser desativados.


## Exemplo de configuração
Se a configuração do limite de largura de banda do nome de domínio de aceleração `cloud.tencent.com` for a seguinte:
![](https://main.qcloudimg.com/raw/772256e11f3c1c9a85ae9cc57315c4f6.png)
Então, o acesso real será:
Se a largura de banda atingir 11 Gbps na China Continental e 4 Gbps fora da China Continental, um erro 404 será gerado para as solicitações de acesso de todos os usuários na China Continental. Já os usuários fora da China Continental ainda poderão desfrutar do serviço de aceleração.

