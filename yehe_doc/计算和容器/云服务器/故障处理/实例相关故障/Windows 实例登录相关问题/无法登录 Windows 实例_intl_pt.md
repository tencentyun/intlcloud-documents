Este documento descreve as possíveis causas de falhas de login da instância do Windows e seus métodos de solução de problemas. Você pode seguir as instruções para identificar a causa do problema e saber como corrigi-lo.

## Possíveis causas
A falha ao fazer login em uma instância do Windows pode ser o resultado de:
- [Problemas de senha](#CryptographicProblem)
- [Alta utilização de largura de banda](#BandwidthUtilization)
- [Carga alta do servidor](#HighServerLoad)
- [Configuração de porta remota inadequada](#RemotePortConfiguration)
- [Regras impróprias do grupo de segurança](#SafetyGroupRule)
- [Erro causado pelo firewall ou software de segurança](#LoginSecuritySoftware)
- [Erro de autenticação durante o acesso pela área de trabalho remota](#AuthenticationError)

Se você não conseguir solucionar o problema com uma ferramenta de diagnóstico, recomendamos que você [faça login por meio do VNC](#VNC) e siga as instruções no CVM.

<span id="TroubleshootingIdeas"></span>
## Solução de problemas

<span id="VNC"></span>
### Login por meio do VNC

Se você não conseguir fazer login em uma instância do Windows por meio de RDP ou software de acesso remoto, poderá fazer login por meio do VNC, o que ajuda a identificar a causa do problema.
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, selecione a instância a ser acessada e clique em **Log In (Fazer login)**, conforme ilustrado abaixo:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela **Fazer login na instância do Windows (Log into Windows instance)** exibida, selecione **Alternative methods (VNC) (Métodos alternativos (VNC))** e clique em **Log In Now (Fazer login agora)**.
> Se você esquecer a senha da instância, poderá redefini-la no console. Para mais informações, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
>
4. Na janela de login exibida, selecione **Send CtrlAltDel (Enviar CtrlAltDel)** no canto superior esquerdo e pressione **Ctrl-Alt-Delete** para abrir a janela de login do sistema, conforme a figura abaixo:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="CryptographicProblem"></span>
### Problemas de senha

**Problema**: a tentativa de login falhou porque você esqueceu a senha, digitou uma senha incorreta ou falhou ao redefinir sua senha.
**Procedimento**: redefina a senha desta instância no [console do CVM](https://console.cloud.tencent.com/cvm/index) e reinicie a instância. Para mais informações, consulte a seção [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Alta utilização de largura de banda

**Procedimento**:
1. Faça login na instância usando [o login por VNC](#VNC).
2. Verifique a utilização da largura de banda da instância e solucione os problemas adequadamente. Para mais detalhes, consulte [Falha de login devido à alta ocupação da largura de banda](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### Carga alta do servidor

**Problema**: O Cloud Monitor mostra uma carga alta na CPU do servidor e o sistema não pode ser acessado remotamente ou o acesso está lento.
**Possível causa**: vírus, trojans, software antivírus de terceiros, erros de aplicativos, de driver e atualizações automáticas de software no back-end podem levar à alta utilização da CPU, causando falhas de login do CVM ou acesso lento.
**Procedimento**:
1. Faça login na instância usando [o login por VNC](#VNC).
2. No **Task Manager (Gerenciador de tarefas)**, localize o processo que causa a maior carga. Para mais detalhes, consulte [Falha ao fazer login em um CVM do Windows devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32405).

<span id="RemotePortConfiguration"></span>
### Configuração de porta remota inadequada

**Problema**: a tentativa de acesso remoto a uma instância falhou, a porta de acesso remoto não é a porta padrão ou foi modificada ou a porta 3389 não está aberta.
**Diagnóstico**: execute o ping no endereço IP público da instância para verificar a conectividade da rede e execute telnet para verificar se a porta está aberta.
**Procedimento**: Consulte [Falha de login remoto devido a problemas de porta](https://intl.cloud.tencent.com/document/product/213/32540) para acessar o procedimento detalhado.

<span id="SafetyGroupRule"></span>
### Regras impróprias do grupo de segurança

**Procedimento**: Solucione o problema com a [ferramenta de verificação de grupo de segurança (porta)](https://console.cloud.tencent.com/vpc/helper).
> Para uma instância do Windows conectada remotamente, você precisa abrir a porta 3389.
> 
![](https://main.qcloudimg.com/raw/27b5aa974a2263719574dfc3bb7c0c6d.png)
Se o problema for causado por um problema de porta do grupo de segurança, você poderá usar a função **Open all ports (Abrir todas as portas)**.
![](https://main.qcloudimg.com/raw/bd91ec53dfd0df6bd1127a7f4f9db35c.png)
Para definir uma regra personalizada para o grupo de segurança, consulte [Adicionar regras para um grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).


<span id="LoginSecuritySoftware"></span>
### Erro causado pelo firewall ou software de segurança

**Problema**: a tentativa de login falhou devido ao firewall do CVM ou software de segurança.
**Diagnóstico**: faça login em uma instância do Windows por meio do VNC para verificar se o firewall está ativado e se softwares de segurança como 360 Total Security ou dongles de segurança estão instalados no servidor.
> Esta operação envolve a desativação do firewall do CVM. Para desativá-lo, verifique se você possui a permissão correspondente.
>
**Procedimento**: desligue o firewall ou o software de segurança instalado e repita a tentativa de acesso remoto. Por exemplo, você pode desativar o firewall do Windows Server 2016 da seguinte forma:
1. Faça login na instância usando [o login por VNC](#VNC).
2. Na área de trabalho do sistema operacional, clique em <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"> e escolha **Control Panel (Painel de controle)**.
3. Na janela **Control Panel (Painel de controle)**, clique em **Windows Firewall (Firewall do Windows)**.
4. Na janela **Windows Firewall (Firewall do Windows)**, clique em **Ativar ou desativar o firewall do Windows** à esquerda para abrir a **Custom Settings (Configurações personalizadas)**.
5. Defina a **Private Network Settings (Configurações de rede privada)** e a **Public Network Settings (Configurações de rede pública)** como **Disable Windows Firewall (Desativar firewall do Windows)** e clique em **OK**.
6. Reinicie a instância e repita a tentativa de acesso remoto.

<span id="AuthenticationError"></span>
### Erro de autenticação durante o acesso pela área de trabalho remota

**Problema**: ao tentar fazer login em uma instância do Windows pela área de trabalho remota, o prompt informa a mensagem “Authentication error. Invalid flag is provided to the function.” (Erro de autenticação. Um sinalizador inválido foi fornecido à função.) ou “Authentication error. The required function is not supported.” (Erro de autenticação. A função necessária não é compatível.) é exibido.
**Possíveis causas**: a Microsoft lançou uma atualização de segurança em março de 2018. Esta atualização ajusta uma vulnerabilidade de execução remota de código no Credential Security Supporting Program (CredSSP) corrigindo como o CredSSP valida as solicitações durante o processo de autenticação. O cliente e o servidor precisam ser atualizados ou o erro anterior pode ocorrer.
**Procedimento**: instale a atualização de segurança (recomendado). Para mais detalhes, consulte [Ocorreu um erro de autenticação ao tentar fazer login em uma instância do Windows remotamente](https://intl.cloud.tencent.com/document/product/213/32421).

## Outras soluções
Após tentar os métodos anteriores, se você ainda não conseguir fazer login na instância do Windows, salve os resultados do seu autodiagnóstico e [envie um ticket](https://console.cloud.tencent.com/workorder/category) para obter ajuda.
