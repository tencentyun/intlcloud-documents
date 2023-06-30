### Regras de correspondência

A instância reservada (Reserved Instance, RI) adquirida corresponde automaticamente às instâncias com pagamento conforme o uso durante o período de vigência da RI. Por enquanto, apenas instâncias do Windowa、Linux são compatíveis. Se você não tiver nenhuma instância que corresponda às especificações da RI, a RI ficará inativa, mas ainda assim incorrerá em taxas. Quando você adquire uma instância com as especificações correspondentes, a RI faz a correspondência imediatamente e o benefício se aplica.  

- As RIs são correspondidas automaticamente às instâncias com pagamento conforme o uso, sem intervenção manual.
- O benefício de faturamento da RI pode se aplicar a um máximo de 3.600 segundos (uma hora) de uso da instância por hora cheia. Você pode executar várias instâncias ao mesmo tempo, mas só pode receber o benefício do desconto da RI para um total de 3.600 segundos por hora cheia; o uso de instância que excede 3.600 segundos em uma hora cheia é faturado de acordo com a taxa de pagamento conforme o uso. 

Por exemplo, se você adquirir uma RI S3.16xlarge256 na Zona 1 do Vale do Silício e executar três instâncias com pagamento conforme o uso S3.16xlarge256 com os mesmos atributos simultaneamente na mesma zona de disponibilidade por uma hora, uma instância será cobrada por uma hora de uso da RI e as outras duas instâncias serão cobradas por duas horas de uso com pagamento conforme o uso. 

No entanto, se você adquirir uma RI S3.16xlarge256 na Zona 1 do Vale do Silício e executar três instâncias com pagamento conforme o uso (A, B e C) com os mesmos atributos na mesma zona de disponibilidade por 20 minutos cada, dentro da mesma hora, o tempo total de execução para as instâncias é de uma hora, o que resulta em uma hora de uso da RI e 0 horas de pagamento conforme o uso, como mostrado abaixo.

![1558602502993](https://main.qcloudimg.com/raw/a812f74455b8b9d8ebbc84e90e26bc04.png)

Se as três instâncias elegíveis estiverem sendo executadas simultaneamente, o benefício de faturamento da RI será aplicado a todas as instâncias ao mesmo tempo por no máximo 3.600 segundos em uma hora cheia; depois disso, o preço com pagamento conforme o uso se aplica.

![1558602155668](https://main.qcloudimg.com/raw/24926b2c2675e2d6959adcf62054f5b1.png)

#### Tempo efetivo

As RIs são faturadas a cada hora. Elas entram em vigor na hora anterior da hora de criação e expiram na próxima hora da hora de expiração. 

Exemplo 1: suponha que você adquiriu uma RI do CVM com período de vigência de 1 ano em 25 de maio de 2019 às 11:15:24, a RI será válida de 25 de maio de 2019 às 11:00:00 a 25 de maio de 2020 às 11:59:59.

Exemplo 2: suponha que você adquiriu uma RI do CVM com período de vigência de 1 ano em 25 de maio de 2019 às 11:00:00, a RI será válida de 25 de maio de 2019 às 11:00:00 a 25 de maio de 2020 às 11:59:59.
