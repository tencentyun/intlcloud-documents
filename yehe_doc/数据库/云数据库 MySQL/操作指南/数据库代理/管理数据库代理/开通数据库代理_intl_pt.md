
Este documento descreve como habilitar o proxy de banco de dados no console do TencentDB for MySQL.

[O proxy de banco de dados](https://intl.cloud.tencent.com/document/product/236/42048) é um serviço de proxy de rede entre o serviço TencentDB e o serviço de aplicativo. Ele é usado para efetuar proxy de todas as solicitações quando o serviço de aplicativo acessa o banco de dados. Ele fornece recursos avançados, como separação automática de leitura/gravação, pool de conexão e persistência de conexão, além de alta disponibilidade, alto desempenho, compatibilidade com OPS e facilidade de uso.


## Observações
- O proxy de banco de dados atualmente é compatível com as seguintes regiões:
  - Pequim (exceto Zonas 1, 2 e 4), Xangai (exceto Zona 1), Guangzhou (exceto Zonas 1 e 2), Chengdu (exceto Zona 1), Chongqing, Nanjing e Hong Kong (China) (exceto Zona 1) ).
  - Tóquio (exceto Zona 1), Bangkok (exceto Zona 1), Virgínia (exceto Zona 1), Vale do Silício (exceto Zona 1), Mumbai (exceto Zona 1) e Seul (exceto Zona 1).
- O proxy de banco de dados atualmente é permitido nas seguintes versões: MySQL v5.7 de dois e três nós (a versão secundária do kernel deve ser 20201230 ou superior). Se você atualizar a versão secundária do kernel da instância de origem, as instâncias somente leitura e de recuperação de desastre associadas serão atualizadas ao mesmo tempo. Para obter mais informações, consulte [Atualização da versão secundária do kernel](https://intl.cloud.tencent.com/document/product/236/36816).

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, selecione a instância de origem para a qual deseja habilitar o proxy de banco de dados e clique em seu ID ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para entrar na página de gerenciamento de instâncias.
2. Na página de gerenciamento de instâncias, selecione a guia **Database Proxy (Proxy de banco de dados)** e clique em **Enable Now (Habilitar agora)**.
![](https://main.qcloudimg.com/raw/46d9e9b30975b51bee00a16c64f31c8b.png)
3. Na janela pop-up, selecione a especificação, a quantidade de nós, clique em ** OK** e atualize.
 - Rede: atualmente, apenas VPC é compatível. A VPC da instância de origem é selecionada por padrão.
 - Especificação de proxy: atualmente, apenas uma especificação é permitida.
 - Quantidade de nós: número de nós de proxy. Recomendamos que você defina a quantidade para 1/8 (arredondado para cima) do número total de núcleos de CPU nas instâncias de origem e somente de leitura; por exemplo, se a instância de origem tiver 4 núcleos de CPU e a instância somente leitura tiver 8 núcleos de CPU, a quantidade de nós recomendada será (4 + 8) / 8 ≈ 2.
 - Grupo de Segurança: é um importante meio de isolamento da segurança da rede. Você pode escolher um grupo de segurança existente ou criar um novo conforme necessário.
<img src="https://main.qcloudimg.com/raw/a3d8fafb1930d0298deb9cf2f08e706c.png"  style="zoom:80%;"> 
4. Após habilitar o serviço com sucesso, você pode gerenciar os nós de proxy e visualizar suas informações básicas na página de proxy do banco de dados. Você também pode modificar o endereço do proxy do banco de dados e o tipo de rede e adicionar comentários na seção **Connection Address (Endereço de conexão)**.
>?
>- Você pode visualizar **Connections (Conexões)** na lista de nós de proxy ou visualizar os dados de monitoramento de desempenho de cada nó de proxy para verificar se o número de conexões nos nós está desbalanceado e, em caso afirmativo, é possível distribuir as conexões clicando em **Rebalance (Rebalanceamento)**.
>- O rebalanceamento fará com que os nós de proxy sejam reiniciados e o serviço ficará indisponível momentaneamente durante a reinicialização. Recomendamos que você reinicie o serviço fora do horário de pico. Certifique-se de que sua empresa tenha um mecanismo de reconexão.
>
![](https://main.qcloudimg.com/raw/083d38858367fd7fe65e90fb92210178.png)
