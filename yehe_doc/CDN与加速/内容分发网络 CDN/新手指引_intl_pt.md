



## Conceitos

Para lidar com o complicado ambiente de rede e corrigir vários problemas de rede nos negócios via Internet, a Tencent Cloud implanta nós de cache de alto desempenho, globalmente, com base na estrutura de rede existente, para criar uma nova arquitetura de rede virtual, possibilitando que você armazene seu conteúdo comercial nos servidores de borda mais próximos de seus usuários, de acordo com suas políticas de cache, encurtando a distância entre usuários e conteúdo, reduzindo a latência de acesso e melhorando a disponibilidade.

Para distinguir melhor entre os serviços de aceleração, a Tencent Cloud fornece produtos diferentes para diferentes tipos de aceleração:

- **CDN** para recursos estáticos: o conteúdo permanece o **mesmo** nas respostas a várias solicitações para o mesmo recurso.
Exemplos incluem: arquivos html, css e js, imagens, vídeos, pacotes de instalação de software, arquivos APK e arquivos compactados.
Cenários recomendados: aceleração de recursos estáticos do site, aceleração de download de arquivos e aceleração de áudio/vídeo.
- **ECDN** para recursos dinâmicos: o conteúdo **varia** nas respostas a várias solicitações para o mesmo recurso.
Exemplos incluem: APIs e arquivos .jsp, .asp, .php, .perl e .cgi.
Cenários recomendados: aceleração dinâmica e aceleração dinâmica/estática.

  

<table>
  <tr>
    <td>Item de comparação</td>
    <td align='middle'><b>CDN</b></td>
    <td align='middle'><b>ECDN</b></td>
  </tr>
  <tr>
    <td>Caso de uso</td>
    <td>Aceleração de recursos de site estático, aceleração de download de arquivos e sites de áudio/vídeo sob demanda</td>
    <td>Comércio eletrônico, pagamento in-game, site financeiro e educação online</td>
  </tr>
  <tr>
    <td>Cobertura</td>
    <td colspan="2" align="middle">China continental<br>Fora da China continental<br>Global</td>
  </tr>
  <tr>
    <td>Modo de faturamento</td>
    <td align="middle">Faturado por hora de tráfego<br>Pacotes de tráfego disponíveis para usuários na China continental. <br>Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/228/2949">Visão geral de cobrança</a> do CDN</td>
    <td align="middle">Faturado por número de solicitações e tráfego excessivo<br>Para mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/570/37505">Visão geral de faturamento</a> do ECDN</td>
  </tr>
  <tr>
    <td>Método de aceleração</td>
    <td align="middle">O conteúdo estático é acelerado e o conteúdo dinâmico é extraído do servidor de origem</td>
    <td align="middle">Aceleração dinâmica e aceleração dinâmica/estática são compatíveis<br></td>
  </tr>
  <tr>
    <td>Reserva de recursos</td>
    <td colspan='2' align='middle'>Mais de 2.800 nós em mais de 70 países/regiões, com uma largura de banda total reservada de mais de 150 Tbps</td>
  </tr>
</table>



Ao conectar um nome de domínio a ser acelerado à Tencent Cloud, você pode selecionar qualquer um dos dois produtos no [console CDN](https://console.cloud.tencent.com/cdn):


Observe que os dois tipos de aceleração usam políticas de aceleração e padrões de faturamento diferentes. Para obter mais informações, consulte [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/228/2949) do CDN e [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/570/37505) do ECDN, respectivamente.





## Exemplo de conexão CDN

![](https://qcloudimg.tencent-cloud.cn/raw/af95ca14834f1fb163b4d98e17f721f6.png)

### Acesso de usuário configurado com aceleração do CDN

Um usuário em Shenzhen acessa um servidor de origem em Pequim cujo endereço é `1.1.1.1` através de `cdntest.com`.

1. O usuário insere o nome de domínio `cdntest.com` para acesso, o DNS local resolve o valor do registro CNAME configurado `cdntest.com.cdn.dnsv1.com` e a solicitação é enviada ao sistema de agendamento DNS proprietário da Tencent e atribuído ao servidor de borda do CDN ideal, próximo ao usuário cujo IP é `2.2.2.2`.
2. O usuário solicita o servidor de borda do CDN cujo IP é `2.2.2.2`. Se o conteúdo tiver sido armazenado em cache, o conteúdo solicitado pelo usuário será retornado e o processo será encerrado.
3. Se o conteúdo solicitado não estiver armazenado em cache no servidor de borda do CDN, ele solicitará o servidor de origem em Pequim cujo endereço é `1.1.1.1`, e o conteúdo solicitado será decidido pelo cabeçalho do host configurado.
4. Depois que o servidor de borda do CDN cujo endereço IP é `2.2.2.2` obtém o recurso do servidor de origem, ele será armazenado em cache no servidor de borda de acordo com as políticas de cache personalizadas e será retornado ao usuário. Em seguida, a solicitação será encerrada.
5. Quando outro usuário próximo a Shenzhen acessar `cdntest.com` novamente, o sistema de agendamento de DNS da Tencent agendará preferencialmente a solicitação para o servidor de borda CDN cujo IP é `2.2.2.2`, pois ele já armazena em cache o conteúdo correspondente. Dessa forma, o usuário pode obter diretamente o conteúdo do servidor de borda sem solicitá-lo ao servidor de origem.

### Conceitos confusos

- Se os usuários finais acessarem sua empresa por meio de `cdntest.com`, então `cdntest.com` será o nome de domínio de aceleração.
- Depois que um nome de domínio de aceleração for conectado, o sistema atribuirá automaticamente um nome de domínio CNAME com o sufixo `.cdn.dnsv1.com` ou `.dsa.dnsv1.com`, como `cdntest.com.cdn.dnsv1.com ` e `cdntest.com.dsa.dnsv1.com`, que precisa ser resolvido no console DNSPod.
- Se o nó CDN não armazenar em cache o conteúdo solicitado pelo usuário, este nó solicitará tal conteúdo em `1.1.1.1`, que é o endereço de origem.
- Quando o nó CDN está solicitando `1.1.1.1`, o endereço realmente solicitado é `originhost.com`, ou seja, `originhost.com` é o cabeçalho do host. Geralmente, o nome de domínio de aceleração e o nome de domínio do cabeçalho do host devem ser os mesmos, o que pode ser ajustado com base nas necessidades do seu negócio.

| Item de configuração          | Descrição |                                                     Posição de uso          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| Nome de domínio de aceleração          | Nome de domínio a ser conectado ao CDN, que é o nome de domínio real acessado pelos usuários finais            | Criar um nome de domínio > Configuração de domínio |
| Endereço de origem/nome de domínio de origem | Endereço IP (nome de domínio) do servidor de origem. Se o conteúdo solicitado não estiver no nó CDN, este endereço (nome de domínio) será acessado para obter o conteúdo solicitado.<br /><br />**Servidor de origem**: servidor que fornece um serviço, que pode processar e responder às solicitações dos usuários. Os usuários finais acessam sua empresa no endereço de origem. Um endereço de origem pode ser um nome de domínio ou endereço IP. **O endereço de origem não pode ser igual ao nome de domínio de aceleração.** | Criar um nome de domínio > Configuração de origem |
| Cabeçalho do host         | O conteúdo do servidor realmente solicitado durante o pull de origem do nó CDN.                            | Criar um nome de domínio > Configuração de origem |
| Nome de domínio CNAME        | Depois que seu nome de domínio de aceleração estiver conectado, o sistema atribuirá automaticamente um nome de domínio CNAME com o sufixo `.cdn.dnsv1.com ou `.dsa.dnsv1.com`.<br />Depois que seus nomes de domínio de aceleração forem mapeados para o nome de domínio CNAME, a Tencent Cloud alterará dinamicamente o endereço IP apontado pelo registro CNAME e atualizará todos os seus nomes de domínio de aceleração, eliminando a necessidade de alterar manualmente os endereços IP apontados para eles. | Configurar CNAME |



## Por que CDN?

#### Problemas de experiência do usuário que podem ocorrer quando os usuários finais acessam diretamente o conteúdo estático no servidor de origem

- Quanto mais distante o usuário final estiver do servidor, mais lento o acesso.
- Quanto maior o número de usuários finais, maiores as taxas de largura de banda da rede.
- A experiência de acesso internacional é fraca.

![](https://qcloudimg.tencent-cloud.cn/raw/cb1dd401c8cbb0e3835d9e410c37c31d.png)

>?Os dados acima são apenas para referência. As flutuações de dados em ambientes de rede complicados são normais.

#### Como o CDN melhora sua experiência de rede

- Depois que o CDN armazena o conteúdo em cache, os usuários finais precisam apenas acessar os nós do CDN próximos para obter o conteúdo estático.
- A pressão da largura de banda no servidor de origem é aliviada e as taxas de rede são reduzidas.
- Os nós implantados globalmente melhoram a experiência de acesso internacional.

![](https://qcloudimg.tencent-cloud.cn/raw/7460b780994e836d97d549b79211f517.png)

>?Os dados acima são apenas para referência. As flutuações de dados em ambientes de rede complicados são normais.

#### Casos de uso recomendados do CDN

- Aceleração de recursos do site estático: O CDN é adequado para armazenar em cache e acelerar **conteúdo estático, como imagens, vídeos e vários arquivos HTML em sites comuns** (sites de portal, comércio eletrônico e UGC, etc.), para proporcionar uma experiência de acesso mais suave.
- Aceleração de download de arquivos: O CDN é adequado para **acelerar downloads de vários arquivos**. Ao entregar arquivos para servidores de borda, o CDN não apenas alivia a pressão da largura de banda durante os horários de pico de download, mas também melhora a experiência de download.
- Aceleração de áudio/vídeo: O CDN é adequada para vários **sites de áudio/vídeo sob demanda**. Com base nos muitos anos de experiência em operações de vídeo online da Tencent, o CDN garante efetivamente que os usuários finais em todas as regiões possam ouvir/assistir fluxos de áudio/vídeo sem problemas, mesmo quando há um grande número de solicitações de acesso simultâneo a recursos de áudio/vídeo.

## Por que ECDN?

### Problemas de experiência do usuário que podem ocorrer quando os usuários finais acessam diretamente o conteúdo dinâmico no servidor de origem

- Os fatores de rede, região e largura de banda afetam as solicitações de recursos e causam problemas como alta latência e alta taxa de perda de pacotes.
- A ligação de rede pode ter uma qualidade ruim ou até mesmo ser bloqueada durante o roteamento.
- O ambiente de rede pública é complicado, comprometendo a experiência normal do serviço.

![](https://qcloudimg.tencent-cloud.cn/raw/3fcb611b6d5c37e63b692daab957350f.png)

>?Os dados acima são apenas para referência. As flutuações de dados em ambientes de rede complicados são normais.



### Como o ECDN melhora sua experiência de rede

- Os usuários finais acessam nós ECDN próximos para operações como acesso a recursos e pull de origem.
- O status de toda a rede é monitorado em tempo real para selecionar a conexão ideal e evitar conexões bloqueadas e de baixa qualidade.

![](https://qcloudimg.tencent-cloud.cn/raw/e8ef115ebb2a4f719454b23e33b2dd6b.png)

>?Os dados acima são apenas para referência. As flutuações de dados em ambientes de rede complicados são normais.



### Casos de uso recomendados de ECDN

- Aceleração Dinâmica/Estática: O ECDN é aplicável a cenários com **recursos dinâmicos e estáticos**. Ele pode sustentar melhor esses cenários reconhecendo automaticamente os recursos dinâmicos, usando diferentes políticas de aceleração e implementando aceleração única para recursos dinâmicos e estáticos. Como a conexão ECDN é usada, **os padrões de cobrança do ECDN devem prevalecer para recursos estáticos e dinâmicos**.
- Aceleração dinâmica: O ECDN é adequado para cenários com **muitas solicitações de recursos dinâmicos**, como batalhas de jogos, transações de comércio eletrônico, transações financeiras e educação online. Ele pode selecionar a ligação ideal para pull de origem usando várias tecnologias, como detecção de rota dinâmica e roteamento inteligente, reduzindo bastante a latência de acesso.

  
### Como ativar o ECDN

1. Se você for um novo usuário e ativar o serviço no <a href="https://console.cloud.tencent.com/cdn">console CDN<a href="https://console.cloud.tencent.com/cdn">, tanto o CDN quanto o ECDN serão ativados, mas o serviço não utilizado não incorrerá em taxas. Para obter mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/228/32978"> Configuração de CDN do zero</a>.
2. Se o CDN estiver ativado, mas o ECDN não estiver, quando você adicionar um nome de domínio para aceleração dinâmica/estática ou aceleração dinâmica pela primeira vez, o sistema ativará automaticamente o ECDN para você, conforme mostrado abaixo:

3. Se você já ativou o ECDN no console original do ECDN, pode enviar um tíquete para migrar sua conta. Após a migração bem-sucedida, você pode usar o ECDN no console do CDN.

>!
>- Aceleração Dinâmica/Estática: é aplicável a cenários de negócios onde são integrados dados dinâmicos e estáticos, como várias homepages de sites.
>- Aceleração dinâmica: é aplicável a cenários como login de conta, transação de pedido, chamada de API e consulta em tempo real.
>
>As taxas geradas por um nome de domínio ECDN serão cobradas de acordo com a [visão geral de faturamento](https://intl.cloud.tencent.com/document/product/570/37505) do ECDN.

 


​	
​	
​	

## Quando usar o SCDN

Se sua empresa tiver requisitos adicionais de segurança, você poderá adquirir um serviço de segurança adicional baseado em CDN, ou seja, SCDN. Para obter mais informações, consulte [Rede de entrega de conteúdo seguro](https://intl.cloud.tencent.com/document/product/1032).



## Como selecionar a região de aceleração

| Localização do usuário final                 | Efeito de aceleração                                             | Região de aceleração selecionada |
| :--------------------------- | ---------------------------------------------------- | ------------ |
 | China continental                     | As solicitações de acesso de usuários globais serão programadas para serviço em nós de cache na China continental  |China continental     |
| Fora da China continental (incluindo Hong Kong, Macau e Taiwan (China)) | Solicitações de acesso de usuários globais serão agendadas para armazenar nós fora da China continental para serviço  | Fora da China continental     |
| Global          | Solicitações de acesso de usuários globais serão programadas para o nó mais próximo para serviço           | Global         |

Tanto o CDN quanto o ECDN têm servidores de borda implantados globalmente para rotear os usuários finais para os nós mais próximos a eles em suas respectivas regiões com base em sua escolha. Observe que os padrões de cobrança variam de acordo com a região de aceleração. Para obter mais informações, consulte a [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949).

>?Se você comprou um pacote de tráfego, verifique se as regiões onde ele está disponível correspondem à sua região de aceleração necessária.



## Configuração do CDN/ ECDN do zero

Este tutorial descreve como configurar rapidamente o CDN/ECDN e os parâmetros relevantes. Clique em [Configuração do CDN do zero](https://intl.cloud.tencent.com/document/product/228/32978) para visualizá-lo.
