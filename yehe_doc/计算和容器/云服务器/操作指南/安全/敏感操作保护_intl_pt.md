## Visão geral
Atualmente, a funcionalidade Proteção de Operações Confidenciais está disponível no CVM. Depois que ela é ativada, a verificação de identidade precisa ser concluída antes de executar operações confidenciais.
Essa funcionalidade pode proteger com eficácia a segurança dos recursos da conta, incluindo desligamento, reinicialização, login pelo VNC, redefinição de senha, encerramento de instância, reinstalação do sistema, ajuste de configuração, carregamento de chave e alternância para o VPC.

## Ativação da proteção de operações
É possível ativar a funcionalidade de proteção de operações no console de [Configurações de segurança](https://console.cloud.tencent.com/developer/security). Para obter mais informações, consulte [Proteção de operações](https://intl.cloud.tencent.com/document/product/378/10740).

## Verificação da proteção de operações
Depois que a proteção de operações estiver ativada, será necessário concluir a verificação de identidade antes de realizar uma operação confidencial:
- Se você ativou a **MFA verification (Verificação MFA)** para a proteção de operações, será necessário inserir o código de verificação dinâmico de 6 dígitos exibido no dispositivo de MFA.
- Se você ativou a **SMS code verification (Verificação por código SMS)** para a proteção de operações, será necessário inserir o código de verificação recebido em seu celular.



