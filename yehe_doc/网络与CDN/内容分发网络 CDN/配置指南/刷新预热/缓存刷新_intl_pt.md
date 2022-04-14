## Visão geral da funcionalidade

O CDN consegue configurar o cache básico. A validade do cache pode ser configurada de acordo com regras como tipos de serviço especificados, diretórios e URLs específicos para limpar regularmente os recursos armazenados em cache nos nós, efetuar pull dos recursos mais recentes do servidor de origem e armazená-los novamente em cache.

Além disso, o CDN pode limpar o cache de URLs ou diretórios especificados em lotes:

- Limpeza de URL: exclui o cache dos recursos correspondentes em todos os nós do CDN.
- Limpeza de diretório: se você selecionar **Purge updated resources (Limpar os recursos atualizados)**, quando um usuário final acessar um recurso no diretório correspondente, será efetuado o pull das informações de `Last-Modify` do recurso do servidor de origem. Se for as mesmas do recurso em cache, o recurso em cache será retornado diretamente; caso contrário, será efetuado pull do recurso atualizado do servidor de origem e armazenado em cache novamente. Se você selecionar **Purge all resources (Limpar todos os recursos)**, quando o usuário acessar um recurso no diretório correspondente, será efetuado pull da versão mais recente do recurso diretamente do servidor de origem e armazenado em cache novamente.

>? Depois que uma limpeza for executada com êxito, o recurso correspondente no nó não terá um cache válido. Quando o usuário iniciar uma solicitação de acesso novamente, o nó efetua o pull do recurso necessário do servidor de origem e o armazena em cache no próprio nó. Se você enviar uma grande quantidade de tarefas de limpeza, muitos caches serão limpos, resultando em um aumento nas solicitações de pull de origem e alta pressão no servidor de origem.

## Casos de uso

### Novas versões de recursos

Quando um recurso é sobrescrito por um novo recurso com o mesmo nome no servidor de origem, você pode enviar uma solicitação para limpar o URL/diretório e limpar todos os caches para que os usuários possam acessar diretamente a versão mais recente do recurso. Isso impedirá que os usuários acessem a versão herdada do recurso armazenado em cache no nó.

### Limpeza de recursos ilegais

Quando recursos ilegais (como recursos relacionados a pornografia, drogas ou jogos de azar) forem encontrados em seu servidor de origem, eles ainda podem estar acessíveis mesmo depois de excluí-los no servidor de origem por causa do cache de nó. Para proteger a segurança do seu ambiente de rede, é possível excluir os recursos armazenados em cache por meio da limpeza de URL.

## Instruções

### Como usar

Faça login no [Console do CDN](https://console.cloud.tencent.com/cdn), clique em **Purge and Prefetch (Limpeza e pré-busca)** na barra lateral esquerda e envie uma tarefa **Purge URL (Limpeza de URL)** ou **Purge Directory (Limpeza de diretório)**. Você pode limpar URLs/diretórios do CDN e do ECDN juntos.
![](https://main.qcloudimg.com/raw/a3442259ffa50bccb60dabf002ea6dfb.png)
![](https://main.qcloudimg.com/raw/d4b01354bab726ea890e8167ccdbaffe.png)
>? Se a funcionalidade de codificação de URL estiver habilitada, os caracteres chineses serão convertidos para o formato codificado de URL durante a limpeza do URL e do diretório.

<span ID = "notes"></span>
Na guia **History (Histórico)**, é possível consultar tarefas por período, palavra-chave e tipo de tarefa especificados. As consultas de palavras-chave aceitam apenas consultas com um nome de domínio ou um URL/diretório limpo por completo:
![](https://main.qcloudimg.com/raw/86e00c9652a635cf0a0007172119be92.png)

>? O console pode retornar até 10.000 logs por vez, que podem ser exportados para um arquivo do Excel. Se você tiver mais de 10.000 tarefas de limpeza, consulte e exporte-as em lotes.

### Precauções

**Limpeza de URL:**

- Até 10.000 URLs podem ser limpos por dia para cada conta com o serviço de aceleração dentro ou fora da China Continental, e até 1.000 URLs podem ser limpos por vez. Para cada conta que usa o serviço do CDN global, a cota diária de limpeza de URL para o serviço de aceleração dentro e fora da China Continental é de 10.000 cada.
>?	
>- Quando sua cota de limpeza diária estiver acabando, é possível aumentá-la por conta própria no console do CDN do Tencent Cloud.
>- A nova cota entrará em vigor imediatamente. A página será atualizada automaticamente. Não é necessário clicar no botão Atualizar com frequência.
>- A cota só pode ser aumentada uma vez por dia. 
>- O aumento da cota em regiões diferentes é independente um do outro.
- É necessário adicionar o identificador de protocolo "http://" ou "https://" ao enviar uma tarefa de limpeza.
- URLs no formato "http://*.test.com/" não são aceitos. Mesmo se você conectar um nome de domínio curinga ao CDN, será necessário enviar os nomes de subdomínio correspondentes para limpeza.
- Ao enviar URLs para limpeza, os nomes de domínio já devem ter sido conectados ao CDN; caso contrário, o envio falhará.
- Por padrão, os URLs serão limpos por regiões de aceleração de nomes de domínio nos URLs.

**Limpeza de diretório:**

- O limite superior para diretórios limpos é 100 por conta, por dia. O limite é definido para o serviço de aceleração dentro e fora da China Continental separadamente. Até 20 diretórios podem ser limpos por vez. 
- É necessário adicionar o identificador de protocolo "http://" ou "https://" ao enviar uma tarefa de limpeza.
- Diretórios no formato "http://*.test.com/" não podem ser limpos. Mesmo se você conectar um nome de domínio curinga ao CDN, será necessário enviar os nomes de subdomínio correspondentes para limpeza.
- Ao enviar URLs para limpeza, os nomes de domínio já devem ter sido conectados ao CDN; caso contrário, o envio falhará.

**Configuração de permissões de subusuários:**

- A limpeza de diretório, a limpeza de URL e a consulta de histórico de limpeza foram integradas ao sistema de permissões mais recente e aceitam a configuração de permissões no nível de recursos (nomes de domínio).
- Para informações sobre o método de atribuição de permissões, consulte [Permissões do console](https://intl.cloud.tencent.com/document/product/228/35229).

## Casos de uso

### Limpeza de diretório – limpar os recursos atualizados

O nome do domínio de aceleração é `purge-test-1251991073.file.myqcloud.com`, o servidor de origem é o Tencent Cloud Object Storage (COS) e os recursos no servidor de origem são os seguintes:
![](https://main.qcloudimg.com/raw/ed694acc98a8d3114c8a9922f7374a1b.png)

1. Inicie solicitações para acessar os recursos `1.txt` e `2.txt` respectivamente. Os nós a serem atingidos podem ser determinados com base em `X-Cache-Lookup: Hit From Disktank3` e `Server: NWS_SPMid`, os recursos serão retornados diretamente pelos nós:
   ![](https://main.qcloudimg.com/raw/9b307b80e7d1c759bb073eb9f2cf4b6c.png)
   ![](https://main.qcloudimg.com/raw/5fed8bff43d699f47235e5d0db1f2447.png)
2. No servidor de origem, substitua `1.txt` por um arquivo com o mesmo nome, e a hora da última modificação do arquivo muda, enquanto `2.txt` permanece o mesmo:
   ![](https://main.qcloudimg.com/raw/798fd6a984813aa3a16eaf43856ff7c2.png)
   ![](https://main.qcloudimg.com/raw/bc0d40200fbc744ed34d8552a95c5671.png)
3. Inicie as solicitações novamente. Como o cache não expirou, o conteúdo herdado do recurso `1.txt` será acessado:
   ![](https://main.qcloudimg.com/raw/b5769a3d7fddaeadfda229115ac59bb8.png)
4. Envie uma tarefa de limpeza de diretório, selecione **Purge updated resources (Limpar os recursos atualizados)** e aguarde a conclusão da limpeza:
   ![](https://main.qcloudimg.com/raw/31346a963f189187852dde17a4bf0309.png)
5. Após a limpeza ser concluída, devido ao `Last-Modified` de `1.txt` ser alterado, a solicitação será encaminhada ao servidor de origem. Como `2.txt` não foi alterado, mesmo após o envio de uma tarefa de limpeza de diretório, ele ainda será atingido e retornado:
   ![](https://main.qcloudimg.com/raw/0ea8c1e0e7caac970b3875d4b3987687.png)
   ![](https://main.qcloudimg.com/raw/84e599b1c9c655e62497fb4bdc8e7918.png)
