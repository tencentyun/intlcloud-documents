Ao desligar ou reiniciar o CVM, pode ocorrer uma falha. Embora seja um evento raro, você pode solucionar esse problema da seguinte forma:

## Possíveis causas

- Alto uso de CPU ou memória.
- O ACPI não foi instalado no CVM do Linux.
- A atualização do sistema do CVM do Windows demora muito.
- O CVM do Windows ainda não tinha concluído a inicialização quando você o comprou pela primeira vez.
- O sistema operacional está danificado devido a algum software instalado ou vírus, como trojan.

## Solução de problemas

### Verifique o uso da CPU/memória

1. Verifique o uso da CPU/memória com base no sistema operacional do CVM.
 - Para CVM do Windows: clique com o botão direito do mouse na “Taskbar (Barra de tarefas)” e selecione **Task Manager (Gerenciador de tarefas)** no CVM.
 - Para CVM do Linux: execute o comando `top` para exibir as informações nas colunas `%CPU` e `%MEM`.
2. Encerre os processos com alto uso de CPU ou memória.
Se você ainda não conseguir desligar ou reiniciar o CVM, realize o [desligamento ou reinicialização forçados](#ForcedShutdownOrRestart).

### Verifique se o ACPI foi instalado
> Esta operação é para um CVM do Linux.
>
Execute o comando a seguir para consultar se existe um processo do ACPI.
```
ps -ef | grep -w "acpid" | grep -v "grep"
```
 - Se existir um processo do ACPI, execute o [desligamento ou reinicialização forçados](#ForcedShutdownOrRestart).
 - Se não existir nenhum processo do ACPI, instale o ACPI. Para obter as operações específicas, consulte [Configuração de gerenciamento de energia do Linux](https://intl.cloud.tencent.com/document/product/213/2129).


### Verifique se o WindowsUpdate está em execução
> Esta operação é para um CVM do Windows.
>
Na interface do sistema operacional do CVM do Windows, clique em **Start (Iniciar)** > **Control Panel (Painel de Controle)** > **Windows Update**, para conferir se algum patch ou programa está sendo atualizado.
- O Windows pode realizar patches quando o sistema está sendo desligado. A atualização pode levar muito tempo, fazendo com que o desligamento/reinicialização do CVM falhe. Recomendamos que você aguarde a conclusão da atualização do Windows e tente desligar ou reiniciar o CVM.
- Se nenhum patch ou programa estiver sendo atualizado, realize o [desligamento ou reinicialização forçados](#ForcedShutdownOrRestart).


### Verifique se o CVM concluiu a inicialização
> Esta operação é para um CVM do Windows.
>
Quando você compra o CVM do Windows pela primeira vez, a inicialização pode demorar mais porque o Sysprep é usado para distribuir imagens. Antes que a inicialização seja concluída, o Windows ignorará as operações de desligamento e reinicialização.
- Se o CVM do Windows que você comprou estiver inicializando, recomendamos que você aguarde a conclusão da inicialização antes de desligar ou reiniciar o CVM novamente.
- Se o CVM concluiu a inicialização, realize o [desligamento ou reinicialização forçados](#ForcedShutdownOrRestart).

### Verifique se o software instalado está normal
 
Use uma ferramenta de verificação ou software antivírus para conferir se o software instalado no CVM está normal ou se foi atacado por vírus, como o trojan.
- Se um erro for identificado, o sistema pode estar danificado, causando falha no desligamento e na reinicialização. Recomendamos que você desinstale o software, faça backup dos dados ou faça uma varredura com software de segurança e reinstale o sistema.
- Se nenhum erro for identificado, realize o [desligamento ou reinicialização forçados](#ForcedShutdownOrRestart).

<span id="MandatoryShutdownOrRestart"></span>
### Desligamento/reinicialização forçados

> O desligamento ou a reinicialização forçados fornecidos pela Tencent Cloud podem ser usados se você não conseguir desligar ou reiniciar o CVM após várias tentativas. Essa funcionalidade permite forçar um desligamento ou reinicialização no CVM, o que pode causar perda de dados ou danificar o sistema de arquivos.
>
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, selecione o CVM que você deseja encerrar ou reiniciar.
 - Para desligar o CVM: clique em **More (Mais)** > **Instance Status (Status da instância)** > **Shutdown (Desligar)**.
 - Para reiniciar o CVM: clique em **More (Mais)** > **Instance Status (Status da instância)** > **Restart (Reiniciar)**.
3. Na janela pop-up **Shutdown (Desligar)** ou **Restart Instance (Reiniciar instância)**, marque **Forced Shutdown (Desligamento forçado)** ou **Forced Restart (Reinicialização forçada)** e clique em **Ok**.
 - Marque **Forced Shutdown (Desligamento forçado)**, conforme mostrado abaixo:
 ![](https://main.qcloudimg.com/raw/22db326eebab11c60e6bbcf8baa23144.png)
 - Marque **Forced Restart (Reinicialização forçada)**, conforme mostrado abaixo:
 ![](https://main.qcloudimg.com/raw/61ae4a4185110b7ff86507e15047211f.png)
