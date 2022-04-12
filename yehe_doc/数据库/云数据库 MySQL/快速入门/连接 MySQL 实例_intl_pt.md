Este documento descreve como se conectar a uma instância inicializada do TencentDB for MySQL em uma rede privada ou pública.

## Preparações
- Você inicializou uma instância do TencentDB for MySQL. Para mais informações, consulte [Inicialização de instância do MySQL](https://intl.cloud.tencent.com/document/product/236/3128).
- Você criou uma conta de banco de dados e autorizou IPs ou intervalos de IP específicos para acessar a instância do TencentDB for MySQL. Para mais informações, consulte [Criação de conta](https://intl.cloud.tencent.com/document/product/236/31900) e [Modificação de endereços de host com permissões de acesso](https://intl.cloud.tencent.com/document/product/236/31903). Ou você pode usar a conta raiz.
- Você configurou regras de grupo de segurança para a instância da CVM e a instância do TencentDB for MySQL para permitir que IPs ou intervalos de IP específicos acessem a instância do TencentDB for MySQL. Para mais informações, consulte [Gerenciamento de grupos de segurança do TencentDB](https://intl.cloud.tencent.com/document/product/236/14470).

## Métodos de conexão
O TencentDB for MySQL pode ser conectado nos seguintes métodos:
- **Conexão de rede privada**: uma instância da CVM pode ser usada para se conectar ao endereço de rede privada de uma instância do TencentDB. Esse método utiliza a rede privada de alta velocidade da Tencent Cloud e apresenta pouco atraso.
 - As duas instâncias devem estar na mesma conta e na mesma [VPC](https://intl.cloud.tencent.com/document/product/215/535) na mesma região, ou ambas na rede clássica.
 - O endereço de rede privada é fornecido pelo TencentDB por padrão e pode ser exibido na lista de instâncias ou na página de detalhes da instância no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
>?As instâncias da CVM e do TencentDB em VPCs diferentes (na mesma conta ou em contas diferentes na mesma região ou em regiões diferentes) podem ser interconectadas pela rede privada por meio do [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).
>
- **Conexão de rede pública**: se você não conseguir acessar a rede privada, poderá se conectar à instância do TencentDB for MySQL em seu endereço de rede pública. O endereço de rede pública precisa ser [ativado manualmente](#waiwang). Ele pode ser exibido na página de detalhes da instância no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e pode ser desativado quando não for mais necessário.
 - O endereço de rede pública pode ser ativado para instâncias de origem nas regiões de Guangzhou, Xangai, Pequim, Chengdu, Chongqing, Nanquim, Hong Kong (China), Singapura, Seul, Tóquio, Vale do Silício e Frankfurt. Confira no console as informações mais recentes sobre as regiões em que o endereço de rede pública pode ser ativado para instâncias somente leitura.
 - A ativação do endereço de rede pública vai expor seus serviços de banco de dados à rede pública, o que pode levar a invasões ou ataques ao banco de dados. Recomendamos que você use a rede privada para se conectar ao banco de dados. 
 - A conexão de rede pública com o TencentDB é adequada para o desenvolvimento ou gerenciamento auxiliar de bancos de dados, mas não para o acesso de negócios no ambiente de produção, pois fatores potencialmente incontroláveis podem levar à indisponibilidade da conexão de rede pública, como ataques DDoS e intermitências de acesso de alto tráfego.


Confira a seguir como se conectar a uma instância do TencentDB for MySQL a partir de instâncias da CVM do Windows e do Linux nas redes pública e privada.
## Conexão a partir de uma instância da CVM do Windows
1. Faça login em uma instância da CVM do Windows. Para mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/10516" target="_blank">Personalização das configurações do CVM no Windows</a>.
2. Baixe um cliente SQL padrão.
>?Recomendamos que você baixe o MySQL Workbench. Clique [aqui](https://dev.mysql.com/downloads/workbench/) e baixe um instalador com base em seu sistema operacional.
>
![](https://main.qcloudimg.com/raw/851ab46468c554097a0cf742017157b7.png)
3. As opções **Login (Fazer login)**, **Sign Up (Criar conta)** e **No thanks, just start my download. (Não, obrigado. Apenas iniciar o download.)** serão exibidas na página. Selecione **No thanks, just start my download. (Não, obrigado. Apenas iniciar o download.)** para baixar rapidamente.
![](https://main.qcloudimg.com/raw/47b195fb37ff584f21038ee54342d362.png)
4. Instale o MySQL Workbench nessa instância da CVM.
>?
>- O Microsoft .NET Framework 4.5 e o Visual C++ Redistributable for Visual Studio 2015 são necessários para a instalação.
>- Você pode clicar em **Download Prerequisites (Baixar pré-requisitos)** no assistente de instalação do MySQL Workbench para acessar a página correspondente para baixá-los e instalá-los. Em seguida, instale o MySQL Workbench.
>
![](https://main.qcloudimg.com/raw/1af292f989f03f3e02e1200b77cb70c1.png)
5. Abra o MySQL Workbench, selecione **Database (Banco de dados)** > **Connect to Database (Conectar ao banco de dados)**, digite o endereço de rede privada (ou pública), o nome de usuário e a senha da sua instância do TencentDB for MySQL, e clique em **OK** para fazer login.
 - **Hostname (Nome do host)**: insira o endereço de rede privada (ou pública), que pode ser exibido com a porta na página de detalhes da instância no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Para o endereço de rede pública, verifique se ele foi ativado conforme as instruções em [Ativação do endereço de rede pública](#waiwang).
 - **Port (Porta)**: porta de rede privada (ou pública).
 - **Username (Nome de usuário)**: o nome de usuário é **root** por padrão. Para conexão de rede pública, recomendamos que você [crie uma conta separada](https://intl.cloud.tencent.com/document/product/236/31900) para facilitar o controle da conexão.
 - **Password (Senha)**: a senha correspondente ao **Nome de usuário**. Se você esqueceu a senha, redefina-a conforme as instruções em [Redefinição de senha](https://intl.cloud.tencent.com/document/product/236/31901).
![](https://main.qcloudimg.com/raw/946b50fb05de11d7c68c2262ac4fe933.png)
6. Após o login bem-sucedido, será exibida a página a seguir, na qual você poderá exibir os modos e objetos do banco de dados MySQL, criar tabelas e realizar operações como inserção e consulta de dados.
![](https://main.qcloudimg.com/raw/33f081e99c384258bbc5ed3683ed4d7d.png)

## Conexão a partir de uma instância da CVM do Linux
1. Faça login na instância da CVM do Linux. Para mais informações, consulte [Personalização das configurações do CVM no Linux](https://intl.cloud.tencent.com/document/product/213/10517).
2. Considerando uma instância da CVM no CentOS 7.2 (64 bits) como exemplo, execute o comando a seguir para instalar o cliente do MySQL.
```
yum install mysql
```
Se `Complete! (Concluído!)` for exibido, o cliente do MySQL foi instalado com êxito.
![](https://main.qcloudimg.com/raw/16c77e28c40ae9be9a182b1c61843ecd.png)
3. Execute a operação correspondente com base no método de conexão:
 - **Conexão de rede privada:**
    1. Execute o comando a seguir para fazer login na instância do TencentDB for MySQL.
```
mysql -h hostname -u username -p
```
      - hostname (nome do host): substitua-o pelo endereço de rede privada da instância de destino do TencentDB for MySQL, que pode ser exibido na página de detalhes da instância no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb).
>?
>- O número da porta padrão do MySQL é 3306.
>- Se o número da porta for 3306, basta substituir `hostname` pelo endereço IP. Por exemplo, se o endereço de rede privada for 10.16.0.11:3306, defina `hostname` como `10.16.0.11`.
>- Se o número da porta não for 3306, é necessário especificar a porta no comando de conexão no formato de `mysql -h hostname -P port -u username -p`, como `mysql -h 10.16.0.11 -P 5308 -u username -p`.
>
		- username (nome de usuário): substitua-o pelo nome de usuário padrão `root`.
    2. Digite a senha correspondente à conta `root (raiz)` da instância do TencentDB for MySQL depois que `Enter password: (Insira a senha:)` for exibido. Se você esqueceu a senha, redefina-a conforme as instruções em [Redefinição de senha](https://intl.cloud.tencent.com/document/product/236/31901).
    Se `MySQL [(none)]>` for exibido, você fez login no MySQL com êxito.
![](https://main.qcloudimg.com/raw/83b8a95cf4b99919b5899510691289b4.png)
   - **Conexão de rede pública:**
    1. Execute o comando a seguir para fazer login na instância do TencentDB for MySQL.
```
mysql -h hostname -P port -u username -p
```
      - hostname (nome do host): substitua-o pelo endereço de rede pública da instância de destino do TencentDB for MySQL, que pode ser exibido junto com a porta na página de detalhes da instância no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Se o endereço de rede pública não tiver sido ativado, ative-o conforme instruído em [Ativação do endereço de rede pública](#waiwang).
      - port (porta): substitua-a pelo número da porta da rede pública.
      - username (nome de usuário): substitua-o pelo nome de usuário de acesso à rede pública. Recomendamos que você [crie uma conta separada](https://intl.cloud.tencent.com/document/product/236/31900) para facilitar o controle da conexão.
    2. Digite a senha correspondente ao nome de usuário da conexão de rede pública depois que `Enter password: (Insira a senha:)` for exibido. Se você esqueceu a senha, redefina-a conforme as instruções em [Redefinição de senha](https://intl.cloud.tencent.com/document/product/236/31901).
    Neste exemplo, o `hostname` é 59281c4exxx.myqcloud.com e a porta de rede pública é 15311.
![](https://main.qcloudimg.com/raw/16839344da3a588be93d814de224277a.png)
4. No prompt `MySQL [(none)]>`, você pode enviar uma instrução SQL para o servidor do MySQL para execução. Para obter as linhas de comando específicas, consulte [Comandos do cliente do MySQL](https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html).
Abaixo é usado `show databases; (exibir bancos de dados;)` como exemplo:
![](https://qcloudimg.tencent-cloud.cn/raw/faa7e8137e03b72f95d7a92faa971a42.png)

## Apêndice 1. Solução de problemas de erros de conexão
Se você encontrar erros de conexão, recomendamos que, em primeiro lugar, você use o [Verificador de conectividade com um clique](https://intl.cloud.tencent.com/document/product/236/31927) para solucionar o problema e, em seguida, encontre a solução correspondente em [Falha de conexão da instância](https://intl.cloud.tencent.com/document/product/236/40333) de acordo com o relatório de verificação.

## Apêndice 2. Método de verificação de conectividade de rede
Recomendamos solucionar e localizar problemas de conectividade de rede rapidamente com o comando `telnet`.

Se a verificação com o `telnet` descobriu que o acesso à rede da instância do TencentDB era bom, mas um erro foi relatado quando você tentou fazer login por meio da linha de comando na instância da CVM, consulte [Perguntas frequentes > Conexão e login > Conexão](https://intl.cloud.tencent.com/document/product/236/37783).

## [Apêndice 3. Ativação do endereço de rede pública](id:waiwang)
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a página de detalhes da instância.
2. Na seção **Basic Info (Informações básicas)**, clique em **Enable (Ativar)** ao lado de **Public Network Address (Endereço de rede pública)**.
>?Se a seção **Basic Info (Informações básicas)** exibir o IP público e a porta, o endereço de rede pública foi ativado.
>
![](https://main.qcloudimg.com/raw/f3300b56af8e152aa457534ffd873002.png)
3. Na janela pop-up, clique em **OK**.
>?
>- Depois que o endereço de rede pública for ativado com êxito, ele poderá ser exibido nas informações básicas.
>- O acesso à rede pública pode ser desativado usando a alternância. Quando ele for ativado novamente, o endereço de rede pública correspondente ao nome de domínio permanecerá o mesmo.
