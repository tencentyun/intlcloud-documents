Este documento descreve as possíveis causas de falhas de login da instância do Linux e os métodos de solução de problemas, ajudando você a detectar, localizar e resolver os problemas.

## Possíveis causas
As principais causas de falhas de login da instância do Linux incluem:
- [Problemas de chave SSH](#UseSSHLogin)
- [Problemas de senha](#CryptographicProblem)
- [Utilização excessiva de largura de banda](#BandwidthUtilization)
- [Carga alta do servidor](#HighServerLoad)
- [Regras incorretas do grupo de segurança](#SafetyGroupRule)


Se você não puder verificar seu problema usando a ferramenta de autodiagnóstico, recomendamos que [faça login no CVM por meio do VNC](#VNC) e solucione o problema passo a passo.

## Solução de problemas
### Login usando o VNC
<span id="VNC"></span>
Se você não puder usar o método padrão (Orcaterm) ou o software de login remoto para fazer login em uma instância do Linux, poderá usar o VNC da Tencent Cloud para fazer login e localizar as causas do problema.
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, selecione a instância a ser acessada e clique em **Log In (Fazer login)**, conforme mostrado na figura abaixo:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. Na janela “Log in to Linux Instance (Login na instância do Linux)” exibida, selecione **Alternative login methods (VNC) (Métodos alternativos de login (VNC))** e clique em **Log In Now (Fazer login agora)**.
> Durante o login, se você esquecer a senha desta instância, poderá redefini-la no console. Para mais informações, consulte [Redefinição da senha da instância](http://intl.cloud.tencent.com/document/product/213/16566).
>
4. Digite o nome de usuário e a senha na caixa de diálogo exibida para concluir o processo de login.

<span id="UseSSHLogin"></span>
### Problemas de SSH
**Problema**: durante o [login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32501), é exibida uma mensagem indicando que a conexão não está disponível ou falhou.
**Etapas**: consulte [Não é possível fazer login em uma instância do Linux usando SSH](https://intl.cloud.tencent.com/document/product/213/32486) para solucionar o problema.

<span id="CryptographicProblem"></span>
### Problemas de senha
**Problema**: não é possível fazer login porque você esqueceu a senha, digitou-a incorretamente ou não conseguiu redefini-la.
**Solução**: redefina a senha desta instância no [console da Tencent Cloud](https://console.cloud.tencent.com/cvm/index) e reinicie a instância.
**Etapas**: para mais informações sobre como redefinir a senha de uma instância, consulte [Redefinição da senha da instância](http://intl.cloud.tencent.com/document/product/213/16566).

<span id="BandwidthUtilization"></span>
### Utilização excessiva de largura de banda
**Problema**: a ferramenta de autodiagnóstico mostra que a utilização da largura de banda está muito alta.
**Etapas**:
1. Faça login na instância usando o [VNC](#VNC).
2. Verifique a utilização da largura de banda da instância e solucione os problemas adequadamente. Para mais detalhes, consulte [Não é possível fazer login devido à alta utilização da largura de banda](https://intl.cloud.tencent.com/document/product/213/32542).

<span id="HighServerLoad"></span>
### Carga alta do servidor
**Problema**: o Tencent Cloud Observability Platform mostra que a carga da CPU do servidor está alta e o sistema não pode ser acessado remotamente ou o acesso está lento.
**Possíveis causas**: vírus, trojans, software antivírus de terceiros, erros de aplicativos, de driver e atualizações automáticas de back-end de software podem levar ao alto uso da CPU, causando falhas de login do CVM ou acesso lento.
**Etapas**:
1. Faça login na instância usando o [VNC](#VNC).
2. Em “Task manager (Gerenciador de tarefas)”, localize o processo com carga alta. Para mais detalhes, consulte [Não é possível fazer login devido ao alto uso de CPU e memória](https://intl.cloud.tencent.com/document/product/213/32387).

<span id="SafetyGroupRule"></span>
### Regras incorretas do grupo de segurança
**Problema**: não é possível fazer login devido a regras incorretas do grupo de segurança.
**Etapas**: solucione o problema usando a [ferramenta de verificação de porta para grupos de segurança](https://console.cloud.tencent.com/vpc/helper).
![](https://main.qcloudimg.com/raw/278c7f0abd9b7224d32fa5402554544a.png)
Se o problema for causado pela configuração incorreta da porta do grupo de segurança, você poderá usar **Open All Tools (Abrir todas as portas)** para abrir todas as portas.
![](https://main.qcloudimg.com/raw/e4a40dafcc9607ce18ee7001129d9655.png)
Se você precisar definir uma regra personalizada para o grupo de segurança, consulte [Adição de regras aos grupos de segurança](https://intl.cloud.tencent.com/document/product/213/34272), para obter informações sobre como reconfigurar as regras do grupo de segurança.



## Outras soluções
Se você ainda não conseguir fazer login na instância do Linux após tentar os métodos de solução de problemas anteriores, salve os resultados do autodiagnóstico e [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
