![](https://qcloudimg.tencent-cloud.cn/raw/0ebdc0f0a97859cd5f41d425838a54ce.png)

## Preparações

### Ativação do CDN

Antes de configurar o CDN, você precisa [ativá-lo](https://intl.cloud.tencent.com/document/product/228/32978) primeiro. Se você já o ativou, siga em frente.

### Conceitos confusos


| Item de configuração        | Descrição                                                     | Posição de uso          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| Nome de domínio de aceleração          | Nome de domínio a ser conectado ao CDN, que é o nome de domínio real acessado pelos usuários finais            | Create a Domain Name (Criar um nome de domínio) > Domain Configuration (Configuração de domínio) |
| Endereço de origem/nome de domínio de origem | Endereço IP (nome de domínio) do servidor de origem. Se o conteúdo solicitado não estiver no nó do CDN, este endereço (nome de domínio) será acessado para obter o conteúdo solicitado.<br /><br />**Servidor de origem**: servidor que fornece um serviço, que pode processar e responder às solicitações dos usuários. Os usuários finais acessam sua empresa no endereço de origem. Um endereço de origem pode ser um nome de domínio ou endereço IP. | Create a Domain Name (Criar um nome de domínio) > Origin Configuration (Configuração de origem) |
| Cabeçalho do host         | O conteúdo do servidor realmente solicitado durante o pull de origem do nó CDN. Isso geralmente é coerente com o nome de domínio de aceleração. Você pode inserir o conteúdo realmente solicitado na solicitação de pull de origem com base em suas necessidades de negócios.                            | Create a Domain Name (Criar um nome de domínio) > Origin Cofiguration (Configuração de origem) |.
| Nome de domínio CNAME        | Depois que seu nome de domínio de aceleração estiver conectado, o sistema atribuirá automaticamente um nome de domínio CNAME com o sufixo `.cdn.dnsv1.com` ou `.dsa.dnsv1.com`.<br />Depois que seus nomes de domínio de aceleração forem mapeados para o nome de domínio CNAME, o Tencent Cloud alterará dinamicamente o endereço IP apontado pelo registro CNAME e atualizará todos os seus nomes de domínio de aceleração, eliminando a necessidade de alterar manualmente os endereços IP apontados para eles. | Configure CNAME (Configuração do CNAME)        |

- **Nome de domínio de aceleração:** se os usuários finais acessarem sua empresa por meio de `cdntest.com`, então `cdntest.com` será o nome de domínio de aceleração.
- **Nome de domínio do CNAME:** depois que um nome de domínio de aceleração for conectado, o sistema atribuirá automaticamente um nome de domínio CNAME com o sufixo `.cdn.dnsv1.com` ou `.dsa.dnsv1.com`, como `cdntest .com.cdn.dnsv1.com` e `cdntest.com.dsa.dnsv1.com`.
- **Endereço de origem:** se o nó do CDN não armazenar em cache o conteúdo solicitado pelo usuário, o nó solicitará tal conteúdo em `1.1.1.1`, que é o endereço de origem.
- **Cabeçalho do host:** quando o nó do CDN está solicitando `1.1.1.1`, se você espera que o endereço realmente solicitado seja `originhost.com`, que é diferente de `cdntest.com` na solicitação do usuário final, então defina o cabeçalho do host para `originhost.com`, e o usuário final acessará o conteúdo em `originhost.com` após pull de origem através de `cdntest.com`. Geralmente, o nome de domínio de aceleração e o nome de domínio do cabeçalho do host devem ser os mesmos, o que pode ser ajustado com base nas necessidades do seu negócio.


## Instruções

Acesse o console do CDN, selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Create a Domain Name (Criar um nome de domínio)**.
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

Você precisa configurar as três partes a seguir para conectar um nome de domínio:

- [Configuração do nome de domínio](#m1)
- [Configuração do servidor de origem](#m2)
- [Configuração do serviço (opcional)](#m3)

[](id:m1)

### Configuração do nome de domínio

1. Selecione a região de aceleração.
2. Insira um nome de domínio de aceleração.
   Se o seu nome de domínio conectado atender a uma das condições a seguir, você precisará verificar sua propriedade conforme as instruções em [Verificação de propriedade do nome de domínio](https://intl.cloud.tencent.com/document/product/228/42693).
   - O nome de domínio está sendo conectado pela primeira vez.
   - O nome de domínio foi conectado por outro usuário.
   - O nome de domínio é um nome de domínio curinga.
3. Selecione um tipo de aceleração.
4. Defina outros itens opcionais (que podem ser modificados em **Domain Management (Gerenciamento de domínio)** posteriormente).

<img src="https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png" width="60%">



##### Descrição do item de configuração 

| Configuração | Descrição
| :------- | :----------------------------------------------------------- |
| Região | **China continental**: todas as solicitações são programadas para armazenar nós em cache na China continental. <br>**Fora da China continental (incluindo Hong Kong/Macau/Taiwan (China))**: todas as solicitações são programadas para armazenar em cache nós fora da China continental. <br>**Global**: as solicitações são programadas para o nó ideal mais próximo. <br><br>**Observações:**<br> os serviços de aceleração dentro e fora da China continental são faturados separadamente. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949). |
| Nome de domínio de aceleração          |1. O nome de domínio pode conter até 81 caracteres.<br>2. O registro de ICP é necessário para nomes de domínio em execução na China continental.<br>3. Subdomínios (`a.test.com` ou `a.b.test.com`) e nomes de domínio curinga (`*.test.com` ou `*.a.test.com`) são compatíveis.<br>4. É preciso [verificar a propriedade do nome de domínio](https://intl.cloud.tencent.com/document/product/228/42693) ao conectar um nome de domínio pela primeira vez, seja ele curinga ou conectado.*<br><br>**Observações:** <br>1.  Se um nome de domínio curinga for conectado aqui, seus nomes de subdomínio e nomes de domínio curinga de segundo nível não podem ser conectados por qualquer outra conta.<br>2. Nomes de domínio no formato `*.test.com` e `*.a.test.com` não podem ser configurados ao mesmo tempo.<br>3. Não é permitida a conexão a nomes de domínio maliciosos ou de alto risco. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/228/32981). |
| Tipo de aceleração | O CDN otimiza o desempenho de aceleração com base no tipo de serviço. Para obter o melhor resultado de aceleração, recomendamos escolher o tipo de aceleração semelhante ao da sua empresa real.  <br><br>**CDN**<br>Aceleração estática: aplicável a cenários de aceleração de recursos de menor escala, como e-commerce, site e fotos de jogos. <br>Aceleração de download: aplicável a cenários de download, como pacotes de instalação de jogos, downloads de arquivos de origem de áudio e vídeo e distribuição de firmware de celular. <br>Aceleração de streaming de vídeo sob demanda: aplicável à educação online e streaming de vídeo sob demanda. <br><br>**ECDN**<br>Aceleração dinâmica/estática: aplicável a cenários de negócios em que dados estáticos e dinâmicos são integrados, como várias páginas iniciais de sites.<br>Aceleração dinâmica: aplicável a cenários como login em conta, transação de pedido, chamada de API e consulta em tempo real .<br><br>**Observação:** <br>Os padrões de faturamento variam de acordo com o tipo de aceleração. Para obter mais informações, consulte [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/228/2949) da CDN e [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/570/37505) da ECDN, respectivamente. |
| Acesso IPv6| O acesso IPv6 fica desabilitado por padrão. Se for habilitado, os nós do CDN podem ser acessados pelo protocolo IPv6. <br><br>**Observações:** <br>• Atualmente, o acesso IPv6 não é suportado devido à atualização da plataforma. Fique atento ao lançamento oficial.<br>• O acesso IPv6 está disponível apenas na China continental. <br />•Para nomes de domínio de aceleração global, se o acesso IPv6 for ativado, ele terá efeito apenas na China continental. |
| Projeto | Projeto é um conjunto de recursos compartilhados por todos os produtos do Tencent Cloud. É possível gerenciá-lo na página [Project Management (Gerenciamento de projetos)](https://console.cloud.tencent.com/project). |
| Tag     | A chave e o valor da tag são obrigatórios. Se você não criou uma tag, crie uma em [Gerenciamento de Tags](https://console.cloud.tencent.com/tag/taglist). |

[](id:m2)

### Configuração do servidor de origem

1. Selecione o tipo de servidor de origem.
2. Selecione o protocolo do pull de origem.
3. Insira o endereço de origem.
4. Configure o cabeçalho do host.

<img src="https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png" width="70%">

##### **Descrição do item de configuração**

| Item de configuração    | Descrição                                                     |
| :-------- | :----------------------------------------------------------- |
| Tipo de Origem | **Origem do cliente**: <br>Selecione esta opção se você já tiver seu próprio servidor de negócios (ou seja, servidor de origem).<br><br>[Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos):<br> Se o COS for usado, você poderá selecionar diretamente o bucket correspondente.<br><br>Armazenamento de objetos de terceiros: <br>uma plataforma de armazenamento de objetos de terceiros que não seja o Tencent Cloud. Atualmente, o AWS S3 e o Alibaba Cloud OSS são compatíveis.<br><br>**Observação:** <br>Esta opção não está disponível para algumas plataformas no momento. Fique atento ao lançamento oficial. |
| Endereço do servidor de origem | **Origem do cliente**: <br>1. Vários IPs podem ser configurados como o servidor de origem e essa sondagem será feita durante o pull de origem. <br>2. É possível configurar a porta (0 a 65535) e o peso (1 a 100) **no formato de** `origin server:port:weight`. <br>A porta pode ser omitida e o formato torna-se `origin server::weight`. <br>**Observação:** Atualmente, o protocolo HTTPS aceita apenas a porta 443. <br>3. É possível configurar um nome de domínio como o servidor de origem e ele deve **deve ser** diferente do nome de domínio de aceleração CDN. <br>**Observação:** usar um nome de domínio de aceleração de CDN conectado como o servidor de origem causará um loop de resolução e uma falha de pull de origem.<br><br>**Tencent Cloud COS:** <br>1. É possível selecionar um bucket do COS Tencent como o servidor de origem.<br>2. Defina o tipo de servidor de origem para o nome de domínio padrão ou site estático de acordo com a configuração do bucket e seu caso de uso real.<br>3. Para um bucket privado, conceda acesso CDN ao bucket.<br><br>**Armazenamento de objetos de terceiros**: <br>1. Se o recurso estiver armazenado em uma plataforma de armazenamento de objetos de terceiros, insira um endereço de acesso válido ao bucket como o servidor de origem. Atualmente, o AWS S3 e o Alibaba Cloud OSS são compatíveis.<br>**Obervação**: `http://` e `http://` não podem ser incluídos. `my-bucket.oss-cn-beijing.aliyuncs.com` e `my-bucket.s3.ap-east-1.amazonaws.com` são compatíveis.<br>2. Para um bucket privado de terceiros, insira a chave válida e ative a autenticação de encaminhamento para acessar o bucket.|
| Protocolo de pull de origem | Essa opção pode ser selecionada com base nos protocolos aceitos pelo servidor de origem: <br>HTTP: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTP. <br><br>HTTPS: as solicitações de acesso HTTP/HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). <br><br>Seguir o protocolo: As solicitações de acesso HTTP usam pull de origem HTTP, já as solicitações de acesso HTTPS usam pull de origem HTTPS (o servidor de origem deve ser compatível com o acesso HTTPS). |
| Cabeçalho do host | Refere-se ao nome de domínio acessado no servidor de origem por um nó do CDN durante o pull de origem.<br><br>**Origem do cliente**:<br>o padrão é o nome de domínio de aceleração. Se um nome de domínio curinga estiver conectado, ele será o nome do subdomínio de acesso real por padrão e poderá ser personalizado.<br><br>**Tencent Cloud COS**:<br>o padrão é o endereço de acesso do bucket, que é o mesmo que o endereço de origem e não pode ser modificado.<br><br>**Armazenamento de objetos de terceiros**: <br>o padrão é o endereço de acesso ao bucket, que é igual ao endereço de origem e não pode ser modificado.|

[](id:m3)

### Configuração do serviço (opcional)

O CDN fornece itens de configuração de serviço comuns para você configurar conforme necessário. Se você não quiser configurar o serviço agora, poderá fazê-lo após conectar o nome de domínio.

<img src="https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png" width="80%">

##### Descrição do item de configuração**

| Configuração | Descrição                                                     |
| :------- | :----------------------------------------------------------- |
| Ignorar string de consulta | Um nó armazena recursos em cache seguindo o mapeamento `Key-Value`, em que ` Key` é o URL do recurso. <br>Se `Ignore Query String` estiver habilitado, os parâmetros após "?" no URL serão ignorados. <br>Caso contrário, `Key` será um URL de recurso completo. <br><br>Por padrão, essa funcionalidade fica **habilitada** para a aceleração de download e de streaming de VOD, mas **não** para a aceleração estática. |
| Ativação de Range GETs | Isso especifica se as solicitações parciais devem ser processadas durante o pull de origem. Pode ser habilitado apenas se o servidor de origem for compatível com GETs de alcance. <br><br/>**Por padrão**, essa funcionalidade fica **habilitada** para o servidor de origem do COS ou download e aceleração de streaming de VOD. |
| Configuração de cache | Validade do cache do nó. Para aceleração estática, os arquivos dinâmicos gerais (como arquivos PHP, JSP, ASP e ASPX) não serão armazenados em cache, e outros arquivos serão armazenados em cache por 30 dias por padrão. Para a aceleração de download e de streaming de VOD, a validade do cache de todos os arquivos é de 30 dias. <br><br>A validade do cache configurado é o tempo mais longo possível, a validade real do cache está relacionada aos recursos nos nós. |

## Conclusão da configuração

Após adicionar o nome de domínio, aguarde a distribuição da configuração do nome de domínio para toda a rede, o que geralmente leva de 5 a 10 minutos.
<img src="https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png" width="80%">

## Etapas subsequentes

Quando a distribuição for concluída, o CDN vai alocar um endereço CNAME correspondente para você. Você precisa configurar o CNAME para usar o serviço do CDN. Para obter instruções detalhadas, consulte [Configuração do CNAME](https://intl.cloud.tencent.com/document/product/228/3121).
