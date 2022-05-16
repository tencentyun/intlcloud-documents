## Visão geral
Para aplicações com altos requisitos de continuidade de serviço, confiabilidade de dados e conformidade, o TencentDB for MySQL fornece instâncias de recuperação de desastres entre regiões diferentes para ajudar a aprimorar sua capacidade de fornecer serviços contínuos a custos baixos e melhorar a confiabilidade dos dados.
>?Uma instância de recuperação de desastres custa o mesmo que a instância de origem (source) associada a ela. Para mais informações, consulte [Preços do produto](https://buy.cloud.tencent.com/price/cdb).

#### Funcionalidades
- Com um endereço de conexão de banco de dados separado, uma instância de recuperação de desastres pode fornecer capacidade de acesso de leitura para vários cenários, como acesso local e análise de dados com custos mais baixos de redundância de dispositivos.
- A sua arquitetura de origem (source)/réplica altamente disponível ajuda a evitar pontos únicos de falha para bancos de dados.
- Os dados são sincronizados em uma rede privada com menor latência e maior estabilidade em comparação com a rede pública. 
- Atualmente, os dados sincronizados pela rede privada são gratuitos durante a promoção. Se forem necessárias cobranças, notificaremos você com antecedência.

#### Como funciona
- Se uma instância do TencentDB for usada como banco de dados de recuperação de desastres, essa instância será o backup da instância de origem (source).
- Quando ocorrer qualquer alteração na instância de origem (source), as informações de log que registram a alteração serão copiadas para a instância de recuperação de desastres e, em seguida, a sincronização de dados será implementada por meio da reprodução do log.
- Se ocorrer alguma falha na instância de origem (source), a instância de recuperação de desastres pode ser ativada em segundos para fornecer capacidade total de leitura/gravação.

## Limites da funcionalidade
- As instâncias de recuperação de desastres podem ser adquiridas apenas para instâncias de origem (source) ativadas para GTID de alta disponibilidade no MySQL 5.6 ou versão posterior com o mecanismo InnoDB com uma especificação de 1 GB de memória e 50 GB de capacidade de disco ou superior. Se sua instância de origem (source) estiver abaixo dessa especificação, primeiro faça o upgrade dela.
>?Se o GTID não estiver ativado, você poderá ativá-lo na página de detalhes da instância no [console](https://console.cloud.tencent.com/cdb/). Essa operação leva muito tempo e a instância será desconectada por vários segundos. Recomendamos fazer isso fora dos horários de pico e adicionar um mecanismo de reconexão nos programas que acessam o banco de dados.
- A especificação mínima de uma instância de recuperação de desastres é de 1 GB de memória e 50 GB de capacidade de disco e deve ser pelo menos 1,1 vezes a capacidade de armazenamento usada pela instância de origem (source).
- Uma instância de origem (source) pode ter no máximo uma instância de recuperação de desastres. Mesmo que a instância de recuperação de desastres existente esteja isolada, você não poderá criar outras.
- A instância de recuperação de desastres não fornece as seguintes funcionalidades: projeto de transferência, reversão, operação SQL, configurações de parâmetros, alteração do conjunto de caracteres, gerenciamento de contas, alteração de porta, importação de dados, log de reversão e instância somente leitura.

## Instruções
### Criação de uma instância de recuperação de desastres
#### Etapa 1. Criar uma instância de recuperação de desastres
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Na lista de instâncias, clique no ID de uma instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a sua página de detalhes.
2. Certifique-se de que a funcionalidade GTID esteja ativada exibindo as informações básicas da instância na página **Instance Details (Detalhes da instância)**. Clique em **Add Disaster Recovery Instance (Adicionar instância de recuperação de desastres)** no diagrama de arquitetura da instância para acessar a página de aquisição da instância de recuperação de desastres.
![](https://main.qcloudimg.com/raw/d41ae3d97935763b180f2e8a26cb2364.png)
3. Na página de aquisição, defina as informações básicas da instância de recuperação de desastres, como **Billing Mode (Modo de faturamento)**, **Region (Região)** e **Sync Policy (Política de sincronização)**.
 - Se a política de sincronização for **Sync Now (Sincronizar agora)**, os dados serão sincronizados imediatamente quando a instância de recuperação de desastres for criada.
 - Se a política de sincronização for **Sync After Creation (Sincronizar após a criação)**, você precisará configurar um link de sincronização de recuperação de desastres após a criação bem-sucedida da instância. Para instruções mais detalhadas, consulte [Criar um link de sincronização](#cjtblj) abaixo.
>?
>- O tempo necessário para concluir a criação depende da quantidade de dados, durante o qual nenhuma operação pode ser executada na instância de origem (source) no console. Faça isso em um momento apropriado.
>- Apenas os dados da instância inteira podem ser sincronizados. Certifique-se de que o espaço em disco é suficiente.
>- Você precisa garantir que a instância de origem (source) esteja com o status “Running (Em execução)” e nenhuma das tarefas de ajuste de configuração, tarefas de reinicialização e outras tarefas de modificação sejam executadas. Caso contrário, a tarefa de sincronização pode falhar.  
4. Após confirmar se tudo está correto, clique em **Buy Now (Comprar agora)** e aguarde a entrega da instância de recuperação de desastres.
5. Retorne à lista de instâncias. Após o status da instância mudar para “Running (Em execução)”, ela poderá ser usada normalmente.

#### [Etapa 2. Criar um link de sincronização (opcional)](id:cjtblj)
>?Se a **Sync Policy (Política de sincronização)** escolhida durante a aquisição da instância for **Sync After Creation (Sincronizar após a criação)**, você precisará configurar um link de sincronização de recuperação de desastres após a criação bem-sucedida da instância. Ao fazer isso, você pode implementar a recuperação remota de desastres.

1. Na página **Instance Details (Detalhes da instância)** da instância de origem (source), você pode exibir o status de sincronização da instância de recuperação de desastres. Clique em **Create Sync Task (Criar tarefa de sincronização)** para criar uma ligação de sincronização de rede privada com a instância de origem (source) para a instância de recuperação de desastres.
![](https://main.qcloudimg.com/raw/f2f941ccf588d54cb2687cc0a9d0a961.png)
2. Insira o nome da tarefa, confirme as informações do banco de dados de origem (source) e destino, e clique em **Save and Next (Salvar e avançar)**.
![](https://main.qcloudimg.com/raw/5a2b3ef40de69af903cc60396d8f1a84.png)
3. Selecione o objeto a ser sincronizado. A sincronização de toda a instância ou de determinadas tabelas é aceita. Atualmente, o tipo de sincronização não pode ser personalizado.
![](https://main.qcloudimg.com/raw/ac3f2db7c68f708ac07bb597a420ae83.png)
4. Clique em **Save and Check (Salvar e verificar)** para verificar a tarefa. Logo após concluir a verificação, clique em **Start Task (Iniciar tarefa)**. Em seguida, você pode exibir os detalhes da tarefa na página **Disaster Recovery Sync (Sincronização de recuperação de desastres)** no console.
![](https://main.qcloudimg.com/raw/4cc319646447bb20a5a76982a0783a49.png)

### Gerenciamento de instâncias de recuperação de desastres
- **Exibir instâncias de recuperação de desastres**
Uma instância de recuperação de desastres pode ser exibida nas regiões em que está localizada. Você pode usar a lista de instâncias para filtrar todas as instâncias em uma região específica.
![](https://main.qcloudimg.com/raw/1ade1aa59f7c5cd74b2cf30299d31cac.png)
- **Exibir a relação entre a instância de origem (source) e a instância de recuperação de desastres**
Clique no ícone à direita de uma instância de recuperação de desastres ou instância de origem (source) para exibir sua relação.
![](https://main.qcloudimg.com/raw/4b98a6b2831c027af52a37050aa16f2d.png)
![](https://main.qcloudimg.com/raw/f08c6d3dd53a40ea544bdadc9e111ee8.png)
- **Exibir atraso de sincronização**
Exiba o atraso de sincronização entre a instância de origem (source) e a instância de recuperação de desastres na parte superior da página **Instance Details (Detalhes da instância)** da instância de recuperação de desastres.
![](https://main.qcloudimg.com/raw/d06a9c821f5ebd04173ee6e453ef5ef2.png)
- **Funcionalidades de instância de recuperação de desastres**
Uma instância de recuperação de desastres tem várias funcionalidades, como exibição de detalhes da instância, monitoramento de instância, gerenciamento de backup e registro em log de consultas lentas.
 
### Promoção de uma instância de recuperação de desastres para instância de origem (source)
Você pode promover uma instância de recuperação de desastres para instância de origem (source) no console conforme necessário.
1. Faça login no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), clique no ID da instância de recuperação de desastres a ser promovida na lista de instâncias e acesse a sua página de gerenciamento.
2. Clique em **Promote to Source Instance (Promover a instância de origem (source))** no canto superior direito, para promover a instância de recuperação de desastres a instância de origem (source). Após a promoção, o link de sincronização com a instância de origem (source) será desconectado, para que a instância promovida possa obter capacidade de gravação de dados e funcionalidade completa do MySQL.
>!O link de sincronização desconectado não pode ser reconectado. Prossiga com cuidado.
> 
![](https://main.qcloudimg.com/raw/c4e1517d56c630ff845c89060402e657.png)

