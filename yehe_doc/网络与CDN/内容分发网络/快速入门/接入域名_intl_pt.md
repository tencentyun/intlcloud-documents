<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

Depois de ativar o CDN, faça o login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda. Clique em **Create a Distribution (Criar uma distribuição)** para adicionar um nome de domínio de aceleração. Depois que um nome de domínio for adicionado, suas configurações serão distribuídas aos nós de cache do CDN em toda a rede sem afetar diretamente seus negócios atuais. Para habilitar a aceleração, é necessário configurar um registro CNAME. Para obter instruções específicas, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).



## Criação de uma distribuição
Clique em **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Create a Distribution (Criar uma distribuição)**.
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

A página de criação de distribuição consiste em três partes:

- Configuração de domínio
- Configuração da origem
- Configuração do serviço

Com base no nome de domínio selecionado e nas configurações do servidor de origem, o CDN recomendará configurações de cache, que podem ser enviadas sem modificações.

### Parte 1: configuração de domínio
Insira o nome de domínio da sua empresa no campo de domínio e selecione o projeto, a região e o tipo de serviço:
<img src="https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png" style="height:280px"/>

**Descrição da configuração:**

| Configuração | Descrição                                                     |
| -------- | ------------------------------------------------------------ |
| Domínio     | 1. O nome de domínio pode conter até 50 caracteres.<br/>2. O nome de domínio deve ter obtido uma declaração ICP do MIIT.<br/>3. Os nomes de subdomínio são aceitos no formato `a.test.com` ou `a.b.test.com` e nomes de domínio curinga no formato `*.test.com` ou `*.a.test.com`. <br/>4. Se o nome de domínio for um domínio curinga, conectado pela primeira vez ou conectado por outro usuário, é necessário concluir a [verificação de propriedade do nome de domínio](#m1).<br/><br/><strong>Observações: </strong><br/>1. Depois que um nome de domínio curinga for conectado, seus nomes de subdomínio e nomes de domínio curinga de segundo nível não podem ser conectados em outra conta. <br/>2. Nomes de domínio nos formatos `*.test.com` e `*.a.test.com` não podem ser configurados ao mesmo tempo.</strong><br/>3. Nomes de domínio contendo caracteres chineses ou caracteres chineses de escape não são aceitos. |
| Projeto | Projeto é um conjunto de recursos compartilhados por todos os produtos do Tencent Cloud. É possível gerenciá-lo na página [Gerenciamento de projetos](https://console.cloud.tencent.com/project). |
| Região | China Continental: as solicitações de acesso de usuários globais serão programadas para os nós de cache na China Continental para aceleração. <br/>Fora da China Continental: as solicitações de acesso de usuários globais serão programadas para os nós de cache fora da China Continental para aceleração. <br/>Global: solicitações de acesso de usuários globais serão programadas para o nó ideal mais próximo para aceleração. <br/><br/><strong>Observação: </strong><br/>Os serviços de aceleração dentro e fora da China Continental são faturados separadamente. Para obter mais informações sobre as políticas de faturamento, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949). |
| Tipo de serviço | O CDN otimiza o desempenho de aceleração com base no tipo de serviço. <br/>Para obter o melhor resultado de aceleração, recomendamos escolher o tipo de serviço semelhante ao da sua empresa real. <br/><br/>Aceleração estática: adequada para cenários de aceleração de recursos em pequena escala, como comércio eletrônico, sites e imagens de jogos.<br/>Aceleração de download: adequada para cenários de download, como instalação de jogos, download de arquivos de origem de áudio/vídeo e distribuição de firmware para celulares. <br/>Aceleração de streaming de VOD: adequada para cenários como educação online e VOD. |
| Acesso IPv6<br>| O acesso IPv6 fica desabilitado por padrão. Se for habilitado, os nós do CDN podem ser acessados pelo protocolo IPv6. Depois de adicionar um nome de domínio, é possível desativá-lo e ativá-lo conforme necessário.<br/><strong><br/>Observações: </strong><br>• Algumas plataformas estão sendo atualizadas; o acesso IPv6 não é compatível no momento. Fique atento ao lançamento oficial.<br/>• O acesso IPv6 está disponível apenas na China Continental. Para nomes de domínio de aceleração global, se o acesso IPv6 for habilitado, ele terá efeito apenas na China Continental. Não é possível habilitá-lo para nomes de domínio com aceleração fora da China Continental.|
| Tag | É possível adicionar até 50 tags.<br/>São aceitas apenas as tags existentes.<br/>A chave e o valor da tag são obrigatórios quando você adiciona uma tag. É possível adicionar ou modificar as tags na [Lista de tags](https://console.cloud.tencent.com/tag/taglist). |

### Parte 2: configuração da origem

Configure as informações do servidor de origem empresarial. Se um nó do CDN não tiver cache de recursos, o nó efetuará pull do recurso do servidor de origem e o armazenará em cache.
![](https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png)

**Descrição da configuração:**

| Configuração | Descrição                                                     |
| -------- | ------------------------------------------------------------ |
| Tipo de origem | Externa: selecione essa opção se você já tiver seu próprio servidor empresarial (ou seja, servidor de origem). <br/><a href = "https://intl.cloud.tencent.com/product/cos">Origem do COS</a>: se os recursos forem armazenados no COS, o bucket pode ser selecionado diretamente como o servidor de origem. |
| Endereço de origem | Externo: <br/>1. Vários IPs podem ser configurados como o servidor de origem, que será verificado durante o pull de origem. <br/>2. É possível configurar a porta (0 a 65535) e o peso (1 a 100) no formato `origin server:port:weight`. A porta pode ser omitida e o formato torna-se `origin server::weight`. Atualmente, o protocolo HTTPS aceita apenas a porta 443. <br/>3. É possível configurar um nome de domínio como o servidor de origem, que deve ser diferente do nome de domínio de aceleração empresarial. |
| Protocolo de pull de origem | Essa opção pode ser selecionada com base nos protocolos aceitos pelo servidor de origem: <br/>HTTP: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTP. <br/>HTTPS: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). <br/>Seguir o protocolo: as solicitações de acesso HTTP usam pull de origem HTTP, já as solicitações de acesso HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). |
| Domínio de origem | Essa opção se refere ao nome de domínio acessado no servidor de origem por um nó do CDN durante o pull de origem. <br/>Se um nome de subdomínio for conectado, será igual ao nome de domínio de aceleração por padrão e poderá ser personalizado. <br/>Se um nome de domínio curinga for conectado, será o nome do subdomínio de acesso real por padrão e poderá ser personalizado. |

### Parte 3: configuração do serviço
Configure o serviço de aceleração de nó:
![](https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png)

**Descrição da configuração:**

| Configuração | Descrição                                                     |
| :------- | :----------------------------------------------------------- |
| Configuração básica | Um nó armazena recursos em cache seguindo o mapeamento `Key-Value`, em que ` Key` é o URL do recurso. Se "Ignore Query String (Ignorar string de consulta)" estiver habilitado, os parâmetros após "?" no URL serão ignorados. Caso contrário, `Key` será um URL de recurso completo. Por padrão, essa funcionalidade fica habilitada para a aceleração de download e de streaming de VOD, mas não para a aceleração estática. |
| Ativação de GETs de alcance | Isso especifica se as solicitações parciais devem ser processadas durante o pull de origem. Ela pode ser habilitada apenas se o servidor de origem for compatível com GETs de alcance. Por padrão, essa funcionalidade fica habilitada para o servidor de origem do COS e a aceleração de streaming de VOD. |
| Configuração de cache | Validade do cache do nó. Para a aceleração estática, a validade do cache de todos os arquivos segue o servidor de origem por padrão. Para a aceleração de download e de streaming de VOD, a validade do cache de todos os arquivos é de 30 dias. A validade do cache configurada é o tempo mais longo possível, a validade real do cache está relacionada aos recursos nos nós. |

## Conclusão da configuração

Clique em **Submit (Enviar)** para adicionar o nome de domínio e aguarde até que a configuração do nome de domínio seja distribuída por toda a rede. Isso levará cerca de 5 a 10 minutos.
![](https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png)

## Operações subsequentes
Quando a distribuição for concluída, o CDN vai alocar um endereço CNAME correspondente para você. Você precisa configurar o CNAME para usar o serviço do CDN. Para obter instruções detalhadas, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:m1)
## Verificação da propriedade do nome de domínio
Se o nome de domínio for um domínio curinga, conectado pela primeira vez ou conectado por outro usuário, é necessário verificar a propriedade do nome de domínio. O nome de domínio pode ser conectado ou recuperado após passar na verificação.
A verificação da propriedade do nome de domínio é obtida por meio da verificação das informações de DNS nas seguintes etapas:
1. Clique em **Verification Method (Método de verificação)** para obter as informações do registro de resolução que serão adicionadas na verificação de DNS. Não feche esta página antes da verificação ser concluída.
   ![img](https://main.qcloudimg.com/raw/c05c0d869a71dbe68092ccee632c2d1a.png)
2. Acesse o seu provedor de serviços de DNS, adicione um registro TXT e insira `_cdnauth` como seu registro de host e o valor do registro gerado aleatoriamente na página "Verification Method (Método de verificação)" como seu valor de registro.
3. Aguarde a resolução de TXT entrar em vigor e clique em **Verify (Verificar)**. Caso a verificação falhe, aguarde até que o registro de DNS entre em vigor para tentar novamente e verifique se o registro de TXT está correto.
