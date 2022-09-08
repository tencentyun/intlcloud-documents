## Visão geral
Se o seu disco em nuvem tiver uma partição MBR que contém o sistema de arquivos, com um tamanho de disco inferior a 2 TB após a expansão, é possível usar um dos seguintes métodos para estender as partições e os sistemas de arquivos:
- [Atribuição da capacidade expandida a uma partição MBR existente](#Add)
- [Formatação da capacidade expandida em uma nova partição MBR independente](#New)


## Pré-requisitos
É possível usar ferramentas de expansão automática, incluindo fdisk, e2fsck e resize2fs para adicionar a capacidade expandida do disco em nuvem ao sistema de arquivos existente em um CVM do Linux. Para garantir uma expansão com êxito, os seguintes requisitos devem ser atendidos:
- A forma de expandir e particionar foi confirmada. Para obter mais informações, consulte [Determinação do método de expansão](https://intl.cloud.tencent.com/document/product/362/39995).
- O sistema de arquivos é EXT2, EXT3, EXT4 ou XFS.
- O sistema de arquivos atual não tem nenhum erro.
- O tamanho do disco após a expansão não excede 2 TB.
- Use o Python versão 2 apenas por causa da compatibilidade com as ferramentas de expansão neste documento.



## Instruções

[](id:Add)
### Atribuição da capacidade expandida a uma partição MBR existente
Execute o seguinte comando como usuário raiz para consultar partições do disco em nuvem.
```
lsblk
```
 - A saída a seguir indica que há apenas uma partição. Nesse caso, é possível realizar a [expansão automática](#AutomaticExpansion) usando ferramentas.
 ![](https://main.qcloudimg.com/raw/297d678489b57dd70171a8882c9416f4.png)
 - A saída a seguir indica que há duas partições: `vdb1` e `vdb2`. Nesse caso, é necessário escolher uma partição a ser estendida conforme as instruções em [expansão manual](#ManualExpansion).
![](https://main.qcloudimg.com/raw/070f2144acc543c84d4ab8ab3db25620.png)

<dx-tabs>
::: Automatic\sExpansion[](id:AutomaticExpansion)
<blockquote class="doc-tip"><p class="doc-tip-tit"><i class="doc-icon-tip"></i>Observação</p>Esse método é aplicável apenas ao cenário em que há apenas uma partição. Se você tiver duas ou mais partições, escolha a [expansão manual](#ManualExpansion).</p>
</blockquote>


1. Execute o seguinte comando como usuário raiz para desmontar a partição.
``` 
umount <Mount point>
```
Considerando o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
umount /data
```
2. Execute o seguinte comando para baixar uma ferramenta de expansão.
```
wget -O /tmp/devresize.py https://raw.githubusercontent.com/tencentyun/tencentcloud-cbs-tools/master/devresize/devresize.py
```
3. Execute o seguinte comando para usar a ferramenta de expansão.
```
python /tmp/devresize.py <Disk path>
```
Considerando o caminho do disco `/dev/vdb` e o sistema de arquivos `vdb1` como exemplo, execute o seguinte comando:
```
python /tmp/devresize.py /dev/vdb
```
 - Se `The filesystem on /dev/vdb1 is now XXXXX blocks long.` for a saída conforme abaixo, a expansão obteve êxito. Em seguida, realize a [etapa 4](#step4MBR).
![](https://main.qcloudimg.com/raw/689209e1d1f8a227274e8e65be07d2ec.png)
 - Se `[ERROR] - e2fsck failed!!` for a saída, realize as seguintes etapas:
   a. Execute o seguinte comando para corrigir a partição em que o sistema de arquivos está localizado.
```
fsck -a <Partition path>
```
Considerando o caminho do disco `/dev/vdb` e o sistema de arquivos `vdb1` como exemplo, execute o seguinte comando:
```
fsck -a /dev/vdb1
```
   b. Depois que a partição for corrigida, execute o seguinte comando novamente para usar a ferramenta de expansão.
```
python /tmp/devresize.py /dev/vdb
```
4. [](id:step4MBR)Execute o seguinte comando para montar manualmente a partição estendida. Este documento usa o ponto de montagem `/data` como exemplo.
```
mount <Partition path> <Mount point>
```
- Se uma partição no caminho da partição `/dev/vdb1` existir antes da expansão, execute o seguinte comando:
```
mount /dev/vdb1 /data
```
5. Execute o seguinte comando para exibir a capacidade da partição após a expansão.
```
df -h
```
Se o resultado semelhante ao da figura a seguir for retornado, a montagem obteve êxito e é possível exibir o disco de dados.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
6. Execute o seguinte comando para exibir as informações de dados da partição original após a expansão e verifique se o novo espaço de armazenamento foi adicionado ao sistema de arquivos.
```
ll /data
```
:::
::: Manual\sExpansion[](id:ManualExpansion)
1. Execute o seguinte comando como usuário raiz para desmontar a partição.
```
umount <Mount point>
```
Considerando o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
umount /data
```
2. Execute o seguinte comando para estender a partição `vdb2`. Substitua `vdb2` por sua partição real ao usar o comando. 
```
growpart /dev/vdb 2
```
3. Execute o seguinte comando para estender o sistema de arquivos da partição.
```
resize2fs /dev/vdb2
```
Se a seguinte saída for retornada, o sistema de arquivos foi estendido.
![](https://main.qcloudimg.com/raw/ba8d2693823a3eb0ccfc4dd097f09ed5.png)

4. [](id:step4MBR)Execute o seguinte comando para montar manualmente a partição estendida. Este documento usa o ponto de montagem `/data` como exemplo.
```
mount <Partition path> <Mount point>
```
Se uma partição no caminho da partição `/dev/vdb2` existir antes da expansão, execute o seguinte comando:
```
mount /dev/vdb2 /data
```
5. Execute o seguinte comando para exibir a capacidade da partição após a expansão.
```
df -h
```
Se o resultado semelhante ao da figura a seguir for retornado, a montagem obteve êxito e é possível exibir o disco de dados.

![](https://main.qcloudimg.com/raw/92cd4cc0e9b1c08975603f73e922266f.png)

6. Execute o seguinte comando para exibir as informações de dados da partição original após a expansão e verifique se o novo espaço de armazenamento foi adicionado ao sistema de arquivos.
```
ll /data
```
:::
</dx-tabs>


[](id:New)
### Formatação da capacidade expandida em uma nova partição MBR independente
1. Execute o seguinte comando como usuário raiz para visualizar a partição montada do disco de dados.
```
df -h
```
Conforme mostrado na figura a seguir, a partição montada do disco de dados é de 20 GB.
![](https://main.qcloudimg.com/raw/4f57fd2e0038dc1fba5a4389d01ab7dc.png)
2. Execute o seguinte comando para exibir o disco de dados que não tem partição após a expansão:
```
fdisk -l
```
Conforme mostrado na figura a seguir, o disco de dados foi expandido para 30 GB.

![](https://main.qcloudimg.com/raw/f21420374b4334a790022c95bac1fe0f.png)

3. Execute o seguinte comando para desmontar todas as partições montadas.
```
umount <Mount point>
```
Considerando o ponto de montagem `/data` como exemplo, execute o seguinte comando:
```
umount /data
```
>? Depois que todas as partições forem desmontadas do disco em nuvem, execute a [etapa 4](#Step4MBR) novamente.
>

4. [](id:Step4MBR)Execute o seguinte comando para criar uma partição.
```
fdisk <Disk path>
```
Considerando o caminho do disco `/dev/vdb` como exemplo, execute o seguinte comando:
```
fdisk /dev/vdb
```
Execute as etapas a seguir em sequência, quando solicitado.
 1. Digite **p** para verificar as partições existentes, como `/dev/vdb1` neste documento.
 2. Digite **n** para criar uma partição.
 3. Digite **p** para criar uma partição principal.
 4. Digite ** 2** para criar a segunda partição principal.
 5. Pressione **Enter** duas vezes para usar o tamanho da partição padrão.
 6. Digite **w** para salvar a tabela de partição e iniciar o particionamento.
 Consulte a figura abaixo:

![](https://main.qcloudimg.com/raw/894ba5a11a73d56a0a165ee7cb49e7c6.png)

>? Este documento usa a criação de uma partição como exemplo. Também é possível criar várias partições para atender às suas necessidades.
>
5. Execute o seguinte comando para exibir a nova partição.
```
fdisk -l
```
A figura a seguir mostra que a nova partição `vdb2` foi criada.
![](https://main.qcloudimg.com/raw/d604d00955d0db5f052e964ecd409cc3.png)
6. Execute o seguinte comando para formatar a nova partição e criar um sistema de arquivos no formato desejado, como EXT2 ou EXT3.
```
mkfs.<fstype> <Partition path> 
```
Considerando EXT4 como exemplo, execute o seguinte comando:
```
mkfs.ext4 /dev/vdb2
```
A figura a seguir mostra a criação bem-sucedida do sistema de arquivos EXT.
![](https://main.qcloudimg.com/raw/db15ed11252e6db8adb706f61ed14225.png)

7. Execute o seguinte comando para criar um ponto de montagem.
```
mkdir <New mount point>
```
Considerando o novo ponto de montagem `/data1` como exemplo, execute o seguinte comando:
```
mkdir /data1
```
8. Execute o seguinte comando para montar manualmente a nova partição.
```
mount <New partition path> <New mount point>
```
Considerando o novo caminho da partição `/dev/vdb2` e o novo ponto de montagem `/data1` como exemplo, execute o seguinte comando:
```
mount /dev/vdb1 /data2
```
9. Execute o seguinte comando para exibir a nova partição.
```
df -h
```
Se o resultado mostrado na figura a seguir for retornado, a montagem obteve êxito e você pode exibir o disco de dados.
![](https://main.qcloudimg.com/raw/465c988014acc85957078335d776bfc3.png)
>? Para permitir que o CVM monte automaticamente um disco de dados na reinicialização ou inicialização, execute a [etapa 10](#AddNewPartINFOstep10) e a [etapa 11](#AddNewPartINFOstep11) para adicionar a nova partição a `/etc/fstab`.

10. [](id:AddNewPartINFOstep10)Execute o seguinte comando para adicionar a partição.
```
echo '/dev/vdb2 /data1 ext4 defaults 0 0' >> /etc/fstab
```
11. [](id:AddNewPartINFOstep11)Execute o seguinte comando para exibir a partição.
```
cat /etc/fstab
```
Se o resultado mostrado na figura a seguir for retornado, a partição foi adicionada com êxito.
![](https://main.qcloudimg.com/raw/761a846bafe385b24dfb322a6ad2977f.png)

## Documentação
[Extensão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)

## Perguntas frequentes
Se você encontrar um problema ao usar o CBS do Tencent Cloud, consulte os seguintes documentos para solucioná-lo, conforme necessário:
- [Perguntas frequentes sobre uso](https://intl.cloud.tencent.com/document/product/362/32409)
- [Perguntas frequentes sobre funcionalidades](https://intl.cloud.tencent.com/document/product/362/32408)
