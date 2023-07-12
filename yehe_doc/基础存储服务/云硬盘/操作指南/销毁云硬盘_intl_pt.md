## Cenário
Quando o disco em nuvem não estiver mais em uso e **tiver sido feito o backup dos dados importantes**, você poderá liberar os recursos virtuais encerrando o disco em nuvem. Depois de encerrar o disco em nuvem, você não será cobrado por ele. **Quando o disco em nuvem é encerrado, todos os dados dele são excluídos ao mesmo tempo e não podem ser recuperados. Os discos em nuvem que forem encerrados não poderão ser recuperados. Prossiga com cuidado.**
O ciclo de vida de um disco em nuvem não elástico segue o do CVM e só pode ser encerrado quando o CVM for encerrado. Para obter mais informações, consulte [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930).
- O ciclo de vida de um disco em nuvem elástico é independente do CVM. Portanto, pode ser encerrado independentemente do CVM. Este artigo descreve as operações para encerrar discos em nuvem elásticos.
Os discos em nuvem elásticos podem ser encerrados pelos seguintes métodos:

- Encerramento manual
  - O encerramento manual é compatível com discos em nuvem com pagamento conforme o uso e entra em vigor imediatamente. 
- Encerramento automático
 - O disco em nuvem com pagamento conforme o uso com saldo negativo por mais de 24 horas será encerrado. Se a taxa de renovação for paga dentro do tempo especificado, o disco pode continuar a ser usado.

## Pré-requisitos
- O disco em nuvem está no status **To Be Mounted (A ser montado)**. Para os discos em nuvem que estão montados, primeiro realize a [desmontagem](https://intl.cloud.tencent.com/document/product/362/32400).
- Você já **fez backup dos dados importantes** de acordo com os requisitos empresariais**.

## Encerramento manual de discos em nuvem com pagamento conforme o uso
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. É possível usar os seguintes métodos para encerrar um disco em nuvem:
    a. Encerramento único: selecione **More (Mais)** > **Terminate/Return (Encerrar/Retornar)** na linha do disco em nuvem de destino com o status **To Be Mounted (A ser montado)**.
    b. Encerramento em lote: selecione vários discos em nuvem de destino com o status **To Be Mounted (A ser montado)** e clique em **Terminate/Return (Encerrar/Retornar)** no topo da lista.

>Quando o disco em nuvem é encerrado, todos os dados dele são excluídos ao mesmo tempo e não podem ser recuperados. Os discos em nuvem que forem encerrados não poderão ser recuperados. Prossiga com cuidado.
>
3. Na caixa pop-up **Terminate Cloud Disk (Encerrar disco em nuvem)**, clique em **Confirm (Confirmar)** para concluir o encerramento.
 O disco em nuvem de destino não será mais faturado e **está completamente encerrado e não pode ser recuperado**.

