<style> 
table th:nth-of-type(1) { width:20%; } 
table th:nth-of-type(2){ width:80%; } 
</style>




Este guia o ajudará a evitar custos extras decorrentes de largura de banda e tráfego extensos em função de ataques maliciosos e hotlinking.

## Controle de acesso

É recomendável ativar o controle de acesso (gratuitamente) para seus nomes de domínio no console, evitando o desperdício de largura de banda.

| Item                                                   | Descrição                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Proteção de hotlink](https://intl.cloud.tencent.com/document/product/228/6292) | Configure uma política de controle de acesso com base no valor do campo do referenciador no cabeçalho da solicitação HTTP, para restringir as fontes de acesso e evitar hotlinks maliciosos. |
| [ Lista de bloqueio/permissão de IP](https://intl.cloud.tencent.com/document/product/228/6298) | Ao definir uma política de controle de acesso baseada em IPs de solicitantes, é possível restringir a origem de acesso para impedir hotlinking e ataques de IPs mal-intencionados. |
| [Limite de acesso de IP](https://intl.cloud.tencent.com/document/product/228/6420) | Ao limitar a quantidade de solicitações de acesso por segundo de um IP cliente a um nó, é possível se defender contra ataques CC de alta frequência e hotlinking por usuários mal-intencionados. |
| [Configuração de autenticação](https://intl.cloud.tencent.com/document/product/228/35237) | Quando a autenticação é configurada, o cliente precisa calcular a assinatura conforme configurada e adicioná-la a uma solicitação enviada ao servidor. O nó do CDN permite a solicitação quando a assinatura é autenticada. |
| [Lista de bloqueio/lista de permissões do UA](https://intl.cloud.tencent.com/document/product/228/37256) | Determina se uma solicitação deve ser permitida com base no `User-Agent` do cabeçalho da solicitação HTTP. |
| [Limite de velocidade de downstream](https://intl.cloud.tencent.com/document/product/228/37257) | Controla a largura de banda de downstream do CDN definindo a velocidade máxima da taxa de transferência de um URL em um servidor.|

## Gestão de tráfego

Recomendamos que você ative o gerenciamento de tráfego e largura de banda gratuitamente para monitorar o tráfego e o uso de largura de banda do seu nome de domínio e receber mensagens de alarme.

| Item                                                   | Descrição                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541) | Você pode configurar um limite superior para o uso da largura de banda do seu nome de domínio. Quando a largura de banda gerada em um período de amostra (5 minutos) exceder o valor que você definiu, as solicitações serão encaminhadas à força para o servidor de origem ou o serviço CDN será suspenso (um erro 404 será retornado para todas as solicitações) para evitar cobranças extras. |
| [Monitoramento](https://console.cloud.tencent.com/monitor/overview) | O Cloud Monitor ajuda a monitorar seus nomes de domínio do CDN e uso de tráfego. Ele também suporta alertas via SMS, e-mail e WeChat se o limite de uso for atingido, permitindo identificar riscos potenciais em tempo hábil. |
| [Gerenciamento de pacotes de tráfego](https://console.cloud.tencent.com/cdn/package)  | Se você usar o método de cobrança por tráfego, poderá definir as políticas de alarme em **Traffic Pack Management (Gerenciamento de pacotes de tráfego)** no console. Uma mensagem de alarme será enviada quando o tráfego restante ficar abaixo do limite. |

## Proteção de segurança

Para proteger sua empresa contra possíveis ataques, é recomendável ativar o SCDN. Ele ajuda a derrotar ataques cibernéticos em todos os aspectos usando limpeza de DDoS, identificação adaptável de CC, proteção WAF inteligente e análise de bot.

Para nomes de domínio conectados ao CDN do Tencent Cloud, você pode habilitar o SCDN facilmente para manter sua empresa longe de ataques da Web, DDoS e CC.

| Recurso         | Descrição |
| :--------------- | :----------------------------------------------------------- |
| Limpeza distribuída | Apoiado por mais de 1.100 nós CDN qualificados e o módulo de limpeza de alto desempenho, esse recurso protege contra vários ataques de tráfego, como inundações de SYN, TCP e ICMP, limpando-os com precisão usando um algoritmo avançado de reconhecimento de recursos. Um único nó aproveitando os data centers Anti-DDoS do Tencent Cloud pode derrotar até 1 Tbps de ataques DDoS. |
| Identificação de ataque CC | Adota tecnologias inteligentes e patenteadas de bloqueio e identificação de ataques CC. Combinando as políticas de bloqueio padrão e as regras personalizadas, os usuários podem filtrar solicitações de acesso mal-intencionado configurando a frequência e o limite de tráfego. |
| Proteção WAF inteligente    | Esse recurso, baseado nas amostras massivas de ataques na web da Tencent, oferece suporte ao discernimento entre as boas solicitações de acesso e as ruins e protege seu servidor real contra ataques da web, incluindo injeção de SQL, ataques XSS e inclusão de arquivos locais em tempo real. Com o mecanismo de IA autodesenvolvido que incorpora a inteligência contra ameaças da Tencent no nível de bilhões, podem ser implementadas a identificação e o bloqueio mais precisos e eficazes de ameaças da Web. |
| Análise de bot     | Integrando-se às regras WAF baseadas em IA do Tencent Cloud, esse recurso oferece suporte à análise de solicitações de aceleração, discernindo entre os bons bots e os ruins e gerenciando regras personalizadas. Ele fornece uma biblioteca de bots que abrange vários bots conhecidos de anúncios, ferramentas de captura de tela, mecanismos de pesquisa, monitoramento de sites e consulta de links e uma tecnologia de IA exclusiva para modelagem de comportamento do usuário e determinação da origem de tráfego anormal. |
| Controle de acesso avançado     | Além das regras básicas definidas com base em IP, lista de bloqueio/permissão de referenciador e UA, esse recurso suporta a criação de uma regra de controle de acesso complexa especificando campos como IP do cliente, URI, referenciador, agente do usuário e parâmetros. A regra também pode ser adaptada a diferentes cenários de aplicação, definindo uma combinação de condições (igual a, incluir ou excluir). |


