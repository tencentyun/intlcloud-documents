# Armazenamento regular de logs do CDN

Este documento descreve como usar o SCF do Tencent Cloud para criar duas funções, a fim de armazenar os logs do CDN no COS de forma regular.

# Etapas principais

Este documento descreve como criar as funções de "armazenamento" e "distribuição de tarefas", usá-las juntas e configurar um gatilho de temporizador para armazenar regularmente logs do CDN no COS.

Existem quatro etapas principais:

A. Preparar a chave de acesso da API do Tencent Cloud e as informações do COS

B. Criar a função de armazenamento (cdn-save-log-into-cos)

C. Criar a função de tarefa (cdn-dispatch-log-jobs)

D. Configurar o temporizador

# Instruções

## A. Prepare os seguintes recursos antes de criar as funções

1. Chave de acesso da API do Tencent Cloud

Acesse a [página de gerenciamento de chave de acesso](https://console.cloud.tencent.com/cam/capi), consulte ou crie uma chave e registre as seguintes informações:

Nome da credencial de acesso (`SecretId`), como `AKIDRVI54XXn10r58oZpmzbBOnwt47xO1LRv`

Chave da credencial de acesso (`SecretKey`), como `3t0SYPHRIpjmAAUPfKM8b4yXnff4Aq56`

2. Bucket do COS

Faça login no [console do COS](https://console.cloud.tencent.com/cos), acesse a **Lista de buckets** para consultar ou criar um bucket, acesse o bucket para exibir suas **Informações básicas** e registre as seguintes informações:

Nome do bucket (`Bucket Name`), como `examples-1251002854`

Região do bucket (`Region`), como `ap-chengdu`

## B. Crie a função de armazenamento (cdn-save-log-into-cos)

1. Faça login no [console do SCF](https://console.cloud.tencent.com/scf) e clique em **Function Service (Serviço de funções)**.

2. Selecione **Create (Criar)** e insira **cdn-save-log-into-cos** como o nome da função.

3. Selecione **Function Template (Modelo de função)**, pesquise com a palavra-chave "CDN", selecione o modelo "cdn-save-log-into-cos" e clique em "Next (Avançar)", para acessar a página de configuração da função:
![](https://main.qcloudimg.com/raw/402a01a22ca748386617afd2fc7255a2.png)

4. Clique em **Complete (Concluir)** para criar a função.
![](https://main.qcloudimg.com/raw/69f87dc5f7314f0cdb21f45684b403ed.png)

## C. Crie a função de tarefa (cdn-dispatch-log-jobs)

1. Faça login no [console do SCF](https://console.cloud.tencent.com/scf) e clique em **Create (Criar)**.

2. Selecione **Function Template (Modelo de função)**, pesquise com a palavra-chave "CDN" e selecione o modelo "cdn-dispatch-log-jobs".

3. Insira **cdn-dispatch-log-jobs** como o nome da função e clique em "Next (Avançar)".

4. Clique em **Complete (Concluir)** para criar a função.

![](https://main.qcloudimg.com/raw/b82b157292163ca06b9f43e74bd1a8de.png)

5. Clique na guia **Function Code (Código da função)**. Na caixa de edição do código, modifique o código Python, inserindo as seguintes informações de configuração:

Na variável `config` na linha 143, insira as informações de configuração correspondentes:

- Defina os campos, como `secret_id`, `secret_key`, `cos_region`, `cos_bucket` e `scf_region`.
- Se você definiu o nome da função conforme as instruções na etapa B, e não quiser modificá-lo, mantenha o valor original de `scf_function`.
- O valor padrão de `cdn_host` é uma matriz vazia (ou seja, os logs de todos os nomes de domínio na conta serão armazenados). Se necessário, você pode inserir a lista de nomes de domínio especificados.

![](https://main.qcloudimg.com/raw/8ed596f7843acacc0e3974057922cd0d.png)

6. Clique em **Save (Salvar)**.

7. Clique em **Test (Testar)** para verificar se o código funciona corretamente. Depois que o programa de teste parar de ser executado, você pode acessar o console do COS e verificar se os logs correspondentes foram armazenados no COS.

## D. Configurar o temporizador

Depois de criar as duas funções acima, a lista no console do SCF será a seguinte:

1. Clique em **cdn-dispatch-log-jobs** para acessar seus detalhes.

![](https://main.qcloudimg.com/raw/55382244ab24832e280b040f284cd09a.png)

2. Clique na guia **Trigger Management (Gerenciamento de gatilho)** e clique em **Create a Trigger (Criar um gatilho)**.

![](https://main.qcloudimg.com/raw/36949d35a75f77515caacee834427064.png)

3. Selecione **Scheduled triggering (Acionamento programado)** como o método de acionamento, insira um nome de tarefa programada personalizada, selecione **Every 5 mins (A cada 5 minutos)** como o período de acionamento e clique em **Submit (Enviar)**.

![](https://main.qcloudimg.com/raw/fe157cb0c234693920c3efc36ed9c7e3.png)

Depois de concluir todas as etapas acima, os logs do CDN serão armazenados regularmente no COS.