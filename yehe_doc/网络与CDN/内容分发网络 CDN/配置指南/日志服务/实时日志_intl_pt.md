## Visão geral da funcionalidade

O CDN pode coletar e publicar logs de acesso em tempo real, permitindo a recuperação e análise rápidas dos dados de log. Você pode acessar rapidamente serviços de registro em log completos, estáveis e confiáveis, como coleta, armazenamento e pesquisa de logs no console do CDN.

>? 
> - Os logs em tempo real foram lançados oficialmente. Você pode fazer login no console com uma conta raiz e ativar essa funcionalidade. Primeiro, você precisa concluir a autorização e ativar o [Cloud Log Service](https://console.cloud.tencent.com/cls/search?region=ap-shanghai).
>- Atualmente, os logs em tempo real não são compatíveis com o envio de logs em regiões fora da China Continental.
>- Os logs em tempo real só podem ser ativados com uma conta raiz.

## Visão geral
Essa funcionalidade pode ser usada para visualizar e analisar o acesso dos usuários em tempo real.

## Conceitos
### Conjunto de logs
Um conjunto de logs é uma unidade de gerenciamento de projeto no serviço de log. Ele é usado para distinguir entre logs de projetos diferentes e corresponde a um item ou aplicativo. O conjunto de logs do CDN tem os seguintes atributos básicos:
+ Nome do conjunto de log: cdn_logset
+ Região: a [região](https://intl.cloud.tencent.com/document/product/614/18940) à qual o conjunto de logs pertence
+ Período de retenção: o período de retenção de dados no conjunto de logs atual
+ Hora de criação: hora de criação do conjunto de logs

### Tópico de logs
Um tópico de logs é a unidade básica de gerenciamento no serviço de log. Um conjunto de logs pode conter vários tópicos de logs e um tópico de logs corresponde a um tipo de aplicativo ou serviço. Recomendamos que você colete logs semelhantes em máquinas diferentes no mesmo tópico de logs. Por exemplo, se um projeto empresarial tem três tipos de logs: log de operação, log de aplicativo e log de acesso, você pode criar um tópico de logs para cada tipo de log.

O sistema de serviço de log gerencia dados de log diferentes com base em tópicos de logs diferentes. Cada tópico de logs pode ser configurado com fontes de dados, regras de índice e regras de envio diferentes. Portanto, um tópico de logs é a unidade básica para configurar e gerenciar dados de logs no serviço de log. Primeiro, é necessário configurar as regras correspondentes, depois de criar um tópico de logs, antes de realizar a coleta, pesquisa, análise e envio de logs.

As funcionalidades do tópico de logs incluem:
- Coletar logs para tópicos de logs.
- Armazenar e gerenciar logs com base em tópicos de logs.
- Pesquisar e analisar logs por tópicos de logs.
- Enviar logs para outras plataformas com base em tópicos de logs.
- Baixar e consumir logs de tópicos de logs.

## Guia de operação
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Log Service (Serviço de log)** na barra lateral esquerda e abra a guia **Real-time Log (Logs em tempo real)** para criar o envio de logs em tempo real.
![](https://main.qcloudimg.com/raw/d6f22b7194f2e3433f9bbee4f4e4a1dc.png)

### Criação de um tópico de logs
Clique em **Create (Criar)** para criar um tópico de logs.
>! Até 10 tópicos de logs podem ser criados em um conjunto de logs.

![](https://main.qcloudimg.com/raw/94136aa047219848f82948e19cd8dc06.png)

### Configuração de um tópico de logs
Insira o nome do novo tópico de logs e selecione os nomes de domínio a serem vinculados a esse tópico.
>!
>- O nome do novo tópico de logs não pode ser igual ao nome de nenhum tópico de logs existente.
>- Um nome de domínio pode ser vinculado a apenas um tópico de logs.
>- Após as informações de configuração serem salvas, a configuração leva cerca de 15 minutos para entrar em vigor.

![](https://main.qcloudimg.com/raw/6e820577732ecc679aae25386683c57e.png)

### Gerenciamento de um tópico de logs
Depois de configurar um tópico de logs, é possível gerenciá-lo. Especificamente, você pode parar/iniciar o envio de logs para o tópico, pesquisar logs no tópico, além de gerenciar ou excluir o tópico de logs.
![](https://main.qcloudimg.com/raw/46d8293f0819b693b4b17fa6a79ca78c.png)

#### Parada/Início do envio de logs
É possível parar/iniciar o envio de logs manualmente para um tópico de logs.
>!
>- Depois que o envio para um tópico de logs for interrompido, todos os logs dos nomes de domínio vinculados ao tópico de logs não serão mais enviados para ele. Os logs que já foram enviados para ele serão retidos. Essa operação terá efeito em cerca de 5 a 15 minutos.
>- Depois que um tópico de logs for iniciado, todos os logs dos nomes de domínio vinculados ao tópico de logs serão enviados para ele. Essa operação terá efeito em cerca de 5 a 15 minutos.

#### Pesquisa
É possível pesquisar logs por tópico de logs. Selecione um tópico de logs desejado e clique em **Search (Pesquisar)** para acessar a página de pesquisa de logs.
+ Intervalo de tempo: é possível pesquisar os dados de log registrados hoje, durante um intervalo de 24 horas (um dos últimos 7 dias) e durante os últimos 7 dias.
+ Classificação: é possível classificar os logs em ordem decrescente ou crescente por tempo de log.
+ Pesquisa: é possível pesquisar por texto completo, valores-chave ou palavras-chave difusas. Para obter mais informações, consulte [Sintaxe de pesquisa do CLS herdada](https://intl.cloud.tencent.com/document/product/614/37882). Para obter mais funcionalidades de pesquisa e análise, use o [Cloud Log Service](https://console.cloud.tencent.com/cls/search?region=ap-shanghai).

![](https://main.qcloudimg.com/raw/dbc8e4aa6ae93062c22cadf4b9373e64.png)


#### Gerenciamento
É possível gerenciar um tópico de logs criado e atualizar a lista de nomes de domínio vinculados a ele.
>? A nova configuração entrará em vigor em 5 a 15 minutos.
>
![](https://main.qcloudimg.com/raw/ce1f6df0d8bde8ce66f7ebfb4a233e6e.png)

#### Exclusão
É possível excluir tópicos de logs manualmente.
>! Depois que um tópico de logs for excluído, todos os logs dos nomes de domínio vinculados ao tópico não serão mais enviados para ele e os logs que já foram enviados para o tópico serão todos apagados. Essa operação terá efeito em cerca de 5 a 15 minutos.

### Descrição dos dados de log

| Campo do log | Tipo de log bruto | Tipo de serviço de log | Descrição |
| ------------- | ------------ | ------------ | ------------------------------------------------------------ |
| app_id        | Integer      | long         | `APPID` da conta do Tencent Cloud                                             |
| client_ip     | String       | text         | IP do cliente                                                    |
| file_size     | Integer      | long         | Tamanho do arquivo                                                     |
| hit           | String       | text         | Acertos/erros do cache. Os acertos em servidores de borda e nós pais do CDN são marcados como acertos |
| host          | String       | text         | Nome de domínio                                                         |
| http_code     | Integer      | long         | Código de status HTTP                                                  |
| isp           | String       | text         | ISP                                                       |
| method        | String       | text         | Método HTTP                                                  |
| param         | String       | text         | Parâmetro transportado em URL                                               |
| proto         | String       | text         | Identificador de protocolo HTTP                                                |
| prov          | String       | text         | Província do ISP                                                   |
| referer       | String       | text         | Informação de referência, ou seja, endereço de origem HTTP                                 |
| request_range | String       | text         | Parâmetro de intervalo, ou seja, intervalo de solicitações                                         |
| request_time  | Integer      | long         | Tempo de resposta (em milissegundos), que se refere ao tempo que um nó leva para responder a um cliente com todos os pacotes de retorno após receber uma solicitação |
| rsp_size      | Integer      | long         | Quantidade de bytes retornados                                                   |
| time          | Integer      | long         | Carimbo de data/hora das solicitações no formato UNIX                                        |
| ua            | String       | text         | Informações do `agente do usuário`                                              |
| url           | String       | text         | Caminho da solicitação                                                     |
| uuid          | String       | text         | ID exclusivo de solicitação                                               |
| version       | Integer      | long         | Versão dos logs em tempo real do CDN                                                    |
