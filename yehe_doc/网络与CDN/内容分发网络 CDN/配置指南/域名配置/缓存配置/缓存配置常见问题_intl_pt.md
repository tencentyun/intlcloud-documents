### O que é a configuração da validade do cache?
A configuração da validade do cache refere-se a um conjunto de políticas de expiração que os nós de cache do CDN devem seguir ao armazenar em cache o conteúdo da sua empresa.
Todos os recursos armazenados em cache nos nós do CDN têm um tempo de expiração. Para os recursos não expirados, quando uma solicitação chegar ao nó, ele retornará diretamente o recurso solicitado ao usuário, de modo a agilizar a aquisição do recurso. Para os recursos expirados, o nó encaminhará a solicitação do usuário ao servidor de origem para readquirir o recurso e, em seguida, armazenará em cache no nó e retornará ao usuário ao mesmo tempo. Um período de validade de cache razoável pode melhorar efetivamente a taxa de acertos de recursos e diminuir a taxa de pull de origem, reduzindo o uso de largura de banda.

### O que é a configuração avançada da validade do cache?
1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda para acessar a página de gerenciamento.
2. Clique em **Manage (Gerenciar)** à direita do nome de domínio em questão.
![](https://main.qcloudimg.com/raw/53c1171f8b1fdec4ddd2f87f6c47fe12.png)
3. Abra a guia **Cache Configuration (Configuração de cache)**, encontre a seção **Node Cache Validity Configuration (Configuração da validade do cache do nó)** e ative a opção **Advanced Cache Validity Configuration (Configuração avançada da validade do cache)**.
![](https://main.qcloudimg.com/raw/b1288410345c3dd92907002ad5929d38.png)
4. Os seguintes resultados são alcançados.
Quando um usuário solicita um determinado recurso do servidor de origem e o cabeçalho HTTP de resposta inclui o campo `Cache-Control` com um valor de `max-age=xxxx`, o período de validade do cache para o recurso no nó será o menor entre o período de validade e o valor `max-age` definidos:
 - Por exemplo, se o `max-age` definido para `/index.html` do servidor de origem for 200 segundos e o período de validade do cache definido para o CDN for 600 segundos, o período real de validade do cache para o arquivo será 200 segundos.
 - Se o `max-age` definido para `/index.html` do servidor de origem for 800 segundos e o período de validade do cache definido para o CDN for 600 segundos, o período real de validade do cache para o arquivo será 600 segundos.

>! Se o campo `Cache-Control` não existir no cabeçalho de resposta do seu servidor de origem, o CDN adicionará o cabeçalho `Cache-Control: max-age=600` por padrão.

### Como posso controlar a validade do cache de arquivos em um navegador?
É possível configurar a validade do cache do navegador no console do CDN. Para obter mais informações, consulte [Configuração da validade do cache do navegador](https://intl.cloud.tencent.com/document/product/228/38932).

### Como ajusto a prioridade da configuração do cache?
Consulte as instruções em [Configuração da validade do cache do nó (herdada)](https://intl.cloud.tencent.com/document/product/228/35317).

### Eu uso meu próprio servidor como o servidor de origem do CDN. Posso configurá-lo para não armazenar em cache um tipo específico de arquivos? Posso definir o período de validade do cache para "0" para desabilitar o armazenamento em cache?
É possível configurar períodos diferentes de validade do cache para tipos de diretórios e arquivos diferentes. Se o período de validade do cache for configurado como 0, o nó do CDN não armazenará o recurso em cache. Assim, o nó do CDN precisará efetuar pull dos recursos relacionados do servidor de origem toda vez que os usuários enviarem solicitações de acesso ao nó. Para obter mais informações sobre as configurações de cache, consulte [Configuração da validade do cache do nó (herdada)](https://intl.cloud.tencent.com/document/product/228/35317).

### Quais configurações de validade de cache são aceitas pelo Tencent Cloud?
O CDN do Tencent Cloud aceita a configurações de validade de cache em várias dimensões, ajuste de prioridade personalizado e políticas de herança de cache (configuração avançada da validade do cache). Um período de validade de cache razoável pode melhorar efetivamente a taxa de acertos de recursos e diminuir a taxa de pull de origem, reduzindo o uso de largura de banda.

### Qual é a configuração de cache padrão do CDN?
A configuração padrão é a seguinte quando um nome de domínio estiver conectado:
- Conexão de nome de domínio com servidor de origem externo: por padrão, o período de validade do cache para todos os arquivos é de 30 dias, exceto para os arquivos dinâmicos (como .php, .jsp, .asp, .aspx). O período de validade do cache para esses arquivos dinâmicos é 0 por padrão, o que significa que todas as solicitações desses arquivos serão encaminhadas diretamente para o servidor de origem.
- Conexão do nome de domínio com o COS como servidor de origem: por padrão, o período de validade do cache para todos os arquivos é de 30 dias.
- A configuração avançada de validade do cache fica desabilitada por padrão.

### O que são as políticas de herança de cache?
Quando um usuário faz uma solicitação de um determinado recurso empresarial, o cabeçalho HTTP de resposta do servidor de origem inclui o campo `Cache-Control`. A política padrão é a seguinte:
- Se o campo `Cache-Control` for `max-age`, o período de validade do cache para este recurso será o período definido para o recurso e não herdará o valor especificado por `max-age`.
- Se o campo `Cache-Control` for `no-cache` ou `no-store`, o nó do CDN não armazenará o recurso em cache.

### O que são as regras de correspondência de cache?
Quando várias políticas de cache são definidas, as prioridades das entradas são determinadas de baixo para cima, com a entrada no final da lista tendo a prioridade mais alta e a do topo tendo a prioridade mais baixa. Por exemplo, suponha que as seguintes políticas de cache sejam definidas para um nome de domínio:
```
Todos os arquivos (30 dias)
.php .jsp .aspx 0 segundo
.jpg .png .gif 300 segundos
/test/*.jpg 400 segundos
/test/abc.jpg 200 segundos
```

Se o nome do domínio for `www.test.com` e o recurso for `www.test.com/test/abc.jpg`, a regra correspondente será a seguinte:
1. Corresponde com a primeira entrada. É atingido, então o período de validade do cache é de 30 dias.
2. Corresponde com a segunda entrada. Não é atingido.
3. Corresponde com a terceira entrada. É atingido, então o período de validade do cache é de 300 segundos.
4. Corresponde com a quarta entrada. É atingido, então o período de validade do cache é de 400 segundos.
5. Corresponde com a quinta entrada. É atingido, então o período de validade do cache é de 200 segundos.

O período final de validade do cache está sujeito ao último resultado correspondente e, portanto, será de 200 segundos.
