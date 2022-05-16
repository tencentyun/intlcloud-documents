## Cenários de operação
Com base nas suas necessidades de operações, você pode devolver as instâncias com pagamento conforme o uso no console por meio de autoatendimento.
- Após uma instância de pagamento conforme o uso for devolvida, ela será movida para a lixeira do TencentDB e retida lá por 24 horas. Durante o período de retenção, a instância não poderá ser acessada, mas poderá ser restaurada.

Quando uma instância for devolvida e seu status mudar para “isolated (isolada)”, nenhuma taxa relacionada a ela será incorrida.
>
>- Após encerramento da instância, seus dados não poderão ser recuperados e seus arquivos de backup também serão encerrados; portanto, os dados não poderão ser restaurados na nuvem. Armazene seus arquivos de backup com segurança em outro lugar com antecedência.
>- Quando a instância for encerrada, seus recursos de IP serão liberados simultaneamente. Se a instância tiver instâncias somente leitura ou instâncias de recuperação de desastres:
> - As instâncias somente leitura serão encerradas ao mesmo tempo.
> - As instâncias de recuperação de desastres desconectarão suas conexões de sincronização e serão promovidas a instâncias mestres automaticamente.


## Instruções
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), selecione a instância em questão na lista de instâncias e selecione **More (Mais)** > **Terminate/Return (Encerrar/Devolver)** ou **Terminate/Return & Refund (Encerrar/Devolver e reembolsar)** na coluna “Operation (Operação)”.
![](https://main.qcloudimg.com/raw/ea0d80564ad54c6c9e3ea43070c71f20.png)
2. Na caixa de diálogo pop-up, selecione “I have read and agreed to Termination Rules (Li e concordo com as Regras de encerramento)” e clique em **Terminate Now (Encerrar agora)**.

>
![](https://main.qcloudimg.com/raw/6e376a4a726195aefee841930577a5b3.png)
