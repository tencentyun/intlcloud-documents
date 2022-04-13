A configuração da validade do cache do nó é atualizada com um modo avançado, que permite configurações mais refinadas. Para obter mais informações, consulte [Configuração da regra de cache do nó](https://intl.cloud.tencent.com/document/product/228/38424) 

## Configuração
O cache de recursos no CDN da Tencent Cloud é acionado por solicitações. Se o nó do CDN que recebe a solicitação do usuário não tiver armazenado o recurso solicitado em cache, ele encaminhará a solicitação ao servidor de origem para efetuar pull do recurso. Após efetuado o pull do recurso pelo nó (com um código de status 2XX retornado), ele será armazenado em cache no nó e retornado ao usuário.

Não é possível gerenciar diretamente os recursos armazenados em cache nos nós do CDN. Se você estiver preocupado que os recursos no servidor de origem sejam alterados, mas os nós do CDN ainda armazenem em cache os recursos herdados e os retornem aos usuários, é possível configurar as regras de cache de nós.

Cada recurso armazenado em cache em um nó do CDN tem validade. Se o recurso armazenado em cache solicitado expirou, ele será considerado inválido mesmo se o recurso ainda estiver armazenado em cache no nó. O nó efetuará pull do recurso do servidor de origem novamente. A regra de cache de nós permite configurar o período de validade do cache para recursos em um tipo, diretório e caminho específicos. É possível configurar esses itens com base em seus cenários de negócios reais.

>! Atualmente, um arquivo de até 32 GB pode ser armazenado em cache, caso contrário, os recursos serão extraídos do servidor de origem.

## Instruções
### Visualização da configuração
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Mude para a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Node Cache Validity Configuration (Configuração da validade do cache do nó)**.
![](https://main.qcloudimg.com/raw/834d620b98c9d7d387547e59a7e6a1f4.png)

### Adição de regras

Atualmente, o CDN permite os quatro tipos seguintes de configuração de regras de validade do cache do nó:
+ Arquivo: o período de validade do cache pode ser configurado pela extensão de arquivo inserida. Extensões diferentes de arquivos devem ser separadas por `;`, ou seja, `jpg;css`.
+ Pasta: o período de validade do cache pode ser configurado pelo caminho do diretório inserido no formato `/test` e não precisa terminar com `/`. Diretórios diferentes devem ser separados por `;`.
+ Arquivo de caminho completo: o período de validade do cache pode ser configurado pelo caminho de arquivo completo inserido no formato de `/index.html`. O caminho de arquivo completo e o tipo de arquivo podem ser combinados para correspondência, como `/test/*.jpg`.
+ Página inicial: o período de validade do cache pode ser configurado pelo diretório raiz.

<img src="https://main.qcloudimg.com/raw/1a72478ce0bc4fc1ef6a22bcb8064a6b.png" style="width:400px"/>

**Limitações de configuração:**
- No máximo 100 regras de cache podem ser adicionadas para um único nome de domínio.
- É possível ajustar a prioridade para várias regras. As regras do final da lista têm prioridade mais alta.
- Em cada regra de tipo de arquivo, pasta e arquivo de caminho completo especificados, até 100 grupos de conteúdo podem ser inseridos. Use ";" para separar conteúdos diferentes, por exemplo, "Tipo de arquivo especificado - jpg;png".
- A validade do cache pode ser definida para até 365 dias.

>! Se o **Advanced Mode (Modo avançado)** for selecionado para uma regra, ela será atualizada de forma abrangente como o modo avançado assim que for enviada e não poderá mais ser restaurada para o modo básico. Para obter mais informações, consulte [Configuração da regra de cache do nó](https://intl.cloud.tencent.com/document/product/228/38424)


#### Configuração avançada de validade do cache
Depois de habilitada, o CDN vai comparar a validade do cache da regra de cache correspondente com o valor "max-age" do servidor de origem e, em seguida, adotará o valor menor como a validade do cache.

- Se o `Max-Age` configurado para `/index.html` do servidor de origem for 200 segundos e a validade do cache configurada para o CDN for 600 segundos, a validade real do cache do arquivo será de 200 segundos.
- Se o `Max-Age` configurado para `/index.html` do servidor de origem for 800 segundos e a validade do cache configurada para o CDN for 600 segundos, a validade real do cache do arquivo será 600 segundos.

>! Depois de habilitada, se o servidor de origem não retornar o campo `Last-Modified`, o CDN o adicionará por padrão e mudará seu valor uma vez a cada 10 minutos.

#### Seguir o servidor de origem
Depois de habilitada, se uma solicitação não corresponder a nenhuma regra de cache, o servidor de origem será seguido.

>! As funcionalidades de seguir o servidor de origem e de configuração avançada de validade do cache não podem ser habilitadas ao mesmo tempo.


### Políticas padrão
Se nenhuma funcionalidade estiver habilitada, nenhuma regra for configurada ou corresponder às solicitações, as políticas padrão serão aplicadas:
- Quando um usuário faz solicitação de um recurso de determinado negócio, se o cabeçalho de resposta HTTP do servidor de origem contiver o campo `Cache-Control`, o `Cache-Control` será seguido.
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, então a validade do cache de recursos nos nós será de 600 segundos.


## Exemplos de configuração
As configurações de validade do cache de nó para o nome de domínio de aceleração `cloud.tencent.com` são as seguintes:
![](https://main.qcloudimg.com/raw/a585a6b560cb0e555b71e08bea179353.png)
A validade real do cache será a seguinte:

1. 400 segundos para o arquivo `/test/def.jpg`.
2. 5 minutos para o arquivo `/test/1.png`.
3. 30 dias para os demais arquivos.
