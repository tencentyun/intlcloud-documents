## Introdução

Este artigo usa o Windows Server 2012 como exemplo para ilustrar como atualizar o sistema operacional Windows.

## Instruções

### Atualização do Windows usando a rede pública
Você pode usar o serviço do Windows Update para atualizar seu sistema operacional. As etapas detalhadas são as seguintes:
1. Faça login na instância do CVM do Windows.
2. Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> -> **Control Panel (Painel de controle)** -> **Windows Update**. A janela **Windows Update** será exibida.
3. Clique em **Check for updates (Verificar atualizações)** e aguarde até que a verificação seja concluída.
4. Após a conclusão da verificação, clique em **N Important Updates Available (N atualizações importantes disponíveis)** ou **N Optional Updates Available (N atualizações opcionais disponíveis)** em "Windows Update". A janela **Choose the Update to Install (Escolha a atualização para instalar)** será exibida.
5. Selecione as atualizações que deseja instalar e clique em **Install (Instalar)**.
Se você for solicitado a reiniciar o sistema após a conclusão da atualização, faça-o.
> Se você fizer login usando VNC depois que a instância for reinicializada e a mensagem "Updating...Do not turn off the power (Atualizando… Não desligue a energia)" ou "Configuration has not been completed (A configuração não foi concluída)" for exibida, não realize um desligamento forçado. Isso pode danificar sua instância do CVM.

### Atualização do Windows usando a rede privada
Se sua instância do CVM não tiver acesso à rede pública, você pode usar o servidor privado do Windows Update do Tencent Cloud para atualizar seu sistema operacional. O servidor Windows Update do Tencent Cloud tem a maioria das atualizações, mas não tem pacotes de driver de hardware e algumas atualizações incomuns. Portanto, serviços incomuns podem não obter atualizações usando o servidor Windows Update do Tencent Cloud.
Siga estas etapas para usar o servidor Windows Update do Tencent Cloud:
1. Faça login na instância do CVM do Windows.
2. Use o Internet Explorer para baixar o arquivo de configuração de rede privada do Tencent Cloud wusin.bat do seguinte endereço:
http://mirrors.tencentyun.com/install/windows/wusin.bat
3. Execute wusin.bat no prompt de comando com privilégio de administrador, conforme mostrado abaixo:
> Se você abrir o wusin.bat usando o Internet Explorer depois de concluir o download, a janela do console será fechada automaticamente e você não poderá observar a saída.
>
Você pode salvar wusin.bat em seu disco rígido, como C:\, e abrir uma janela de prompt de comando com privilégio de administrador para executá-lo.

Se você não deseja mais usar o servidor Windows Update do Tencent Cloud, pode fazer o download do wusout.bat para limpá-lo. Siga estas etapas para fazer isso:
1. Faça login na instância do CVM do Windows.
2. Use o Internet Explorer para baixar o arquivo de configuração de rede privada do Tencent Cloud wusout.bat do seguinte endereço:
http://mirrors.tencentyun.com/install/windows/wusout.bat
3. Execute wusout.bat no prompt de comando com privilégio de administrador, conforme mostrado abaixo:
> Se você abrir o wusout.bat usando o Internet Explorer depois de concluir o download, a janela do console será fechada automaticamente e você não poderá observar as informações de saída.
>
Você pode salvar wusout.bat em seu disco rígido, como C:\, e abrir uma janela de prompt de comando com privilégio de administrador para executá-lo.
