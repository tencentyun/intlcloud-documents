## Cenário

O sistema de arquivos do Windows normalmente usa o formato NTFS ou FAT32, já o sistema de arquivos do Linux costuma usar formatos da série EXT. Quando o sistema operacional de um CVM é alterado de Windows para Linux, o disco de dados do CVM permanece no mesmo formato do sistema operacional original. Como resultado, após a reinstalação do sistema, o CVM pode não conseguir acessar o sistema de arquivos do disco de dados. Este documento descreve como ler um disco de dados no sistema Windows original após a reinstalação do sistema operacional do Windows para o Linux.

## Instruções

### Ativação de um sistema Linux para aceitar NTFS 

1. Faça login no CVM do Linux após a reinstalação.
2. Execute o comando a seguir para instalar o programa de software ntfsprogs, a fim de ativar o CVM do Linux para aceitar o acesso ao sistema de arquivos NTFS.
>? Este documento usa o CentOS como exemplo. Observe que tipos de sistemas Linux diferentes requerem comandos de instalação diferentes. Portanto, sempre execute o comando de instalação correspondente para o seu tipo de sistema operacional.
>
```
yum install ntfsprogs
```


### Montagem de um disco de dados do CVM do Windows para o CVM do Linux

>? Se o disco de dados em seu CVM do Windows foi montado no CVM do Linux, ignore esta operação.
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na barra lateral esquerda, clique em **[Cloud Block Storage](https://console.cloud.tencent.com/cvm/cbs)** para acessar a página de gerenciamento dele.
3. Selecione o disco de dados do Windows a ser montado e **More (Mais)** > **Mount (Montar)**.
4. Na janela "Mount to CVM (Montar no CVM)" exibida, selecione o CVM do Linux em questão e clique em **OK**.
5. Faça login no CVM do Linux no qual o disco de dados do Windows foi montado.
6. Execute o comando a seguir para consultar o disco de dados montado no CVM do Windows.
```
parted -l
```
Informações semelhantes às seguintes serão retornadas:
```
Model: Virtio Block Device (virtblk)
Disk /dev/vdb: 53.7GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
Number  Start   End     Size    File system  Name                          Flags
 1      17.4kB  134MB   134MB                Microsoft reserved partition  msftres
 2      135MB   53.7GB  53.6GB  ntfs         Basic data partition
```
7. Execute o comando a seguir para montar o disco de dados.
```
mount -t ntfs-3g data disk path mount target
```
Por exemplo, para montar o disco de dados em `/dev/vdb2` para `/mnt`, execute o seguinte comando:
```
mount -t ntfs-3g /dev/vdb2 /mnt
```
Como o sistema de arquivos pode ser reconhecido pelo sistema operacional, o sistema Linux pode ler e gravar dados diretamente no disco de dados montado.

