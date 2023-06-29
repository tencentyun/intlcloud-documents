## Casos de uso

Depois de conectar um nome de domínio ao CDN do Tencent Cloud, você pode fazer login no [console do CDN](https://console.cloud.tencent.com/cdn), selecionar **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda para visualizar a lista de nomes de domínio de aceleração.

É possível ajustar as colunas exibidas, ativar/desativar em lote o serviço de aceleração para nomes de domínio e alterar projetos, tags e configurações de nomes de domínio em lote.

## Guia de operações

### Ajuste das colunas exibidas

Clique no ícone ![img](https://main.qcloudimg.com/raw/c8528c5a51cbea35ecb7e0414b51267e.png) à direita da barra de pesquisa para ver todas as colunas disponíveis. Escolha as colunas que deseja exibir, cancele as que deseja ocultar e ajuste a ordem:
![img](https://main.qcloudimg.com/raw/790ae4b6c47b8b5ccd72e517701d34db.png)



### Exportação da lista de configuração

Clique no ícone ![img](https://main.qcloudimg.com/raw/16b5654ecd298d7cadc63b243413a31d.png) à direita da barra de pesquisa para exportar os detalhes da lista de nomes de domínio em um arquivo Excel. É possível selecionar até 1.000 nomes de domínio para exportar por vez.



### Alteração de projetos

É possível alterar os projetos de nomes de domínio em execução.

- Alterar o projeto de um nome de domínio: à direita do nome de domínio em questão, clique em **More (Mais)** -> **Modify Project (Modificar Projeto)**.

- Alterar em lote os projetos de vários nomes de domínio: marque os nomes de domínio em questão e clique em **More Actions (Mais ações)** -> **Edit Project (Editar projeto)** na parte superior. É possível alterar os projetos de até 50 nomes de domínio por vez.




### Edição de tags

- Alterar a tag de um nome de domínio: clique no nome de domínio em questão para entrar em sua página de configuração, abra a guia *Basic Configuration (Configurações básicas)**, clique no ícone de lápis à direita de **Tag** na seção **Basic Information (Informações básicas)**.
- Alterar em lote as tags de vários nomes de domínio: marque os nomes de domínio em questão e clique em **More Actions (Mais ações)** -> **Edit Tag (Editar tag)** na parte superior. É possível alterar as tags de até 50 nomes de domínio por vez. As alterações não entram em vigor imediatamente, atualize para exibir as novas tags.	



### Desativação do serviço de aceleração

É possível desativar o serviço de aceleração para nomes de domínio em execução normal. Depois que o serviço de aceleração for desativado para um nome de domínio, suas configurações serão desativadas nos nós de cache do CDN em toda a rede. Se as solicitações de acesso ao nome de domínio ainda forem redirecionadas aos nós do CDN, um erro 404 será retornado. Portanto, antes de desativar um nome de domínio, certifique-se de que seu registro CNAME seja resolvido para um endereço CNAME fora do CDN.

> !O consumo não será mais gerado depois que o serviço de aceleração for completamente desativado.

- Desativar o serviço de aceleração para um nome de domínio: à direita do nome de domínio em questão, clique em **More (Mais)** -> **Disable (Desativar)**.
- Desativar em lote o serviço de aceleração para vários nomes de domínio: marque os nomes de domínio ativados e clique em **More Actions (Mais ações)** -> **Disable Acceleration (Desativar aceleração)** na parte superior.



### Ativação do serviço de aceleração

É possível ativar o serviço de aceleração para nomes de domínio desativados, a fim de distribuir suas configurações para nós de cache em toda a rede novamente.

- Ativar o serviço de aceleração para um nome de domínio: à direita de um nome de domínio desativado, clique em **More (Mais)** -> **Enable (Ativar)**.
- Ativar em lote o serviço de aceleração para vários nomes de domínio: marque os nomes de domínio desativados e clique em **More Actions (Mais ações)** -> **Enable Acceleration (Ativar aceleração)** na parte superior.

> !Se um nome de domínio ativado não tiver operações ou consumo por 3 meses, ele será considerado inativo e o CDN desativará automaticamente seu serviço de aceleração.



### Exclusão de nomes de domínio de aceleração

Se os nomes de domínio estiverem com o status **Disabled (Desativado)**, você pode excluí-los. Assim que forem excluídos, suas configurações serão apagadas e não poderão ser restauradas, e seus dados estatísticos não poderão mais ser visualizados. Opere com cuidado.

- Excluir um nome de domínio: à direita do nome de domínio em questão, clique em **More (Mais)** -> **Delete (Excluir)**.
- Excluir em lote vários nomes de domínio: marque os nomes de domínio desativados e clique em **More Actions (Mais ações)** -> **Delete (Excluir)** na parte superior.



### Alteração em lote de configurações	

A funcionalidade Alterar Configurações em Lote permite que você altere um item de configuração de vários nomes de domínio ao mesmo tempo. Para obter mais informações, consulte [Alteração em lote de configurações](https://intl.cloud.tencent.com/document/product/228/39911).	




### Cópia de configurações

A funcionalidade Copiar Configuração permite duplicar as configurações de um nome de domínio de aceleração existente para um ou vários novos nomes de domínio de aceleração. Para obter mais informações, consulte [Cópia de configurações](https://intl.cloud.tencent.com/document/product/228/38936).






