## Cenário
Este documento descreve como gerenciar grupos de posicionamento disperso. Para obter mais informações sobre o grupo de posicionamento, consulte [Grupo de posicionamento](https://intl.cloud.tencent.com/document/product/213/15486).

## Instruções
### Criação de um grupo de posicionamento

1. Faça login no [console do grupo de posicionamento do CVM](https://console.cloud.tencent.com/cvm/ps).
2. Clique em **Create (Criar)**.
3. Na janela que é exibida, insira um nome para o grupo de posicionamento e selecione a camada do grupo de posicionamento.
4. Clique em **OK** para concluir a criação.

### Inicialização de uma instância no grupo de posicionamento
1. Vá para a [página de aquisição do CVM](https://buy.cloud.tencent.com/?tab=custom&step=1&devPayMode=hourly&regionId=33&instanceType=SA2.SMALL1&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR).
2. Conclua a aquisição conforme solicitado na página.
Durante o processo de aquisição, certifique-se de realizar as seguintes operações:
 - Ao configurar o CVM, clique em **Advanced Configuration (Configuração avançada)**, selecione **Add Instance to Placement Group (Adicionar instância ao grupo de posicionamento)** e selecione um grupo de posicionamento existente.
 Se nenhum grupo de posicionamento existente atender aos seus requisitos, [crie um](https://console.cloud.tencent.com/cvm/ps?regionId=1) no console.
 - Ao confirmar as informações de configuração, insira a quantidade total de instâncias a serem incluídas no grupo de posicionamento, que deve ser menor que o limite de quantidade definido para o grupo de posicionamento.


### Modificação do grupo de posicionamento de uma instância
> Atualmente, só é possível alterar o nome de um grupo de posicionamento. Para fazer isso, conclua as seguintes etapas.
>
1. Faça login no [console do grupo de posicionamento do CVM](https://console.cloud.tencent.com/cvm/ps).
2. Passe o cursor sobre o ID ou nome do grupo de posicionamento de destino e clique em <img src="https://main.qcloudimg.com/raw/beb5eae230dc169f7274bda7a19a5aa6.png" style="margin: 0;"></img>.
3. Na janela exibida, insira o novo nome.
4. Clique em **OK** para concluir a modificação.

### Exclusão de um grupo de posicionamento
> É possível excluir um grupo de posicionamento que precisa ser substituído ou que não é mais necessário. É necessário encerrar todas as instâncias em execução no grupo de posicionamento antes de excluí-lo. Para fazer isso, conclua as seguintes etapas.
>
1. Faça login no [console do grupo de posicionamento do CVM](https://console.cloud.tencent.com/cvm/ps).
2. Clique em **Number of Instances (Quantidade de instâncias)** para o grupo de posicionamento a ser excluído, para ir para a página de gerenciamento de instância e encerrar todas as instâncias no grupo.
3. Retorne ao console do grupo de posicionamento, selecione o grupo a ser excluído e clique em **Delete (Excluir)**.
6. Na janela exibida, clique em **OK** para finalizar a exclusão.
É possível excluir um único grupo de posicionamento ou vários em lotes.
