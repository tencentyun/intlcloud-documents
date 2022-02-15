## Cenários de operação 
Este documento descreve como excluir uma tabela no console do TcaplusDB.
>Se você excluir uma tabela inteira, todos os seus dados serão completamente apagados e não poderão ser recuperados; portanto, faça-o com cuidado.
>
Uma tabela com o status "RUNNING (EM EXECUÇÃO)" pode ser excluída. Depois de excluída, ela será movida para a lixeira, mas seus dados ainda existem.

## Pré-requisitos
Você criou uma tabela. Para obter mais informações, consulte [Criação de tabela](https://intl.cloud.tencent.com/document/product/1016/32715).

## Instruções
1. Acesse a página [Lista de tabelas](https://console.cloud.tencent.com/tcaplusdb/table) e selecione a tabela em questão. Selecione **More (Mais)** > **Delete (Excluir)** na coluna "Operation (Operação)" ou selecione várias tabelas e clique em **Batch Delete (Excluir em lote)** na parte superior.
![](https://main.qcloudimg.com/raw/4698c628245093b1597caa2166f68cae.png)
2. Na caixa de diálogo "Delete (Excluir)" exibida, clique em **Confirm (Confirmar)** e a tabela será movida para a lixeira.
3. Selecione **Recycle Bin (Lixeira)** na barra lateral esquerda. Na lixeira, você pode **excluir** uma tabela inteira do seu sistema ou **restaurá-la** para o status "RUNNING (EM EXECUÇÃO)".
![](https://main.qcloudimg.com/raw/f752d04243ff5bdf7aff655d493781fa.png)

   
