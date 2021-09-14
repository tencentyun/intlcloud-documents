## Cenário

Quando você precisar montar um disco em nuvem elástico que é um **disco de dados** em outro CVM, é possível desmontar esse disco em nuvem elástico de um CVM e, em seguida, montá-lo em outros CVMs. **A desmontagem de um disco em nuvem elástico não apaga os dados desse disco.**
Atualmente, a desmontagem de discos em nuvem elásticos que são **disco de dados** é compatível. Não é possível desmontar discos do sistema ou discos em nuvem não elásticos. **Para desmontar um disco em nuvem, você deve executar operações `umount` (Linux) ou offline (Windows). Caso contrário, o disco em nuvem elástico pode não ser reconhecido pelo CVM na próxima vez que for montado**

## Pré-requisitos

Antes de desmontar o disco de dados, certifique-se de compreender os seguintes pré-requisitos:
- Em sistemas operacionais Windows:
 - Para evitar a perda de dados, recomendamos que você suspenda as operações de leitura e gravação em todos os sistemas de arquivos do disco. Caso contrário, os dados que não foram lidos ou gravados serão perdidos.
 - Ao desmontar um disco em nuvem elástico, defina primeiro o disco para o estado offline. Caso contrário, você não conseguirá remontar o disco em nuvem elástico, a menos que reinicie o CVM. Isso é mostrado na figura a seguir:
- Em sistemas operacionais Linux:
 - Primeiro, você deve [fazer login](https://intl.cloud.tencent.com/document/product/213/5436) na instância e executar uma operação `umount` no disco em nuvem elástico que deseja desmontar. Se você forçar diretamente a desmontagem sem executar a operação `umount`, pode ocorrer o problema mostrado na figura a seguir durante o desligamento e a inicialização:
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
- Se você criar um volume lógico LVM no CVM, desmontar o disco diretamente do console fará com que parte dos dados do dispositivo permaneçam na memória do CVM. Se um aplicativo do CVM tentar percorrer ou acessar esse dispositivo, ocorrerá um erro de sistema. Como resultado, primeiro você deve executar as seguintes operações (esse exemplo considera que o volume lógico /dev/test/lv1 é criado com base em /dev/vdb1 e é montado no diretório /data):
 a. Execute o comando `umount /data` para desmontar o disco do ponto de montagem correspondente no CVM.
 b. Execute o comando `lvremove /dev/test/lv1` para remover o LV. Caso haja vários LVs, remova todos os LVs um por um.
 c. Execute o comando `vgremove test` para remover o VG.
 d. Execute o comando `pvremove /dev/vdb1` para remover o PV.
 e. Modifique o arquivo `/etc/fstab` para evitar a montagem contínua do LV correspondente na próxima inicialização.

## Instruções

### Uso do console para desmontar discos em nuvem

1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. É possível usar os seguintes métodos para desmontar um disco em nuvem:
    a. Desmontagem única: na linha do disco em nuvem de destino com o status **Mounted (Montado)**, clique em **More (Mais)** > **Unmount (Desmontar)**.
    b. Desmontagem em lote: selecione vários discos em nuvem de destino com o status **Mounted (Montado)** e clique em **Unmount (Desmontar)** no topo da lista.
3. Na caixa de prompt **Unmount Cloud Disk (Desmontar disco em nuvem)** que é exibida, verifique o aviso e clique em **Confirm (Confirmar)** para desmontar.

### Uso de API para desmontar discos em nuvem

É possível usar a API `DetachDisks` para desmontar um disco em nuvem. Para obter mais informações, consulte [Desmontagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/16316).

