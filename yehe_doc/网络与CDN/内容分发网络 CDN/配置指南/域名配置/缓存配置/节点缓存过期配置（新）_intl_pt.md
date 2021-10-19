
## Visão geral das configurações

O cache de recursos no CDN do Tencent Cloud é acionado por solicitações. Quando um usuário inicia uma solicitação de acesso a um recurso, se o nó do CDN que recebe a solicitação não tiver armazenado o recurso solicitado em cache, ele encaminhará a solicitação ao servidor de origem para efetuar pull do recurso. Após efetuado o pull do recurso pelo nó (com um código de status 2XX retornado), ele será armazenado em cache no nó e retornado ao usuário.

Não é possível gerenciar diretamente os recursos armazenados em cache nos nós do CDN. Se você estiver preocupado que os recursos no servidor de origem serão alterados, mas os nós do CDN ainda armazenarão em cache os recursos herdados e os retornarão aos usuários, é possível configurar as regras de cache de nós.


## Guia de configuração

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar a sua página de configuração. Mude para a guia ***Cache Configuration (Configuração de cache)** para localizar a seção **Node Cache Validity Configuration (Configuração da validade do cache do nó)**.

Ao adicionar um nome de domínio de aceleração, regras de validade de cache de nó padrão são adicionadas com base em tipos diferentes de serviço de aceleração e podem ser modificadas conforme necessário.
- Se a aceleração estática for selecionada, os arquivos dinâmicos gerais (como arquivos PHP, JSP, ASP e ASPX) não serão armazenados em cache por padrão e outros arquivos serão configurados para seguir o servidor de origem por padrão.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- Se a aceleração de download ou de streaming de VOD for selecionada, a validade do cache padrão de todos os arquivos será de 30 dias.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adição de regras

As regras de cache do nó podem ser aplicadas a determinados tipos de arquivos, pastas e arquivos de caminho completo:
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


- Seguir o servidor de origem: siga o cabeçalho `Cache-Control` do servidor de origem.
 - Quando o cabeçalho de resposta HTTP do servidor de origem contém o campo `Cache-Control`:
 Se `Cache-Control` for `max-age`, o valor max-age será usado como a validade do cache do nó.
 Se `Cache-Control` for `no-cache/no-store/private`, o nó do CDN não armazenará o recurso em cache.
 - Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, o nó do CDN não armazenará o recurso em cache.
**Observação:** Algumas plataformas podem ter a política padrão: quando um recurso for solicitado pela primeira vez, a solicitação será encaminhada ao servidor de origem e os nós do CDN armazenarão o recurso em cache. Se o recurso for solicitado novamente e o nó for atingido, o CDN adicionará o cabeçalho de resposta `Cache-Control: max-age=600`.
- Cache: configura a validade do cache de recursos nos nós.
- Forçar cache: configura se deseja ignorar o `Cache-Control: no-cache/no-store/private` do servidor de origem. O padrão é "Não".
**Observação:** Se forçar cache for configurado como "Sim", a validade do cache do nó será definida para o valor configurado aqui.
　　Se forçar cache for configurado como "Não" e o campo `Cache-Control` do servidor de origem for `no-cache/no-store/private`, os nós do CDN não armazenarão os recursos em cache mesmo que a validade do cache esteja configurada.
- Sem cache: os nós do CDN não armazenam recursos em cache.






#### Limitações de configuração

- No máximo 20 regras de cache podem ser adicionadas para um único nome de domínio.
- A prioridade da regra pode ser ajustada: as regras do final da lista têm prioridade mais alta.
**Observação:** Atualmente, a funcionalidade "No max-age (Sem max-age)" está sendo atualizada e não é compatível. Fique atento ao lançamento oficial. Se você configurou a regra, exclua-a ou modifique a regra para "All Files (Todos os arquivos)".
- Em cada regra de tipo de arquivo, pasta e arquivo de caminho completo especificados, até 100 grupos de conteúdo podem ser inseridos. Use ";" para separar conteúdos diferentes, por exemplo, "Tipo de arquivo especificado - jpg;png".


>! Se houver alguma configuração da validade do cache de nó legado (ou seja, o modo básico), ela será atualizada de forma abrangente assim que for enviada como o modo avançado e não poderá mais ser restaurada para o modo básico.



### Políticas padrão

As políticas padrão abaixo serão aplicadas se não houver nenhuma regra configurada ou acerto.
- Quando um usuário faz uma solicitação de um determinado recurso empresarial, se o cabeçalho de resposta HTTP do servidor de origem contiver o campo `Cache-Control`, o `Cache-Control` será seguido.
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, então a validade do cache de recursos nos nós será de 600 segundos.

## Exemplos de configuração

As configurações de validade do cache de nó para o nome de domínio de aceleração `www.test.com` são as seguintes:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

O cache real será:

- Mesmo que `Cache-Control` seja `no-cache/no-store/private`, a validade de `www.test.com/abc.jpg` será de 10 dias.
- `www.test.com/def.php` não será armazenado em cache para nós.



