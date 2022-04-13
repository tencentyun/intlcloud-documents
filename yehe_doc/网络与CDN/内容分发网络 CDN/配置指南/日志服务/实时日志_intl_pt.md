<blockquote class="d-mod-alarm">
              <div class="d-mod-title d-alarm-title">
                <i class="d-icon-alarm"></i>Aviso:
              </div>
               <p>O valor do campo "HTTP/3" para o identificador de protocolo HTTP em logs gerais estará na versão beta a partir de 13 de setembro de 2021, o que não afetará o console e as APIs do CDN. Observe que obter dados de log de pacotes de log offline pode exigir ajustes.</br></br>O acesso QUIC está na versão beta. Para obter mais detalhes, consulte <a href="https://cloud.tencent.com/document/product/228/51800">QUIC</a>.</p>
            </blockquote>



## Funcionalidades

O CDN pode coletar e publicar logs de acesso em tempo real, permitindo a recuperação e análise rápidas dos dados de log. Você pode acessar rapidamente serviços de registro em log completos, estáveis e confiáveis em um só lugar, como coleta, armazenamento e pesquisa de logs no console do CDN.

>? 
> - Os Logs em tempo real foram lançados oficialmente. Você pode fazer login no console com uma conta raiz e ativar essa funcionalidade. Observe que é preciso concluir a autorização e ativar o [Cloud Log Service](https://console.cloud.tencent.com/cls/search?region=ap-shanghai) antes do primeiro uso.
>- Atualmente, os Logs em tempo real não são compatíveis com o envio de logs em regiões fora da China continental.
>- Os Logs em tempo real só podem ser ativados com uma conta raiz.
>- Os nomes de domínio do CDN e do ECDN não podem ser adicionados ao mesmo tópico de log.

## Casos de uso
Essa funcionalidade pode ser usada para visualizar e analisar o acesso dos usuários em tempo real.

## Conceitos
### Conjunto de logs
Um conjunto de logs é uma unidade de gerenciamento de projeto no serviço de log. Ele é usado para distinguir entre logs de projetos diferentes e corresponde a um item ou aplicativo. O conjunto de logs do CDN tem os seguintes atributos básicos:
+ Nome do conjunto de log: cdn_logset
+ Região: a [região](https://intl.cloud.tencent.com/document/product/614/18940) à qual o conjunto de logs pertence
+ Período de retenção: o período de retenção de dados no conjunto de logs atual
+ Hora de criação: hora de criação do conjunto de logs

### Tópico de log
Um tópico de log é a unidade básica de gerenciamento no serviço de log. Um conjunto de logs pode conter vários tópicos de log e um tópico de log corresponde a um tipo de aplicativo ou serviço. Recomendamos que você colete logs semelhantes em máquinas diferentes no mesmo tópico de log. Por exemplo, se um projeto empresarial tem três tipos de logs: log de operação, log de aplicativo e log de acesso, você pode criar um tópico de log para cada tipo de log.

O sistema de serviço de log gerencia dados de log diferentes com base em tópicos de log diferentes. Cada tópico de log pode ser configurado com fontes de dados, regras de índice e regras de envio diferentes. Portanto, um tópico de log é a unidade básica para configurar e gerenciar dados de log no serviço de log. Criado um tópico de log, é necessário configurar as regras correspondentes antes de realizar a coleta, pesquisa, análise e envio de logs.

As funcionalidades do tópico de log incluem:
- Coletar logs para tópicos de log.
- Armazenar e gerenciar logs com base em tópicos de log.
- Pesquisar e analisar logs por tópicos de log.
- Enviar logs para outras plataformas com base em tópicos de log.
- Baixar e consumir logs de tópicos de log.

## Instruções
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), clique em **Log Service (Serviço de log)** na barra lateral esquerda e abra a guia **Real-time Log (Logs em tempo real)** para criar o envio de logs em tempo real.
![](https://main.qcloudimg.com/raw/d6f22b7194f2e3433f9bbee4f4e4a1dc.png)

### Criação de um tópico de log
Clique em **Create (Criar)** para criar um tópico de log.
>! Um conjunto de logs pode conter até 50 tópicos de log.
>
![](https://main.qcloudimg.com/raw/94136aa047219848f82948e19cd8dc06.png)

### Configuração de um tópico de log
Insira o nome do novo tópico de log e selecione os nomes de domínio a serem vinculados a esse tópico.
>!
>- O nome do tópico deve ser único.
>- Um nome de domínio pode ser vinculado a apenas um tópico de log.
A configuração terá efeito em cerca 15 minutos.
>
![](https://main.qcloudimg.com/raw/6e820577732ecc679aae25386683c57e.png)

### Gerenciamento de um tópico de logs
Depois de configurar com êxito um tópico de log, você pode gerenciá-lo conforme necessário. Especificamente, você pode parar/iniciar o envio de logs para o tópico de log, pesquisar logs no tópico de log, gerenciar ou excluir o tópico de log.
![](https://main.qcloudimg.com/raw/46d8293f0819b693b4b17fa6a79ca78c.png)

#### Parada/Início do envio de logs
Você pode parar ou iniciar o envio de logs manualmente para um tópico de logs.
>!
>- Depois que o envio a um tópico de logs for interrompido, este não receberá mais nenhum dos logs dos nomes de domínio vinculados. Os logs que já tiverem sido enviados serão retidos. Essa operação terá efeito em cerca de 5 a 15 minutos.
>- Depois que o envio para um tópico de log for iniciado, todos os logs dos nomes de domínio vinculados serão enviados para ele. Essa operação terá efeito em cerca de 5 a 15 minutos.

#### Pesquisa de logs
É possível pesquisar logs por tópico de log. Selecione um tópico de log desejado e clique em **Search (Pesquisar)** para acessar a página de pesquisa de log.
+ Intervalo de tempo: é possível pesquisar os dados de log registrados hoje, durante um intervalo de 24 horas (um dos últimos 7 dias) e durante os últimos 7 dias.
+ Classificação: é possível classificar os logs em ordem decrescente ou crescente por tempo de log.
+ Pesquisa: é possível pesquisar logs por texto completo, valores-chave ou palavras-chave difusas. Para obter mais informações, consulte [Sintaxe de pesquisa do CLS herdada](https://intl.cloud.tencent.com/document/product/614/37882). Para obter mais funcionalidades de pesquisa e análise, use o [Cloud Log Service](https://console.cloud.tencent.com/cls/search?region=ap-shanghai).

![](https://main.qcloudimg.com/raw/dbc8e4aa6ae93062c22cadf4b9373e64.png)


#### Gerenciamento
É possível gerenciar um tópico de log criado e atualizar a lista de nomes de domínio vinculados a ele.
>? A nova configuração entrará em vigor dentro de 5 a 15 minutos.
>
![](https://main.qcloudimg.com/raw/ce1f6df0d8bde8ce66f7ebfb4a233e6e.png)

#### Excluindo tópicos de log
É possível excluir tópicos de log manualmente.
>! Depois que um tópico de log é excluído, ele deixa de aceitar o envio de novos logs dos nomes de domínio vinculados e limpa completamente todos os logs que contém. Esta operação terá efeito em cerca de 5 a 15 minutos.

### Descrição dos dados de log

| Campo do log      | Tipo de log bruto | Tipo de serviço de log | Descrição                                                         |
| ------------- | ------------ | ------------ | ------------------------------------------------------------ |
| app_id        | Integer      | long         | `APPID` da conta da Tencent Cloud                                             |
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
| referer       | String       | text         | Informação de referenciador, ou seja, endereço de origem HTTP                                 |
| request_range | String       | text         | Parâmetro de intervalo, ou seja, intervalo de solicitações                                         |
| request_time  | Integer      | long         | Tempo de resposta (em milissegundos), que se refere ao tempo que um nó leva para retornar todos os pacotes ao cliente depois de receber uma solicitação.|
| request_port  | String      | long         |  Porta que conecta o cliente e os nós do CDN. Este campo será exibido como `-` se a porta não existir. |
| rsp_size      | Integer      | long         | Quantidade de bytes retornados                                                   |
| time          | Integer      | long         | Carimbo de data/hora das solicitações no formato UNIX (em segundos)                                        |
| ua            | String       | text         | Informações do `User-Agent`                                              |
| url           | String       | text         | Caminho da solicitação                                                     |
| uuid          | String       | text         | ID exclusivo de solicitação                                               |
| version       | Integer      | long         | Versão de log em tempo real do CDN                                                    |
