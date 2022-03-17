## Modo de recuperação do Windows

A **Windows Recovery (Recuperação do Windows)** é uma funcionalidade de recuperação automática do Windows. Quando o Windows detecta alguns problemas do sistema e acredita que a execução contínua causará danos ao sistema, essa funcionalidade de reparo automático impedirá o Windows de inicializar e fornecerá **System Recovery Options (Opções de recuperação do sistema)** aos usuários para reparar, fazer backup ou restaurar o sistema. 
As **System Recovery Options (Opções de recuperação do sistema)** incluem **Startup Repair (Reparo de inicialização)**, **System Restore (Restauração do sistema)** e **Windows Memory Diagnostic (Diagnóstico de memória do Windows)**, que podem ajudar os usuários a corrigir problemas, fazer backup de dados e restaurar o sistema.
Se você não puder fazer login remotamente em um CVM e vir a figura a seguir ao fazer login no CVM por meio do console, significa que o CVM do Windows entrou no modo de recuperação.
![](//mc.qcloudimg.com/static/img/e278c336a415066dcb8fc58333395ac3/image.png)

## Motivos
O sistema pode entrar no modo de recuperação nas seguintes situações:
- **A energia foi desligada enquanto o Windows estava em execução ou desligando.** O sistema Windows foi desligado à força por meio do console. Ambos os cenários podem causar perda de dados críticos.
- **A energia foi desligada durante a atualização do Windows.** Isso pode causar perda de dados de atualização críticos.
- **O sistema foi danificado por trojans ou vírus.**
- **Havia bugs nos principais serviços do Windows**. O Windows detectou um risco.
- **O sistema perdeu dados críticos ou foi danificado**. Os arquivos do sistema foram corrompidos devido a operação incorreta.

## Precauções
As precauções recomendadas são as seguintes:
 - Faça login no console para monitorar o processo de desligamento de um sistema Windows. O Tencent Cloud permite o desligamento normal que vem com um mecanismo de tempo limite. Se o processo de desligamento não tiver sido concluído dentro do período determinado, uma mensagem de falha será retornada. Se o processo de desligamento for lento ou o Windows Update iniciar, não force o desligamento; em vez disso, espere até que o desligamento seja concluído. Para obter mais informações, consulte [Cenários de falha no desligamento](https://intl.cloud.tencent.com/document/product/213/2917#shutdown-failure-scenarios).
 - Verifique se existem programas ou processos anormais no sistema, como trojans ou vírus.
 - Verifique se o gerenciamento do sistema e o software antivírus estão funcionando corretamente.
 - Instale as atualizações do Windows quando solicitado, principalmente atualizações importantes e de segurança.
 - Verifique os logs de eventos do sistema regularmente para corrigir erros nos serviços principais.

## Soluções
 Se o Windows entrar no modo de recuperação, execute as etapas a seguir para continuar a inicialização ou permitir que o Windows repare automaticamente os problemas menores.
1. Faça login no CVM por meio do [console do CVM](https://console.cloud.tencent.com/cvm).
2. Na página do modo de recuperação exibida, clique em **Next (Avançar)**.
![](//mc.qcloudimg.com/static/img/94a1cf0f55d2c449a9d026bbbad5e4cd/image.png)
3. Na janela **System Recovery Options (Opções de recuperação do sistema)**, clique em **Next (Avançar)** para usar a solução padrão, conforme mostrado abaixo:
![](//mc.qcloudimg.com/static/img/d178865f822d2146eb3bb58f1b851294/image.png)
4. Clique em **Restart (Reiniciar)** e pressione **F8** rapidamente.
![](//mc.qcloudimg.com/static/img/ab2fdd697015fcb7e53b287052086b65/image.png)
5. Escolha **Start Windows Normally (Iniciar o Windows normalmente)**.
 ![](https://main.qcloudimg.com/raw/c3c62a6d77a2fe41d0ad02899faa06ed.png)
Se a inicialização falhar, reinstale o sistema por meio do console. Para obter mais informações, consulte [Reinstalação do sistema por meio do console](https://intl.cloud.tencent.com/document/product/213/4933#useConsole).


