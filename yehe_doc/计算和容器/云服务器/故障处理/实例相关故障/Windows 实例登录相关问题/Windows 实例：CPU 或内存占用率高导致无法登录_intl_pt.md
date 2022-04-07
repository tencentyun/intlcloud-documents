Este documento descreve como solucionar falhas de login no CVM do Windows devido à alta utilização de CPU ou memória.
> O método a seguir tomou como base o Windows Server 2012 R2. As etapas podem variar de acordo com as versões do sistema operacional (SO).

## Possíveis causas

Hardware, processos do sistema, processos de serviço, trojans e vírus podem causar alta utilização de CPU ou memória, resultando em lentidão na velocidade de resposta de serviço ou falha de login no CVM. Você pode usar o [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248/32799) para criar um limite de alarme para uso de CPU ou memória. Você será notificado imediatamente quando exceder o limite configurado.

## Solução de problemas

1. Identifique o processo responsável pela alta utilização de CPU ou memória.
2. Analise o processo.
 - Se for um processo não íntegro, a causa pode estar atrelada a um vírus ou trojan. Feche o processo ou use um antivírus para verificar o sistema.
 - Se for um processo de serviço, verifique se a alta utilização de CPU ou memória é causada pelo tráfego de acesso e se pode ser otimizada.
 - Se for um processo de componente da Tencent Cloud, [envie um ticket](https://console.cloud.tencent.com/workorder/category) para obter ajuda.

## Ferramentas

**Task Manager (Gerenciador de tarefas)**: um gerenciador de aplicativos e processos incluído no sistema operacional Microsoft Windows. Ele fornece informações sobre o desempenho do computador e o software em execução, como os nomes dos processos em execução, a carga da CPU, o uso da memória, a E/S, os usuários conectados e os serviços do Windows.
- **Processes (Processos)**: uma lista de todos os processos em execução.
- **Performance (Desempenho)**: estatísticas de desempenho do sistema, como o uso geral da CPU e o uso atual da memória.
- **Users (Usuários)**: todos os usuários com sessões.
- **Details (Detalhes)**: uma versão aprimorada da guia de processos, incluindo informações detalhadas sobre o PID, o status, o uso de CPU e o uso de memória.
- **Services (Serviços)**: uma lista de todos os serviços, incluindo aqueles que não estão em execução.


## Método de solução de problemas

### Login na instância do CVM usando VNC
> Se você não conseguir fazer login na instância do CVM devido à alta utilização de CPU ou memória, recomendamos [fazer login na instância do Windows via VNC](https://intl.cloud.tencent.com/document/product/213/32496). 
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, localize a instância do CVM e clique em **Log In (Fazer login)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela pop-up “Log into Windows instance (Fazer login na instância do Windows)”, selecione **Alternative login methods (VNC) (Métodos de login alternativos (VNC))** e clique em **Log In Now (Fazer login agora)** para fazer login na instância do CVM.
4. Na janela pop-up de login, selecione “Send CtrlAltDel (Enviar CtrlAltDel)” no canto superior esquerdo e clique em **Ctrl-Alt-Delete** para acessar a página de login do SO, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Exibição do uso de recursos de processos

1. No CVM, clique com o botão direito na “taskbar (barra de tarefas)” e selecione **Task Manager (Gerenciador de tarefas)**, conforme mostrado na figura a seguir:
![](https://main.qcloudimg.com/raw/a795f4948fae3eab8a44ec0a3a4ee352.png)
2. Exiba o uso de recursos na janela “Task Manager (Gerenciador de tarefas)”, conforme mostrado na figura a seguir:
> Você pode clicar na coluna CPU ou memória para classificar os processos em ordem crescente ou decrescente.
>
![](https://main.qcloudimg.com/raw/56a4be427be5046a15a05b02abbacf66.png)

### Análise de processos

Analise os processos no Gerenciador de tarefas para identificar as causas e solucionar os problemas adequadamente.
#### Quando a causa o problema é um processo do sistema
Se um processo do sistema for responsável pela alta utilização de CPU e memória, solucione conforme a seguir:
1. Verifique o nome do processo.
 Alguns vírus usam nomes semelhantes aos processos do sistema, como svch0st.exe, explore.exe, iexplorer.exe etc.
2. Verifique a localização do arquivo executável (.exe) de um processo.
 Geralmente, o arquivo executável de um processo do sistema fica localizado em `C:\Windows\System32`, com assinaturas e descrições válidas. Para localizar o arquivo executável de um processo, como `svchost.exe`, dentro do Gerenciador de Tarefas, clique com o botão direito no processo e selecione **Open file location (Abrir local do arquivo)**.
 - Se o arquivo executável não estiver em `C:\Windows\System32`, sua instância do CVM pode estar com vírus. Utilize um software antivírus para procurá-lo ou corrija o problema manualmente.
 - Se o arquivo executável estiver em `C:\Windows\System32`, reinicie a instância do CVM ou encerre os processos do sistema desnecessários, mas seguros.

Veja abaixo a lista dos processos comuns do sistema:
 - Processo inativo do sistema: exibe a porcentagem de tempo que o processador está inativo
 - system: indica o processo de gerenciamento de memória
 - explorer: indica o processo de gerenciamento de área de trabalho e arquivos
 - iexplore: indica o processo do Microsoft Internet Explorer
 - csrss: indica o subsistema runtime no cliente ou servidor da Microsoft
 - svchost: informa o processo do sistema para DLL em execução
 - Taskmgr: mostra o gerenciador de tarefas
 - Isass: exibe o serviço de autoridade de segurança local

#### O que causa o problema é um processo não íntegro
Se a alta utilização de CPU ou memória for causada por um processo com um nome inusitado, como xmr64.exe (um malware de mineração de criptomoedas), a instância do CVM estar infectada com um vírus ou trojan. Recomendamos usar buscador para verificar.
 - Se o processo for um vírus ou trojan, use um aplicativo antivírus para excluir o vírus ou trojan. Se necessário, faça backup dos dados e reinstale o sistema operacional.
 - Se o processo não for um vírus ou trojan, reinicie a instância do CVM ou encerre os processos desnecessários, mas seguros.

#### Quando o problema é um processo de serviço
Se um processo de serviço como IIS, HTTPD, PHP ou Java causar o problema, recomendamos uma análise mais detalhada.
Por exemplo, verifique se o seu volume de atividades é alto.
- Se for, recomendamos [fazer o upgrade da configuração](https://intl.cloud.tencent.com/document/product/213/2178) da instância do CVM. Enquanto isso, você pode otimizar os processos de serviço.
- Se não for, use os logs de erros de serviço para analisar melhor o problema. Por exemplo, verifique se configurações incorretas de parâmetros levam ao desperdício de recursos.

#### Quando o problema é um processo da Tencent Cloud

- Se um processo de componente da Tencent Cloud causar o problema, [envie um ticket](https://console.cloud.tencent.com/workorder/category) para entrar em contato conosco e obter ajudar.

