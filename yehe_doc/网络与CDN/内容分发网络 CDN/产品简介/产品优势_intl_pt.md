## Amplas reservas de recursos
### Nós na China Continental
O CDN tem mais de 2 mil nós de cache implantados em todas as províncias da China Continental, com uma largura de banda total reservada de mais de 110 Tbps. Todos são data centers do Tencent Cloud de alto desempenho e segurança com redes de ISPs de ótima qualidade. Além disso, o Tencent Cloud fortaleceu as conexões com a China Mobile, China Unicom, China Telecom e mais de 50 ISPs de pequeno e médio porte, e criou quatro nós centrais para melhorar significativamente o efeito de aceleração do CDN.
![img](https://main.qcloudimg.com/raw/c7af2903e117b831a68bbaaf13967181.png)

### Nós fora da China Continental
O CDN está trabalhando ativamente na aceleração global desde 2017. Em maio de 2021, o CDN tinha mais de 800 nós de cache em mais de 70 países e regiões com uma largura de banda total reservada de mais de 40 Tbps, ajudando sua empresa a se tornar global com facilidade e velocidade.
![image-20200210165753661](https://main.qcloudimg.com/raw/034a95d5f46fb8bf848c0a53dd265611.png)

| Região | Distribuição |
| ------ | ------------------------------------------------------------ |
| Ásia   | Hong Kong (China), Taiwan (China), Macau (China), Japão, Coreia, Vietnã, Singapura, Tailândia, <br/>Filipinas, Malásia, Indonésia, Índia, Turquia, Arábia Saudita, Emirados Árabes Unidos, Mianmar, <br/>Camboja, Iraque, Kuwait, Catar, Omã, Israel, Mongólia |
| América do Norte   | Estados Unidos, Canadá, México                                         |
| América do Sul   | Brasil, Argentina, Colômbia, Peru, Equador, Chile                 |
| Europa   | Reino Unido, Rússia, Alemanha, Itália, Polônia, Suécia, Irlanda, Romênia, <br/>Espanha, Portugal, França, Holanda, Bélgica, Áustria, Dinamarca, Finlândia |
| África   | África do Sul, Egito, Tanzânia                                         |
| Oceania | Austrália, Nova Zelândia                                             |

## Programação inteligente global

Ao acessar recursos, vários fatores, incluindo a rede do ISP, a região do cliente e a largura de banda da rede do servidor de origem do IDC, podem afetar o tempo de resposta e a experiência do usuário.

Por meio do monitoramento em tempo real dos vínculos em toda a rede e usando o sistema de programação e a tecnologia de roteamento inteligente do GSLB de projeto próprio do Tencent Cloud, o CDN programa as solicitações de acesso dos usuários aos nós de extremidade ideais para a aceleração. Isso garante que os usuários tenham acesso aos recursos de forma rápida e estável.

## Configuração rápida
É possível usar o CDN para acelerar seus serviços por meio de um processo de configuração simples e rápido, sem necessidade de modificações adicionais.

Depois de criar sua conta do Tencent Cloud e concluir a verificação de identidade, você pode ativar o serviço do CDN. Não é necessário pagamento antecipado. Adicione seu nome de domínio empresarial no console do CDN e aguarde cerca de cinco minutos para que a configuração do nome de domínio seja distribuída para os nós de cache em toda a rede. Durante esse processo, como o serviço de aceleração ainda não entrou em vigor, sua empresa não será afetada.

Ao habilitar o serviço de aceleração, é necessário modificar a configuração da resolução do CNAME por meio de seu provedor de serviços de nome de domínio. O serviço de aceleração entrará em vigor quando o DNS entrar em vigor.

## Uma variedade de funcionalidades

O CDN vem com um console completo e fácil de usar, no qual você pode alterar os itens de configuração e visualizar os dados de monitoramento conforme necessário:

**Gerenciamento de domínio**
+ É possível adicionar, excluir, ativar e desativar nomes de domínio.
+ É possível alternar as regiões de aceleração e selecionar ""Mainland China (China Continental)"", ""Outside Mainland China (Fora da China Continental)"" ou ""Global"" para o escopo de aceleração.
+ É possível personalizar a página da lista de nomes de domínio para exibir, filtrar e consultar itens de configuração.

**Configuração de domínios**
+ É possível configurar um servidor de origem externo (lista de IPs ou nomes de domínio) ou usar o COS como um servidor de origem. São aceitos round robin, pull de origem ponderado e backup dinâmico do servidor de origem.
+ É possível configurar políticas de controle de acesso personalizadas, como lista de bloqueio/permissões referenciais, lista de bloqueio/permissões de IPs, proteção de hotlink de carimbo de data/hora e limite de frequência de acesso de IPs.
+ É possível personalizar o tempo de expiração do cache do nó, cache do código de status e cache do cabeçalho HTTP.
+ O CDN permite a configuração de otimizações para a vinculação de pull de origem entre fronteiras, os GETs de alcance e o acompanhamento/redirecionamento de pull de origem 301/302.
+ O CDN aceita a aceleração HTTPS, a aceleração HTTP/2 e o redirecionamento forçado de solicitações.
+ É possível configurar o limite de largura de banda e personalizar itens de configuração avançada, como cabeçalho de resposta HTTP, compressão automática e SEO.

**Limpeza de cache**
+ É possível fazer a autolimpeza de todo o cache da rede, bem como a limpeza de diretório e URL.

**Monitoramento em tempo real**
+ O CDN permite o monitoramento em tempo real da largura de banda, do tráfego, da taxa de acerto de tráfego, da quantidade de solicitações e de todos os códigos de status gerados por solicitações de acesso em uma granularidade de 1 minuto. As estatísticas podem ser filtradas por projeto, nome de domínio, província, ISP e protocolo para apresentar uma visão abrangente do status do serviço.
+ O CDN permite o monitoramento em tempo real da largura de banda do pull de origem, do tráfego, da quantidade de solicitações, da taxa de falha e de todos os códigos de status gerados por solicitações de pull de origem em uma granularidade de 1 minuto. As estatísticas podem ser filtradas por projeto ou nome de domínio para ajudá-lo a visualizar o status do servidor de origem com praticidade.
+ É possível visualizar relatórios em tempo real da distribuição de usuários por região internacionalmente ou por ISP na China Continental.
+ O CDN fornece relatórios operacionais diários, semanais e mensais para manter você atualizado sobre as flutuações dos negócios.

**Serviço de registro em log**
+ Todos os logs gerados por solicitações de acesso são agrupados por hora e podem ser baixados.
+ Os logs de acesso ao CDN podem ser coletados e publicados em tempo real para pesquisar e analisar os dados do log rapidamente.

**APIs do CDN**
O CDN fornece [APIs](https://intl.cloud.tencent.com/document/product/228/31719) para todas as funcionalidades compatíveis listadas acima a fim de permitir o uso de serviço personalizado. Você e sua equipe podem gerenciar, monitorar, exibir e analisar seus negócios com praticidade por meio dessas APIs.
