## Cenário de operação

Reiniciar a instância do CVM é um método comum para mantê-la. É equivalente a reiniciar o sistema operacional do computador local. Este documento descreve como reiniciar instâncias.

## Observações
 - **Preparação para reiniciar instâncias:** a instância não pode fornecer serviços durante a reinicialização. Antes de reiniciar o CVM, certifique-se de que ele parou de receber solicitações de serviço.
 - **Como reiniciar instâncias:** recomendamos que você reinicie uma instância usando as operações de reinicialização fornecidas pelo Tencent Cloud em vez de executar o comando de reinicialização na instância (como o comando relaunch (reiniciar) no Windows e o comando reboot (reiniciar) no Linux).
 - **Tempo de reinicialização:** normalmente, leva apenas alguns minutos para reiniciar uma instância.
 - **Recursos físicos das instâncias:** reiniciar uma instância não altera seus recursos físicos. Seus endereços IP públicos e privados, bem como os dados armazenados, não serão alterados.
 - **Faturamento:** Reiniciar uma instância não iniciará um novo período de faturamento da instância.

## Direções

Você pode reiniciar as instâncias por meio dos seguintes métodos:
- [Usar o console para reiniciar as instâncias](#consoleRestart)
- [Usar API para reiniciar as instâncias](#apiRestart)

<span id="consoleRestart"></span>
### Uso do console para reiniciar as instâncias

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Na página de gerenciamento da instância, selecione o método de reinicialização da instância com base na quantidade real de instâncias a serem reiniciadas.
 - Reinicialização de uma única instância: na linha da instância que você deseja reiniciar, clique em **More (Mais)** > **Instance Status (Status da instância)** > **Restart (Reiniciar)**, conforme mostrado abaixo:
 ![Reinicialização de uma única instância](https://main.qcloudimg.com/raw/56eb6421097130f3f424f582ff3d9f14.png)
 - Reinicialização de várias instâncias: marque todas as instâncias que deseja reiniciar e clique em **Restart (Reiniciar)** no topo da lista para reiniciar as instâncias em lote. Se não puderem ser reiniciadas, o motivo será exibido, conforme mostrado abaixo:
![Reinicialização de várias instâncias](https://main.qcloudimg.com/raw/c6eb646bd8d19e5484d43be3b9cac9bf.png)
> Uma única instância também pode ser reiniciada usando esse método.

<span id="apiRestart"></span>
### Uso de API para reiniciar as instâncias
Consulte [API RebootInstances](https://intl.cloud.tencent.com/document/product/213/33243).
