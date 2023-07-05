## Cenário
Ao tentar se conectar remotamente a uma instância do Windows pelo próprio Windows, você receberá a seguinte mensagem:
![](https://main.qcloudimg.com/raw/8c79cadc3e14c9c4e0cbb5303b79f74a.png)

Você não pode se conectar ao computador remoto usando a Área de Trabalho Remota por um destes motivos:
1) O acesso remoto ao servidor não está ativado.
2) O computador remoto está desligado.
3) O computador remoto não está disponível na rede.

Verifique se o computador remoto está ligado e conectado à rede e se o acesso remoto está ativado.


## Possíveis causas

As causas mais comuns para esse problema, dentre outras, estão listadas a seguir. Solucione o problema de acordo com as circunstâncias propriamente ditas.
- A instância está em um estado anormal.
- O CVM não possui um endereço IP público ou a largura de banda da rede pública é 0.
- A porta de login remoto (porta 3389 por padrão) não está aberta para a Internet nos grupos de segurança vinculados à instância.
- Os serviços de Área de Trabalho Remota não foram iniciados.
- As configurações da Área de Trabalho Remota estão incorretas.
- As configurações do firewall do Windows estão incorretas.

## Etapas de solução de problemas

### Verificar se a instância está em execução
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, verifique se a instância está em **Running (Em execução)**, conforme mostrado na figura a seguir:
![CVM list page](https://main.qcloudimg.com/raw/03cf75228bc468d2e436f876f229ebc9.png)
 - Se estiver, [verifique se o CVM possui um endereço IP público](#step01).
 - Se não estiver, inicie a instância do Windows.

<span id="step01"></span>
### Verificar se o CVM possui um endereço IP público
Verifique se o CVM possui um endereço IP público no console do CVM, conforme mostrado na figura abaixo:
![No public IP addresses](https://main.qcloudimg.com/raw/58c75d68372069652ec09ab93cfdbdc0.png)
 - Se possuir, [verifique se você comprou uma largura de banda de rede pública](#step02).
 - Se não possuir, [solicite um endereço IP público elástico e o vincule ao CVM](https://intl.cloud.tencent.com/document/product/213/16586).
 
<span id="step02"></span>
### Verificar se você comprou uma largura de banda de rede pública
Verifique se a largura de banda da rede pública é de 0 Mbps. Você precisa garantir pelo menos 1 Mbps de largura de banda de rede pública.
 - Se for, aumente a largura de banda para 1 Mbps ou mais [ajustando a configuração da rede](https://intl.cloud.tencent.com/document/product/213/15517).
![](https://main.qcloudimg.com/raw/29b771d9de5d1ecdadb872c0378a31c7.png)
 - Se não for, [verifique se a porta de login remoto (3389) da instância foi aberta para a Internet](#step03).

<span id="step03"></span>
### Verificar se a porta de login remoto (3389) da instância está aberta para a Internet
1. Na página de gerenciamento de instâncias no console do CVM, clique no ID ou no nome da instância de login para acessar a página de detalhes da instância.
2. Na página da guia “Security Groups (Grupos de segurança)”, verifique se a porta de login remoto (porta 3389 por padrão) foi aberta para a Internet nos grupos de segurança vinculados à instância, conforme mostrado na figura a seguir:
![Security groups](https://main.qcloudimg.com/raw/28b5f0a038dd354346745bd97f724350.png)
 - Se sim, [verifique as configurações do sistema da instância do Windows](#step04).
 - Se não, edite as regras do grupo de segurança correspondente para abrir a porta para a Internet. Para mais instruções, consulte [Adição de uma regra de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).

<span id="step04"></span>
### Verificar as configurações do sistema da instância do Windows
1. [Faça login na instância do Windows usando VNC](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png) e verifique as configurações do sistema da instância do Windows.
> As operações a seguir usam o Windows Server 2012 como exemplo.
>
2. No sistema operacional da instância conectada, clique com o botão direito em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, selecione **Run (Executar)**, digite **services.msc** em **Run (Executar)** e pressione Enter para acessar a janela “Service (Serviço)”.
3. Clique duas vezes em “Remote Desktop Services (Serviços de Área de Trabalho Remota)” para acessar a janela “Remote Desktop Services Properties (Propriedades dos Serviços de Área de Trabalho Remota)” e verifique se eles estão em execução, conforme mostrado na figura a seguir:
![Remote Desktop Services](https://main.qcloudimg.com/raw/6c781636c69eacae76a08b88f9e32b99.png)
 - Se estiverem, vá para a [etapa 4](#step04_4).
 - Se não estiverem, defina o “Startup type (Tipo de inicialização)” como “Automatic (Automática)” e clique em **Start (Iniciar)** para definir o “Service status (Status do serviço)” como “Running (Em execução)”.
4. <span id="step04_4">Clique com o botão direito em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, selecione **Run (Executar)**, insira **sysdm.cpl** em **Run (Executar)**, e pressione Enter para acessar a janela “System Settings (Configurações do sistema)”.</span>
5. Na página da guia “Remote (Remoto)”, verifique se o “Remote Desktop (Área de Trabalho Remota)” está definido como “Allow remote connections to this computer (Permitir conexões remotas a este computador)”, conforme mostrado a figura abaixo:
![Remote Desktop settings](https://main.qcloudimg.com/raw/cbf2b2797bd48777008753f389574674.png)
 - Se estiver, vá para a [etapa 6](#step04_6).
 - Se não estiver, defina a Área de Trabalho Remota para “Allow remote connections to this computer (Permitir conexões remotas a este computador)”.
6. <span id="step04_6">Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> e selecione **Control Panel (Painel de controle)** para abri-lo.</span>
7. No “Control Panel (Painel de controle)”, selecione **System and Security (Sistema e segurança)** > **Windows Defender Firewall** para abri-lo.
8. No “Windows Defender Firewall”, verifique o seu status, conforme a figura a seguir:
![Windows Defender Firewall status](https://main.qcloudimg.com/raw/e74937594a03c141e6e5ac753f025d91.png)
 - Se o estado estiver “On (Ativado)”, vá para [etapa 9](#step04_9).
 - Se o estado estiver “Off (Desativado)”, [envie um ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
9. <span id = “step04_9”>No “Windows Defender Firewall”, selecione **Allow an app through Windows Firewall (Permitir um aplicativo no firewall do Windows)** para acessar a janela “Allowed apps (Aplicativos permitidos)”.</span>
10. Nessa janela, verifique se a “Remote Desktop (Área de Trabalho Remota)” está selecionada em “Allowed apps and features (Aplicativos e recursos permitidos)”, conforme mostrado na figura a seguir:
![Selecting Remote Desktop](https://main.qcloudimg.com/raw/dfed8792ce1dd8b32bee4aaa02ef6bbf.png)
 - Se estiver, vá para a [etapa 11](#step04_11).
 - Se não estiver, selecione “Remote Desktop (Área de Trabalho Remota)” para habilitá-la no firewall do Windows.
11. <span id = “step04_11”>No “Windows Defender Firewall”, selecione **Turn Windows Defender Firewall on or off (Ativar ou desativar o Windows Defender Firewall)** para acessar a janela “Customize Settings (Personalizar configurações)”.</span>
12. Nessa janela, defina o “Private network settings (Configurações de rede privada)” e o “Public network settings (Configurações de rede pública)” como “Turn off Windows Defender Firewall (not recommended) (Desativar o Windows Defender Firewall (não recomendado))”, conforme mostrado na figura a seguir:
![Turning off Windows Defender Firewall](https://main.qcloudimg.com/raw/5d5f8c4d7b783bc1018e03368ae400bc.png)

Se você ainda não conseguir se conectar à instância do Windows pela Área de Trabalho Remota após concluir as etapas anteriores, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

