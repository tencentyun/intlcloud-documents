## Cenários de operação 
Este documento descreve como fazer backup de uma tabela no console do TcaplusDB.

## Pré-requisitos
Você criou uma tabela. Para obter mais informações, consulte [Criação de tabela](https://intl.cloud.tencent.com/document/product/1016/32715).

## Instruções
### Backup automático
O TcaplusDB fará o backup automático das tabelas à 1h (horário de Pequim) todos os dias, e os dados do backup serão retidos por 7 dias, após os quais serão excluídos automaticamente.

### Backup manual
Se você deseja fazer o backup de uma tabela manualmente, você pode fazê-lo no console.
**Método 1:**
1. Acesse a página [Lista de tabelas](https://console.cloud.tencent.com/tcaplusdb/table), selecione a tabela em questão e clique em **More (Mais)** > **Back up (Fazer backup)** na coluna "Operation (Operação)", ou selecione várias tabelas e clique em **Batch Backup (Backup em lote)** na parte superior.
2. Na caixa de diálogo pop-up de backup, digite os comentários e clique em **Confirm (Confirmar)** para fazer backup das tabelas selecionadas.

**Método 2:**
Acesse a página [Lista de tabelas](https://console.cloud.tencent.com/tcaplusdb/table), clique em um ID de tabela para acessar a página de detalhes da tabela e clique em **Manual Backup (Backup manual)** no canto superior direito para fazer backup da tabela.

