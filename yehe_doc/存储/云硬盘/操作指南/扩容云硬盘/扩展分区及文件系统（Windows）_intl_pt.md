## Introdução

Depois de [expandir um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5747), é preciso atribuir sua capacidade expandida a uma partição existente ou formatá-la em uma nova partição independente.
- Se você expandir um disco em nuvem montado em um CVM em execução, será necessário **Rescan Disk (Examinar novamente o disco)** para reconhecer a capacidade do disco após a expansão.
- Se você expandir um disco em nuvem que está desmontado ou montado em um CVM inativo, a capacidade do disco após a expansão será reconhecida automaticamente.

>!
>- Estender o sistema de arquivos pode afetar os dados existentes. É altamente recomendável que você [crie um snapshot](https://intl.cloud.tencent.com/document/product/362/5755) manualmente para fazer backup de seus dados antes da operação.
>- Para estender o sistema de arquivos, é preciso [reiniciar a instância](https://intl.cloud.tencent.com/document/product/213/4928) ou examinar novamente o disco, o que levará à interrupção dos negócios por um determinado período. Recomendamos que você escolha um momento apropriado para essa operação.
>- Depois de estender o sistema de arquivos, é altamente recomendável que você [examine novamente os discos](#Scanning) para reconhecer a capacidade. Se você **Refresh (Atualizar)** o sistema ou fizer outras operações, a capacidade expandida pode não ser reconhecida.
>


## Pré-requisitos

- Você [expandiu a capacidade do disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5747).
- Você [montou o disco em nuvem](https://intl.cloud.tencent.com/document/product/362/32401) em um CVM do Windows e criou um sistema de arquivos.
- Você [fez login](https://intl.cloud.tencent.com/document/product/213/5435) no CVM do Windows no qual deseja estender as partições e o sistema de arquivos.
>?Este documento descreve como expandir um disco montado em um CVM no Windows Server 2012 R2. A expansão pode variar ligeiramente com os sistemas operacionais, portanto, esse documento é apenas para referência.
>

## Instruções
>!
>- Se você [expandir um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5747) que está montado em um CVM em execução, deve [examinar novamente o disco](#Scanning) para reconhecer a capacidade do disco em nuvem expandida antes de [estender os volumes](#Extending).
>- Se você [expandir um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5747) que está desmontado ou montado em um CVM inativo, pode prosseguir diretamente para [estender o volume](#Extending).

<span id="Scanning"></span>
### Examinar novamente o disco
1. Clique com o botão direito em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> e selecione **Computer Management (Gerenciamento do computador)**.
2. Na barra lateral esquerda da janela **Computer Management (Gerenciamento do computador)**, selecione **Storage (Armazenamento)** -> **Disk Management (Gerenciamento do disco)**.
3. Clique com o botão direito em **Disk Management (Gerenciamento do disco)** e selecione **Rescan Disks (Examinar novamente os discos)**, conforme mostrado abaixo:
4. Depois que a varredura for concluída, verifique se o disco de dados tem o tamanho após a expansão. (Neste exemplo, a varredura mostra que o disco em nuvem foi expandido de 10 GB para 50 GB). 

<span id="Extending"></span>
### Extensão de volumes

1. Clique com o botão direito em qualquer área branca do espaço em disco. Selecione **Extend Volume (Estender o volume)**.
2. Siga o Assistente de extensão de volume para estender o volume.
A nova capacidade do disco de dados será adicionada ao volume original.

## Ações relacionadas
‏[Extensão de sistemas de arquivos do Linux](https://intl.cloud.tencent.com/document/product/362/31602)
