## Visão geral

A instância reservada (RI) oferece um desconto para as instâncias com pagamento conforme o uso. Este documento descreve como criar RIs pelo console.

## Direções
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Clique em **Reserved Instance (Instância reservada)** na barra lateral esquerda para entrar na página de gerenciamento.
3. Clique em **Create Reserve Instance (Criar instância reservada)** para adquirir RIs.

![image-20200909172355330](https://main.qcloudimg.com/raw/f604c27f8faeded74797d78d66ada9c2.png)

4. Configure as seguintes informações conforme solicitado pela página:

| Parâmetro        | Obrigatório/Opcional | Descrição                               |
| ------------------ | --------- | ------------------------------------------------------------ |
| Região/Zona de disponibilidade  | Obrigatório      | A região e a zona de disponibilidade em que as instâncias com pagamento conforme o uso correspondentes estão localizadas.           |
| Sistema operacional    | Obrigatório      | Windows、Linux OS.                                    |
| Validade         | Obrigatório      | Período de vigência da RI: 1 ano.                    |
| Instância         | Obrigatório     | O tipo de instância com pagamento conforme o uso que você deseja que corresponda à RI.</br>Essas instâncias com pagamento conforme o uso devem corresponder exatamente aos atributos da RI para se beneficiar do desconto no faturamento durante o período de vigência da RI.  |
| Nome da RI | Opcional      | É definido pelo usuário. <li> O padrão do nome da RI é “unnamed (sem nome)” se este parâmetro for deixado em branco.</li>  <li> Você pode inserir qualquer nome dentro de 60 caracteres.</li> |
| Modo de faturamento     | Obrigatório      | Selecione uma opção de faturamento conforme necessário:</br> <ul><li>**All Upfront (Pagamento total adiantado)**: você paga por todo o período de vigência da RI com um pagamento adiantado. Esta opção oferece o maior desconto em comparação com as outras duas opções abaixo.</li><li>**Partial Upfront (Pagamento parcial adiantado)**: você faz um pagamento inicial baixo e, depois, paga as taxas da instância a uma tarifa mensal ou tarifa horária com desconto durante o período de vigência da RI. </li></ul> |
| Quantidade         | Obrigatório      | Quantidade de RIs que você deseja adquirir                             |


5. Clique em **Purchase Now (Adquirir agora)** e conclua o pagamento. Depois, você pode acessar o console de [Instância reservada](https://console.cloud.tencent.com/cvm/reservedinstances/) para consultar, pesquisar e gerenciar suas RIs. Nesta página, você pode clicar em **Create Instance (Criar instância)** para criar instâncias do CVM ou clicar em **View Bill (Visualizar fatura)** para consultar os detalhes dos descontos da RI.

   ![image-20200909173059650](https://main.qcloudimg.com/raw/86912bb5b8ceabbb071fbb6cfa06cadf.png)
