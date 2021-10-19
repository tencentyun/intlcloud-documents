


## Visão geral das configurações

O CDN do Tencent Cloud usa o formato `Key-Value` para mapear recursos durante o armazenamento em cache, em que `Key` é a chave do cache e um identificador exclusivo do recurso armazenado em cache. Ao configurar regras de chave de cache, é possível configurar as funcionalidades Ignorar string de consulta e Não diferenciar maiúsculas de minúsculas no URL de cache para o conteúdo de tipos diferentes de arquivo, a fim de otimizar as chaves de cache.



### Ignorar string de consulta

- Quando um usuário acessa o recurso por meio de um URL, a solicitação de acesso pode conter alguns parâmetros para fins especiais. Por exemplo, os seguintes URLs são usados para representar duas imagens diferentes:
`http://cloud.tencent.com/1.jpg?version=1`
`http://cloud.tencent.com/1.jpg?version=2`
Nesse cenário, você precisa desabilitar o Ignorar string de consulta e usar um URL completo como a chave de cache para armazenar imagens em cache e distinguir entre recursos.

- Se você usar o parâmetro de assinatura de carimbo de data/hora para autenticação de acesso em um cenário de áudio/vídeo:
`http://cloud.tencent.com/1.mp4?sign=XXXXXX`
Nesse cenário, é necessário habilitar o Ignorar string de consulta e usar a parte do URL antes de "?" (ou seja, `http://cloud.tencent.com/1.mp4`) como a chave de cache. Dessa forma, o nó armazenará em cache apenas um recurso, e o cache poderá ser acessado diretamente por meio da autenticação de assinatura, mesmo se a assinatura do carimbo de data/hora continuar mudando.

### Não diferenciar maiúsculas de minúsculas no URL de cache

Se as letras maiúsculas dos caminhos de URL de recursos forem relevantes para o conteúdo de recursos em sua empresa, é possível desabilitar "Não diferenciar maiúsculas de minúsculas no URL de cache".
Se as letras maiúsculas dos caminhos de URL de recursos forem irrelevantes para o conteúdo de recursos em sua empresa, é possível habilitar "Não diferenciar maiúsculas de minúsculas no URL de cache", para melhorar a taxa de acerto.
>!A plataforma está sendo atualizada e a funcionalidade Não diferenciar maiúsculas de minúsculas no URL de cache não pode ser habilitada no momento.

## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Selecione a guia **Cache Configuration (Configuração de cache)** para encontrar a seção **Cache Key Rule Configuration (Configuração de regra de chave de cache)**.

Ao adicionar um nome de domínio de aceleração, por padrão, a funcionalidade Ignorar string de consulta fica habilitada ou desabilitada com base em diferentes tipos de negócios de aceleração.

- Se a aceleração estática for selecionada, a funcionalidade Ignorar string de consulta ficará desabilitada por padrão. Na configuração da chave de cache, a funcionalidade Ignorar string de consulta de todas as regras de arquivos será sincronizada para **Not Filter (Não filtrar)**.
- Se a aceleração de download ou de streaming de VOD for selecionada, a funcionalidade Ignorar string de consulta ficará habilitada por padrão. Na configuração da chave de cache, a funcionalidade Ignorar string de consulta de todas as regras de arquivos será sincronizada para *Filter All (Filtrar tudo)**.


![](https://main.qcloudimg.com/raw/1f53ed863618b442233dd3e1bba6229b.png)

### Adição de regras

Você pode adicionar regras de cache conforme necessário.
<img src="https://main.qcloudimg.com/raw/48becf925518b2595097eddf7b4ec6d5.png" height="250" width="438" />

#### Limitações de configuração

- Cada nome de domínio pode ser configurado com até 20 regras de chave de cache (incluindo as padrão).
- A prioridade da regra pode ser ajustada: as regras do final da lista têm prioridade mais alta (a prioridade das regras padrão não pode ser ajustada).
- Em cada regra de tipo de arquivo, pasta e arquivo de caminho completo especificados, até 100 grupos de conteúdo podem ser inseridos. Use ";" para separar conteúdos diferentes, por exemplo, "Tipo de arquivo especificado - jpg;png".
- Ignorar string de consulta – Reserva parâmetros especificados.
  - Todos os arquivos: até 6 nomes de parâmetros podem ser inseridos; cada um pode conter até 20 caracteres.
  - Tipo de arquivo/pasta/arquivo de caminho completo especificados: até 5 nomes de parâmetros podem ser inseridos; cada um pode conter até 20 caracteres.
    Separe cada nome de parâmetro com ";". Por exemplo: key1;key2;key3.

### Modificação de regras

Você pode clicar em **Modify (Modificar)** para modificar as regras de chave de cache adicionadas.

>!As regras padrão aceitam a modificação das configurações de Ignorar string de consulta e Não diferenciar maiúsculas de minúsculas no URL de cache, já o tipo e o conteúdo não podem ser modificados.

### Exclusão de regras

Você pode clicar em **Delete (Excluir)** para excluir as regras de chave de cache adicionadas (exceto as padrão).


## Exemplos de configuração

Se a configuração da regra da chave de cache do nome de domínio de aceleração `www.test.com` for a seguinte:
![](https://main.qcloudimg.com/raw/8c3f7f534c5fa849ca1594a0a244d840.png)

Então, o acesso real será:

Um cliente acessou os recursos `www.test.com/abc.jpg?version=1&colour=red` e `www.test.com/abc.JPG?version=1&colour=red`, as duas solicitações chegaram ao nó X do CDN, no qual os recursos não são armazenados em cache.

- Será efetuado o pull do servidor de origem para a imagem `abc.jpg`, e a imagem será armazenada em cache no nó X do CDN. Como a funcionalidade Ignorar string de consulta está habilitada e **Filter All (Filtrar tudo)** está selecionado, a parte do URL `www.test.com/abc.jpg` antes de "?" será usada como a chave do cache.
- O cliente acessou o recurso `www.test.com/abc.JPG?version=1&colour=red`, e como a funcionalidade Não diferenciar maiúsculas de minúsculas no URL de cache está desabilitada, o recurso em cache `www.test.com/abc.jpg` não será atingido, será efetuado o pull do servidor de origem para a imagem `abc.JPG`, a imagem será armazenada em cache no nó X do CDN e `www.test.com/abc.JPG` será usado como a chave de cache.



