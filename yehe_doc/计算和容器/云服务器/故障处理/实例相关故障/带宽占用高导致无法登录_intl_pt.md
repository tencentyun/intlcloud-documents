
Este documento descreve como diagnosticar e solucionar problemas de login do CVM do Linux ou Windows causados pelo alto uso de largura de banda.

## Problemas
- No [console do CVM](https://console.cloud.tencent.com/cvm/index), os dados de monitoramento de largura de banda do CVM indicam tanto que o uso de largura de banda é muito alto quanto falha de conexão com o CVM.

## Localização e solução de problemas

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Selecione o CVM a ser verificado e clique em **Log In (Fazer login)**. Verifique a figura abaixo para mais detalhes.
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. Na janela **Log into Windows/Linux instance (Fazer login na instância do Windows/Linux)**, selecione **Alternative login methods (VNC) (Métodos de login alternativos (VNC))** e clique em **Log In Now (Fazer login agora)** para fazer login no CVM.
4. Na janela de login exibida, selecione **Send Remote Command (Enviar comando remoto)** no canto superior esquerdo e clique em **Ctrl-Alt-Delete** para acessar a interface de login do sistema conforme abaixo:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### CVMs do Windows
Após fazer o login no CVM do Windows com o VNC, execute as operações a seguir:
> As operações a seguir usam um CVM com o sistema Windows Server 2012 como exemplo.
>
1. No CVM, clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>. Selecione o **Task Manager (Gerenciador de tarefas)** para abrir a janela dele.
2. Selecione a página da guia **Performance (Desempenho)** e clique em **Open Resource Monitor (Abrir monitor de recursos)**. Verifique a figura abaixo para mais detalhes.
![](https://main.qcloudimg.com/raw/a635da7e769cc1424b225674803e5cb1.png)
3. Quando ele abrir, verifique qual processo consome mais largura de banda. De acordo com a sua atividade em si, determine se o processo é normal. Verifique a figura abaixo para mais detalhes.
![](https://main.qcloudimg.com/raw/6a131472fc52bb4f5c4d5f57a1b7b010.png)
 - Se o processo que consome muita largura de banda estiver normal, verifique se é devido a alterações no volume de acesso, e se você precisa otimizar a capacidade ou [fazer upgrade das configurações do CVM](https://intl.cloud.tencent.com/document/product/213/2178).
 - Se o processo que consome muita largura de banda for anormal, pode haver um vírus ou um trojan. Você pode encerrar o processo por conta própria ou usar um software de segurança. Você também pode reinstalar o sistema após o backup dos dados.
 > Nos sistemas Windows, muitos processos de vírus são disfarçados como processos do sistema. Você pode usar as informações do processo em **Task Manager (Gerenciador de tarefas)** > **Processes (Processos)** para realizar a inspeção preliminar:
 > Os processos normais do sistema têm assinaturas e descrições completas, e a maioria deles está localizada no diretório C:\Windows\System32. Os programas de vírus podem ter o mesmo nome que os processos do sistema, mas não possuem assinaturas ou descrições. A localização também será anormal.
 > 
 - Se o processo que consome muita largura de banda for um processo de componente da Tencent Cloud, [envie um ticket](https://console.cloud.tencent.com/workorder/category) para entrar em contato conosco. Ajudaremos você a localizar e solucionar o problema.

### CVMs do Linux
Após usar o VNC para fazer login no CVM do Linux, realize as seguintes operações:
> As operações a seguir usam um CVM com o sistema CentOS 7.6 como exemplo.
>
1. Execute o comando a seguir para instalar a ferramenta iftop. A ferramenta iftop é um gadget de monitoramento de tráfego para o CVM do Linux.
```
yum install iftop -y
```
> Para o sistema Ubuntu, execute o comando `apt-get install iftop -y`.
>
2. Execute o comando a seguir para instalar o lsof.
```
yum install lsof -y
```
3. Execute o comando a seguir para executar o iftop. Verifique a figura abaixo para mais detalhes.
```
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`、`=>` indica a direção do tráfego
 - TX indica o tráfego de entrega
 - RX indica o tráfego recebido
 - TOTAL indica o tráfego total
 - cum indica o tráfego total desde o momento em que o iftop começa a funcionar até agora
 - peak indica os picos de tráfego
 - rates indica o tráfego médio nos últimos 2 s, 10 s e 40 s, respectivamente
4. De acordo com o IP do tráfego consumido no iftop, execute o comando a seguir para verificar o processo conectado a este IP.
```
lsof -i | grep IP
```
Por exemplo, se o IP do tráfego consumido for 201.205.141.123, execute o comando a seguir:
```
lsof -i | grep 201.205.141.123
```
Se os resultados a seguir forem retornados, a largura de banda do CVM é consumida principalmente pelo processo do SSH.
```
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. Exiba o processo que consome largura de banda e determine se o processo é normal.
 - Se o processo que consome muita largura de banda estiver normal, verifique se é devido a alterações no volume de acesso, e se você precisa otimizar a capacidade ou [fazer upgrade das configurações do CVM](https://intl.cloud.tencent.com/document/product/213/2178).
 - Se o processo que consome muita largura de banda for anormal, pode haver um vírus ou um trojan. Você pode encerrar o processo por conta própria ou usar um software de segurança. Você também pode reinstalar o sistema após o backup dos dados.
 - Se o processo que consome muita largura de banda for um processo de componente da Tencent Cloud, [envie um ticket](https://console.cloud.tencent.com/workorder/category) para entrar em contato conosco. Ajudaremos você a localizar e solucionar o problema.


Recomendamos que você verifique a localização do IP de destino em [What Is My IP Address](https://whatismyipaddress.com/). Se a localização do IP estiver em outros países/regiões, o risco de segurança é maior.

