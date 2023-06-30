## Visão geral

PostgreSQL é um sistema de gerenciamento de banco de dados relacional de código aberto que enfatiza a escalabilidade e a conformidade com os padrões. O PostgreSQL é ideal para sistemas de processamento de transações online complexas (OLTP) de nível empresarial. Suporta tipos de dados NoSQL (JSON/XML/hstore) e Sistema de Informações Geográficas (GIS). Apresentando alta confiabilidade e integridade de dados, o PostgreSQL é adequado para sites, sistemas de aplicativos de localização, processamento de objetos de dados complexos e outros casos de uso.

Este documento descreve como construir um sistema PostgreSQL em uma instância CVM executando CentOS 7.

## Software
Este documento usa o seguinte software como exemplo para construir o PostgreSQL.
Linux: Sistema operacional Linux. Este documento usa a versão CentOS 7.6 como exemplo.
PostgreSQL: Sistema de gerenciamento de banco de dados relacional. Este documento usa o PostgreSQL 11.2 como exemplo.


## Pré-requisitos
- Duas instâncias CVM criadas. Uma instância do CVM funciona como o nó primário e a outra funciona como o nó secundário.
Para obter mais informações, consulte [Criação de instâncias por meio da página de compra do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
- As regras do grupo de segurança para as duas instâncias do CVM já foram configuradas. Abra a porta 5432.
Para obter mais informações, consulte [Adicionar regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).

## Instruções

### Configuração do nó primário

1. Faça login na instância primária do CVM.
2. Execute o seguinte comando para atualizar todos os pacotes, versões do sistema e kernels.
```
yum update -y
```
3. Execute o seguinte comando para instalar o repositório de armazenamento PostgreSQL.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Execute o seguinte comando para instalar o pacote do cliente.
```
yum install postgresql11
```
5. Execute o seguinte comando para instalar o pacote do servidor.
```
yum install postgresql11-server
```
6. Execute o seguinte comando para inicializar o banco de dados.
```
/usr/pgsql-11/bin/postgresql-11-setup initdb
```
7. Execute o seguinte comando para iniciar o serviço.
```
systemctl start postgresql-11
```
8. Execute o seguinte comando para habilitar a inicialização automática do serviço.
```
systemctl enable postgresql-11
```
9. Execute o seguinte comando para alternar para o usuário `postgres`.
```
su - postgres
```
10. Execute o seguinte comando para entrar no terminal PostgreSQL.
```
psql
```
11. Execute o seguinte comando para definir a senha do usuário `postgres`.
```
ALTER USER postgres WITH PASSWORD 'Senha personalizada';
```
12. Execute o seguinte comando para criar uma conta de banco de dados (como `postuser`) e definir a senha, permissão de login e permissão de backup.
```
create role account name login replication encrypted password 'Senha personalizada';
```
Por exemplo, use o seguinte comando para criar uma conta de banco de dados nomeando `postuser` com a senha `postuser`:
```
create role postuser login replication encrypted password 'postuser';
```
13. Execute o seguinte comando para verificar se a conta foi criada.
```
SELECT usename from pg_user;
```
Se o seguinte resultado for retornado, isso indica que a conta foi criada com sucesso.
```
usename  
 ----------
postgres
postuser
(2 rows)
```
14. Execute o seguinte comando para verificar se a permissão foi definida.
```
SELECT rolname from pg_roles;
```
Se o seguinte resultado for retornado, isso indica que a permissão foi definida com sucesso.
```
rolname  
 ----------
postgres
postuser
(2 rows)
```
15. Digite **\q** e pressione **Enter** para sair do terminal PostgreSQL.
16. Digite **exit** e pressione **Entrar** para sair do PostgreSQL.
17. Execute o seguinte comando para abrir o arquivo `pg_hba.conf`.
```
vim /var/lib/pgsql/11/data/pg_hba.conf
```
18. Pressione **i** para mudar para o modo de edição. Adicione as duas linhas a seguir a `IPv4 local connections`.
```
host    all             all             <IPv4 IP range of the secondary node’s VPC>          md5     #Habilitar a criptografia de senha MD5 para conexões nos intervalos de IP do VPC
host    replication     database account        <IPv4 IP range of the secondary node’s VPC>        md5     ##Permitir a sincronização de dados do banco de dados `replication`.
```
Por exemplo, se a conta do banco de dados for `postuser` e o intervalo de IP IPv4 do VPC do nó secundário for `192.10.0.0/16`, adicione o seguinte conteúdo a `IPv4 local connections`:
```
host    all             all             192.10.0.0/16          md5
host    replication     postuser        192.10.0.0/16          md5
```
19. Pressione **Esc** e digite **:wq** para salvar o arquivo.
20. Execute o seguinte comando para abrir o arquivo `postgresql.conf`
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
21. Pressione **i** para entrar no modo de edição, localizar e modificar os seguintes parâmetros:
```
listen_addresses = 'xxx.xxx.xxx.xxx'   #Os endereços IP privados que são ouvidos.
max_connections = 100    #As conexões máximas. O valor de `max_connections` para o nó secundário deve ser maior do que para o nó primário
wal_level = hot_standby  #Ativar o modo de espera ativa.
synchronous_commit = on  #Ativar replicação síncrona
max_wal_senders = 32     #O número máximo de processos de sincronização
wal_sender_timeout = 60s ##O valor de tempo limite para a instância de replicação de streaming para enviar dados.
```
22. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
23. Execute o seguinte comando para reiniciar o serviço.
```
systemctl restart postgresql-11
```

### Configuração do nó secundário

1. Faça login na instância secundária do CVM.
2. Execute o seguinte comando para atualizar todos os pacotes, versões do sistema e kernels.
```
yum update -y
```
3. Execute o seguinte comando para instalar o repositório de armazenamento PostgreSQL.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Execute o seguinte comando para instalar o pacote do cliente.
```
yum install postgresql11
```
5. Execute o seguinte comando para instalar o pacote do servidor.
```
yum install postgresql11-server
```
6. Execute o seguinte comando e use o utilitário pg_basebackup para criar um diretório de backup:
```
pg_basebackup -D /var/lib/pgsql/11/data -h Private IP of primary node -p 5432 -U Database account -X stream -P
```
Por exemplo, se o IP privado do nó primário for `192.10.123.321`, e a conta do banco de dados for `postuser`, execute o seguinte comando:
```
pg_basebackup -D /var/lib/pgsql/11/data -h 192.10.123.321 -p 5432 -U postuser -X stream -P
```
Digite a senha conforme solicitado e pressione **Enter**. Se o seguinte for retornado, isso indica que o diretório de backup foi criado com sucesso.
```
Senha: 
24526/24526 kB (100%), 1/1 tablespace
```
7. Execute o seguinte comando para copiar os arquivos de configuração do nó primário.
```
cp /usr/pgsql-11/share/recovery.conf.sample /var/lib/pgsql/11/data/recovery.conf
```
8. Execute o seguinte comando para abrir o arquivo `recovery.conf`.
```
vim /var/lib/pgsql/11/data/recovery.conf
```
9. Pressione **i** para alternar para o modo de edição, localize e modifique os seguintes parâmetros:
```
standby_mode = on     #Declarar o nó secundário
primary_conninfo = ‘host=<Private IP of the primary node> port=5432 user=Database account password=Database password’ #Informações de conexão do nó primário
recovery_target_timeline = ‘latest’ #Sincronizar os dados mais recentes usando replicação de streaming
```
10. Pressione **Esc** e digite **:wq** para salvar o arquivo.
11. Execute o seguinte comando para abrir o arquivo `postgresql.conf`
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
12. Pressione **i** para alternar para o modo de edição, localize e modifique os seguintes parâmetros:
```
listen_addresses = 'xxx.xx.xx.xx'   #Os endereços IP privados que são ouvidos.
max_connections = 1000             #As conexões máximas. O valor de `max_connections` para o nó secundário deve ser maior do que para o nó primário
hot_standby = on                   #Ativar modo de espera ativa
max_standby_streaming_delay = 30s  #O atraso máximo para replicação de streaming
wal_receiver_status_interval = 1s  # O intervalo máximo para o nó secundário relatar seu status para o nó primário
hot_standby_feedback = on          #Habilitar o nó secundário para relatar erros durante a replicação.
```
13. Pressione **Esc** e digite **:wq** para salvar o arquivo.
14. Execute o seguinte comando para modificar o grupo e o proprietário do diretório de dados:
```
chown -R postgres.postgres /var/lib/pgsql/11/data
```
15. Execute o seguinte comando para iniciar o serviço.
```
systemctl start postgresql-11
```
16. Execute o seguinte comando para habilitar a inicialização automática do serviço.
```
systemctl enable postgresql-11
```

### Verificação da implementação
Execute o seguinte para verificação a implementação.
1. Execute o seguinte comando para verificar o processo `sender` no nó primário:
```
ps aux |grep receiver
```
Se o seguinte for retornado, indica que o processo `sender` está disponível.
![](https://main.qcloudimg.com/raw/d25daabc3d32c58237dd20d871e6852a.png)
2. Execute o seguinte comando para verificar o processo `receiver` no nó secundário:
```
ps aux | grep receiver
```
Se o seguinte for retornado, indica que o processo `receiver` está disponível.
![](https://main.qcloudimg.com/raw/961283ed95a9640ba2121f5fafba2a7b.png)
3. No nó primário, execute os seguintes comandos em sequência para verificar o status do nó secundário no terminal PostgreSQL.
```
su - postgres
```
```
psql
```
```
selecione * from pg_stat_replication;
```
Se o seguinte for retornado, indica que o status do nó secundário está disponível.
![](https://main.qcloudimg.com/raw/c85b5324929a4bffddd92c9dce906d56.png)
4. Verifique se o nó secundário sincroniza os dados com o nó primário.
 1. No nó primário, execute o seguinte comando para entrar no terminal PostgreSQL e criar um banco de dados (como `testdb`).
```
su - postgres
```
```
psql
```
```
create database testdb;
```
 2. No nó secundário, execute os seguintes comandos em sequência para entrar no terminal PostgreSQL e verificar se o nó secundário está sincronizado.
```
su - postgres
```
```
psql
```
```
"l",
```
Se o seguinte for retornado, isso indica que o nó secundário foi sincronizado com sucesso.
![](https://main.qcloudimg.com/raw/2912a3d9892665469bff1768c76c7ae9.png)




