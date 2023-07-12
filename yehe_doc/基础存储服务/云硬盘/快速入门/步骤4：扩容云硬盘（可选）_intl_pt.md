## Visão geral
Você pode expandir um disco em nuvem para aumentar seu espaço de armazenamento. Este documento descreve como expandir um disco em nuvem pelo console e atribuir sua capacidade expandida a um sistema de arquivos existente.
>?Para obter mais informações sobre a expansão de discos em nuvem, consulte [Expansão da capacidade de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5747).
>

## Observações
Para proteger dados importantes, você pode [criar um snapshot](https://intl.cloud.tencent.com/document/product/362/5755) para fazer backup dos dados do seu disco em nuvem antes de expandi-lo.

## Pré-requisitos
Já ter [inicializado o disco em nuvem `cbs-test`](https://intl.cloud.tencent.com/document/product/362/31646).

## Orientações

#### Expansão de discos em nuvem (Windows)
### Expansão de discos em nuvem pelo console.
1. Faça login no console do CVM e clique em [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) na barra lateral à esquerda. 
2. Localize o disco em nuvem que será expandido e clique em **More (Mais)** > **Expand (Expandir)** na coluna **Operation (Operação)** à direita.

3. Na janela pop-up **Expand Disk Capacity (Expandir capacidade do disco)**, selecione uma nova capacidade e clique em **Next (Avançar)**.
4. Clique em **Adjust Now (Ajustar agora)**.

### Reescaneamento do disco
>?Este documento usa um CVM com Windows Server 2012 R2 DataCenter 64-bit chinês instalado como exemplo. As etapas podem ser diferentes dependendo da versão do sistema operacional. 
>
1. Faça login no CVM como administrador. Consulte [Login em uma instância do Windows usando RDP](https://intl.cloud.tencent.com/document/product/213/5435). 
2. Na área de trabalho, clique com o botão direito em <img src="https://main.qcloudimg.com/raw/3d815ac1c196b47b2eea7c3a516c3d88.png" style="margin:-6px 0px"> no canto inferior esquerdo e selecione **Computer Management (Gerenciamento do computador)**.
3. Clique com o botão direito em **Disk Management (Gerenciamento do disco)** e selecione **Rescan Disk (Reescanear disco)**.
4. Após escanear, confira se o tamanho do disco de dados foi expandido.

### Expansão de sistemas de arquivos de uma partição existente
>?Neste exemplo, nós atribuiremos a capacidade expandida a uma unidade de disco E existente. Para obter mais informações, consulte [Expansão de partições e sistemas de arquivos (Windows)](https://intl.cloud.tencent.com/document/product/362/31601).
>
1. Clique com o botão direito em qualquer lugar no espaço em branco do disco e selecione **Extend Volume (Expandir volume)**.
2. Siga as instruções do assistente de expansão de volume para aumentar o volume.
A nova capacidade do disco de dados será adicionada ao volume original.

#### Expansão de discos em nuvem (Linux)
### Expansão de discos em nuvem pelo console.
1. Faça login no console do CVM e clique em [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) na barra lateral à esquerda. 
2. Localize o disco em nuvem que será expandido e clique em **More (Mais)** > **Expand (Expandir)** na coluna **Operation (Operação)** à direita.
3. Na janela pop-up **Expand Disk Capacity (Expandir capacidade do disco)**, selecione uma nova capacidade e clique em **Next (Avançar)**.
4. Clique em **Adjust Now (Ajustar agora)**.

### Expansão de um sistema de arquivos
>?
>- Este documento usa um CVM com CentOS 7.8 instalado como exemplo. As etapas podem ser diferentes dependendo da versão do sistema operacional. 
>- Neste exemplo, nós atribuiremos a capacidade expandida a `/dev/vdb`. Para obter mais informações, consulte [Expansão online de partições e sistemas de arquivos](https://intl.cloud.tencent.com/document/product/362/39999).
>
1. Execute o comando a seguir para expandir o sistema de arquivos EXT.
```
resize2fs /dev/vdb
​``` 
A informação a seguir será exibida:

![](https://main.qcloudimg.com/raw/181bba4f10d3d5b48e2cbf331121affd.png)
2. Execute o comando a seguir para ver o resultado.
```
df -TH
``` 
Se for retornada uma informação semelhante ao mostrado abaixo, significa que o sistema de arquivos foi expandido.

![](https://main.qcloudimg.com/raw/7bb79ee4eca78a6ae77d2747967c0647.png)



## Documentação
- [Cenários de expansão do disco em nuvem](https://intl.cloud.tencent.com/document/product/362/31600)
- [Visão geral dos snapshots](https://intl.cloud.tencent.com/document/product/362/31638)
