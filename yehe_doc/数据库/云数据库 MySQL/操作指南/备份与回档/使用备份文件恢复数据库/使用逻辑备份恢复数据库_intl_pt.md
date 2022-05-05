## Visão geral
>?Para economizar capacidade de armazenamento, backups físicos e lógicos no TencentDB for MySQL serão compactados com o qpress e depois empacotados com o xbstream oferecidos pela Percona.

O TencentDB for MySQL é compatível com [backup lógico](https://intl.cloud.tencent.com/document/product/236/37796). No console, você pode criar manualmente arquivos de backup lógico de uma instância inteira ou bancos de dados/tabelas especificados e fazer download deles. Este documento descreve como restaurar manualmente os dados de arquivos de backup lógico.

- O método de restauração descrito neste documento se aplica apenas ao Linux.
- Para obter mais informações sobre como restaurar dados no Windows, consulte [Migração de dados offline > Migração de dados com ferramenta de linha de comando](https://intl.cloud.tencent.com/document/product/236/8464).
- Arquiteturas de instâncias compatíveis: MySQL de dois ou três nós

## Instruções
### Etapa 1. Baixe o arquivo de backup
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique no ID da instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a página de gerenciamento de instâncias.
2. Na guia **Backup and Restore (Fazer backup e restaurar)** > **Data Backup List (Lista de backup de dados)**, localize o arquivo de backup a ser baixado e clique em **Download (Fazer download)** na coluna **Operation (Operação)**.
3.  Recomendamos que você copie o link de download na caixa de diálogo pop-up, faça login em uma instância [(Linux) da CVM na mesma VPC que a instância do TencentDB](https://intl.cloud.tencent.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), e execute o comando `wget` para download pela rede privada em uma velocidade maior.
>?
>- Você também pode clicar em **Download (Fazer download)** para baixá-lo diretamente, o que pode levar mais tempo.
>- Formato de comando`wget`: wget -c 'backup file download address' -O custom filename.xb
>
Exemplo
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### Etapa 2. Descompacte o arquivo de backup
Descompacte o arquivo de backup com xbstream.
>?xbstream pode ser baixado no [site oficial da Percona](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Selecione Percona XtraBackup v2.4.6 ou posterior. Para obter mais informações sobre instalação, consulte [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
```
xbstream -x < teste0.xb
```
>?Substitua `test0.xb` pelo seu arquivo de backup.
>
O resultado da descompactação é mostrado abaixo:
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### Etapa 3. Descompacte o arquivo de backup
1. Baixe o qpress executando o seguinte comando:
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0"
http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?Se um erro for exibido durante o download do `wget`, você pode ir ao [site oficial do QuickLZ](http://www.quicklz.com/) para baixar o qpress localmente e enviá-lo para a instância da CVM do Linux. Para obter mais informações, consulte [Upload de arquivos via SCP para uma CVM do Linux](https://intl.cloud.tencent.com/document/product/213/2133).
2. Extraia os arquivos binários qpress executando o seguinte comando:
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Descompacte o arquivo de backup com o qpress.
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?Encontre o arquivo de backup com extensão `.sql.qp` por tempo de descompressão e substitua `cdb-jp0zua5k_backup_20191202182218` por seu nome de arquivo.
>
O resultado da descompressão é conforme mostrada abaixo:
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### Etapa 4. Importe o arquivo de backup para o banco de dados de destino
Importe o arquivo .sql para o banco de dados de destino executando o seguinte comando:
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- Este documento usa como exemplo a importação para uma instância local do MySQL com a porta 3306. Você pode substituí-lo conforme necessário.
>- Substitua `cdb-jp0zua5k_backup_20191202182218.sql` pelo arquivo .sql extraído pelo qpress.
