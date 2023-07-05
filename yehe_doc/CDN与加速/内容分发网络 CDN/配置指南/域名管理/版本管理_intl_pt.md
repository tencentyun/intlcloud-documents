
## Funcionalidades

O CDN do Tencent Cloud permite o gerenciamento de versões para um único nome de domínio. É possível criar uma configuração para cada versão de nome de domínio e implantá-la no ambiente de produção e no ambiente de preparo.

- Ambiente de produção: o ambiente ativo onde os serviços de aceleração são colocados em operação.
- Ambiente de preparo: uma área restrita para testar apenas as configurações de nome de domínio. Este ambiente é criado em pequena escala e deve ser usado apenas para testes de configuração de nome de domínio no console. Não deve ser usado para a execução de negócios reais ou testes de desempenho.

>!
>1. A região de aceleração deve estar na China Continental. O nome de domínio não deve usar certificados externos e a funcionalidade [Otimização de imagens](https://cloud.tencent.com/document/product/228/43121) não deve ser ativada.
>2. Apenas uma versão pode ser implantada por vez em cada ambiente.
>3. A atualização de URL é aceita no ambiente de produção e no ambiente de preparo, já a atualização do diretório e a pré-busca de URL são permitidas apenas no ambiente de produção. Para obter mais informações, consulte [Limpeza e pré-busca](https://intl.cloud.tencent.com/document/product/228/6299).
>4. Recursos de monitoramento de dados e uso, como [configuração de limite de largura de banda](https://intl.cloud.tencent.com/document/product/228/7541), estão disponíveis apenas no ambiente de produção.


## Casos de uso

- Aplicável ao teste beta para configuração de nome de domínio



[](id:open)
## Ativação do gerenciamento de versões

Faça login no [Console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Domain Management (Gerenciamento de domínio)** para exibir a lista de nomes de domínio. Clique no nome do domínio em questão, para acessar a página de configuração, e marque **Enable Version Management (Ativar gerenciamento de versões)** no canto superior direito.
![](https://main.qcloudimg.com/raw/8c60d15a989ded86ad697f4cc8e588ea.png)

Depois que o gerenciamento de versões for ativado, a Ver.1 será criada com a configuração de nome de domínio atual e implantada tanto no ambiente de produção quanto no ambiente de preparo.

## Gerenciamento de versões

Depois de ativar o gerenciamento de versões, é possível exibir e gerenciar as versões na página **Version Management (Gerenciamento de versões)**. Cada versão é identificada por um número de versão Ver.n (n = 1,2,3,...).
Para acessar a página de gerenciamento de versões, você pode selecionar **More (Mais)** > **Version Management (Gerenciamento de versões)**, na coluna de operação na lista de nomes de domínio. Você também pode clicar em um nome de domínio para localizar **Version Management (Gerenciamento de versões)** em sua página de configuração.
![](https://main.qcloudimg.com/raw/5646d1b1a5c812dc04af690b9efb457c.png)



### Adição de versões
Clique em **Add Version (Adicionar versão)**. Por padrão, será criada uma versão com base na configuração atual do ambiente de produção. Você pode modificar a configuração conforme necessário e, em seguida, criar a versão.
![](https://main.qcloudimg.com/raw/f748948c5a279709b713b2da4dfa7fb9.png)

>! Se você receber uma mensagem de erro depois de enviar a nova versão, não é necessário criar outra. Volte para a página de gerenciamento de versões e modifique a versão que você enviou.

### Edição de versões

A versão mais recente pode ser editada antes de ser lançada no ambiente de preparo. Você pode selecionar **More (Mais)** > **Edit (Editar)** na coluna de operação.
![](https://main.qcloudimg.com/raw/b874c1ce46736815efe6ade4147e7a5a.png)
As versões históricas (todas as versões anteriores à versão mais recente), independentemente de terem sido lançadas no ambiente de preparo, só podem ser exibidas, mas não editadas.

>!Antes de adicionar uma nova versão, certifique-se de que todas as versões existentes foram lançadas. Caso contrário, a versão não lançada se tornará uma versão histórica que não pode ser editada e lançada no ambiente de preparo.


### Lançamento de versões

Para os nomes de domínio com o gerenciamento de versões ativado, lance as versões da seguinte maneira:

1. Localize a versão que precisa ser lançada para o ambiente de preparo, selecione **More (Mais)** > **Release to the staging environment (Lançar para o ambiente de preparo)** na coluna de operação.
![](https://main.qcloudimg.com/raw/06196f7c4bef077be3721ece2682f48b.png)
2. O CDN atribuirá um IP IPv4 ao nome de domínio. Para testar a versão implantada no ambiente de preparo, modifique os HOSTS do cliente e aponte o nome do domínio para o IP.
3. Se quiser ajustar a configuração e testar novamente, é necessário adicionar e enviar uma nova versão e, em seguida, repetir as etapas 1 e 2.
4. Após o teste, clique em ** Sync to Production Env. (Sincronizar com o ambiente de produção)** ao lado do número da versão, para sincronizá-la com o ambiente de produção e implantar a configuração no site ativo. 
![](https://main.qcloudimg.com/raw/a6eb38ef147e2347654c8c6b21cd1819.png)
5. Se você precisar alterar a versão no ambiente de produção, repita as etapas 1 a 4.

>!
>- Você só pode lançar a versão mais recente (aquela com o maior número de versão) para o ambiente de preparo. As versões históricas só podem ser exibidas.
>- A configuração especial de back-end ou as atualizações de plataforma serão lançadas diretamente no ambiente de produção.
>- No caso da configuração especial de back-end e atualização de plataforma, podem ocorrer conflitos durante a sincronização do ambiente de preparo com o ambiente de produção, e você receberá uma mensagem de erro sobre a “configuração especial de back-end”. Nesse caso, você deve criar outra versão para lançar.
>- O IP do ambiente de preparo não deve ser alterado com frequência. Mas, para garantir a precisão, é recomendável obter um novo IP clicando no botão Atualizar, todas as vezes antes de testar.



### Exibição de versões

Se você deseja exibir os detalhes de configuração de uma versão, clique em **View (Exibir)** na coluna de operação.


### Ativação/desativação de versões
Clique em **Disable (Desativar)** na seção do ambiente de produção. A versão implantada no ambiente de produção e no ambiente de preparo será desativada ao mesmo tempo, indicando que o nome de domínio será desativado e o serviço de aceleração será encerrado.
![](https://main.qcloudimg.com/raw/7a09e9b936cdeae90283315dcac900b7.png)
Para ativar a versão novamente, clique em **Enable (Ativar)** na seção do ambiente de produção, e a versão será ativada tanto no ambiente de produção quanto no de preparo.

## Desativação do gerenciamento de versões

Depois de desativá-lo, a versão implantada no ambiente de produção será introduzida como a configuração ativa. Todas as outras versões existentes serão descartadas e não podem ser restauradas.

Você pode clicar em **Enable Version Management (Ativar gerenciamento de versões)** para ativá-lo novamente, conforme necessário.


## Observações:

Para nomes de domínio com gerenciamento de versões ativado:
- Funcionalidades de configuração em lote, como [configuração de cópia](https://intl.cloud.tencent.com/document/product/228/38936) e [configuração de alteração em lote](https://intl.cloud.tencent.com/document/product/228/39911), não são aceitas.
- Não é possível configurar um certificado para um nome de domínio na página de gerenciamento de certificados no console.
- Ao ativar ou desativar a aceleração para um nome de domínio, a versão implantada no ambiente de produção e no ambiente de preparo será ativada ou desativada de acordo.
- A tag e o projeto do nome de domínio são editáveis.
- Para alterar a região de aceleração e o tipo de serviço, você deve primeiro desativar o gerenciamento de versões. 
