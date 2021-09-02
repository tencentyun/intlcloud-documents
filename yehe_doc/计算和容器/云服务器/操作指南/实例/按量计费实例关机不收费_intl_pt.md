## Visão geral
Se você habilitar a funcionalidade "No Charge when Shut Down (Sem Cobranças Quando Desligada)" ao desligar uma instância com pagamento conforme o uso, o faturamento dos recursos de CPU e memória dessa instância será interrompido. No entanto, os discos em nuvem (disco do sistema e disco de dados), a largura de banda da rede pública, as imagens e outros componentes principais da instância do CVM continuam a ser faturados.
>! Quando essa funcionalidade estiver habilitada, os recursos de CPU e memória da instância **não serão mantidos** e o endereço IP público **será liberado automaticamente** após o desligamento. Para obter mais informações sobre a funcionalidade, seus limites de uso e impactos, consulte a [Funcionalidade Sem Cobranças Quando Desligada para as instâncias com pagamento conforme o uso](https://intl.cloud.tencent.com/document/product/213/19918).

## Direções
### Desligamento de uma instância pelo console
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm).
2. Escolha o método de operação apropriado com base em suas necessidades reais.
 - Desligamento de uma única instância:
    1. Selecione a instância que deseja desligar e clique em **More (Mais)** > **Instance Status (Status da instância)** > **Shut down (Desligar)** na coluna **Operation (Operação)** à direita.
    2. Marque **CVM No Charge when Shut down (CVM Sem Cobranças Quando Desligada)** e clique em **OK**.
    Se a instância não for compatível com essa funcionalidade, **"No Charge when Shut Down" is not supported ("Sem Cobranças Quando Desligada" não é compatível)** será exibido na lista de instâncias.
 - Desligamento de várias instâncias:
    1. Selecione todas as instâncias que deseja desligar e clique em **Shut down (Desligar)** no topo da lista para desligar as instâncias em lotes.
    Os motivos são fornecidos para as instâncias que não podem ser desligadas.
	 2. Marque **CVM No Charge when Shut down (CVM Sem Cobranças Quando Desligada)** e clique em **OK**.
		Se a instância não for compatível com essa funcionalidade, **"No Charge when Shut Down" is not supported ("Sem Cobranças Quando Desligada" não é compatível)** será exibido na lista de instâncias.

### Desligamento de uma instância por API
É possível usar a API `StopInstances` para desligar uma instância. Para obter mais detalhes, consulte [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235). Para habilitar essa funcionalidade por API, adicione o seguinte parâmetro:

| Nome do parâmetro | Obrigatório | Tipo | Descrição |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| StoppedMode | Não | String |A funcionalidade "Sem Cobranças Quando Desligada" está disponível apenas para as instâncias com pagamento conforme o uso.<br>**Valores válidos:**<br>KEEP_CHARGING: a instância incorre em taxas após o desligamento<br>STOP_CHARGING: sem cobranças quando desligada<br>**Valor padrão:**<br>KEEP_CHARGING |



