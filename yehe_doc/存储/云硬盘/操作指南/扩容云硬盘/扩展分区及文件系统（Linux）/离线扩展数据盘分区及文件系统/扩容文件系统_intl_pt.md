## Visão geral
Este documento descreve como estender um sistema de arquivos após fazer login na instância do CVM. Este método é adequado para cenários em que o sistema de arquivos é criado diretamente sem particionar o disco em nuvem.

## Instruções
1. Execute o seguinte comando para determinar o tipo de sistema de arquivos.
```
df -ihT
```
 - O seguinte resultado mostra um sistema de arquivos EXT.
![](https://main.qcloudimg.com/raw/198ad9bcb209db6ed1934e02f3234f8b.png)
 - O seguinte resultado mostra um sistema de arquivos XFS.
![](https://main.qcloudimg.com/raw/50ecea03c960daa2d04b734226ad69a0.png)
2. Use o comando específico do sistema de arquivos para estender o sistema de arquivos.
 - Considerando `/dev/vdb` como exemplo, execute o seguinte comando para estender um sistema de arquivos EXT:
```
resize2fs /dev/vdb
```
Se a seguinte saída de comando for retornada, a expansão obteve êxito.
![](https://main.qcloudimg.com/raw/9f68b0ab1e6446943da4e426df92919b.png)
 - Considerando `/dev/vdc` como exemplo, execute o seguinte comando para estender um sistema de arquivos XFS:
```
xfs_growfs /dev/vdc
```
Se a seguinte saída de comando for retornada, a expansão obteve êxito.
![](https://main.qcloudimg.com/raw/56fac50edbb153585adb67b2eb246cf4.png)
3. Execute o seguinte comando para exibir o espaço em disco do sistema de arquivos.
```
df -h
```
