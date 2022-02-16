## Cenários de operação
Você pode criar um alarme para avisá-lo sobre a mudança de status de um produto na nuvem e enviar mensagens relacionadas. O alarme criado determina se uma notificação de alarme precisa ser disparada de acordo com os resultados da comparação entre uma métrica de monitoramento e um limite específico a cada intervalo.
Você pode tomar as medidas preventivas ou corretivas apropriadas em tempo hábil quando o alarme for disparado. Portanto, alarmes criados corretamente podem ajudá-lo a melhorar a robustez e a confiabilidade de seus aplicativos. Para obter mais informações sobre alarmes, consulte [Configuração de alarmes](https://intl.cloud.tencent.com/document/product/248/38916) no Cloud Monitor.

Se quiser enviar uma mensagem de alarme para um status específico de um produto, primeiro você precisa criar uma política de alarme, que possui três componentes obrigatórios: o nome, o tipo e a condição de disparo do alarme. Cada política de alarme é um conjunto de condições de disparo de alarme na relação lógica OR (OU), ou seja, desde que uma das condições de disparo seja satisfeita, o alarme será disparado. A notificação de alarme será enviada a todos os usuários associados à política de alarme. Eles podem tomar as medidas adequadas quando receberem a notificação.

>Certifique-se de ter definido o destinatário do alarme padrão; caso contrário, a política de alarme padrão do TencentDB não conseguirá enviar notificações.


## Instruções
### Criação de política de alarme
1. Faça login no [console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) e selecione **Alarm Configuration (Configuração de alarme)** > **Alarm Policy (Política de alarme)** na barra lateral esquerda.
2. Na lista de políticas de alarme, clique em **Add (Adicionar)**.
3. Defina o nome da política, o tipo de política, o produto alvo, o objeto de alarme e a condição de disparo.
 - Policy Type (Tipo de política): selecione "TcaplusDB".
 - Alarm Object (Objeto de alarme): selecione todos os objetos ou tabelas especificadas. O objeto a ser associado pode ser encontrado selecionando a região na qual o objeto está localizado ou pesquisando o ID do objeto.
 - Trigger Condition (Condição de disparo): um disparo de alarme é uma condição semântica que consiste em métrica, relação de comparação, limite, período estatístico e duração.
 - Os canais de alarme aceitos incluem SMS e e-mail.
4. Depois de confirmar todas as informações, clique em **Complete (Concluir)**.

### Associação de objeto
Depois que a política de alarme for criada, você poderá associar alguns objetos de alarme a ela. Quando um objeto de alarme satisfizer uma condição de disparo de alarme, uma notificação de alarme será enviada.
1. Na lista de políticas de alarme, clique no nome de uma política para entrar na página de gerenciamento dela.
2. Clique em **Add Object (Adicionar objeto)** na página de gerenciamento da política de alarme.
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Selecione o serviço desejado do Tencent Cloud e clique em **Apply (Aplicar)** para associá-lo à política de alarme.

### Configuração do destinatário do alarme
Os destinatários do alarme são aqueles que receberão as mensagens do alarme.
1. Na lista de políticas de alarme, clique no nome de uma política.
2. Na página de gerenciamento da política de alarme, selecione **Alarm Recipient Object (Objeto destinatário do alarme)** e clique em **Edit (Editar)**.
3. Selecione o grupo de usuários a ser notificado, defina as opções relevantes e clique em **Save (Salvar)**.

