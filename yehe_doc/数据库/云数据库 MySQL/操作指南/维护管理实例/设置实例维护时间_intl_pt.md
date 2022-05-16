## Visão geral
A janela de manutenção é um conceito muito importante para o TencentDB for MySQL. Para garantir a estabilidade de sua instância do TencentDB for MySQL, o sistema de back-end realiza operações de manutenção na instância durante a janela de manutenção de tempos em tempos. É altamente recomendável que você defina uma janela de manutenção aceitável para a sua instância, geralmente fora dos horários de pico, para minimizar possíveis impactos nas operações.

Além disso, é recomendável que as operações que envolvem a migração de dados também sejam executadas durante a janela de manutenção, como o ajuste de especificação da instância, o upgrade da versão da instância e o upgrade do kernel da instância. Atualmente, a janela de manutenção é permitida em instâncias de origem (source), réplicas somente leitura e instâncias de recuperação de desastres.

Considerando como exemplo o upgrade da especificação da instância de banco de dados, como esta operação envolve migração de dados, após a conclusão do upgrade, pode ocorrer uma desconexão momentânea do banco de dados. Quando o upgrade é iniciado, a **Switch Time (Hora de alternância)** pode ser selecionada como **During maintenance time (Durante o período de manutenção)**, para que a alternância de especificação da instância seja ativada na próxima **maintenance window (janela de manutenção)** após a conclusão do upgrade da instância. Observe que, ao fazer isso, a alternância não ocorrerá imediatamente após a conclusão do upgrade da especificação do banco de dados; em vez disso, a sincronização continuará até que a instância inicie a próxima **maintenance window (janela de manutenção)** quando a alternância será executada. Dessa forma, o tempo total necessário para o upgrade da instância pode ser estendido.

>?
>- Antes da manutenção do TencentDB for MySQL, serão enviadas notificações para os contatos configurados em sua conta da Tencent Cloud por SMS e e-mail.
>- A alternância de instância é acompanhada por uma desconexão do banco de dados com duração de apenas alguns segundos. Certifique-se de que suas instalações tenham um mecanismo de reconexão.

## Instruções
### Configuração da janela de manutenção
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de detalhes.
2. Na seção **Maintenance Info (Informações de manutenção)**, clique em **Modify (Modificar)**.
![](https://main.qcloudimg.com/raw/388e3aa6ca18c6cb947eb4d053ad1eb5.png)
3. Na caixa de diálogo pop-up, selecione **Maintenance Window (Janela de manutenção)** e **Maintenance Time (Período de manutenção)** e clique em **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/91738d5593aad8f573fde932420ae9fe.png)

<span id="lijiqiehuan"></span>
### Alternância imediata
Se uma tarefa estiver configurada para ser alternada durante a janela de manutenção, mas você precisar alterá-la com urgência em circunstâncias especiais, clique em **Switch Now (Alternar agora)** na coluna **Operation (Operação)**.
![](https://main.qcloudimg.com/raw/fd9780d4f9e1d8094bcb82f215deb366.png)

>?
>- A alternância imediata é aplicável a operações que envolvem migração de dados, como o ajuste de especificação da instância, o upgrade de versão da instância e o upgrade de kernel da instância.
>- Para upgrade de versão, se estiver associado a várias instâncias, a alternância será executada na ordem de réplica somente leitura para instância de origem (source).
