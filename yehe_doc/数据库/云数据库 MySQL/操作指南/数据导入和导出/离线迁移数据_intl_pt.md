Este documento descreve como migrar dados no console ou com a ferramenta de linha de comando.

## Migração de dados por meio do console
Existem dois modos de migração de dados através do console: backup físico e backup lógico. Para obter mais informações, consulte:
- [Restauração de banco de dados do backup físico(https://intl.cloud.tencent.com/document/product/236/31910)
- [Restauração de banco de dados do backup lógico](https://intl.cloud.tencent.com/document/product/236/31909)

<span id="AA"></span>
## Migração de dados com ferramenta de linha de comando
1. Gere o arquivo SQL a ser importado com a ferramenta de linha de comando MySQL "mysqldump" da seguinte forma:
>!
>- Os arquivos de dados exportados usando mysqldump devem ser compatíveis com a especificação SQL da sua versão do TencentDB for MySQL. Você pode fazer login no banco de dados e obter as informações da versão do MySQL executando o comando `select version();`. O nome do arquivo SQL gerado pode conter letras, dígitos e sublinhados, mas não "test".
>- Certifique-se de que as mesmas versões de banco de dados de origem e destino, conjuntos de caracteres de banco de dados de origem e destino e versões da ferramenta mysqldump sejam usadas. Você pode especificar o conjunto de caracteres usando o parâmetro --default-character-set .
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
Aqui, `options` é a opção de exportação, `db_name` é o nome do banco de dados, `tbl_name` é o nome da tabela e `bak_pathname` é o caminho de exportação.
Para mais informações sobre como exportar dados com mysqldump, consulte a [documentação oficial do MySQL](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).
2. Importe dados para o banco de dados de destino com a ferramenta de linha de comando MySQL da seguinte maneira:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Aqui, `hostname` é o servidor de destino para restauração de dados, `port` é a porta do servidor de destino, `username` é o nome de usuário do banco de dados no servidor de destino e `bak_pathname` é o caminho completo para o arquivo de backup.

### Migração de dados (Windows)
1. Use a versão Windows do mysqldump para gerar o arquivo SQL a ser importado. Para obter mais informações, consulte a descrição em [Migração de dados com ferramenta de linha de comando](#AA).
2. Digite o prompt de comando e importe os dados para o banco de dados de destino com a ferramenta de linha de comando MySQL.
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [Efetue login no banco de dados MySQL de destino](https://dev.mysql.com/doc/refman/5.7/en/connecting.html), execute o comando `show databases;` e você verá que o banco de dados de backup foi importado para o banco de dados de destino.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### Migração de dados (Linux)
Este documento usa uma instância de CVM do Linux como exemplo. Para obter mais informações sobre como acessar um banco de dados de uma instância de CVM, consulte <a href="https://intl.cloud.tencent.com/document/product/236/3130" target="_blank">Acesso ao banco de dados MySQL</a>.

1. [Efetue login na instância CVM](https://intl.cloud.tencent.com/document/product/213/2936) e gere o arquivo SQL a ser importado com a ferramenta de linha de comando MySQL "mysqldump". Tome o banco de dados `db_blog` no TencentDB como exemplo:
![](https://main.qcloudimg.com/raw/de40c98620c6fdd96bc7839645b70103.png)
2. Use a ferramenta de linha de comando MySQL para restaurar os dados no banco de dados de destino.
3. Efetue login no banco de dados MySQL de destino, execute o comando `show databases;` e você verá que o banco de dados de backup foi importado para o banco de dados de destino.
![](https://main.qcloudimg.com/raw/072f4b0c6f2353cdd1bab1ca9b87a783.png)

## Problemas com o conjunto de caracteres de arquivos de dados importados
1. Se nenhum conjunto de caracteres for especificado durante a importação do arquivo de dados para o TencentDB, aquele definido pelo banco de dados será usado.
2. Caso contrário, o conjunto de caracteres especificado será usado.
3. Se o conjunto de caracteres especificado for diferente daquele do TencentDB, o texto ilegível será exibido.

Para obter mais informações, consulte a descrição do conjunto de caracteres em <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">Limites de uso</a>.


