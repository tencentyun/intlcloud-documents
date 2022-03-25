Este artigo descreve como encerrar e liberar uma instância do Cloud Virtual Machine (CVM). Para obter mais informações sobre a expiração, consulte [Notificações de expiração](https://intl.cloud.tencent.com/document/product/213/2181).

## Visão geral

Se você não precisa mais de uma instância, pode encerrá-la. A instância encerrada é movida para a Lixeira. Você pode renovar, restaurar ou liberar as instâncias na Lixeira.

>! Se sua conta estiver em atraso, você precisará adicionar fundos antes de restaurar as instâncias com pagamento conforme o uso.
>

Você pode usar os seguintes métodos para encerrar e liberar as instâncias com pagamento conforme o uso:
 - **Encerramento manual:** se sua conta estiver em situação regular, você pode encerrar manualmente uma instância com pagamento conforme o uso. Uma instância com pagamento conforme o uso é liberada depois de permanecer na Lixeira por mais de 2 horas.
 - **Encerramento programado:** você pode programar um horário (até o segundo) para encerrar automaticamente uma instância com pagamento conforme o uso. Você pode selecionar uma hora futura para encerrar os recursos. Uma instância encerrada usando o encerramento programado não vai para a Lixeira e é liberada imediatamente. Você pode [cancelar um encerramento programado](https://intl.cloud.tencent.com/document/product/213/4930) a qualquer momento antes da hora programada.
 - **Encerramento automático por expiração ou quando a conta estiver em atraso**: uma instância com pagamento conforme o uso com saldo negativo será automaticamente liberada após 2 horas e 15 dias. Nas primeiras 2 horas, o faturamento continua e você ainda pode usar a instância. No entanto, nos próximos 15 dias a instância será encerrada e o faturamento será interrompido. As instâncias com pagamento conforme o uso não podem ser movidas para a Lixeira depois que sua conta estiver em atraso. Em vez disso, você precisa verificar a instância na lista de instâncias do CVM. Você pode continuar a usar a instância se [renová-la](https://intl.cloud.tencent.com/document/product/213/6143) dentro do tempo especificado.

|  | Encerramento manual (não está em atraso) | Encerramento programado (não está em atraso) | Encerramento automático por expiração ou quando a conta está em atraso |
|---------|---------|---------|---------|
| Instâncias com pagamento conforme o uso | Depois do encerramento, as instâncias com pagamento conforme o uso serão liberadas depois de serem mantidas na Lixeira por no máximo 2 horas. |As instâncias para as quais o encerramento programado foi definido serão liberadas imediatamente conforme programado, em vez de irem para a Lixeira. | Quando sua conta está em atraso, nas primeiras 2 horas, o faturamento continua e você ainda pode usar a instância. No entanto, nos próximos 15 dias a instância será encerrada e o faturamento será interrompido. As instâncias com pagamento conforme o uso não são movidas para a Lixeira depois que sua conta estiver em atraso. Se a instância não for renovada dentro desse período, ela será liberada.|



## Impactos
O que acontecerá com os dados, EIPs e cobranças de uma instância depois que ela for encerrada:
- **Faturamento**: assim que uma instância for encerrada ou liberada, não haverá mais cobrança.
- **Dados da instância:** os discos locais e os discos em nuvem não elásticos montados na instância serão todos liberados e os dados nesses discos serão perdidos. Faça backup dos dados com antecedência. Os discos em nuvem elásticos seguem seu próprio ciclo de vida.
- **EIP:** os EIPs (incluindo endereços IP em ENIs secundários) de uma instância encerrada serão mantidos e os endereços IP inativos podem incorrer em cobranças. Se você não precisa mais deles, libere-os o mais rápido possível.



## Encerramento e liberação de instâncias com pagamento conforme o uso

Para as instâncias com pagamento conforme o uso, você pode escolher o encerramento imediato ou o encerramento programado.

### Encerramento de instâncias usando o console

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Escolha um dos seguintes:
    - **Encerrar uma única instância**: encontre a instância desejada na lista e clique em **More (Mais)** -> **Instance Status (Status da instância)** -> **Terminate/Return (Encerrar/Retornar)** no lado direito.
    - **Encerrar as instâncias em lotes**: selecione todas as instâncias desejadas e clique em **More (Mais)** -> **Terminate/Return (Encerrar/Retornar)** na parte superior da interface. Para instâncias que não puderem ser encerradas, os motivos serão exibidos.
3. Na janela pop-up, escolha **Immediate Termination (Encerramento imediato)** ou **Scheduled Termination (Encerramento programado)**.
 	 - **Encerramento imediato**: você pode optar por liberar os recursos imediatamente ou em 2 horas. Se você escolher liberar os recursos imediatamente, os dados da instância serão apagados e não poderão ser restaurados.
 	 - **Encerramento programado**: se você escolher o encerramento programado, você precisa especificar a hora de encerramento. A instância é encerrada e liberada naquela hora e os dados não podem ser restaurados.
4. Clique em **Next (Avançar)** para confirmar os recursos a serem encerrados ou mantidos.
5. Clique em **Start Termination (Iniciar encerramento)**.

### Cancelamento de um encerramento programado

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Na lista de instâncias, encontre a instância desejada e o **Scheduled Termination (Encerramento programado)** correspondente na coluna **Instance Billing Plan (Plano de faturamento da instância)**. Mova o cursor sobre <img src="https://main.qcloudimg.com/raw/2b612d7419315e76aaa9a7f3a7c9a447.png" style="margin: 0;"></img> para exibir a caixa de diálogo do encerramento programado, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/2a57f29e939d794df1a25f41b0a4880a.png)
3. Clique em **Cancel (Cancelar)**. Uma caixa de diálogo é exibida solicitando que você confirme o cancelamento.
4. Na caixa de diálogo, confirme as informações da instância para a qual deseja cancelar o encerramento programado e clique em **OK**. O cancelamento entra em vigor imediatamente, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/4ee8b052dad3f348f726ba74956d95c5.png)

## Encerramento de instâncias usando as APIs do Tencent Cloud

Para obter mais informações, consulte [API TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234).
