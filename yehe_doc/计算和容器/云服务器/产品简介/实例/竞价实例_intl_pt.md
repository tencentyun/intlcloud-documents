## O que é uma instância spot?
As instâncias spot são um novo modo de instâncias do CVM que apresentam um preço competitivo e um mecanismo de interrupção do sistema, o que significa que você pode adquirir uma instância spot a um preço menor, mas o sistema pode reavê-la automaticamente. Quando você usa uma instância spot, as operações são quase similares àquelas da instância do CVM com pagamento conforme o uso, e incluem operações de console, login remoto, implantação de serviços e associação com um VPC.

- Referência: [Perguntas frequentes > Sobre a instância > Instâncias spot](https://intl.cloud.tencent.com/document/product/213/17817)
- Referência: [Instâncias spot](https://intl.cloud.tencent.com/document/product/213/17926)

## Políticas especiais para o estágio atual
- **Desconto fixo**: todas as instâncias spot estão disponíveis com um desconto fixo, que é 80% do preço de instâncias com pagamento conforme o uso da mesma especificação. Os descontos para alguns tipos de instâncias podem ser ligeiramente ajustados.
- **Interrupção do sistema por saldo insuficiente**: no momento, as instâncias spot não serão interrompidas por motivos de preço, ou seja, preço de mercado maior do que sua oferta, mas podem ser interrompidas se as instâncias spot estiverem em escassez. Se o suprimento for insuficiente, o Tencent Cloud reaverá aleatoriamente as instâncias spot alocadas.
- **Disponível em quase todas as regiões**: as instâncias spot estão disponíveis em quase todas as regiões do Tencent Cloud. Os tipos de instâncias compatíveis com as instâncias spot são similares àqueles compatíveis com as de pagamento conforme o uso. Para saber as regiões mais recentes e os tipos de instâncias compatíveis, consulte [Instâncias spot – Regiões compatíveis e tipos de instâncias >>](https://intl.cloud.tencent.com/document/product/213/17817).

## Características do produto
### 1. Custo-benefício
![](https://main.qcloudimg.com/raw/8179ef6629ac0a0b4b9c3c9cd6f80ffa.png)
As instâncias spot são vendidas com um desconto de até 90% sobre os preços de instâncias com pagamento conforme o uso.
- **Faixa de desconto**: as instâncias spot são vendidas com um desconto de até 90% do preço de instâncias com pagamento conforme o uso da mesma especificação.
- **Exclusões**: o desconto se aplica apenas à CPU e à memória do CVM. Outros itens de cobrança relacionados ao CVM, incluindo discos do sistema, discos de dados, largura de banda e imagens pagas, não fazem parte do desconto.
- **Flutuações de preço**: o desconto é mantido por um determinado período. No entanto, se houver aquisições em massa numa zona de disponibilidade, o preço pode variar. Atualmente, o desconto está fixado em 80%.

### 2. Mecanismo de interrupção do sistema
![](https://main.qcloudimg.com/raw/a4db964d52400b9a00d3c7e96c0b833d.png)
Ao contrário das instâncias com pagamento conforme o uso que só podem ser liberadas por usuários, as instâncias spot podem ser interrompidas pelo sistema por motivos de preço ou de disponibilidade de recursos.
![](https://main.qcloudimg.com/raw/824a585f8dfeb1914f4d72ea1eafdb6c.png)
- **Preço**: se o preço de mercado for maior do que sua melhor oferta, as instâncias spot serão reavidas. No entanto, no momento atual, o preço de mercado será fixado.
- **Disponibilidade de recursos**: se as instâncias spot estiverem em escassez, o Tencent Cloud reaverá as instâncias spot proporcionalmente à falta. Assim que o fornecimento estiver estabilizado, você poderá solicitar as instâncias spot novamente.

## Cenários não aplicáveis
Como as instâncias spot podem ser interrompidas, o ciclo de vida delas não está sob seu controle. Portanto, não é recomendado executar serviços com alta exigência de estabilidade em uma instância spot. Por exemplo:
- Serviços de banco de dados
- Serviços online e de sites sem balanceadores de carga
- Nós de controle do núcleo em uma arquitetura distribuída
- Trabalho prolongado de computação de big data com duração superior a 10 horas

## Cenários e setores aplicáveis
### Cenários aplicáveis
- Computação de big data
- Serviços online e de sites com balanceadores de carga
- Serviço web crawler (rastreador web)
- Outros cenários de computação com granularidade fina ou suporte para reinicialização do ponto de verificação

### Setores aplicáveis
- Sequenciamento e análise genética
- Análise de forma cristalina de fármaco
- Transcodificação e renderização de vídeos
- Análise de dados financeiros e de transações
- Processamento de imagens e multimídia
- Cálculos científicos, como em geografia e hidromecânica

## Restrições
- **Cota**: a cota de instâncias spot limita a quantidade total de núcleos de vCPU de todas as instâncias spot que você possui em uma zona de disponibilidade. Atualmente, cada conta pode ter até 50 núcleos de vCPU em cada zona de disponibilidade. Para solicitar uma cota maior, envie um tíquete.
- **Restrição de operação 1**: o upgrade e o degrade das configurações não são compatíveis com as instâncias spot.
- **Restrição de operação 2**: não é possível alterar o método de cobrança de instâncias spot para assinatura mensal.
- **Restrição de operação 3**: as instâncias spot não são compatíveis com a funcionalidade "No Charges when Shut Down" (Sem cobranças quando desligada).
- **Restrição de operação 4**: as instâncias spot não são compatíveis com a reinstalação de sistema.

## Práticas recomendadas
### 1. Divisão de tarefas
- Divida uma tarefa prolongada em subtarefas de granularidade fina para reduzir a possibilidade de interrupção.
- Use um pacote de big data como o EMR, que acompanha um mecanismo de divisão.

### 2. Uso de balanceadores de carga para garantir a estabilidade dos serviços online e de sites
- Utilize balanceadores de carga, como o CLB, na camada de acesso.
- Utilize uma combinação de algumas instâncias com pagamento conforme o uso e muitas spot para os recursos de back-end.
- Monitore as interrupções de instâncias spot e remova as instâncias que estão prestes a serem interrompidas do CLB.

### 3. Uso de um modo de agendamento calculado compatível com a reinicialização do ponto de verificação
- Armazene os resultados de cálculos intermediários em produtos de armazenamento permanente como o COS, o CFS e o NAS.
- Monitore quais instâncias estão prestes a serem interrompidas usando metadados e salve os resultados de cálculos dentro do período de retenção de 2 minutos.
- Continue o último cálculo quando uma instância spot for reiniciada.
