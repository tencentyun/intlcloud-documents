## Visão geral
O Extundelete é uma ferramenta, de código aberto, para recuperação de dados. Com recursos poderosos, suporta a recuperação de partições ext3 e ext4 de arquivos excluídos acidentalmente de disco de dados, desde que o disco não seja gravado após o acidente. Este documento descreve como usar o Extundelete para recuperar rapidamente os dados excluídos acidentalmente em um Tencent Cloud CVM CentOS 7.7.
O Tencent Cloud também oferece [instantâneos](https://intl.cloud.tencent.com/document/product/362/5755), [imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942) e [Armazenamento de objetos em nuvem](https://intl.cloud.tencent.com/document/product/436/6222) para armazenar dados. Recomendamos que você faça backups regulares dos dados para aumentar a segurança dos dados.

## Software
- Linux: Sistema operacional Linux. Este documento usa a versão CentOS 7.7 como exemplo.
- Extundelete: ferramenta, de código aberto, para recuperação de dados. Este documento usa o Extundelete 0.2.4 como exemplo.


## Instruções
>!Consulte [Criação de instantâneos](https://intl.cloud.tencent.com/document/product/362/5755) e [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942) para fazer backup dos dados antes de realizar as operações, de forma que você possa recuperar a instância para o status inicial se ocorrer um problema.
>

### Instalação do Extundelete
1. Execute o seguinte comando para instalar as dependências e bibliotecas do Extundelete.
>!
> - O Extundelete requer o libext2fs versão 1.39 ou posterior.
> - Para suportar o formato ext4, instale o e1fsprogs versão 1.41 ou posterior. É possível usar o comando `dumpe2fs` para visualizar a versão. 
>
```
yum -y install  bzip2  e2fsprogs-devel  e2fsprogs  gcc-c++  make
```
2. Faça download do pacote de instalação do [Extundelete](https://sourceforge.net/projects/extundelete/).
3. Execute os comandos a seguir em sequência para descompactar o pacote de instalação Extundelete e acessar o diretório.
```
tar -xvjf extundelete-0.2.4.tar.bz2
```
```
cd extundelete-0.2.4 
```
4. Execute os seguintes comandos em sequência para compilar e instalar o Extundelete.
```
./configure   
```
```
make && make install
```
Após a conclusão da instalação, você poderá ver o arquivo executável "extundelete" no diretório `usr/local/bin`.

### Testando a recuperação de dados
Recupere os dados conforme necessário, executando as etapas a seguir.
1. Inicialize e particione o disco de dados consultando [Inicialização de discos em nuvem (menores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597). Execute o seguinte comando para visualizar os discos existentes e as partições disponíveis.
```
fdisk -l
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/34abb1b0c7a1f6fb4ff233a42a781123.png)
2. Execute os seguintes comandos em sequência para criar um ponto de montagem e montar a partição. Este documento usa a montagem da partição `/dev/vdb1` para `/test` como exemplo.
```
mkdir /test
```
```
mount /dev/vdb1 /test
```
3. Execute os seguintes comandos em sequência para criar o arquivo de teste "hello" no ponto de montagem.
```
cd /test
```
```
echo test > hello
```
4. <span id="Step4"></span>Execute o seguinte comando para registrar o valor MD5 do arquivo "hello". Este valor pode ser usado para comparar os arquivos originais e recuperados.
```
md5sum hello
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/230d4c9a4456df8b3623c0bd401d878a.png)
5. Execute os seguintes comandos em sequência para excluir o arquivo "hello".
```
rm -rf hello
```
```
cd ~
```
```
fuser -k /test
```
6. Execute o seguinte comando para desmontar a partição.
```
umount /dev/vdb1
```
7. Execute o seguinte comando para pesquisar a partição em busca de arquivos excluídos acidentalmente.
```
extundelete --inode 2 /dev/vdb1
```
As seguintes informações serão exibidas:
![](https://main.qcloudimg.com/raw/97a64a2e0de658f4ed55500f162b1eb7.png)
8. Execute o seguinte comando para usar o Extundelete para recuperar o arquivo.
```
/usr/local/bin/extundelete  --restore-inode 12  /dev/vdb1
```
Depois que o arquivo for recuperado, você verá a pasta `RECOVERED_FILES` no diretório de mesmo nível.
9. Acesse a pasta `RECOVERED_FILES`, verifique o arquivo recuperado e execute o seguinte comando para obter o valor MD5.
```
md5sum Recovered file
```
Se o valor MD5 obtido for o mesmo do arquivo "hello" gravado na [Etapa 4](#Step4), os dados foram recuperados com sucesso.
