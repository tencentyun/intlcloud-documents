Este artigo descreve como solucionar falhas de login remoto causada(s) por problema(s) em porta(s).
> Como exemplo, uma instância do CVM executando o Windows Server 2012 foi usada para descrever as etapas.
>

## Ferramentas
Você pode usar as seguintes ferramentas para verificar se os problemas de login estão relacionados a portas e configurações de grupos de segurança:
- [Autodiagnóstico](https://console.cloud.tencent.com/workorder/check) 
- [Ajuda do grupo de segurança (porta)](https://console.cloud.tencent.com/vpc/helper) 

Se constatado se o problema é de configuração do grupo de segurança, use **Open all ports (Abrir todas as portas)** no [Ajudante do grupo de segurança (porta)](https://console.cloud.tencent.com/vpc/helper) para abrir as portas relacionadas e tentar fazer login novamente. Se você ainda não conseguir fazer login após abrir as portas, consulte o guia de solução de problemas abaixo.

## Solução de problemas

### Verificação da conectividade de rede

Você pode usar o comando Ping para testar a conectividade de rede do seu PC. Você deve executar o teste em computadores em diferentes ambientes de rede (como diferentes intervalos de IP ou ISPs) para verificar se é um problema de rede local ou de servidor.

1. Abra a ferramenta de linha de comando em seu computador local.
 - Windows: Clique em **Start (Iniciar)** -> **Run (Executar)** e insira **cmd**. Uma janela de prompt de comando será exibida.
 - MacOS: Abra uma janela do Terminal.
2. Execute o comando a seguir para testar a conexão de rede.
```
ping + CVM_Instance_public_IP_address
```
Por exemplo, `ping 139.199.xxx.xxx`.
 - Se você receber resultados semelhantes aos mostrados na figura a seguir, sua conexão de rede com a instância do CVM está normal. Nesse caso, [verifique a configuração da área de trabalho remota](#F2).
![](https://main.qcloudimg.com/raw/52e6c15bc862dd7724643747ed8abcfb.png)
 - Se a mensagem **Request Timeout (Tempo limite da solicitação)** for exibida, a conexão entre a rede e a instância do CVM não está funcionando corretamente. Nesse caso, consulte [Falha no ping do endereço IP da instância](https://intl.cloud.tencent.com/document/product/213/14639) para mais alternativas de solução de problemas.
3. Execute o comando a seguir para verificar se a porta remota está aberta.
```
telnet CVM_instance_public_IP_address port_number
```
Por exemplo, `telnet 139.199.xxx.xxx 3389`, conforme a figura abaixo:
![](https://mc.qcloudimg.com/static/img/e18be3704977545d5c952d3a583f2ccc/image.png)
 - Caso apareça uma tela preta apenas com o cursor, significa que a porta (3389) está aberta. Para a próxima etapa, [verifique se o serviço de área de trabalho remota está ativado na instância](#F2).
 - Se a conexão falhar, conforme mostrado na figura a seguir, significa que ocorreu um erro de rede. Sendo assim, verifique o erro de acordo com o resultado do teste.
 ![](https://main.qcloudimg.com/raw/e3996140e2c1895d2ba2b1dfa637f998.png)
 
<span id = "F2"></span>
### Verificação da configuração da área de trabalho remota

#### Login na instância do CVM usando VNC

> É recomendável usar o VNC para fazer login somente se os métodos de login padrão falharem.
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Selecione o CVM desejado e clique em **Log In (Fazer login)**, conforme a seguinte figura:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. A página **Log into Windows instance (Fazer login na instância do Windows)** será exibida. Selecione **Alternative login method (VNC) (Método alternativo de login (VNC))** e clique em **Log In Now (Fazer login agora)** para fazer login na instância do CVM.
4. A página de login será exibida. Selecione **Send Ctrl-Alt-Del (Enviar Ctrl-Alt-Del)** no canto superior esquerdo e clique em **Ctrl-Alt-Delete** para acessar a interface de login do sistema, conforme a seguinte figura:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

#### Verificando se a área de trabalho remota está habilitada na instância do CVM

1. Faça login na instância do CVM. Clique com o botão direito em **This Computer (Este computador)** na área de trabalho e selecione **Properties (Propriedades)** para abrir a janela **System (Sistema)**.
2. Na janela **System (Sistema)**, selecione **Advanced System Configurations (Configurações avançadas do sistema)** para abrir a janela **System Properties (Propriedades do sistema)**.
3. Na janela **System Properties (Propriedades do sistema)**, selecione a guia **Remote (Remoto)**. Verifique se **Allow remote connections to this computer (Permitir conexões remotas a este computador)** em **Remote Desktop (Área de trabalho remota)** está marcado, conforme a figura abaixo:
![](https://main.qcloudimg.com/raw/2ee4d1abf5ebf351ed814d6644bc7d58.png)
 - Se estiver marcado, a conexão remota está habilitada. Em seguida, você deve [verificar se as portas de acesso remoto estão abertas](#F3).
 - Se estiver desmarcado, selecione **Allow remote connections to this computer (Permitir conexões remotas a este computador)** e tente se conectar à instância novamente.

<span id = "F3"></span>
### Verificando se as portas de acesso remoto estão abertas

1. Faça login na instância do CVM. Clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> para abrir uma janela do **Windows PowerShell**.
2. Na janela **Windows PowerShell**, execute o comando a seguir para verificar o status da área de trabalho remota que, por padrão, usa a porta 3389.
```
netstat -ant | findstr 3389
```
 - Se você receber resultados semelhantes aos mostrados na figura a seguir, o status está normal. Você pode tentar [reiniciar a área de trabalho remota](#F4) e se conectar à instância novamente para verificar se a conexão foi bem-sucedida.
![](https://main.qcloudimg.com/raw/5206af71e86f8126e9e6845bbeef21b2.png)
 - Se nenhuma conexão for exibida, significa que a área de trabalho remota não está funcionando corretamente. Você pode [verificar se as portas da área de trabalho remota no registro estão coerentes](#F5).

<span id = "F5"></span>
### Verificando se as portas da área de trabalho remota no registro estão corretas

> Esta seção descreve como verificar os valores de **TCP PortNumber (Número da porta TCP)** e **RDP Tcp Port Number (Número da porta TCP do RDP)**. Eles devem ser iguais.
>
1. Faça login na instância do CVM, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>, selecione <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>e insira **regedit**. Pressione **Enter** para abrir a janela **Registry Editor (Editor do registro)**.
2. No painel de navegação à esquerda, expanda os seguintes diretórios: **HKEY_LOCAL_MACHINE** -> **SYSTEM** -> **CurrentControlSet** -> **Control** -> **Terminal Server** -> **Wds** -> **rdpwd** -> **Tds** -> **tcp**.
3. Localize o PortNumber em **tcp** e registre o número da porta (3389 por padrão), conforme o exemplo abaixo:
![](https://main.qcloudimg.com/raw/6762d059263b1c589414461e522d1e9f.png)
4. No painel de navegação à esquerda, expanda os seguintes diretórios: **HKEY_LOCAL_MACHINE** -> **SYSTEM** -> **CurrentControlSet** -> **Control** -> **Terminal Server** -> **WinStations** -> **RDP-Tcp**.
5. Localize o PortNumber em **RDP-Tcp** e verifique se o valor de PortNumber em **RDP-Tcp** é o mesmo que em **tcp**, conforme mostrado no exemplo a seguir:
![](https://main.qcloudimg.com/raw/9d68cec10e75afe621beb6c914d393cb.png)
 - Se não forem iguais, siga a [Etapa 6](#F5_step6).
 - Se forem iguais, [reinicie a área de trabalho remota](#F4).
6. Clique duas vezes em PortNumber em **RDP-Tcp**.
7. Na caixa de diálogo exibida, modifique o **Value Data (Dados de valor)** para um número de porta livre entre 0 e 65535. Certifique-se de que **TCP PortNumber (Número da porta TCP)** e **RDP Tcp PortNumber (Número da porta TCP do RDP)** são iguais e clique em **OK**.
7. Reinicie a instância usando o [console do CVM](https://console.cloud.tencent.com/cvm) e tente se conectar remotamente à instância novamente para verificar se a conexão foi bem-sucedida.


<span id = "F4"></span>
### Reinicialização da área de trabalho remota

1. Faça login na instância do CVM. Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> e selecione <img src="https://main.qcloudimg.com/raw/5b5e3abb2f39cb719a4119ba77b74447.png" style="margin: 0;"></img>. Digite **services.msc** e pressione **Enter** para abrir a janela **Services (Serviços)**.
2. Na janela **Services (Serviços)**, clique com o botão direito em **Serviços de área de trabalho remota** e selecione **Restart (Reiniciar)** para reiniciar o serviço de área de trabalho remota, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/396ee711bb64c8fb1966112a81dd0fd4.png)

## Se tudo falhar

Se você ainda não conseguir fazer login remotamente após realizar as etapas mencionadas acima, [envie um ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2) para obter ajuda.
