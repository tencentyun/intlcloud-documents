## Cenários de operação 
Este documento descreve como modificar uma tabela no console do TcaplusDB. Se você deseja modificar a definição da estrutura de uma tabela, pode fazê-lo modificando a tabela sob a condição de que a nova definição atenda às regras de modificação de tabelas do TcaplusDB.

## Pré-requisitos
Você criou uma tabela. Para obter mais informações, consulte [Criação de tabela](https://intl.cloud.tencent.com/document/product/1016/32715).

## Instruções
1. Acesse a página [Lista de tabelas](https://console.cloud.tencent.com/tcaplusdb/table) e selecione a tabela em questão. Selecione **More (Mais)** > **Modify (Modificar)** na coluna "Operation (Operação)" ou selecione várias tabelas e clique em **Batch Modify (Modificar em lote)** na parte superior.
2. Na caixa de diálogo "Modify (Modificar)" exibida, carregue ou selecione um novo arquivo de definição de tabela e clique em **Compare Difference (Comparar as diferenças)**.
> 
>- O campo da chave principal não pode ser excluído.
>- O nome e o tipo do campo da chave principal não podem ser modificados.
>- Você não pode adicionar novos campos de chave principal.
>- Um campo geral marcado como obrigatório não pode ser excluído.
>- O nome e o tipo de campos com o mesmo identificador não podem ser modificados.
>- Um novo campo geral deve ser nomeado de acordo com a convenção de nomenclatura.
>
![](https://main.qcloudimg.com/raw/407bf6c819bf9b60d4ebd18928904a6b.png)
3. Na caixa de diálogo pop-up, você pode exibir o resultado da comparação. Se sua nova definição de tabela não atender às regras de modificação de tabelas do TcaplusDB, um prompt será exibido.
![](https://main.qcloudimg.com/raw/087642d98430e6e1d066ae5dfc202f1a.png)
4. Clique em **Preview (Visualizar)** na coluna "Comparison Preview (Visualização da comparação)" para exibir a comparação entre as estruturas da tabela nova e antiga.
![](https://main.qcloudimg.com/raw/997d4e6cd91e2815a8534f44e2ee10de.png)
5. Após confirmar todas as informações, clique em **Confirm (Confirmar)** para enviar sua solicitação de modificação da tabela, e um prompt será retornado se a modificação for bem-sucedida.
![](https://main.qcloudimg.com/raw/53fc68f54fcbaf6726874e9af3c26463.png)
   Ao final da modificação, você pode exibir a estrutura da nova tabela na página de configuração da tabela.
   
