## Introdução ao LVM
O Gerenciador de volume lógico (LVM, na sigla em inglês) divide seus discos ou partições em unidades de extensões físicas (PEs, na sigla em inglês) com o mesmo tamanho ao criar uma camada lógica sobre os discos e as partições. Ele combina diferentes discos e partições no mesmo grupo de volume (VG, na sigla em inglês), para que você possa criar volumes lógicos (LVs, na sigla em inglês) no VG, e os sistemas de arquivos nos LVs.
Em comparação com o uso de partições de disco diretamente, o LVM permite o escalonamento elástico dos seus sistemas de arquivos.
- O sistema de arquivos não está mais limitado pelo tamanho do disco físico. Na verdade, ele pode ser distribuído em vários discos:
Por exemplo, você pode adquirir 3 discos em nuvem elásticos de 4 TB e usar o LVM para criar um sistema de arquivos maior com até 12 TB.
- Você pode redimensionar os LVs de forma dinâmica em vez de reparticionar seus discos.
Quando a capacidade do VG do LVM não consegue atender às suas necessidades, você pode adquirir um disco em nuvem elástico à parte, montá-lo na sua instância do CVM e escalonar seu VG adicionando o disco em nuvem a ele.

## Criação do LVM

<dx-alert infotype="explain" title="">
Os exemplos a seguir usam 3 discos em nuvem elásticos para criar um sistema de arquivos redimensionável de forma dinâmica por meio do LVM:
![](https://main.qcloudimg.com/raw/81086e80477ff7e374e7c3f0fe9d2788.png)
</dx-alert>

### Etapa 1: criar um volume físico (PV)
1. [Faça login no seu CVM do Linux](https://intl.cloud.tencent.com/document/product/213/5436) como usuário raiz.
2. Execute o seguinte comando para criar os PVs:

```
pvcreate <disk path 1> ... <disk path N>
```
Use `/dev/vdc`, `/dev/vdd` e `/dev/vde` como exemplo e execute:
```
pvcreate /dev/vdc /dev/vdd /dev/vde
```
A figura a seguir mostra a saída do comando quando a criação obtém êxito:
![](https://main.qcloudimg.com/raw/5b92a6c7878e22906599af48bfa09d95.png)

3. Veja os volumes físicos no sistema atual com o comando:

```
lvmdiskscan | grep LVM
```
![](https://main.qcloudimg.com/raw/1de75af4a49c2deea689a2576eb075d9.png)

### Etapa 2: criar um grupo de volume (VG)
1. Execute o seguinte comando para criar um grupo de volume:

```
vgcreate [-s <specified PE size>] <VG name> <PV path>.
```
Considere que você queira criar um VG chamado “lvm_demo0” e execute:
```
vgcreate lvm_demo0 /dev/vdc /dev/vdd
```
A figura a seguir mostra a saída do comando quando a criação obtém êxito:
![](https://main.qcloudimg.com/raw/3b8dba3329f62e85d2075fad10898632.png)

Quando a mensagem "Volume group <VG name> successfully created (Grupo de volume <VG name> criado com êxito)" for exibida, significa que seu VG foi criado com êxito.
 - Após a criação, você pode adicionar um novo PV ao VG com o comando:

```
vgextend VG name New PV path
```
A figura a seguir mostra a saída do comando quando a operação obtém êxito:
![](https://main.qcloudimg.com/raw/105e5a77472f173ffd4a58624f20a863.png)
 - Após criado, você pode executar `vgs`, `vgdisplay` ou outros comandos para exibir os VGs no sistema atual, conforme mostrado abaixo:

![](https://main.qcloudimg.com/raw/309c991d32cf4b801ddbe8d898f1bfbb.png)

### Etapa 3: criar um volume lógico (LV)

1. Execute o seguinte comando para criar um LV:

```
lvcreate [-L <LV size>][-n <LV name>] <VG name>.
```
Considere que você queira criar um volume lógico de 8 GB chamado "lv_0" e execute:
```
lvcreate -L 8G -n lv_0 lvm_demo0.
```
A figura a seguir mostra a saída do comando quando a criação obtém êxito:
![](https://main.qcloudimg.com/raw/ed6d2f827ae7c4a4630bf17e24d90df2.png)

<dx-alert infotype="explain" title="">
Execute `pvs` e você verá que os 8 GB vêm apenas de `/dev/vdc`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/2718d08f7c74b7b469a23473a1398dfe.png)
</dx-alert>

### Etapa 4: criar e montar um sistema de arquivos
1. Crie um sistema de arquivos em um LV existente usando o comando:

```
mkfs.ext3 /dev/lvm_demo0/lv_0.
```
2. Monte o sistema de arquivos com o comando:

```
mount /dev/lvm_demo0/lv_0 vg0/.
```
A figura a seguir mostra a saída do comando quando a montagem obtém êxito:
![](https://main.qcloudimg.com/raw/2a7701636c2604d67e0743de4f9a6af1.png)

### Etapa 5: realizar escalonamento dinâmico no seu volume lógico e no sistema de arquivos

<dx-alert infotype="notice" title="">
LVs podem ser escalonados de forma dinâmica apenas quando a capacidade do VG não está totalmente utilizada. Ao escalonar a capacidade de um LV, você também precisa escalonar o sistema de arquivos criado nesse LV.
</dx-alert>

1. Escalone um LV executando este comando:

```
lvextend [-L +/- <capacity amount>] <LV path>.
```
Considere que você queira aumentar a capacidade do LV chamado “lv_0” em 4 GB, então execute:
```
lvextend -L +4G /dev/lvm_demo0/lv_0.
```
A figura a seguir mostra a saída do comando quando o escalonamento obtém êxito:

![](https://main.qcloudimg.com/raw/eccd7d6aec587eb90ec655a384367595.png)

<dx-alert infotype="explain" title="">
Execute `pvs` e você verá que `/dev/vdc` foi totalmente usado, e 2 GB foram usados de `/dev/vdd`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/189155ca377ef9550c4587ca78ab5b27.png)
</dx-alert>

2. Escalone o sistema de arquivos com o comando

```
resize2fs /dev/lvm_demo0/lv_0.
```
A figura a seguir mostra a saída do comando quando o escalonamento obtém êxito:
![](https://main.qcloudimg.com/raw/2e37f35678014ab1ca398fe5470a754b.png)
Após a conclusão, você pode executar o comando a seguir para ver se a capacidade do seu LV mudou para 12 GB:
```
df -h
```
