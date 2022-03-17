## Análise do processo de desligamento do CVM

### Processo de desligamento
>?Consulte [Desligar instâncias](https://intl.cloud.tencent.com/document/product/213/4929) para obter as operações relacionadas.
>
O processo de desligamento de uma instância do Windows do Tencent Cloud é o seguinte:
1. O host envia o comando de desligamento via libvirt no protocolo QMP para o componente `qemu`.
2. O componente `qemu` transfere o comando de desligamento para o CVM interrompendo o ACPI (para obter mais informações, consulte os documentos técnicos sobre VMCS).
3. Depois de receber o sinal de desligamento, a instância do Windows fecha os aplicativos e os processos de serviço.
4. Feche o processo do serviço principal.
5. Desligue a energia.
>! A sequência de fechamento dos aplicativos e serviços na etapa 3-4 pode variar de acordo com as configurações do sistema.

O Windows é um sistema de software proprietário. Ele fornece APIs que permitem que programas em modo kernel e modo usuário intervenham no processo de desligamento. Alguns serviços do Windows em execução também afetarão o processo de desligamento, aumentarão o tempo de desligamento e causarão falha no desligamento.

### Desligamento forçado
Em um cenário de virtualização, além dos métodos de desligamento, como desligamento normal inicializado pelo sinal do sistema e notificação de mensagens, você também pode forçar o desligamento do CVM por meio do **forced shutdown (desligamento forçado)**.
O desligamento forçado pode afetar o Windows e a experiência do usuário nos dois seguintes aspectos:
1. Um desligamento forçado interrompe alguns serviços e aplicativos e causa operações anormais, como documentos não salvos e processos do WindowsUpdate não concluídos.
2. Durante o processo de desligamento, o sistema NTFS (ou o sistema FAT32 anterior) do Windows grava os dados principais no disco. Um desligamento forçado pode resultar em falha de gravação e fazer com que o Windows acredite que o sistema de arquivos NTFS está danificado.

Portanto, recomendamos que você **primeiro use o desligamento normal** em uma instância do Windows.

## Cenários de falha no desligamento
O sistema Windows pode ter problemas que afetam o processo de desligamento e causam falha no desligamento, incluindo, mas não se limitando a:
1. Um processo do WindowsUpdate pode prolongar o tempo de desligamento. O sistema Windows pode executar operações de patch durante o processo de desligamento e exibir uma mensagem como "Please do not power off or unplug your computer (Não desligue ou desconecte o computador)".
2. Se o sistema Windows tiver o mecanismo "Shutdown Event Tracker (Controlador de eventos de desligamento)" ativado e precisar ser desligado devido a algum serviço do sistema ou erro de driver, o sistema exigirá que o usuário envie uma descrição do erro com base na configuração. O sistema vai aguardar até que você conclua essas operações antes de desligar.
3. O Windows não permite o desligamento sem login. Nessa configuração, o comando de desligamento normal enviado do host virtual será descartado pelo Windows, portanto, ele não será encerrado.
4. Antes do desligamento, o Windows transmitirá uma mensagem para todos os serviços e aplicativos. Se os aplicativos não derem respostas afirmativas, o Windows não iniciará o desligamento. Nesse caso, você pode configurar o Windows para ignorar esse processo de resposta.
5. Se você configurar o gerenciamento de energia no Windows para ignorar ou não fazer nada **When I press the power button (Quando eu pressiono o botão liga/desliga)**, o Windows vai ignorar o evento de desligamento recebido do host virtual.
6. Com base nas configurações de gerenciamento de energia, o Windows entrará no modo de suspensão e ignorará o evento de desligamento.
7. Se o próprio sistema Windows for danificado devido a software mal-intencionado ou infecções por Trojans ou outros vírus, o Windows pode impedir o desligamento.

O Tencent Cloud resolveu a maioria das falhas no desligamento ao liberar a imagem pública do Windows para garantir o desligamento normal. No entanto, se o seu Windows estiver infectado com vírus ou Trojans, o sistema estiver danificado ou as configurações do Windows forem ajustadas novamente, o desligamento normal pode falhar.
**O desligamento forçado envolve riscos. Portanto, recomendamos que você o use apenas quando realmente for necessário.**


