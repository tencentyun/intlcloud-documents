O TencentDB for MySQL permite a atualização automática ou manual de versão secundária do kernel. A atualização adiciona novos recursos, melhora o desempenho e corrige problemas.
Para obter detalhes sobre a versão secundária do kernel do TencentDB for MySQL, consulte [Atualizações de versão do kernel](https://intl.cloud.tencent.com/document/product/236/35989).

>?Atualmente, as instâncias básicas de nó único não permitem a atualização de versão secundária do kernel.

## Visão geral
- **Atualização automática**:
 - Cenário 1: quando um bug grave ou vulnerabilidade de segurança ocorre no TencentDB for MySQL, o sistema realizará a atualização da versão secundária do kernel do banco de dados durante a janela de manutenção e enviará notificações de atualização por meio do Centro de mensagens do console e via SMS.
 - Cenário 2: quando uma instância do TencentDB for MySQL é migrada devido a um upgrade/downgrade de configuração de instância, expansão/redução da capacidade de armazenamento ou upgrade de versão do banco de dados etc., o sistema atualizará automaticamente o kernel da instância para a versão secundária mais recente.
- **Atualização manual**:
Você também pode atualizar manualmente a versão secundária do kernel no console.


## Regras de atualização
- Se uma instância a ser atualizada estiver associada a outras instâncias (por exemplo, instância de origem e réplicas somente leitura), essas instâncias serão atualizadas juntas para garantir a consistência dos dados.
- A atualização do TencentDB for MySQL envolve a migração de dados. O tempo necessário para migrar uma instância depende do tamanho dos dados da mesma. Sua empresa não será afetada durante a atualização e poderá ser acessada normalmente.

## Observações
- A alternância de instância pode ser necessária após a conclusão da atualização da versão (ou seja, a instância do MySQL pode ser desconectada por alguns segundos). Recomendamos que os aplicativos sejam configurados com o recurso de reconexão automática e que a alternância de instância seja realizada durante a janela de manutenção da instância. Para obter mais informações, consulte [Configuração da janela de manutenção da instância](https://intl.cloud.tencent.com/document/product/236/10929).
- Se o número de tabelas em uma única instância exceder um milhão, a atualização pode falhar e o monitoramento do banco de dados pode ser afetado. Certifique-se de que o número de tabelas em uma única instância não seja superior a um milhão.
- A versão secundária do kernel não pode ser rebaixada depois de atualizada.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique no ID da instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para entrar na página de detalhes da instância.
2. Na seção **Configuration Info (Informações de configuração)**, clique em **Upgrade Kernel Minor Version (Atualizar versão secundária do kernel)**.
![](https://main.qcloudimg.com/raw/3fda3cffc784b3cde619e698d728d486.png)
3. Na caixa de diálogo pop-up, selecione o horário de alternância e clique em **Upgrade (Atualizar)**.
>!Como a atualização do banco de dados envolve a migração de dados, após a conclusão da atualização, pode ocorrer uma desconexão muito curta do banco de dados MySQL, com duração de apenas alguns segundos. Recomendamos que você selecione **During maintenance time (Durante o período de manutenção)** como o período de alternância para que ela seja iniciada no próximo período de manutenção, após a conclusão da atualização da instância.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c758e092bce297bbfeb553297bf9b266.png)

