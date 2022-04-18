
Este documento descreve como habilitar a separação de leitura/gravação do proxy de banco de dados no console do TencentDB for MySQL.

Com o recurso de [separação de leitura/gravação do proxy do banco de dados](https://intl.cloud.tencent.com/document/product/236/41093), você pode configurar o endereço do proxy do banco de dados em seu aplicativo para encaminhar automaticamente solicitações de gravação para a instância de origem e solicitações de leitura para a instância somente leitura.

## Pré-requisitos
- Ter [habilitado o proxy de banco de dados](https://intl.cloud.tencent.com/document/product/236/41087).
- Ter [criado uma instância somente leitura](https://intl.cloud.tencent.com/document/product/236/7270) para a instância de origem. Se nenhuma instância somente leitura tiver sido criada, a página de habilitação do recurso solicitará que você compre uma.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, selecione uma instância de origem com proxy habilitado e clique em seu ID ou em **Manage (Gerenciar)**  na coluna **Operation (Operação)** para entrar na página de gerenciamento de instâncias.
2. Na página de gerenciamento de instâncias, selecione **Database Proxy (Proxy de banco de dados)** > **Read/Write Separation (Separação de leitura/gravação)** > **Enable Now (Habilitar agora)**.
![](https://main.qcloudimg.com/raw/b07508f045b727ca63c294b707159474.png)
3. Na janela exibida, defina itens de configuração como **Remove Delayed RO Instances (Remover instâncias RO atrasadas)** e peso e clique em **OK**.
>!
>- Somente instâncias de origem e somente leitura que estão no status **Running (Em execução)** podem ser adicionadas ao proxy de banco de dados.
>- Atualmente, instâncias somente leitura remotas ou atrasadas não podem ser montadas no proxy de banco de dados.
>
 - **Remove Delayed RO Instances (Remover instâncias de RO atrasadas)**: especifique se deseja ativar a política de remoção. Se uma exceção de replicação (como atraso ou interrupção de replicação) ocorrer em uma instância somente leitura, o proxy de banco de dados removerá a instância temporariamente da separação de leitura/gravação. O limite de atraso é de 10 segundos por padrão e pelo menos 1 instância somente leitura deve ser mantida.
 >?O conjunto **Delay Threshold (Limite de atraso)** e **Least RO Instances (Menos instâncias de RO)** têm efeito apenas para novas conexões.
 >
    - Se o atraso de uma instância somente leitura exceder o limite, a instância será removida, seu peso será automaticamente definido como 0 após a remoção e o sistema enviará um alarme para você (você deve assinar o alarme da "remoção de nó montado no proxy do banco de dados" primeiro. Para a configuração, consulte [Políticas de alarme (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457)).
    - A instância será colocada de volta no proxy do banco de dados quando seu atraso cair abaixo do limite. Não importa se a remoção de instância somente leitura atrasada está habilitada, uma instância somente leitura que é removida devido a uma falha de instância se juntará novamente ao proxy de banco de dados quando for reparada.
    - Depois que **Least RO Instances (Menos instâncias de RO)** for definido, se o proxy do banco de dados descobrir que o número de instâncias somente leitura sendo roteadas é menor que o valor definido, ele adicionará instâncias somente leitura excepcionais para a separação de leitura/gravação até que o número de instâncias na separação de leitura/gravação seja maior ou igual ao valor definido.
Observação: se uma falha fatal (como tempo de inatividade) ocorrer em uma instância somente leitura, ela não poderá ser retida e contada em **Least RO Instances (Menos instâncias de RO)**.
 - **Assign Read Weight (Atribuir peso de leitura)**: dois métodos de atribuição de peso (atribuição automática pelo sistema e atribuição personalizada) são suportados para configurar os pesos de leitura das instâncias de origem e somente leitura. O valor do peso deve ser um número inteiro entre 0 e 100.
 >?A atribuição de peso de leitura configurada tem efeito imediato para todas as conexões.
 >
    - O proxy do banco de dados atribuirá o tráfego de solicitação de leitura de acordo com os pesos definidos; por exemplo, se os pesos de duas instâncias somente leitura forem 10 e 20, respectivamente, seu tráfego de solicitação de leitura será atribuído em uma proporção de 1:2.
    - O peso aqui refere-se apenas ao peso da solicitação de leitura, pois as solicitações de gravação são roteadas diretamente para o banco de dados de origem sem participar do cálculo de peso; por exemplo, se um cliente enviar 10 instruções de gravação e 10 instruções de leitura, e a proporção dos pesos de instância de origem e somente leitura for 1:1, a instância de origem receberá 10 instruções de gravação e 5 instruções de leitura, e a instância somente leitura receberá apenas 5 instruções de leitura.
    - Se você selecionar **Assigned by system (Atribuído pelo sistema)**, o sistema atribuirá pesos automaticamente com base na especificação de CPU e memória da instância, e você só poderá definir o peso da instância de origem neste caso.
    - Se o peso de uma instância somente leitura for 0, o proxy de banco de dados não se conectará à instância. Se seu peso for alterado de 0 para outro valor, o peso terá efeito apenas para novas conexões.
 - **Failover**: recomendamos que você habilite este parâmetro, para que o proxy de banco de dados possa enviar solicitações de leitura para a instância de origem se todas as instâncias somente leitura forem excepcionais.
 >?O recurso de failover configurado tem efeito apenas para novas conexões.
 >
Se esse parâmetro estiver desabilitado, quando uma instância somente leitura for excepcional, as solicitações de leitura não serão enviadas para a instância de origem (para evitar que a instância de origem seja afetada por uma alta carga de leitura). No entanto, todas as solicitações de leitura falharão, e, em seguida, o proxy de banco de dados fechará proativamente a conexão com o cliente.
 - **Apply to Newly Added RO Instances (Aplicar a instâncias de RO recém-adicionadas)**: depois que esse parâmetro for habilitado, as instâncias somente leitura criadas posteriormente para a instância de origem serão adicionadas automaticamente ao proxy do banco de dados.
![](https://main.qcloudimg.com/raw/f2eb858b2b37fd134913738b243a17e8.png)
4. Após habilitar com sucesso o recurso de separação de leitura/gravação, você pode visualizar suas informações básicas e diagrama de arquitetura e modificar os itens de configuração relevantes na guia **Read/Write Separation (Separação de leitura/gravação)**.
  - Você pode clicar em **Modify (Modificar)** no canto superior direito para configurar **Remove Delayed RO Instances (Remover instâncias de RO atrasadas)**, atribuir pesos e modificar outros itens de configuração novamente.
  - Você pode clicar em **Disable Read/Write Separation (Desabilitar separação de leitura/gravação)** no canto superior direito para desabilitar a separação de leitura/gravação do proxy de banco de dados.
![](https://main.qcloudimg.com/raw/098c9fae971719881b6d20eee6ba0e73.png)
