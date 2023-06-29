<style> 
table th:nth-of-type(1) {width:20%; } 
table th:nth-of-type(2){ width:45%; } 
table th:nth-of-type(3){ width:16%; } 
table th:nth-of-type(4){ width:19%; } 
</style>

## Setembro de 2021
| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Limite de alarme para limite de largura de banda |O CDN oferece suporte à configuração de um limite de alarme para limite de largura de banda. Quando a proporção da largura de banda de acesso para o limite de largura de banda atingir esse valor, uma mensagem de alarme será enviada.|2 de setembro de 2021|[Configuração do limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541)|


## Agosto de 2021
| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Configuração rápida do CNAME|Os recursos de resolução e configuração foram interconectados entre o CDN do Tencent Cloud e o [DNSPod](https://console.dnspod.cn/). Para nomes de domínio hospedados no DNSPod do Tencent Cloud, você pode configurar o CNAME com menos etapas no [console do CDN](https://console.cloud.tencent.com/cdn/domains) para habilitar a aceleração do CDN.|26 de agosto de 2021|Configuração rápida do CNAME|
|Status inválido para pré-busca de URL| Um novo status de cache "Inválido" é adicionado. Para pré-busca inválida, o servidor de origem retornará um código de status de erro, como 4XX/5XX.|18 de agosto de 2021|[Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000)|
|Novo campo de log|Um novo campo de log é adicionado. Trata-se de uma porta que conecta o cliente e os nós CDN.|6 de agosto de 2021|[Baixar logs](https://intl.cloud.tencent.com/document/product/228/6316)|





## Julho de 2021
| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Console CDN-ECDN | O console CDN integra o serviço ECDN. Um novo usuário pode ativar os serviços CDN e ECDN sem pagar pelo serviço que não é usado. Se você tiver apenas o serviço CDN ativado, o serviço ECDN será ativado automaticamente depois que você adicionar um nome de domínio ECDN pela primeira vez. | 26 de julho de 2021 | [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734)|
|Pull de origem para um bucket de terceiros | Oferece suporte à extração de recursos de um bucket de terceiros como AWS S3 e Alibaba Cloud OSS. A autenticação de pull de origem pode ser habilitada. | 14 de julho de 2021 | [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289) |



## Junho de 2021

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Aumento de limpeza diária de URL e de cota de pré-busca | Quando você estiver ficando sem limpeza de URL e cota de pré-busca, poderá aumentá-las rapidamente. | 23 de junho de 2021 | [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299) [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000) |
|Consulte o IP do nó pull de origem de nomes de domínio de aceleração no console | Oferece suporte à consulta do IP do nó pull de origem (incluindo endereço IP e intervalo de IP) de nomes de domínio de aceleração. | 23 de junho de 2021 | Consulta de nó de pull de origem|





## Março de 2021

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
|Configuração de alteração em lote|Permite a alteração das configurações de nomes de domínio para vários nomes de domínio de aceleração em lotes, aumentando a eficiência da configuração.|31 de março de 2021 |[Configuração de alteração em lote](https://intl.cloud.tencent.com/document/product/228/39911)|
|QUIC beta|Liberação do CDN QUIC beta.| 2 de março de 2021|[QUIC](https://intl.cloud.tencent.com/document/product/228/39746)|
|Configuração do tamanho de solicitações POST|Permite a configuração do tamanho máximo de solicitações POST.|2 de março de 2021 |[Configuração do tamanho de solicitações POST](https://intl.cloud.tencent.com/document/product/228/39747)|



## Dezembro de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Configuração avançada de pull de origem | Permite configurações de pull de origem mais refinadas, incluindo pull de origem com base no caminho (especificando o tipo de arquivo, a pasta, o arquivo de caminho completo ou a página inicial) e pull de origem com base na região de IP do cliente (que não está disponível em todas as localizações), etc.| 29 de dezembro de 2020 | [Configuração avançada de pull de origem](https://intl.cloud.tencent.com/document/product/228/39745) |
| Acesso IPv6 totalmente compatível na China continental | O acesso IPv6 está disponível na China continental. Você pode habilitá-lo para permitir que endereços IPv6 acessem nós CDN. | 14 de dezembro de 2020 | [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734) |
| Configuração da validade do cache do navegador | Permite a personalização de políticas de cache do navegador do cliente para reduzir a taxa de pull de origem. | 7 de dezembro de 2020 | [Configuração de validade do cache do navegador](https://intl.cloud.tencent.com/document/product/228/38932) |
| Reescrita de URL de origem | Permite a configuração de regras de reescrita de URL de origem. | 7 de dezembro de 2020 | [Configuração da reescrita de URL de origem](https://intl.cloud.tencent.com/document/product/228/38933) |
| Configuração da versão do TLS | Permite a ativação e a desativação de versões do TLS conforme necessário. | 7 de dezembro de 2020 | [Configuração da versão do TLS](https://intl.cloud.tencent.com/document/product/228/38934) |
| Página de erro personalizada | Permite o redirecionamento de uma solicitação com o código de status especificado para o URL especificado. | 7 de dezembro de 2020 | [Página de erro personalizada](https://intl.cloud.tencent.com/document/product/228/38935) |
|Atualização da ferramenta de autodiagnóstico | Agora, a ferramenta de autodiagnóstico aceita nomes de domínio que foram conectados às regiões de aceleração "Global" e "Fora da China continental".|3 de dezembro de 2020| [Ferramenta de autodiagnóstico](https://intl.cloud.tencent.com/document/product/228/6304)|

## Novembro de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Atualização da configuração do cabeçalho de solicitações de pull de origem | Permite a configuração do cabeçalho referenciador. | 25 de novembro de 2020 | [Solicitar configuração do cabeçalho](https://intl.cloud.tencent.com/document/product/228/37037) |
| Copiar configuração | Permite a cópia das configurações de um nome de domínio de encaminhamento existente para um ou vários nomes novos de domínio de encaminhamento. | 3 de novembro de 2020 | [Cópia de configuração](https://intl.cloud.tencent.com/document/product/228/38936) |


## Outubro de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Lançamento oficial do serviço de log em tempo real | Os logs de acesso do CDN podem ser coletados e publicados em tempo real para uma rápida recuperação e análise dos dados de log. | 29 de outubro de 2020 | [Logs em tempo real](https://intl.cloud.tencent.com/document/product/228/35380) |
|Verificação da propriedade dos nomes de domínio|Para evitar a apropriação de nomes de domínio, a verificação da propriedade dos nomes de domínio é necessária para conectar um novo nome de domínio ao CDN do Tencent Cloud.|14 de outubro de 2020|[Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734)|




## Agosto de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ---------------------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Reescrita de URL de acesso               | Permite a configuração de regras de reescrita de URL para redirecionar URLs com o código 302 para o URL especificado. | 13 de agosto de 2020 | [Configuração da reescrita de URL de acesso](https://intl.cloud.tencent.com/document/product/228/38074) |
| Fechamento das portas para acessos da China continental   | Permite o fechamento das portas de acesso 80, 8080 e 443 conforme necessário.                      | 13 de agosto de 2020 | [Configuração da porta de acesso da China continental](https://intl.cloud.tencent.com/document/product/228/39879) |
| Aumento da quantidade de IPs permitidos/bloqueados para 200 | Permite a adição de até 200 IPs permitidos/bloqueados.       | 13 de agosto de 2020 | [Configuração da lista de bloqueio/permissões de IPs](https://intl.cloud.tencent.com/document/product/228/6298) |

## Junho de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------ | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Configuração da lista de bloqueio/permissões de agente do usuário (UA)          | Determina se nega ou permite solicitações de acordo com o cabeçalho de solicitação HTTP `User-Agent`. | 30 de junho de 2020 | [Configuração da lista de bloqueio/permissões de agente do usuário (UA)](https://intl.cloud.tencent.com/document/product/228/37256) |
| Configuração do limite de velocidade de downstream             | Controla a largura de banda de acesso ao CDN definindo o limite de velocidade de downstream em um URL.      | 30 de junho de 2020 | [Configuração do limite de velocidade de downstream](https://intl.cloud.tencent.com/document/product/228/37257) |
| Configuração da não distinção entre maiúsculas e minúsculas para chaves de cache       | Configura a opção de ignorar a capitalização de letras para chaves de cache (a distinção entre maiúsculas de minúsculas é o padrão)    | 30 de junho de 2020 | [Configuração de regra de chave de cache](https://intl.cloud.tencent.com/document/product/228/35316) |
| Configuração de cabeçalho de solicitação de pull de origem | Permite a adição de informações de cabeçalho especificadas à solicitação de pull de origem, como transportar o IP real do cliente. | 30 de junho de 2020 | [Solicitar configuração do cabeçalho](https://intl.cloud.tencent.com/document/product/228/37037) |
| Configuração rápida de HSTS           | Permite adicionar o cabeçalho `strict-transport-security`.                  | 30 de junho de 2020 | [Configuração de HSTS](https://intl.cloud.tencent.com/document/product/228/37036) |
| Configuração de grampeamento OCSP            | Lança a configuração rápida de grampeamento OCSP completa para melhorar a eficiência do handshake TLS e acelerar a autenticação do usuário. | 30 de junho de 2020 |  [Configuração de grampeamento OCSP](https://intl.cloud.tencent.com/document/product/228/35216)|

## Abril de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Otimização de imagens | Permite a habilitação de compressão WebP, Guetzli e TPG para imagens solicitadas e qualificadas, a fim de reduzir efetivamente o tráfego downstream gerado pela transferência de imagens e reduzir custos.| 27 de abril de 2020| Otimização de imagem|
| Ativação manual do serviço CDN global| Libera o serviço de aceleração global para os usuários globais.<br>Os usuários podem ativar o serviço CDN global facilmente no console por conta própria. | 15 de abril de 2020 | [Configuração do CDN do zero](https://intl.cloud.tencent.com/document/product/228/32978) |


## Março de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Funcionalidade de recuperação de nome de domínio atualizada| Permite a resolução e a verificação da propriedade do nome de domínio, a recuperação de nomes de domínio e a conexão de nomes de domínio curinga.  | 3 de março de 2020 | [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734) |
| Nova configuração do tempo limite de pull de origem | Permite o ajuste de períodos de tempo limite para a conexão TCP de pull de origem e o carregamento de dados para garantir um pull de origem normal. | 3 de março de 2020 | [Configuração do tempo limite de pull de origem](https://intl.cloud.tencent.com/document/product/228/35227) |

## Fevereiro de 2020

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Versão beta do serviço de log em tempo real | Os logs de acesso do CDN podem ser coletados e publicados em tempo real para uma rápida recuperação e análise dos dados do log. | 24 de fevereiro de 2020 | [Logs em tempo real](https://intl.cloud.tencent.com/document/product/228/35380) |

## Dezembro de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Global CDN <br>O recurso de relatório mensal de operações é suportado | O recurso de relatório mensal de operações no console do CDN da China continental e do console do CDN no exterior foi mesclado para melhorar a análise do status dos negócios de qualquer mês no ano passado. | 23 de dezembro de 2019 | [Análise de dados](https://intl.cloud.tencent.com/document/product/228/32923) |

## Novembro de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------- | --------------------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN global <br>Limpeza de cache | Oferece suporte ao recurso de limpeza de cache no console para regiões dentro e fora da China continental. | 14 de novembro de 2019 | [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299) |
| CDN global <br>Pré-busca de cache | Oferece suporte ao recurso de pré-busca de cache no console para regiões dentro e fora da China continental. | 14 de novembro de 2019 | [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| CDN global <br>Download de log | Oferece suporte ao download dos logs do CDN no console para regiões dentro e fora da China continental. | 14 de novembro de 2019 | [Download Logs](https://intl.cloud.tencent.com/document/product/228/6316) |

## Outubro de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------- | --------------------------------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Reformulação da página de análise estatística | Após a atualização das APIs de dados do CDN no exterior, a análise de dados será atualizada para a análise de dados global.| 21 de outubro de 2019| [Análise de dados](https://intl.cloud.tencent.com/document/product/228/32923) |

## Maio de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------------------- | -------------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Atualização da ferramenta de autodiagnóstico | Permite o diagnóstico de região e status e a atualização de lista. | 29 de maio de 2019 | [Ferramenta de autodiagnóstico](https://intl.cloud.tencent.com/document/product/228/6304) |

## Abril de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------------------- | ------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN global<br>Permite a marcação no nível de nome de domínio | Acelera a consulta de nomes de domínio e melhora a eficiência do gerenciamento de nomes de domínio. | 16 de abril de 2019 | [Pesquisa de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/32913) |

## Março de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------------------- | ---------------------------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>É possível configurar o limite de largura de banda | Esse recurso evita hotlinking por usuários mal-intencionados que podem gerar grandes quantidades de largura de banda e aumentar drasticamente os custos. | 18 de março de 2019 | [Configuração do limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541) |
| CDN no exterior <br>É possível configurar Range GETs | Melhora muito a eficiência da entrega de arquivos grandes, acelera a resposta e reduz a pressão no servidor de origem. | 18 de março de 2019 | [Configuração de Range GETs](https://intl.cloud.tencent.com/document/product/228/7184) |

## Janeiro de 2019

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------------------------- | ------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Agora, o IPv6 é compatível (em beta) | A aceleração IPv6 foi lançada em beta e é compatível com ISPs em todas as províncias da China continental. | 18 de janeiro de 2019 | [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734) |

## Dezembro de 2018

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Mais opções de proteção de hotlink de carimbo de data/hora são compatíveis | Mais formatos de proteção de hotlink de carimbo de data/hora são aceitos. | 20 de dezembro de 2018 | [Configuração da proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292) |
| CDN da China continental <br>A API para consulta de dados com granularidade de 1 minuto é compatível| Permite consultar os dados faturáveis reais com granularidade de 1 minuto e acessar os dados de monitoramento em tempo real. | 6 de dezembro de 2018 | [DescribeBillingData](https://intl.cloud.tencent.com/document/product/228/37472)<br>[DescribeCdnData](https://intl.cloud.tencent.com/document/product/228/31734) |

## Novembro de 2018

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Reformulação da página de monitoramento de dados | Agora, as principais métricas de monitoramento podem ser facilmente visualizadas. | 30 de novembro de 2018 | [Configuração do painel](https://intl.cloud.tencent.com/document/product/228/32918) |
| CDN no exterior <br>Permite o faturamento por região | Uma zona de faturamento do CDN no exterior é determinada pela região onde o nó de cache do CDN está localizado, e as taxas de serviço do CDN continuarão a ser cobradas com base no uso e preço unitário específico da zona.| 29 de novembro de 2018 | [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949) |
| CDN da China continental <br>Todos os cabeçalhos podem ser armazenados em cache | Permite o armazenamento em cache rápido de todos os cabeçalhos do CDN da China continental. | 29 de novembro de 2018 | [Configuração de cache do cabeçalho HTTP](https://intl.cloud.tencent.com/document/product/228/35319) |

## Maio de 2018

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Várias lógicas de limpeza são aceitas para a limpeza de diretório | Várias lógicas foram adicionadas ao CDN da China continental para ajudar a limpar os recursos armazenados em cache nos nós do CDN regularmente. Os nós vão efetuar pull dos recursos mais recentes do servidor de origem e armazenar em cache novamente. | 31 de maio de 2018 | [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299) |

## Janeiro de 2018

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>É possível configurar a proteção de hotlink de carimbo de data/hora | Ao definir uma política de controle de acesso no valor do campo do referenciador no cabeçalho da solicitação HTTP, a fonte de acesso pode ser restrita para impedir hotlinking por usuários mal-intencionados. | 30 de janeiro de 2018 | [Configuração de proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292) |
| CDN da China continental <br>É possível personalizar a validade do cache do código de status 404 | Permite a configuração personalizada de validade do cache do código de status 404. | 30 de janeiro de 2018 | [Configuração do cache de código de status](https://intl.cloud.tencent.com/document/product/228/35318) |

## Novembro de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------- | ------------------------- | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Ajuste dos prazos para processamento de pagamentos em atraso | Os prazos para processamento de pagamentos em atraso no CDN são ajustados. | 9 de novembro de 2017 | [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/228/2949) |

## Setembro de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>Permite o redirecionamento forçado de HTTPS 301 | Permite a reescrita forçada de todas as solicitações HTTP que chegam no nó do CDN para solicitações HTTPS. Oferece suporte ao redirecionamento 301 permanente. | 30 de setembro de 2017 | [Configuração de redirecionamento forçado](https://intl.cloud.tencent.com/document/product/228/35214) |
| CDN da China continental <br>É possível configurar o período de validade do cache da página inicial | Permite configurar um conjunto de regras de expiração que os nós de cache do CDN devem seguir ao armazenar em cache o conteúdo de negócios. | 30 de setembro de 2017 | [Configuração de validade do cache do nó (herdado)](https://intl.cloud.tencent.com/document/product/228/35317) |

## Julho de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------- | -------------------------------- | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Lançamento do recurso de análise estatística | Essa funcionalidade mantém você informado sobre a distribuição e o uso dos usuários. | 7 de julho de 2017 | [Análise de dados](https://intl.cloud.tencent.com/document/product/228/32923) |

## Abril de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Permite a consulta da região do nó | Permite consultar se um IP especificado pertence a um nó do Tencent Cloud e o status do serviço.| 12 de abril de 2017 | DescribeCdnIp |
| CDN da China continental <br>Permite a consulta de propriedade de IP em lote | Essa funcionalidade permite que você consulte em lote se os IPs especificados pertencem a nós de cache do CDN da China continental e verifique as respectivas regiões de serviço de aceleração, províncias e ISPs. | 12 de abril de 2017 | [Verificar Tencent IP](https://intl.cloud.tencent.com/document/product/228/10747) |
| CDN da China continental <br>Permite a exportação rápida de nomes de domínio | Essa funcionalidade permite que você exporte rapidamente a lista de nomes de domínio do CDN. | 12 de abril de 2017 | [Operações de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5736) |

## Março de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Lançamento da funcionalidade de cache avançado | Essa funcionalidade permite que você ajuste o período de validade do cache do nó dinamicamente, definindo o valor `Max-Age` no cabeçalho de resposta HTTP `Cache-Control` do servidor de origem. | 15 de março de 2017 | [Configuração de validade do cache do nó (herdado)](https://intl.cloud.tencent.com/document/product/228/35317) |



## Janeiro de 2017

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Permite a personalização do cabeçalho HTTP | Essa funcionalidade permite adicionar um cabeçalho personalizado na mensagem de resposta retornada para implementar o acesso entre origens quando um recurso de negócios for solicitado. | 12 de janeiro de 2017 | [Configuração do cabeçalho HTTP](https://intl.cloud.tencent.com/document/product/228/35320) |

## Dezembro de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ----------------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN da China continental <br>É possível configurar o limite de largura de banda para nomes de domínio | Impede hotlinking por usuários mal-intencionados, o que pode aumentar drasticamente o uso da largura de banda e resultar em custos exorbitantes. | 14 de dezembro de 2016 | [Configuração do limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541) |
| CDN da China continental <br>Aceita o redirecionamento forçado de HTTPS | Essa funcionalidade permite especificar um método de redirecionamento e a reescrita forçada de todas as solicitações HTTP que chegam no nó do CDN para solicitações HTTPS.| 14 de dezembro de 2016 | [Configuração de redirecionamento forçado](https://intl.cloud.tencent.com/document/product/228/35214) |
| O CDN da China continental aceita a configuração do servidor de origem principal/secundário | Essa funcionalidade garante a alta disponibilidade de pull de origem. | 14 de dezembro de 2016 | [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289) |
| CDN da China continental <br>Permite a troca entre servidores de origem do cliente e do COS | Essa funcionalidade permite que você altere o tipo do servidor de origem principal do servidor de origem do cliente para o servidor de origem do COS e vice-versa. | 14 de dezembro de 2016 | [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289) |
| CDN da China continental <br>É possível configurar Range GETs | Essa funcionalidade pode melhorar significativamente a eficiência da entrega de arquivos grandes, acelerar as respostas e reduzir a pressão no servidor de origem. | 14 de dezembro de 2016 | [Configuração de Range GETs](https://intl.cloud.tencent.com/document/product/228/7184) |
| CDN no exterior <br>Permite a otimização de pull de origem entre fronteiras | O CDN no exterior permite a otimização de pull de origem entre fronteiras.  | 14 de dezembro de 2016 | [Tipos de dados](https://intl.cloud.tencent.com/document/product/228/31739) |

## Novembro de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>Permite a limpeza e pré-busca             | O CDN no exterior agora oferece suporte aos recursos de limpeza e pré-busca de cache. | 25 de novembro de 2016 | [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299)<br> [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| CDN no exterior <br>Permite o download de log de acesso | Lançamento da funcionalidade de log de acesso do CDN no exterior para ajudar você a analisar o acesso dos usuários. | 25 de novembro de 2016 | [Download Logs](https://intl.cloud.tencent.com/document/product/228/6316) |
| CDN no exterior <br>O servidor de origem do COS é compatível | Os recursos estáticos no COS podem ser conectados ao CDN no exterior para aceleração global e entrega aos clientes usuários. | 1 de novembro de 2016 | [COS como servidor de origem do CDN](https://intl.cloud.tencent.com/document/product/228/32977) |

## Outubro de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| CDN no exterior <br>A aceleração HTTPS é compatível | É possível carregar certificados para implantação ou implantar diretamente certificados hospedados no Serviço de certificados SSL do Tencent Cloud para a plataforma do CDN. Dessa forma, você pode habilitar o serviço de aceleração HTTPS para implementar a transferência de dados criptografados em toda a rede. | 28 de outubro de 2016 | [Guia da configuração de HTTPS](https://intl.cloud.tencent.com/document/product/228/35213) |
| CDN da China continental <br>Permite o monitoramento em tempo real dos dados de pull de origem | Essa funcionalidade permite que você visualize as curvas de monitoramento nas últimas 6 horas com granularidade de 1 minuto.  | 26 de outubro de 2016 | [Monitoramento de pull de origem](https://intl.cloud.tencent.com/document/product/228/32921) |
| Permite a configuração de certificados em lote   | É possível configurar os certificados em lotes no console.   | 26 de outubro de 2016 | [Permissões do console](https://intl.cloud.tencent.com/document/product/228/35229) |

## Setembro de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| É possível configurar o limite de acesso de IP | Ao limitar a quantidade de solicitações de acesso por segundo de um IP cliente a um nó, é possível se defender contra ataques CC de alta frequência e impedir hotlinking por usuários mal-intencionados. | 23 de setembro de 2016 | [Configuração do limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420) |

## Agosto de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| -------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Permite o ajuste de prioridade da regra de validade do cache | É possível ajustar as prioridades de várias regras de validade do cache. | 22 de agosto de 2016 | [Configuração de validade do cache do nó (herdado)](https://intl.cloud.tencent.com/document/product/228/35317) |
| É possível configurar a lista de bloqueio/permissões de IPs | Ao definir uma política de controle de acesso em IPs de solicitações de usuários, é possível restringir efetivamente a fonte de acesso para impedir hotlinking de IPs mal-intencionados e ataques.| 11 de agosto de 2016 | [Configuração da lista de bloqueios de IP/lista de permissões](https://intl.cloud.tencent.com/document/product/228/6298) |
| Suporte à ferramenta de autodiagnóstico | Essa ferramenta permite a detecção da resolução de DNS de nomes de domínio conectados, qualidade de vínculo, status do nó, servidor de origem e consistência de acesso aos dados.| 11 de agosto de 2016 | [Ferramenta de auto-diagnóstico](https://intl.cloud.tencent.com/document/product/228/6304) |

## Julho de 2016

| Atualização | Descrição | Data de lançamento | Documentação |
| --------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Permite a configuração de otimização de SEO   | Essa funcionalidade resolve o problema de pesos incorretos nos resultados da pesquisa de nomes de domínio devido às mudanças frequentes de IP pelo CDN. Ao identificar se um IP de acesso pertence a um mecanismo de pesquisa, é possível optar por efetuar pull do recurso diretamente do servidor de origem, garantindo a estabilidade do peso do mecanismo de pesquisa. | 19 de julho de 2016 | [Configuração da otimização de SEO](https://intl.cloud.tencent.com/document/product/228/35219) |
| Permite a personalização do cabeçalho HTTP | Essa funcionalidade permite adicionar um cabeçalho personalizado na mensagem de resposta retornada para implementar o acesso entre origens quando um recurso de negócios for solicitado. | 19 de julho de 2016 | [Configuração do cabeçalho HTTP](https://intl.cloud.tencent.com/document/product/228/35320) |

## Junho de 2016

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| ------------------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Lançamento da funcionalidade de pré-busca de recursos<br>(Em teste beta)   | O CDN fornece uma funcionalidade de pré-busca de recursos que permite carregar recursos especificados em um nó de cache simplesmente enviando a lista de recursos no console do CDN em vez de esperar que as solicitações do usuário sejam acionadas.| 30 de junho de 2016| [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000) |
| Abertura da entrada para o aplicativo do CDN no exterior <br>(Em teste beta) | Você pode solicitar a habilitação da aceleração do CDN no exterior nesta página. | 30 de junho de 2016 | [Aceleração no exterior](https://intl.cloud.tencent.com/product/cdn)          |
| Lançamento da funcionalidade de relatório operacional mensal do CDN | Seu status de negócios mensal é exibido em várias dimensões para facilitar a análise das operações empresariais.| 13 de junho de 2016|[Análise de dados](https://intl.cloud.tencent.com/document/product/228/32923) |

## Abril de 2016

| Atualização | Descrição | Data de lançamento | Documentação |
| ------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Certificados HTTPS gratuitos de terceiros são fornecidos | É possível acessar o [console do Serviço de certificados SSL](https://console.cloud.tencent.com/ssl) para solicitar um certificado gratuito de terceiros fornecido pela TrustAsia. | 29 de abril de 2016 | [FAQs sobre HTTPS](https://intl.cloud.tencent.com/document/product/228/11206) |

## Março de 2016

| Atualização | Descrição | Data de lançamento | Documentação |
| ------------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| O CDN permite a consulta de propriedade de IP | Essa funcionalidade permite que você verifique se um IP especificado pertence a um nó de cache do CDN da China continental, além das respectivas região de serviço de aceleração, província e ISP. | 4 de março de 2016 | [Verificar IP Tencent](https://intl.cloud.tencent.com/document/product/228/10747) |

## Janeiro de 2016

| Atualização | Descrição | Data de lançamento | Documentação |
| ----------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| O CDN é compatível com o servidor de origem do COS | Os recursos estáticos no COS podem ser conectados ao CDN para aceleração global e entrega aos clientes usuários. | 20 de janeiro de 2016 | [COS como servidor de origem do CDN](https://intl.cloud.tencent.com/document/product/228/32977) |

## Outubro de 2015

| Atualização | Descrição                                               | Data de lançamento   | Documentação                                                     |
| --------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| Lançamento da funcionalidade de monitoramento do status de toda a rede para o CDN | Essa funcionalidade permite que você monitore o status de latência e disponibilidade dos ISPs em todas as províncias da China continental e em cada região fora da China continental. | 10 de outubro de 2015 | [Monitoramento de status de toda a rede](https://intl.cloud.tencent.com/document/product/228/6311) |

## Agosto de 2015

| Atualização | Descrição | Data de lançamento | Documentação |
| -------------------------- | --------------------------------------- | ---------- | ------------------------------------------------------------ |
| Permite a coleta de estatísticas multidimensionais (como código de status de acesso) | É possível coletar as estatísticas de códigos de status 2XX/3XX/4XX/5XX. | 8 de agosto de 2015 | [Monitoramento de acesso](https://intl.cloud.tencent.com/document/product/228/32920) |

## Junho de 2015

| Atualização | Descrição | Data de lançamento | Documentação |
| -------------------- | -------------------- | ---------- | ------------------------------------------------------------ |
| Limpeza de diretório | Os recursos podem ser limpos por diretório. | 12 de junho de 2015 | [Limpeza de cache](https://intl.cloud.tencent.com/document/product/228/6299) |
| Funcionalidade de pré-busca para arquivos grandes | Pode ser feita a pré-busca de arquivos grandes. | 12 de junho de 2015 | [Pré-busca de cache](https://intl.cloud.tencent.com/document/product/228/39000) |

## Maio de 2015

| Atualização | Descrição | Data de lançamento | Documentação |
| ---------------------------------- | ------------------------------------ | ---------- | ------------------------------------------------------------ |
| A validade do cache herda o `cache-control` do servidor de origem | A validade do cache herda o parâmetro `cache-control` do servidor de origem. | 18 de maio de 2015 | [Configuração de validade do cache do nó (herdado)](https://intl.cloud.tencent.com/document/product/228/35317) |

## Abril de 2015

| Atualização | Descrição | Data de lançamento | Documentação |
| ---------------------- | ------------------------------------------------------------ | ---------- | ------------------------------------------------------------ |
| É possível configurar o domínio de origem | O CDN permite a modificação de domínios de origem. | 20 de abril de 2015 | [Configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289) |
| É possível configurar a proteção de hotlink do referenciador | Ao definir uma política de controle de acesso no valor do campo do referenciador no cabeçalho da solicitação HTTP, a fonte de acesso pode ser restringida para impedir hotlinking por usuários mal-intencionados. | 20 de abril de 2015 | [Configuração de proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292) |
| Lançamento de funcionalidades avançadas, como a validade de cache | É possível especificar a validade do cache de recursos de um determinado tipo ou recursos em um determinado diretório ou caminho. | 20 de abril de 2015 | [Configuração de validade do cache do nó (herdado)](https://intl.cloud.tencent.com/document/product/228/35317) |

## Março de 2015

| Atualização | Descrição | Data de lançamento | Documentação |
| ---------------------------------- | ---------------------------------------- | ---------- | ------------------------------------------------------------ |
| O CDN permite a conexão de servidores de origem de clientes e hospedados em FTP | Servidores de origem de clientes e hospedados em FTP são compatíveis. | 15 de março de 2015 | [Adição de nomes de domínio](https://intl.cloud.tencent.com/document/product/228/5734) |
| Faturamento por largura de banda e o faturamento por tráfego permitidos  | O CDN fornece dois modos de faturamento: faturamento por largura de banda e faturamento por tráfego. | 15 de março de 2015 | [Visão geral de faturamento](https://intl.cloud.tencent.com/document/product/228/2949) |















