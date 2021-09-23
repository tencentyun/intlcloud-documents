## Visão geral
Se o seu disco em nuvem tiver uma partição GPT que contém o sistema de arquivos, é possível usar um dos seguintes métodos para estender as partições e os sistemas de arquivos:
- [Atribuição da capacidade expandida a uma partição GPT existente](#Add)
- [Formatação da capacidade expandida em uma nova partição GPT independente](#New)



## Pré-requisitos
É possível usar ferramentas de expansão automática, incluindo e2fsck e resize2fs para adicionar a capacidade expandida do disco em nuvem ao sistema de arquivos existente em um CVM do Linux. Para garantir uma expansão com êxito, os seguintes requisitos devem ser atendidos:
- A forma de expandir e particionar foi confirmada. Para obter mais informações, consulte [Determinação do método de expansão](https://intl.cloud.tencent.com/document/product/362/39995).
- O sistema de arquivos é EXT ou XFS.
- O sistema de arquivos atual não tem nenhum erro.


## Instruções

[](id:Add)
### Atribuição da capacidade expandida a uma partição GPT existente
1. Execute o seguinte comando como usuário raiz para confirmar as alterações na capacidade do disco em nuvem.
```
parted <Disk path> print
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
parted /dev/vdc print
```
Se uma mensagem conforme mostrada na figura a seguir aparecer no processo, digite `Fix`.
![](https://main.qcloudimg.com/raw/bdc9f2fcb281e24ec5799e73c08535eb.png)
O tamanho do disco em nuvem é 2.040 GB após a expansão e a capacidade da partição existente é de 10,7 GB, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/40a1141f65ba7ac15b8dac4b94e0d6a5.png)
2. Execute o seguinte comando para verificar se o disco em nuvem tem partições montadas.
```
mount | grep '<Disk path>' 
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
mount | grep '/dev/vdc'
```
 - O seguinte resultado indica que o disco em nuvem tem uma partição (vdc1) montada em `/data`.
![](https://main.qcloudimg.com/raw/61ae197d19c522f6ebd1e9c7bf4b4d88.png)
Execute o seguinte comando para desmontar **todas as partições** do disco em nuvem.
```
umount <Mount point>
```
Considerando o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
umount /data
```
 - O seguinte resultado indica que não há partição montada. Prossiga para a próxima etapa.
![](https://main.qcloudimg.com/raw/4a6d070830fd0629a336836fd6b4c1fd.png)
3. Execute o seguinte comando para usar a ferramenta de partição parted.
```
parted '<Disk path>'
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
parted '/dev/vdc'
```
4. Execute o seguinte comando para alterar a unidade do padrão “GB” para “sector” para exibição e operação.
```
unit s
```
5. [](id:step5)Execute o seguinte comando para exibir as partições e registrar seus valores `Start`.
```
print
```
>! Registre os valores `Start`. Depois que uma partição é excluída e uma nova é criada, o valor `Start` deve permanecer inalterado. Caso contrário, os dados podem ser perdidos.
>
![](https://main.qcloudimg.com/raw/a4b3b6710d2d03549c26b8efd7d844db.png)
6. Execute o seguinte comando para excluir a partição existente.
```
rm <Partition Number>
```
Por exemplo, execute o seguinte comando para excluir a partição “1” do disco em nuvem.
```
 rm 1
```
7. Execute o seguinte comando para confirmar a exclusão. As informações retornadas são as mostradas abaixo:
```
print
```
![](https://main.qcloudimg.com/raw/fbac9760d06da56e3f3be3a61309cc10.png)
>!É possível executar imediatamente o comando `rescue` e inserir os valores `Start` e `End` conforme solicitado para restaurar uma partição que foi excluída acidentalmente.
>
8. Execute o seguinte comando para criar uma nova partição principal.
```
mkpart primary <Start sector of the original partition> 100%
```
O 100% no comando indica que essa partição vai para o fim do disco. Digite o valor `Start` obtido na [etapa 5](#step5). Neste documento, o setor inicial da partição original é 2048s (ou seja, o valor `Start` é 2048s), execute o seguinte comando:
```
mkpart primary 2048s 100%
```
Se aparecer um status conforme mostrado na figura a seguir, digite `Ignore`.
![](//mccdn.qcloud.com/static/img/c45966e20dc856817c65fd6b81155e4a/image.png)
9. Execute o seguinte comando para verificar se a nova partição foi criada com êxito.
```
print
```
Se o resultado mostrado na figura a seguir for retornado, a nova partição foi criada com êxito.
![](https://main.qcloudimg.com/raw/823646dcfd0e42ece63a37338e0d4e16.png)
10. Execute o seguinte comando para fechar a ferramenta parted.
```
quit
```
11. Execute o seguinte comando para verificar a partição estendida.
```
e2fsck -f <Partition path>
```
Considerando a nova partição “1” (seu caminho da partição é `/dev/vdc1`) como exemplo, execute o seguinte comando:
```
e2fsck -f /dev/vdc1
```
A figura a seguir mostra a saída do comando.
![](https://main.qcloudimg.com/raw/12c917c78829014cd784e3f184c01eed.png)
12. Use um comando específico do sistema de arquivos para redimensionar cada sistema de arquivos na nova partição.
 - Execute o seguinte comando no **EXT file system (Sistema de arquivos EXT)**.
```
resize2fs <Partition path>
```
Considerando o caminho da partição `/dev/vdc1` como exemplo, execute o seguinte comando:
```
resize2fs /dev/vdc1
```
Se o resultado mostrado na figura a seguir for retornado, a expansão obteve êxito.
![](https://main.qcloudimg.com/raw/7daebff27ce10c66b63c2b35c9712418.png)
 - Execute o seguinte comando no **XFS file system (Sistema de arquivos XFS)**.
```
xfs_growfs <Partition path>
```
Considerando o caminho da partição `/dev/vdc1` como exemplo, execute o seguinte comando:
```
xfs_growfs /dev/vdc1
```
13. Execute o seguinte comando para montar manualmente a nova partição.
```
mount <Partition path> <Mount point>
```
Considerando o caminho da partição `/dev/vdc1` e o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
mount /dev/vdc1 /data
```
14. Execute o seguinte comando para exibir a nova partição.
```
df -h
```
Se o resultado mostrado na figura a seguir for retornado, a montagem obteve êxito e você pode exibir o disco de dados.
![](https://main.qcloudimg.com/raw/476829f5a9cb6aef62f3cace31cb2586.png)

[](id:New)
### Formatação da capacidade expandida em uma nova partição GPT independente
1. Execute o seguinte comando como usuário raiz para confirmar as alterações na capacidade do disco em nuvem.
```
parted <Disk path> print
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
parted /dev/vdc print
```
Se uma mensagem conforme mostrada na figura a seguir aparecer no processo, digite `Fix`.
![](https://main.qcloudimg.com/raw/c69cd8b3741675f1a96715c4679ce6e6.png)
O tamanho do disco em nuvem é 2.147 GB após a expansão e a capacidade da partição existente é de 2.040 GB, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/8d8e72b1a5716443673453f67c1d798d.png)
2. Execute o seguinte comando para verificar se o disco em nuvem tem partições montadas.
```
mount | grep '<Disk path>' 
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
mount | grep '/dev/vdc'
```
 - O seguinte resultado indica que o disco em nuvem tem uma partição (vdc1) montada em `/data`.
![](https://main.qcloudimg.com/raw/1703f6594a1fbff86dd1d1dfb2ab124d.png)
Execute o seguinte comando para desmontar **todas as partições** do disco em nuvem.
```
umount <Mount point>
```
Considerando o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
umount /data
```
 - O seguinte resultado indica que não há partição montada. Prossiga para a próxima etapa.
![](https://main.qcloudimg.com/raw/d10d74c1fff5e8ffdb306d5acb664ae1.png)
3. Execute o seguinte comando para usar a ferramenta de partição parted.
```
parted '<Disk path>'
```
Considerando o caminho do disco `/dev/vdc` como exemplo, execute o seguinte comando:
```
parted '/dev/vdc'
```
4. [](id:Step4)Execute o seguinte comando para exibir as partições e registrar seus valores `End`, que serão usados como o deslocamento inicial da próxima partição.
```
print
```
![](https://main.qcloudimg.com/raw/7f11b89e481035897d525fa8a93cb7e7.png)
5. Execute o seguinte comando para criar uma partição principal. Essa partição começa no final das partições existentes e abrange todo o novo espaço no disco.
```
mkpart primary start end
```
Obtenha o valor `End` na [etapa 4](#Step4). Nesse exemplo, o valor `End` é 2.040 GB, execute o seguinte comando:
```
mkpart primary 2040GB 100%
```
6. Execute o seguinte comando para verificar se a nova partição foi criada.
```
print
```
Se a seguinte saída for retornada, a partição foi criada.
![](https://main.qcloudimg.com/raw/5e1418caaddf22932ac624ff906cf302.png)
7. Execute o seguinte comando para fechar a ferramenta parted.
```
quit
```
8. Execute o seguinte comando para formatar a nova partição em EXT2, EXT3, etc. conforme necessário.
```
mkfs.<fstype> <Partition path> 
```
Considerando EXT4 como exemplo, execute o seguinte comando: 
```
mkfs.ext4 /dev/vdc2
```
9. Execute o seguinte comando para montar manualmente a nova partição.
```
mount <Partition path> <Mount point>
```
Considerando o caminho da partição `/dev/vdc2` e o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
mount /dev/vdc2 /data
```
10. Execute o seguinte comando para exibir a nova partição:
```
df -h
```
Se o resultado mostrado na figura a seguir for retornado, a montagem obteve êxito e você pode exibir o disco de dados.
![](https://main.qcloudimg.com/raw/cd9d36d49388882f0cb898c13d565bb0.png)

## Documentação
[Extensão de partições e sistemas de arquivos (Windows)](https://cloud.tencent.com/document/product/362/6737)

## Perguntas frequentes
Se você encontrar um problema ao usar o CBS do Tencent Cloud, consulte os seguintes documentos para solucioná-lo, conforme necessário:
- [Perguntas frequentes sobre uso](https://intl.cloud.tencent.com/document/product/362/32409)
- [Perguntas frequentes sobre funcionalidades](https://intl.cloud.tencent.com/document/product/362/32408)
