
## Visão geral
>?Para economizar a capacidade de armazenamento, os backups físicos e lógicos no TencentDB for MySQL devem ser compactados com o qpress e depois empacotados com o xbstream oferecidos pela Percona.
>
O Percona XtraBackup tem código aberto e pode ser usado para fazer backup e restaurar bancos de dados. Este documento descreve como usar o XtraBackup para restaurar um arquivo de backup físico da instância do TencentDB for MySQL para um banco de dados auto-construído na CVM.
- O XtraBackup é compatível apenas com o sistema operacional Linux.
- Para obter mais informações sobre como restaurar dados no Windows, consulte [Migração offline de dados > Migração de dados com ferramenta de linha de comando](https://intl.cloud.tencent.com/document/product/236/8464).

## Pré-requisitos
- Baixe e instale o XtraBackup.
 - Para MySQL 5.6 e 5.7, baixe o Percona XtraBackup 2.4.6 ou superior no [site oficial da Percona](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Para obter mais informações sobre instalação, consulte [Documentação do XtraBackup 2.4 da Percona](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
 - Para MySQL 8.0, baixe o Percona XtraBackup 8.0.22-15 ou superior no [site oficial da Percona](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#). Para obter mais informações sobre instalação, consulte [Documentação do Percona XtraBackup 8.0](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html).
- Arquiteturas de instâncias suportadas: MySQL de dois ou três nós
- Instâncias com criptografia de dados habilitada não podem ser restauradas de um backup físico.

## Instruções
>?Este documento usa uma instância de CVM executando CentOS e uma instância MySQL v5.7 como exemplo.
>
### Etapa 1. Baixe o arquivo de backup
Você pode baixar backups de dados e backups de log de instâncias do TencentDB for MySQL no console.
>?Cada IP pode ter até 10 links de download por padrão, com um limite de velocidade de download de 20–30 Mbps cada.
>
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a respectiva página de gerenciamento.
2. Na guia **Backup and Restore (Fazer backup e restaurar)** > **Data Backup List (Lista de backup de dados)**, localize o arquivo de backup a ser baixado e clique em **Download** na coluna **Operation (Operação)**.
3. Copie o endereço de download na caixa de diálogo pop-up, [faça login na CVM do Linux na mesma VPC que a instância do TencentDB](https://intl.cloud.tencent.com/document/product/213/10517), e execute `wget` para baixar o arquivo pela rede privada de alta velocidade.
>?
>- Você também pode clicar em **Download** para baixá-lo diretamente. No entanto, isso pode levar mais tempo.
>- Formato de comando`wget`: wget -c 'backup file download address' -O custom filename.xb 
>
O exemplo é o seguinte:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O /data/test.xb
```

### Etapa 2. Restaurar dados
#### 2.1 Descompacte o arquivo de backup
Execute o comando `xbstream` para descompactar o arquivo de backup no diretório de destino.
```
xbstream -x --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- O diretório de destino `/data/mysql` é usado como exemplo neste documento. Você pode substituí-lo pelo diretório que você realmente usa para armazenar o arquivo de backup.
>- Substitua `/data/test.xb` pelo seu arquivo de backup.
>
O resultado da descompactação é mostrado abaixo:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 Descompacte o arquivo de backup
1. Baixe o qpress executando o seguinte comando:
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10. http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?Se um erro for exibido durante o download do `wget`, você pode ir ao [site oficial do QuickLZ](http://www.quicklz.com/) para baixar o qpress localmente e enviá-lo para a instância da CVM do Linux. Para obter mais informações, consulte [Enviar arquivos por upload do Linux ou MacOS para a CVM do Linux via SCP](https://intl.cloud.tencent.com/document/product/213/2133).
>
2. Extraia os arquivos binários do qpress executando o seguinte comando.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Descompacte todos os arquivos `.qp` no diretório de destino executando o seguinte comando do qpress:
```
xtrabackup --decompress --target-dir=/data/mysql
```
>?
>- `/data/mysql` é o diretório de destino onde o arquivo de backup foi armazenado anteriormente. Você pode substituí-lo pelo diretório que você realmente usa.
>- A opção `--remove-original` é suportada apenas no Percona Xtrabackup v2.4.6 e posterior.
>- Por padrão, `xtrabackup` não excluirá os arquivos originais durante a descompactação. Se você deseja excluí-los após a conclusão da descompactação, adicione o parâmetro `--remove-original` ao comando acima.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 Prepare o arquivo de backup
Depois que um arquivo de backup é descompactado, você precisa executar a operação "apply log" executando o comando a seguir.
```
xtrabackup --prepare  --target-dir=/data/mysql
```
Se o resultado da execução contiver a saída a seguir, significa que a preparação foi bem-sucedida.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
#### 2.4 Modificar o arquivo de configuração
1. Execute o seguinte comando para abrir o arquivo `backup-my.cnf`.
```
vi /data/mysql/backup-my.cnf
```
>?O diretório de destino `/data/mysql` é usado como exemplo neste documento. Você pode substituí-lo pelo diretório que você realmente usa.
>
2. Considerando os problemas de versão existentes, os seguintes parâmetros precisam ser comentados a partir do arquivo extraído `backup-my.cnf`.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://qcloudimg.tencent-cloud.cn/raw/6d56154cb19d16b56520199290a0c574.png)

#### 2.5 Modificar atributos de arquivo
Modifique os atributos do arquivo e verifique se os arquivos são de propriedade do usuário `mysql`.
```
chown -R mysql:mysql /data/mysql
```
![](https://qcloudimg.tencent-cloud.cn/raw/12fbe7f70fefa19fd7af5ac2f95bfdb8.png)

### Etapa 3. Inicie o processo mysqld e faça login para verificação
1. Inicie o processo mysqld.
```
mysqld_safe --defaults-file=/data/mysql/backup-my.cnf --user=mysql --datadir=/data/mysql &
```
2. Faça login no cliente para verificação.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## Perguntas frequentes sobre backup
Consulte [Problemas comuns](https://intl.cloud.tencent.com/document/product/236/9036) e [Motivos da falha](https://intl.cloud.tencent.com/document/product/236/34394).
