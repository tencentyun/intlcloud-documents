## Visão geral
Este artigo descreve como instalar o MySQL 8.0 em uma instância CVM com Windows Server 2012 R2 Datacenter Edition 64 bits. 
O SQL Server é talvez o software de banco de dados mais popular do Windows. No entanto, é comercial e requer que você obtenha sua própria licença. Como alternativa, você pode comprar [instâncias de CDB para o banco de dados SQLServer do Tencent Cloud](https://intl.cloud.tencent.com/product/sqlserver?from_cn_redirect=1).

## Procedimento

### Fazer download do MySQL
1. Faça login na instância do CVM.
2. Abra uma janela do navegador e vá para o [site oficial do MySQL](https://www.mysql.com/) para fazer download do arquivo de instalação do MySQL.

### Instalação do MySQL

1. Inicie o instalador do MySQL clicando duas vezes no arquivo de instalação. A janela **Choose a Setup Type (Selecionar um tipo de configuração)** é exibida. Selecione **Developer Default (Padrão do desenvolvedor)** e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/4077db7bfe9f7b97e1d7ddd649efa966.png)
2. Na janela **Check Requirements (Verificar requisitos)** que aparece, clique em **Execute (Executar)** e resolva os requisitos não atendidos conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/16a5f7190d7720562681528072cf8129.png)
3. Clique em **Next (Avançar)**.
4. Na janela **Installation (Instalação)**, clique em **Execute (Executar)** para instalar os pacotes necessários, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/1b4a3e338bb816e7c47b4603a7a1dbb4.png)
5. Clique em **Next (Avançar)** quando a instalação do pacote terminar para abrir a janela **Product Configuration (Configuração do produto)**.


### Configuração do MySQL

#### Configuração do serviço MySQL

1. Na janela **Product Configuration (Configuração do produto)**, clique em **Next (Avançar)** para abrir a janela **High Availability (Alta disponibilidade)**.
2. Selecione **Standalone MySQL Server/Classic MySQL Replication (MySQL Server autônomo/Replicação MySQL clássica)** e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/5355f286598388f9e9846bf8122e6d98.png)
3. Na janela **Type and Networking (Tipo e rede)**, mantenha a configuração padrão. Clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
> 
> - A rede TCP/IP está habilitada por padrão.
> - A porta 3306 é usada por padrão.
> 
![](https://main.qcloudimg.com/raw/fbece2fafb34beb5825ae294a8e214fd.png)
4. Na janela **Authentication Method (Método de autenticação)**, mantenha a configuração padrão. Clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/402624aaf02dce01ca2912d3548c03de.png)
5. Defina uma senha de raiz e clique em **Next (Avançar)** conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/a0472f0b93c590997e78c2f590a0f901.png)
6. Na janela **Windows Service (Serviço do Windows)**, mantenha a configuração padrão e clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/a85625c446218a275e743ff0ec599ece.png)
7. Na janela **Apply Configuration (Aplicar configuração)**, clique em **Execute (Executar)**.
![](https://main.qcloudimg.com/raw/2ee6000630d88774951ddf8aaea16fbb.png)
8. Clique em **Finish (Concluir)** para concluir a configuração do MySQL.

#### Configuração do roteador MySQL

1. Na janela **Product Configuration (Configuração do produto)**, clique em **Next (Avançar)**.
2. Na janela **MySQL Router Configuration (Configuração do roteador MySQL)**, mantenha a configuração padrão e clique em **Finish (Concluir)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/adece1334b6e1579eb2ace782cf47c59.png)

#### Configuração de amostras do MySQL

1. Na janela **Product Configuration (Configuração do produto)**, clique em **Next (Avançar)**.
2. Na janela **Connect to Server (Conectar ao servidor)**, insira a senha de raiz. Clique em **Check (Verificar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/ab8637391012a14ab2e5160c61675912.png)
3. Depois que a senha for autenticada com sucesso, clique em **Next (Avançar)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/bff0aece8da11d15a52f4db91b4d7e69.png)
4. Na janela **Apply Configuration (Aplicar configuração)**, clique em **Execute (Executar)**.
![](https://main.qcloudimg.com/raw/8fe1f90eed50860e064044b314719cf6.png)
5. Clique em **Finish (Concluir)** para finalizar a configuração de amostra do MySQL.
6. Na janela **Product Configuration (Configuração do produto)**, clique em **Next (Avançar)**.
7. Na janela **Installation Complete (Instalação concluída)**, selecione o componente do ambiente MySQL que deseja iniciar e clique em **Finish (Concluir)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/13f46296b85b00ce7e3bd08be13108c9.png)
 - Se o MySQL Workbench for iniciado, a instalação do MySQL foi bem-sucedida, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/288f4cfbf1a9671b73dff64a940e0dc1.png)
 - Se o MySQL Shell for iniciado, a instalação do MySQL foi bem-sucedida, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/90b788ffe3a8f92e0e5e70f35fb94356.png)


### Adicionar regras de grupo de segurança

Adicione uma regra de entrada para permitir o tráfego na porta 3306 para o grupo de segurança que está vinculado à instância CVM na qual o MySQL está instalado.




