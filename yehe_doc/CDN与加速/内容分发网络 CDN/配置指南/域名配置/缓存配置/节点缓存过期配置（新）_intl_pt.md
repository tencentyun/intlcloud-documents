## Configuração

O cache de objetos é acionado por solicitações. Quando um nó CDN recebe uma solicitação e o cache do objeto solicitado não está disponível, a solicitação será encaminhada para a origem. Em seguida, o objeto é extraído, armazenado em cache no nó CDN e servido ao solicitante.

Não é possível gerenciar diretamente os recursos armazenados em cache nos nós do CDN. No entanto, você pode controlar o armazenamento em cache configurando políticas de armazenamento em cache do nó, por exemplo, para garantir que o recurso servido esteja atualizado.

>! Atualmente, um arquivo de até 32 GB pode ser armazenado em cache. Objetos com mais de 32 GB serão servidos a partir da origem.

## Instruções

### Visualização da configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, localize o nome de domínio desejado e clique em **Manage (Gerenciar)** -> **Cache Configuration (Configuração de cache)** -> **Node Cache Validity Configuration (Configuração da validade do cache do nó)**.

Quando você adiciona um nome de domínio, uma regra de validade de cache de nó é adicionada por padrão de acordo com o tipo de aceleração. Você pode alterá-lo se necessário.

- **Aceleração estática**:  arquivos dinâmicos comuns (como arquivos PHP, JSP, ASP e ASPX) não são armazenados em cache por padrão, e o cache de outros arquivos será válido por 30 dias por padrão.
 ![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- Para aceleração de download ou de streaming de vídeo sob demanda, a validade do cache padrão de todos os arquivos será de 30 dias.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adição de regras

As regras de cache do nó podem ser aplicadas à extensão de arquivo especificada (como `jpg;png`), pastas (como `/test`) e arquivos de caminho completo (como `/test/1.jpg`):
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />

- Seguir o servidor de origem: siga o cabeçalho `Cache-Control` do servidor de origem.
- Quando o cabeçalho de resposta HTTP do servidor de origem contém o campo `Cache-Control`:
  Se `Cache-Control` for `max-age`, o valor max-age será usado como a validade do cache do nó.
   Se `Cache-Control` for `no-cache/no-store/private`, o nó do CDN não armazenará o recurso em cache.
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, o nó do CDN não armazenará o recurso em cache.
  **Observação:** algumas plataformas podem ter a política padrão: quando um recurso for solicitado pela primeira vez, a solicitação será encaminhada ao servidor de origem e os nós do CDN armazenarão o recurso em cache. Se o recurso for solicitado novamente e o nó for atingido, o CDN adicionará o cabeçalho de resposta `Cache-Control: max-age=600`.
- ** Cache**: configura a validade do cache de recursos nos nós.
- ** Forçar cache**: configura se deseja ignorar o `Cache-Control: no-cache/no-store/private` do servidor de origem. O padrão é "Não".
  **Observação:** Se **Forçar cache** for configurado como **Sim**, a validade do cache do nó será definida para o valor configurado aqui.
  　　Se **Forçar cache** for configurado como **Não** e o campo `Cache-Control` do servidor de origem for `no-cache/no-store/private`, os nós do CDN não armazenarão os recursos em cache mesmo que a validade do cache esteja configurada.
- Sem cache: os nós do CDN não armazenam recursos em cache.





#### Limitações de configuração

- No máximo 100 regras de cache podem ser adicionadas para um único nome de domínio.
- Você pode reorganizar as regras para ajustar as respectivas prioridades. Regras em lugares mais baixos têm prioridades mais altas.
  **Observação:** Atualmente, a funcionalidade **No max-age (Sem max-age)** está sendo atualizada e não é compatível. Fique atento ao lançamento oficial. Se você configurou a regra, exclua-a ou modifique-a para **All Files (Todos os arquivos)**.
- Em cada regra de extensão de arquivo, pasta e arquivo de caminho completo especificados, até 100 grupos de conteúdo podem ser inseridos. Use ";" para separar conteúdos diferentes, por exemplo, "Tipo de arquivo especificado - jpg;png".

>! Se houver alguma configuração da validade do cache de nó legado (ou seja, o modo básico), ela será atualizada de forma abrangente assim que for enviada como o modo avançado e não poderá mais ser restaurada para o modo básico.



### Políticas padrão

Se nenhuma regra for configurada ou corresponder às solicitações, as políticas padrão serão aplicadas:

- Quando um usuário faz uma solicitação de um determinado recurso empresarial, se o cabeçalho de resposta HTTP do servidor de origem contiver o campo `Cache-Control`, o `Cache-Control` será seguido.
- Se o cabeçalho de resposta HTTP do servidor de origem não contiver o campo `Cache-Control`, então a validade do cache de recursos nos nós será de 600 segundos.

## Exemplos de configuração

Se as configurações de validade do cache de nó para o nome de domínio de aceleração `www.test.com` forem as seguintes:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

O cache real será:

- Mesmo que `Cache-Control` seja `no-cache/no-store/private`, a validade de `www.test.com/abc.jpg` será de 10 dias.
- `www.test.com/def.php` não será armazenado em cache para nós.
