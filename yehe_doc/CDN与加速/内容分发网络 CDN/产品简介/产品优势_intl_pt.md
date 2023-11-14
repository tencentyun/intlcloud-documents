## Amplas reservas de recursos

O CDN da Tencent Cloud tem uma sólidas reservas de recursos com mais de 2.800 nós de cache em mais de 70 países e regiões, uma largura de banda total reservada de mais de 160 Tbps e mais de 100 milhões de conexões ativas, ajudando a proteger seus negócios.

### Nós na China continental

O CDN tem mais de 2.000 nós de cache implantados em todas as províncias da China continental, com uma largura de banda total reservada de mais de 110 Tbps. Todos são data centers do Tencent Cloud de alto desempenho e segurança com redes de ISPs de ótima qualidade. Além disso, o Tencent Cloud fortaleceu as conexões com a China Mobile, China Unicom, China Telecom e mais de 50 ISPs de pequeno e médio porte, e criou quatro nós centrais para melhorar significativamente o efeito de aceleração do CDN.
![img](https://main.qcloudimg.com/raw/c7af2903e117b831a68bbaaf13967181.png)

| Região | Distribuição |
| :--- | :----------------------------------------------------------- |
| Leste da China | Xangai, Jiangsu, Zhejiang, Anhui, Jiangxi, Shandong, Fujian       |
| Norte da China | Pequim, Tianjin, Shanxi, Hebei, Mongólia Interior             |
| China central | Henan, Hubei, Hunan                                       |
| Noroeste da China | Shaanxi, Gansu, Qinghai, Ningxia, Xinjiang, oeste da Mongólia Interior |
| Sul da China | Guangdong, Hainan, Guangxi                               |
| Sudoeste da China | Chongqing, Sichuan, Guizhou, Yunnan, Tibete                   |
| Nordeste da China | Heilongjiang, Jilin, Liaoning, leste da Mongólia Interior                   |

### Nós fora da China continental

O CDN vem trabalhando diligentemente na aceleração global desde 2017. Desde maio de 2021, o CDN conta com mais de 8,00 nós de cache em mais de 70 países e regiões com uma largura de banda total reservada de mais de 50 Tbps, ajudando sua empresa a se tornar global de forma fácil e rápida.
![image-20200210165753661](https://main.qcloudimg.com/raw/034a95d5f46fb8bf848c0a53dd265611.png)

| Região | Distribuição |
| :----- | :----------------------------------------------------------- |
| América do Norte | Estados Unidos, México, Canadá |
| América do Sul | Brasil, Colômbia, Peru, Equador, Chile, Argentina |
| Ásia | Hong Kong (China), Macau (China), Taiwan (China), Japão, Coreia do Sul, Mongólia, Vietnã, Laos, Singapura, Tailândia, Filipinas, Mianmar, Camboja, Malásia, Indonésia, Índia, Bangladesh, Nepal, Paquistão, Kuwait , Quirguistão, Catar, Israel, Turquia, Iraque, Arábia Saudita, Omã, Emirados Árabes Unidos, Bahrein, Líbano |
| África | Djibuti, Quênia, Madagascar, Ilhas Maurício, Egito, África do Sul |
| Oceania | Austrália, Nova Zelândia                                             |
| Europa | Itália, Áustria, Polônia, Finlândia, Dinamarca, Bélgica, Suécia, Espanha, França, Holanda, Alemanha, Reino Unido |

## Programação inteligente global

Ao acessar recursos, vários fatores, incluindo a rede de ISP, a região do cliente e a largura de banda da rede do servidor de origem do IDC, podem afetar o tempo de resposta e a experiência do usuário.

Por meio do monitoramento em tempo real dos vínculos em toda a rede e usando o sistema de programação e a tecnologia de roteamento inteligente do GSLB, de projeto próprio do Tencent Cloud, o CDN programa as solicitações de acesso dos usuários aos nós de borda ideais para a aceleração. Isso garante para os usuários acesso rápido e estável a recursos.

## Configuração rápida

Você pode usar o CDN para acelerar seus serviços por meio de um processo de configuração simples e rápido, sem necessidade de modificações adicionais.

Depois de criar sua conta do Tencent Cloud e concluir a verificação de identidade, você pode ativar o serviço do CDN. Não é necessário pagamento antecipado. Adicione seu nome de domínio empresarial no console do CDN e aguarde cerca de cinco minutos para que a configuração do nome de domínio seja distribuída para os nós de cache em toda a rede. Durante esse processo, como o serviço de aceleração ainda não entrou em vigor, sua empresa não será afetada.

Ao habilitar o serviço de aceleração, é necessário modificar a configuração da resolução do CNAME por meio de seu provedor de serviços de nome de domínio. O serviço de aceleração entrará em vigor quando o DNS entrar em vigor.

## Uma variedade de funcionalidades

O CDN vem com um console completo e fácil de usar no qual você pode alterar os itens de configuração e visualizar os dados de monitoramento conforme necessário:

**Gerenciamento de domínio**

- É possível adicionar, excluir, ativar e desativar nomes de domínio.
- É possível alternar as regiões de aceleração e selecionar "Mainland China (China continental)", "Outside Mainland China (Fora da China continental)" ou "Global" para o escopo de aceleração.
- É possível personalizar a página da lista de nomes de domínio para exibir, filtrar e consultar itens de configuração.

**Configuração de domínios**

- É possível configurar um servidor de origem externo (lista de IPs ou nomes de domínio) ou usar o COS como um servidor de origem. São aceitos round robin, pull de origem ponderado e backup dinâmico do servidor de origem.
- É possível configurar políticas de controle de acesso personalizadas, como lista de bloqueio/lista de desbloqueio do referenciador, lista de bloqueio/lista de desbloqueio de IP, proteção de hotlink de carimbo de data/hora e limite de frequência de acesso de IP.
- É possível personalizar o tempo de expiração do cache do nó, cache do código de status e cache do cabeçalho HTTP.
- O CDN permite a configuração de otimizações para a vinculação de pull de origem entre fronteiras, os Range GETs e o acompanhamento/redirecionamento de pull de origem 301/302.
- O CDN aceita a aceleração HTTPS, a aceleração HTTP/2 e o redirecionamento forçado de solicitações.
- É possível configurar o limite de largura de banda e personalizar itens de configuração avançada, como cabeçalho de resposta HTTP, compressão automática e SEO.

**Limpeza de cache**

- É possível fazer a autolimpeza do cache de toda a rede, bem como a limpeza de diretório e URL.

**Monitoramento em tempo real**

- O CDN permite o monitoramento em tempo real da largura de banda, do tráfego, da taxa de acerto de tráfego, da quantidade de solicitações e de todos os códigos de status gerados por solicitações de acesso em uma granularidade de 1 minuto. As estatísticas podem ser filtradas por projeto, nome de domínio, província, ISP e protocolo para apresentar uma visão abrangente do status do serviço.
- O CDN permite o monitoramento em tempo real da largura de banda do pull de origem, do tráfego, da quantidade de solicitações, da taxa de falha e de todos os códigos de status gerados por solicitações de pull de origem em uma granularidade de 1 minuto. As estatísticas podem ser filtradas por projeto ou nome de domínio para ajudá-lo a visualizar convenientemente o status do servidor de origem.
- É possível visualizar relatórios em tempo real da distribuição de usuários por região, internacionalmente, ou por ISP na China continental.
- O CDN fornece relatórios operacionais diários, semanais e mensais para manter você atualizado sobre as flutuações dos negócios.

**Serviço de log**

- Todos os logs gerados por solicitações de acesso são agrupados por hora e podem ser baixados.
- Os logs de acesso do CDN podem ser coletados e publicados em tempo real para pesquisar e analisar os dados de log rapidamente.

**APIs do CDN**
O CDN fornece [APIs](https://intl.cloud.tencent.com/document/product/228/31719) para todos os recursos compatíveis listados acima, proporcionando o uso personalizado do serviço. Você e sua equipe podem gerenciar, monitorar, exibir e analisar os seus negócios, de modo conveniente, através dessas APIs.
