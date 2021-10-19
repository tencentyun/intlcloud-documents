### Como são coletadas as estatísticas de largura de banda no monitoramento de acesso?
Cada nó do CDN coleta dados de tráfego em tempo real e os relata ao centro de computação, que agrega os dados em dados de tráfego total e exibe as estatísticas de largura de banda dividindo o tráfego total pela duração de uso.
**Exemplo:**
- Se o tráfego total gerado em um minuto for 6 MB, a largura de banda correspondente será (6 * 8) / 60 = 0,8 Mbps.
- Como o uso da largura de banda faturada é calculado com base nas estatísticas com uma granularidade de 5 minutos, o valor da largura de banda correspondente é o tráfego total em 5 minutos / 300 segundos.

### Por que o tráfego nas informações de monitoramento é diferente daquele no log?
O tráfego contabilizado com base nos bytes downstream no log de um nome de domínio acelerado é limitado aos dados na camada de aplicativos, já o tráfego gerado por transferências de dados reais pela rede é cerca de 5 a 15% maior do que o tráfego da camada de aplicativos.
- Consumo por cabeçalhos TCP/IP: em solicitações HTTP baseadas em TCP/IP, cada pacote tem um tamanho máximo de 1.500 bytes e inclui cabeçalhos TCP e IP de 40 bytes, que geram tráfego durante a transferência, mas não podem ser contabilizados pela camada de aplicativo. O custo dessa parte é de cerca de 3%.
- Retransmissão TCP: durante a transferência normal de dados pela rede, cerca de 3 a 10% dos pacotes são perdidos na internet e retransmitidos pelo servidor. Esse tipo de tráfego não pode ser contabilizado pela camada de aplicativos, que representa 3 a 7% do tráfego total.

Como um padrão do setor, o tráfego faturável é a soma do tráfego da camada de aplicativos e as sobrecargas descritas acima. O CDN do Tencent Cloud considera 10% como a proporção de sobrecargas, então, o tráfego monitorado é cerca de 110% do tráfego registrado em log.

### Como eu calculo a taxa de acertos de tráfego?
Por padrão, o CDN habilita o cache L2 (camada de borda e camada intermediária). Enquanto uma solicitação atingir uma das camadas para obter resposta, ela será contada como um acerto de nó do CDN.
Taxa de acertos de tráfego = (tráfego downstream total - tráfego de pull de origem) / tráfego downstream total.

### Como faço para corrigir o problema de baixa taxa de acertos de tráfego?
- Verifique se o cache foi limpo: a limpeza do cache limpa o conteúdo especificado no nó, levando a uma taxa de acertos de tráfego temporariamente baixa.
- Verifique se recursos novos foram colocados no servidor de origem: uma grande quantidade de recursos novos pode causar pulls de origem por nós do CDN, levando a uma baixa taxa de acertos de tráfego.
- Verifique se o servidor de origem está funcionando corretamente: se estiver com defeito com vários erros 4XX ou 5XX, a taxa de acertos de tráfego será afetada.
- Verifique se a política de expiração de cache está configurada corretamente: verifique a seção "Cache Rules (Regras de cache)" na guia Cache Configuration (Configuração de cache) no console. As políticas de expiração do cache são exibidas em ordem crescente por prioridade, ou seja, uma política tem precedência sobre a que está acima dela.
- Verifique se os Range GETs (GETs de alcance) estão ativados: verifique a seção "Range GETs Configuration (Configuração de GETs de alcance)" na guia Origin Configuration (Configuração da origem) no console. Se estiverem desativados, será efetuado pull dos arquivos em sua totalidade, em vez de várias partes, conforme solicitado durante o pull de origem, o que aumenta o tráfego de pull de origem e reduz a taxa de acertos.
- Verifique se Ignore Query String (Ignorar string de consulta) está ativado: verifique a seção "Ignore Query String (Ignorar string de consulta)" na guia Access Control (Controle de acesso) no console. Se estiver desativado, o cache será executado com base no caminho completo. Nesse caso, se o mesmo recurso for solicitado por parâmetros diferentes, ele não poderá ser correspondido e será armazenado em cache várias vezes, reduzindo a taxa de acertos de tráfego.

### As estatísticas de código de status incluem todos os códigos de status?

Sim. Na nova versão da análise estatística do CDN, as curvas de monitoramento são desenhadas para todos os códigos de status gerados pelos servidores de origem, facilitando a solução de problemas.

### Como são calculadas as estatísticas do distrito e do ISP?
As estatísticas do distrito e do ISP são calculadas com base nos IPs do cliente no log de acesso. Como o cálculo é concluído com base no log, os dados faturáveis simplesmente acumulados diferem dos dados faturáveis quando "all districts (todos os distritos)" ou "all ISPs (todos os ISPs)" estiver selecionado. Para obter mais informações, consulte a pergunta nº 2 acima.


### Como é gerado o tráfego de pull de origem do CDN?

O tráfego de pull de origem do CDN é gerado durante as três situações abaixo:
1. O recurso solicitado não foi armazenado em cache no nó do CDN e foi obtido do servidor de origem.
2. O servidor de origem com limpeza manual foi sincronizado com o nó.
3. O servidor de origem foi limpo automaticamente.

### O que devo fazer se o tráfego do meu CDN tiver uma exceção ou estiver sob ataques DDoS ou CC?

Se você acredita que o tráfego da sua empresa está absurdamente alto, você pode baixar os logs para verificar as condições de acesso da sua empresa e definir as restrições de acesso adequadamente. Por padrão, o CDN não conhece sua lógica empresarial, portanto, não restringirá as solicitações de acesso. Portanto, você precisa configurar as restrições com base em suas condições empresariais. Para obter mais informações, consulte [Download de log](https://intl.cloud.tencent.com/document/product/228/6316).

Para evitar solicitações mal-intencionadas ou ataques CC/DDoS ao seu site, é altamente recomendável que você conclua as seguintes configurações:
1. Configuração de proteção de hotlink: é possível controlar o acesso aos recursos da sua empresa. Ao definir uma política de controle de acesso no valor do campo referencial no cabeçalho da solicitação HTTP, é possível restringir a fonte de acesso para evitar hotlinking por usuários mal-intencionados. Para obter mais informações, consulte [Configuração de proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292).
2. Configuração da lista de bloqueio/permissões de IP: é possível criar políticas de filtragem para IPs de origem de solicitações de usuários com base em suas necessidades empresariais, ajudando a evitar hotlinking e ataques de IPs mal-intencionados. Para obter mais informações, consulte[Configuração da lista de bloqueio/permissões de IP](https://intl.cloud.tencent.com/document/product/228/6298).
3. Configuração de limite de acesso de IP: é possível se defender contra ataques CC, limitando a quantidade de solicitações de acesso por segundo a um nó permitido para um IP de cliente. Depois que a configuração for habilitada, um erro 514 será retornado para solicitações que excederem o limite de QPS. Definir um limite de frequência inferior pode afetar o uso da sua empresa por usuários normais de alta frequência. Portanto, defina o limite de acordo com suas condições e uso empresariais reais. Para obter mais informações, consulte [Configuração de limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420).
4. Configuração do limite de largura de banda: é possível configurar um limite de largura de banda para um nome de domínio. Quando a largura de banda consumida pelo nome de domínio exceder esse limite em um ciclo estatístico (5 minutos), todas as solicitações de acesso serão encaminhadas ao servidor de origem ou o serviço do CDN será desabilitado dependendo da sua configuração (em ambos os casos, um erro 404 será ser retornado para todos os pedidos de acesso). Para obter mais informações, consulte [Configuração do limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541).

### Há um atraso no uso de APIs para consultar dados? De quanto tempo?
Há um certo atraso no uso de APIs para consultar dados. As consultas de dados em tempo real, como dados de acesso e dados de faturamento, têm um atraso de cerca de 5 a 10 minutos, já as consultas de dados analíticos, como classificações, têm atrasos de aproximadamente meia hora. Os dados são calibrados no back-end por volta das 3 da manhã, horário de Pequim.



