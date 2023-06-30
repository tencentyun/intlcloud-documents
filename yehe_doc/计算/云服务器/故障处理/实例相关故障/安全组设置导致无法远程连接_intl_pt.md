
Este documento descreve como solucionar o problema que impede o usuário de se conectar remotamente a um CVM devido a problemas de configuração do grupo de segurança.

## Ferramenta de diagnóstico

Você pode usar a [Verificação de portas](https://console.cloud.tencent.com/vpc/helper) para verificar se o problema é causado pelas configurações do grupo de segurança.
1. Faça login na [Verificação de portas](https://console.cloud.tencent.com/vpc/helper).
2. Na página **Port Verification (Verificação de portas)**, selecione a instância a ser verificada e clique em **Quick Check (Verificação rápida)**. Verifique a figura abaixo para mais detalhes.
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
Se a verificação mostrar que a instância tem portas fechadas, você pode selecionar **Open all ports (Abrir todas as portas)** para abrir todas as portas originais do CVM para a Internet e tentar fazer login remoto novamente.

<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## Modificação das configurações do grupo de segurança

Se optar por não usar **Open all ports (Abrir todas as portas)** para abrir todas as portas originalmente usadas pelo CVM para a Internet ou precisar personalizar a porta de login remoto, você poderá usar a configuração personalizada das regras de entrada e saída do grupo de segurança para resolver falhas de login remoto. Para mais informações, consulte [Modificação de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34825).
