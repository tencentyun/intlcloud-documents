
## Cenário
É possível ajustar a mídia do hardware de armazenamento conforme necessário.
O Tencent Cloud fornece dois tipos de armazenamento em bloco: o [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/213/4953) e o [Armazenamento local](https://intl.cloud.tencent.com/document/product/213/5798). Atualmente, a mudança de discos locais para discos em nuvem é compatível. Este documento descreve como alterar o tipo de mídia do disco.
As desvantagens dos CVMs com discos locais:
- Não é possível personalizar a configuração devido ao limite de recursos do host.
- Funcionalidades como os snapshots e a aceleração da criação não são compatíveis.
- Baixa confiabilidade de dados.
- As falhas de host terão um impacto mais longo.

Para evitar as desvantagens de CVMs com discos locais, é possível alterar os CVMs existentes com discos locais em sua conta para CVMs com discos em nuvem.

<span id="LocalDiskPrecondition"></span>
## Pré-requisitos
- **Status do CVM**
 Esta operação só pode ser realizada quando um CVM está no estado **Desligado**. Primeiro, desligue o CVM.
- **Tipo do CVM**
 - A mudança de discos locais para discos em nuvem não é compatível em CVMs spot.
 - A mudança de discos locais para discos em nuvem não é compatível em CVMs dedicados.
 - A mudança de discos locais para discos em nuvem não é compatível em CVMs como big data modelos D1 e D2 e alta E/S modelos I3 e I4.
 - A mudança de discos locais para discos em nuvem não é compatível em instâncias de bare-metal.
- **Configuração do CVM**
 - É possível alterar os discos locais para discos em nuvem apenas quando houver pelo menos um **disco local regular** ou **disco local SSD** entre o disco do sistema e os discos de dados do CVM.
 - É possível alterar os discos locais para discos em nuvem apenas quando os discos em nuvem estão disponíveis na zona de disponibilidade do CVM e o tamanho dos discos locais está dentro da faixa aceita pelos discos em nuvem.
 - Se o disco do sistema e os discos de dados do CVM forem discos locais, quando você alterar o tipo de mídia do disco, ele se aplicará a **todos** os discos locais do CVM. Também será possível configurar o tipo de disco em nuvem para cada disco separadamente.
 Isso significa que quando você altera o tipo de mídia do disco para um CVM cujos discos são todos locais, não é possível alterar apenas o disco do sistema ou apenas os discos de dados para discos em nuvem. Se você fizer a alteração, ela se aplicará a todos os discos.
 - Alterar o tipo de mídia de um disco não altera seu tamanho. Depois de alterar o tipo de mídia, é possível [expandir os discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5747).
 - Alterar os discos locais para discos em nuvem não mudará o ciclo de vida de um CVM, o ID da instância, o IP de redes interna/externa, o nome do disco nem o ponto de montagem.

<span id="LocalDiskNotice"></span>
## Observações

- Quando você altera um disco local para um disco em nuvem, todos os dados do disco local precisam ser copiados para o disco em nuvem. Dependendo do tamanho do disco e da velocidade de transmissão, isso pode demorar um pouco. 
- Só é possível alterar os discos locais para discos em nuvem, não o contrário.
- **Recomenda-se iniciar e fazer login no CVM para verificar se há perda de dados após a conclusão da alteração**.

## Instruções
1. Faça login no console do CVM e acesse **Instances (Instâncias)**.
> Se o CVM já tiver sido desligado, vá para a [Etapa 3](#step3).
2. À direita do CVM que você deseja alterar, clique em **More (Mais)** > **Instance Status (Status da instância)** > **Shutdown (Desligar)** para desligar o CVM.
<span id="step3"></span>
3. À direita do CVM que você deseja alterar, clique em **More (Mais)** > **Resource Adjustment (Ajuste de recursos)** > **Change Disk Media Type (Alterar tipo de mídia do disco)**.
4. Na janela pop-up, selecione o tipo de disco em nuvem que deseja usar para o disco do sistema e os discos de dados, marque a caixa de consentimento e clique em **Convert Now (Converter agora)**.
5. Verifique novamente as informações, efetue o pagamento, se aplicável, e aguarde a conclusão do processo.
 
