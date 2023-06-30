## Cenário
A porta padrão do CVM é suscetível a varredura e ataque por software mal-intencionado. Portanto, é necessário alterar a porta remota padrão do CVM para uma porta menos comum, a fim de evitar a incapacidade de acessar remotamente o CVM devido a tais ataques. Isso garante a segurança do CVM.

As modificações na porta só serão válidas se forem feitas nas regras do grupo de segurança e no CVM simultaneamente. Você pode modificar a porta remota padrão do CVM conforme descrito abaixo. O método de modificação varia de acordo com o sistema operacional do CVM.
- [Modificação da porta remota padrão de um CVM do Windows](#ModifyWindowsCVMPort)
- [Modificação da porta remota padrão de um CVM do Linux](#ModifyLinuxCVMPort)

## Instruções

<span id="ModifyWindowsCVMPort"></span>
### Modificação da porta remota padrão de um CVM do Windows
> As operações a seguir usam um Windows Server 2012 como exemplo. O procedimento pode variar um pouco dependendo do sistema operacional e do idioma.
>
1. [Faça login em uma instância do Windows usando VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. No sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"> para abrir a janela "Windows PowerShell (PowerShell do Windows)".
3. Na janela "Windows PowerShell (PowerShell do Windows)", digite **regedit** e pressione **Enter** para abrir a janela "Registry Editor (Editor de registro)".
4. No painel de navegação de registro do lado esquerdo, expanda as seguintes hierarquias em sequência: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **Wds** > **rdpwd** > **Tds** > **tcp**.
5. <span id="Windows_step05"></span>Localize PortNumber em **tcp**. Em seguida, altere o valor de PortNumber de 3389 para um número de porta desocupada no intervalo de 0 a 65535, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/7044cef95fd7e56b56946afdb64de346.png)
6. No painel de navegação de registro do lado esquerdo, expanda as seguintes hierarquias em sequência: **HKEY_LOCAL_MACHINE** > **SYSTEM** > **CurrentControlSet** > **Control** > **Terminal Server** > **WinStations** > **RDP-Tcp**.
7. Localize e altere PortNumber em **RDP-Tcp** para ser o mesmo que em **tcp**.
![](https://main.qcloudimg.com/raw/fa54eb32c20dcc8a7c942c8e707fa665.png)
8. (Opcional) Se um firewall estiver ativado para seu CVM, certifique-se de adicionar a nova porta à lista de permissões do firewall e configurar para permitir a conexão.
 1. Na janela "Windows PowerShell (PowerShell do Windows)", digite **wf.msc** e pressione **Enter** para abrir a janela "Windows Firewall with Advanced Security (Firewall do Windows com segurança avançada)".
 2. Nela, selecione **Inbound Rules (Regras de entrada)** e clique em **New rule (Nova regra)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/ac93eed862e215971073912030fdbc41.png)
 3. Na página "Rule Type (Tipo de regra)" na janela "New Inbound Rule Wizard (Assistente de nova regra de entrada)", selecione **Port (Porta)** e clique em **Next (Avançar)**.
 4. Na página "Protocol and Ports (Protocolo e portas)" na janela **New Inbound Rule Wizard (Assistente de nova regra de entrada)**, selecione **TCP** e digite o número da porta definido na [Etapa 5](#Window_step05) em **Specific Port (Porta específica)**. Em seguida, clique em **Next (Avançar)**, conforme mostrado na figura a seguir.
 ![](https://main.qcloudimg.com/raw/73a7ca280f4f6b733d687597014b57b4.png)
 5. Na página**Action (Ação)** na janela "New Inbound Rule Wizard (Assistente de nova regra de entrada)", selecione **Allow connections (Permitir conexões)** e clique em **Next (Avançar)**.
 6. Na página "Profile (Perfil)" na janela "New Inbound Rule Wizard (Assistente de nova regra de entrada)", selecione o perfil padrão e clique em **Next (Avançar)**.
 7. Na página "Name (Nome)" na janela "New Inbound Rule Wizard (Assistente de nova regra de entrada)", insira o nome da regra e clique em **Finish (Concluir)**.
9. Na janela "Windows PowerShell (PowerShell do Windows)", digite **services.msc** e pressione **Enter** para acessar a janela "Services (Serviços)".
10. Localize e clique com o botão direito do mouse em **Remote Desktop Services (Serviços de área de trabalho remota)** na janela "Services (Serviços)". Em seguida, selecione **Restart (Reiniciar)** para reiniciar o serviço de login remoto.
11. Consulte [Modificação de regras de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34825) para modificar a regra do grupo de segurança com a porta de protocolo "TCP:3389", alterando o número da porta para aquele definido na [Etapa 5](#Windows_step05).
![](https://main.qcloudimg.com/raw/a447d7e69ce95d349f0d78b5b72b9228.png)


<span id="ModifyLinuxCVMPort"></span>
### Modificação da porta remota padrão de um CVM do Linux
>
> - Antes de modificar a porta remota padrão, recomendamos que você adicione o número da porta SSH e teste se ela foi conectada ao CVM. Em seguida, exclua a porta padrão 22. Certifique-se de que a porta padrão 22 não possa ser conectada ao CVM quando a nova porta falhar ao se conectar ao CVM.
> - As operações a seguir usam o CentOS 7.3 como exemplo. As operações específicas variam ligeiramente de acordo com a versão e o idioma do sistema operacional.
>
1. [Faça login em uma instância do Linux usando VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Execute o seguinte comando para modificar o arquivo de configuração:
```
vim /etc/ssh/sshd_config
```
3. <span id="Linux_step03"></span>Pressione **i** para mudar para o modo de edição e adicionar uma nova porta. Adicione `Port x` (em que x é o número da nova porta) em uma nova linha abaixo de `#Port 22` e exclua `#` para comentar a `Port 22`, como mostrado na figura a seguir.
Por exemplo, adicione `Port 23456` na linha.
![](https://main.qcloudimg.com/raw/54e5d9b4301271fbbeca8b2718b985dc.png)
4. Pressione **Esc**, digite **:wq** e salve a alteração.
5. Execute o seguinte comando para que a nova configuração entre em vigor:
```
systemctl restart sshd.service
```
6. (Opcional) Configure o firewall.
 - Por padrão, o serviço iptables é usado como firewall para CVMs do Linux com CentOS anterior ao 7. Configure o firewall conforme abaixo se as regras de iptables tiverem sido configuradas para o CVM.
    1. Execute o seguinte comando para configurar o firewall:
```
iptables -A INPUT -p tcp --dport <New port number> -j ACCEPT
```
Por exemplo, se o número da nova porta for 23456, execute o seguinte comando:
```
iptables -A INPUT -p tcp --dport 23456 -j ACCEPT
```
    2. Execute o seguinte comando para reiniciar o firewall:
```
service iptables restart
```
 - O serviço do Firewalld é usado como firewall para CVMs do Linux com CentOS 7 ou posterior. Configure o firewall conforme abaixo se o serviço Firewalld tiver sido ativado no CVM.
Execute o seguinte comando para permitir o acesso pelo número da porta adicionado na [Etapa 3](#Linux_step03):
```
firewall-cmd --add-port=<New port number>/tcp --permanent
```
Por exemplo, se o número da nova porta for 23456, execute o seguinte comando:
```
firewall-cmd --add-port=23456/tcp --permanent
```
Se `success` for retornado, a porta foi configurada.
7. Consulte [Modificação de regras de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34825) para modificar a regra do grupo de segurança com a porta de protocolo "TCP:22", alterando o número da porta para aquele definido na [Etapa 3](#Linux_step03).
![](https://main.qcloudimg.com/raw/add0bba23dc32f73b5d1fbbdad71c9ab.png)


## Verificação

### CVMs do Windows

1. Suponha que o sistema operacional Windows esteja instalado no computador local. Abra a caixa de diálogo "Remote Desktop Connection (Conexão de área de trabalho remota)".
2. Insira o `IP da Internet do servidor do Windows: número da porta após modificação` após **Computer (Computador)** e clique em **Connect (Conectar)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/1452f968e3c2c4d4c1083bdf0742df9d.png)
3. Insira a conta de administrador e a senha conforme solicitado e clique em **OK**.
Se a interface do sistema operacional do CVM do Windows for exibida, a conexão foi estabelecida.
> Se você fizer login no CVM do Windows usando um arquivo RDP, modifique o parâmetro `full address:s` no arquivo RDP, conforme mostrado na figura abaixo:
>[](https://main.qcloudimg.com/raw/84dd85a9547fc64f2daccba32f1d59d7.png)
>

### CVMs do Linux

1. Suponha que o PuTTY seja usado para login remoto. Inicie o cliente do PuTTY.
2. Na janela "PuTTY Configuration (Configuração do PuTTY)", insira o endereço IP público do CVM do Linux, defina **Port (Porta)** como o número da nova porta e clique em **Open (Abrir)**, conforme mostrado na figura a seguir.
![](https://main.qcloudimg.com/raw/c89c2064ed82e738fd60fcab39b09206.png)
3. Insira o nome de usuário e a senha do CVM do Linux conforme solicitado e pressione **Enter**.
Se a saída a seguir for exibida, a conexão foi estabelecida.
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
4. Depois de usar a nova porta para estabelecer uma conexão com o CVM do Linux, execute o seguinte comando:
```
vim /etc/ssh/sshd_config
```
5. Pressione **i** para mudar para o modo de edição e adicione `#` na frente da `Port 22` para comentar a porta.
6. Pressione **Esc**, digite **:wq** e salve a alteração.
7. Execute o comando a seguir para que a nova configuração entre em vigor. Certifique-se de usar a nova porta para o próximo login remoto no CVM do Linux.
```
systemctl restart sshd.service
```
