
## Visão geral

A Migração de serviço é uma plataforma desenvolvida pela Tencent Cloud para ajudar as empresas a migrar sistemas operacionais, aplicativos e dados de aplicativos de um servidor de origem para um Cloud Virtual Machine (CVM) ou um Cloud Block Storage (CBS). Ela ajuda a atender às necessidades corporativas de nuvem, migração entre nuvens, migração entre contas ou regiões e implantação de nuvem híbrida.

A migração de serviço inclui a migração offline e online. A migração offline inclui:
- A [migração de instância offline](#cvmStep) permite que você migre imagens do disco do sistema para um CVM específico.
- A [migração de dados offline](#csmStep) permite que você migre imagens do disco de dados para um CBS específico.

## Pré-requisitos

A migração offline requer o Cloud Object Storage (COS). Certifique-se de que sua região seja compatível com o COS.
Para obter mais informações sobre as regiões compatíveis com o COS, consulte [Regiões e pontos de extremidade de acesso](https://intl.cloud.tencent.com/document/product/436/6224).

## Preparações

>! 
> - Atualmente, a migração de serviço do Tencent Cloud aceita imagens nos formatos qcow2, vhd, vmdk e raw. Recomendamos o uso do formato de imagem compactado para reduzir o tempo de transmissão e migração.
> - A região do COS para onde as imagens são carregadas deve ser a mesma de onde está localizado o CVM para o qual você deseja migrar.
> - Durante a migração offline, o tamanho do arquivo de imagem carregado não pode ser maior do que a capacidade do disco para o qual você deseja migrar. Se o tamanho do arquivo de imagem for 50 GB, o disco do sistema deve ter pelo menos 50 GB.
> - A migração offline não é compatível com snapshot (nome de arquivo semelhante a \*-00000\*.vmdk).

 - Crie uma imagem para o servidor que precisa ser migrado conforme as instruções na documentação de criação de imagens.
    - Para Windows, consulte [Preparação de imagem do Windows](https://intl.cloud.tencent.com/document/product/213/17815).
    - Para Linux, consulte [Preparação de imagem do Linux](https://intl.cloud.tencent.com/document/product/213/17814).
 - Carregue o arquivo de imagem criado para o COS.  
    - Como os arquivos de imagem são grandes, o upload usando o navegador pode falhar. Recomendamos usar a ferramenta COSCMD para fazer o upload de imagens. Para obter mais informações, consulte [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
    - Se as imagens exportadas de outras plataformas em nuvem forem pacotes compactados (como arquivos .tar.gz), é possível carregá-los diretamente para o COS.
 - Obtenha o endereço do COS da imagem enviada.
No [console do COS](https://console.cloud.tencent.com/cos5/bucket), localize o arquivo de imagem que você acabou de enviar e veja as informações dele para obter o link do arquivo.
 - Prepare o CVM ou o CBS para onde será feita a migração.
[Clique aqui para adquirir um CVM >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&regionId=8).
[Clique aqui para ver as instruções de aquisição do CBS >>](https://intl.cloud.tencent.com/document/product/362/32414).


## Instruções

<span id="cvmStep"></span>
### Migração de instância offline

1. Faça login no console do CVM e clique em **[Service Migration (Migração de serviço)](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** na barra lateral esquerda.
2. Clique em **Create an instance migration task (Criar uma tarefa de migração de instância)**.
3. Conclua as etapas de preparação conforme solicitado e clique em **Next (Avançar)**.
4. Selecione a região, insira as informações de configuração, como nome da tarefa, link do COS e a instância do CVM para a qual migrar. Em seguida, clique em **Complete (Concluir)** para criar uma tarefa de migração.
Durante a migração, é possível sair da página [Service Migration (Migração de serviço)](https://console.cloud.tencent.com/cvm/csm/index?rid=4) ou fechá-la. Também é possível retornar a essa página a qualquer momento para verificar o andamento da tarefa. 
>!  
> - O arquivo do COS deve ser configurado com permissões de leitura pública e gravação privada. Para obter mais informações, consulte [Definição da permissão de acesso a objetos](https://intl.cloud.tencent.com/document/product/436/13327).
> - A capacidade do disco do sistema da instância para a qual você deseja migrar não pode ser menor que o tamanho do arquivo de imagem carregado. Caso contrário, a tarefa falhará.
> 

<span id="csmStep"></span>
### Migração de dados offline

1. Faça login no console do CVM e clique em **[Service Migration (Migração de serviço)](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** na barra lateral esquerda.
2. Clique em **Create a data migration task (Criar uma tarefa de migração de dados)**.
3. Conclua as etapas de preparação conforme solicitado e clique em **Next (Avançar)**.
4. Selecione a região, insira as informações de configuração, como nome da tarefa, link do COS e o disco em nuvem para o qual migrar. Em seguida, clique em **Complete (Concluir)** para criar uma tarefa de migração.
Durante a migração, é possível sair da página [Service Migration (Migração de serviço)](https://console.cloud.tencent.com/cvm/csm/index?rid=4) ou fechá-la. Também é possível retornar a essa página a qualquer momento para verificar o andamento da tarefa. 
>! A capacidade do disco do CBS para o qual você deseja migrar não pode ser menor que o tamanho do arquivo de imagem carregado. Caso contrário, a tarefa falhará.
>

## Perguntas frequentes

Para obter mais informações, consulte [Sobre a migração de serviço](https://intl.cloud.tencent.com/document/product/213/32395).






