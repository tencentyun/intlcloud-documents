## Visão geral da funcionalidade

Ao configurar a validade do cache do navegador, é possível personalizar as políticas de cache do navegador do cliente para reduzir a taxa de pull de origem.

> ?Quando uma solicitação chegar, se o recurso solicitado estiver armazenado em cache no navegador, ele será retornado diretamente. Caso contrário, a solicitação será encaminhada aos nós de cache do CDN. Se o recurso ainda não puder ser encontrado no nó de cache, a solicitação será encaminhada ao servidor de origem.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia **Cache Configuration (Configuração de cache)** para encontrar a seção **Browser Cache Validity Configuration (Configuração da validade do cache do navegador)**.
![](https://main.qcloudimg.com/raw/d74acc06100e385c87176d62459f12a6.png)



### Adição de regras

Clique em **Add Rule (Adicionar regra)** para adicionar regras de validade do cache do navegador para o tipo de arquivo, diretório de arquivo, caminho de arquivo e página inicial especificados.
<img src="https://main.qcloudimg.com/raw/d98a14185f9e9d41d682fb356601e9e5.jpg" style="height:220px"/>

- Seguir o servidor de origem: siga o cabeçalho `Cache-Control` do servidor de origem. Se o servidor de origem não tiver um cabeçalho CC ou seu cabeçalho CC for `no-cache/no-store/private`, o navegador não armazenará os recursos em cache.
- Cache: se o cabeçalho CC do servidor de origem não for `no-cache/no-store/private`, as regras de validade do cache do navegador serão aplicadas; caso contrário, o navegador não armazenará os recursos em cache.
- Sem cache: nenhum recurso é armazenado em cache em um navegador.


**Limitações de configuração**

- Cada nome de domínio pode ter até 20 regras. Apenas uma regra "All Files (Todos os arquivos)" e "Homepage (Página inicial)" pode ser adicionada.
- É possível ajustar a prioridade para várias regras. As regras do final da lista têm prioridade mais alta.
- Em cada regra de tipo de arquivo, diretório de arquivo e caminho de arquivo especificados, até 50 grupos de conteúdo podem ser inseridos. Use ";" para separar conteúdos diferentes, por exemplo, Tipo de Arquivo Especificado: jpg;png.
- Os caracteres chineses não são aceitos.

### Políticas padrão
Se nenhuma regra for configurada ou corresponder às solicitações, as políticas padrão serão aplicadas:
- Quando um usuário faz uma solicitação de um determinado recurso empresarial, se o cabeçalho de resposta HTTP do servidor de origem contiver o campo `Cache-Control`, o `Cache-Control` será seguido.
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, então a validade do cache de recursos no navegador será de 600 segundos.

Quando há regras de validade de cache de nó configuradas (guia de configuração: [Configuração da validade do cache do nó (Nova)](https://intl.cloud.tencent.com/document/product/228/38424)) ou correspondidas:
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, o navegador não armazenará os recursos em cache.
- Se o cabeçalho de resposta HTTP do servidor de origem contiver o campo `Cache-Control`, então o cache do navegador seguirá `Cache-Control`.
