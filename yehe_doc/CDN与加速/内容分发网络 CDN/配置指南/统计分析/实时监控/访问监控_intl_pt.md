>Este documento descreve a nova versão do console. Ele fornece estatísticas mais abrangentes e detalhadas e é usado como base para o faturamento. Recomendamos que você use a nova versão.
## Descrições das métricas
### Métricas na página de visão geral
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Statistics (Estatísticas)** > **Realtime Monitoring (Monitoramento em tempo real)** na barra lateral esquerda para acessar a página de gerenciamento. A guia **Access Monitoring (Monitoramento de acesso)** é exibida por padrão. As curvas de monitoramento de todos os nomes de domínio com granularidade de 1 minuto nas últimas 6 horas serão retornadas, incluindo as seguintes métricas:
+ Largura de banda: calculada dividindo o tráfego total em um minuto por 60 segundos.
+ Taxa de acertos de tráfego: (tráfego downstream total - tráfego de pull de origem) / tráfego downstream total em um minuto.
+ Porcentagem do código de status da solicitação: gráfico de porcentagem dos códigos de status (2XX/3XX/4XX/5XX) retornados no período selecionado.
+ Códigos de status de solicitação 2XX: os códigos de status gerados pelo monitoramento de código de status 2XX serão contabilizados.
+ Códigos de status de solicitação 3XX: os códigos de status gerados pelo monitoramento de código de status 3XX serão contabilizados.
+ Códigos de status de solicitação 4XX: os códigos de status gerados pelo monitoramento de código de status 4XX serão contabilizados.
+ Códigos de status de solicitação 5XX: os códigos de status gerados pelo monitoramento de código de status 5XX serão contabilizados.

### Dados na página de detalhes
Clique em **View Details (Exibir detalhes)** em cada métrica para acessar a página de detalhes da métrica.
![](https://main.qcloudimg.com/raw/3aae6ee3d47dadae74ca59667b6d7310.png)
Também é possível alternar para outra métrica selecionando-a na lista suspensa no canto superior esquerdo da página de detalhes.
![](https://main.qcloudimg.com/raw/5262321ca413e2a24274a0d0fe086263.png)
Na página de detalhes, é possível visualizar os seguintes dados de métrica:
+ Largura de banda: largura de banda de pico total, curva da largura de banda em tempo real e classificações da largura de banda de nomes de domínio (de grande a pequeno).
+ Tráfego: tráfego total, curva do tráfego em tempo real, classificações do tráfego de nomes de domínio (de alto a baixo) e classificações do tráfego de URLs (de alto a baixo).
+ Taxa de acertos de tráfego: taxa de acertos de tráfego, curva da taxa de acertos de tráfego em tempo real e classificações da taxa de acerto de tráfego de nomes de domínio (de alto a baixo).
+ Solicitações: quantidade total de solicitações, curva da contagem de solicitações em tempo real, classificações da contagem de solicitações de nomes de domínio (de alto a baixo) e classificações da contagem de solicitações de URLs (de alto a baixo)
+ Porcentagem dos códigos de status: gráfico circular dos códigos de status 2XX, 3XX, 4XX e 5XX e suas contagens e porcentagens.
+ Códigos de status 2XX: curva de monitoramento em tempo real dos códigos de status 2XX e seus códigos de substatus e classificações dos códigos de status 2XX de nomes de domínio (de alto a baixo).
+ Códigos de status 3XX: curva de monitoramento em tempo real dos códigos de status 3XX e seus códigos de substatus e classificações dos códigos de status 3XX de nomes de domínio (de alto a baixo).
+ Códigos de status 4XX: curva de monitoramento em tempo real dos códigos de status 4XX e seus códigos de substatus e classificações dos códigos de status 4XX de nomes de domínio (de alto a baixo).
+ Códigos de status 5XX: curva de monitoramento em tempo real dos códigos de status 5XX e seus códigos de substatus e classificações dos códigos de status 5XX de nomes de domínio (de alto a baixo).


## Descrição da granularidade
### Granularidade na página de visão geral
A página de monitoramento oferece opções para exibir curvas de dados em granularidade de 1 minuto, 5 minutos, 1 hora ou 1 dia. A granularidade de tempo mínima que pode ser exibida varia de acordo com o período selecionado.
+ Período ≤ 6 horas: a granularidade de tempo mínima é de 1 minuto. A latência para exibir a curva de 1 minuto é de cerca de 5 a 10 minutos.
+ 6 horas < período ≤ 24 horas: a granularidade de tempo mínima é de 5 minutos. A latência para exibir a curva de 5 minutos é de cerca de 5 a 10 minutos.
+ 24 horas < período ≤ 31 dias: a granularidade de tempo mínima é de 1 hora.
+ Período > 31 dias: a granularidade de tempo mínima é de 1 dia.


### Granularidade na página de detalhes
As opções de granularidade de tempo na página de detalhes de métricas são as seguintes:
+ Período ≤ 1 dia: a granularidade de tempo mínima é de 1 minuto. A latência para exibir a curva de 1 minuto é de cerca de 5 a 10 minutos.
+ 1 dia < período ≤ 31 dias: A granularidade de tempo mínima pode ser 5 minutos, 1 hora ou 1 dia.
+ Período > 31 dias: a granularidade de tempo mínima é de 1 dia.

>!
>- Atualmente, a consulta de dados com granularidade de estatísticas de 1 minuto só é aceita na China Continental. A granularidade mínima para consulta de dados históricos é 5 minutos.
>- O período máximo de consulta é de 90 dias.


### Descrição da agregação
O método para agregar dados de 1 minuto em dados de 5 minutos, 1 hora ou 1 dia varia de acordo com a métrica de dados.
+ Largura de banda: a menor granularidade fornecida pelo CDN para monitorar dados de largura de banda é de 1 minuto. Com base no padrão do setor, as taxas costumam ser cobradas por granularidade de 5 minutos, que é calculada considerando a média dos valores de dados de 1 minuto. Portanto, os dados de largura de banda em uma granularidade de 1 hora ou 1 dia podem ser calculados com base no valor máximo de largura de banda de 5 minutos.
+ Tráfego: os dados de tráfego em uma granularidade de 5 minutos, 1 hora ou 1 dia são obtidos pela agregação de dados de tráfego de 1 minuto.
+ Taxa de acertos de tráfego: com base na granularidade selecionada, a taxa de acertos de tráfego é calculada usando a fórmula "(tráfego downstream total - tráfego de pull de origem) / tráfego downstream total" em vez de tirar a média dos valores de dados de 1 minuto.
+ Quantidade de solicitações e códigos de status: os dados em uma granularidade de 5 minutos, 1 hora ou 1 dia são obtidos pela agregação de dados de 1 minuto.


## Descrição da fonte de dados
### Dados faturáveis e dados de log
- Os dados coletados com base nos bytes downstream no log de um nome de domínio de aceleração são dados na camada de aplicativos, já o tráfego gerado durante as transferências reais de dados pela rede é de 5 a 15% mais do que os dados da camada de aplicativos.
 + Consumo por cabeçalhos TCP/IP: nas solicitações HTTP baseadas em TCP/IP, cada pacote tem um tamanho máximo de 1.500 bytes e inclui cabeçalhos TCP e IP de 40 bytes, que geram tráfego durante a transferência, mas não podem ser contados pela camada de aplicativos. O custo dessa parte é de cerca de 3%.
 + Retransmissão TCP: Durante a transferência normal de dados pela rede, cerca de 3 a 10% dos pacotes são perdidos na Internet e o servidor retransmitirá as partes perdidas. Esse tráfego não pode ser contabilizado pela camada de aplicativos, que representa 3 a 7% do tráfego total.
- Como um padrão do setor, os dados faturáveis são a soma dos dados da camada de aplicativos e as sobrecargas mencionadas acima. O CDN do Tencent Cloud considera 10% como a proporção de sobrecargas, então o tráfego/a largura de banda faturável monitorado(a) é cerca de 110% dos dados registrados em log.
- Exceto para tráfego e largura de banda, todas as outras métricas são coletadas na camada de aplicativos. Devido a flutuações da rede, as estatísticas exibidas na página de monitoramento são ligeiramente diferentes daquelas no log, pois a perda de dados pode ocorrer durante o pull de log de nós ou relatórios de dados por servidores.

### Descrição da fonte de dados
+ Se a opção **statistical district (distrito estatístico)** ou **ISP** não for selecionada como um filtro, todos os dados consultados serão dados faturáveis.
+ Se a opção **statistical district (distrito estatístico)** ou **ISP** for selecionada como um filtro, os dados precisam ser correspondidos para cálculo por IP do cliente no log de acesso, e todos os dados consultados serão dados de log.

## Descrição de filtros
+ Atualmente, a consulta por **statistical district (distrito estatístico)** e **ISP** não é aceita. Você só pode consultar todos os ISPs por distrito ou consultar todos os distritos por ISP.
+ Atualmente, o monitoramento de pull de origem não aceita a filtragem por área estatística ou ISP.
+ Atualmente, o monitoramento de pull de origem não aceita a filtragem por solicitação HTTPS/HTTP.



