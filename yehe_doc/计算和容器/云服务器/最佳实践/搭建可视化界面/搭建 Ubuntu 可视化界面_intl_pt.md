## Visão geral
O Virtual Network Console (VNC) é um software de ferramenta de controle remoto desenvolvido pelo AT&T European Research Laboratory. Um software de código aberto baseado em sistemas operacionais UNIX e Linux, o VNC apresenta capacidade robusta de controle remoto, alta eficiência e grande praticidade. Seu desempenho é comparável ao de qualquer software de controle remoto no Windows ou Mac. Este documento irá guiá-lo sobre como construir uma área de trabalho visual do Ubuntu usando VNC.

## Pré-requisitos
Ter adquirido um CVM Linux com o sistema operacional Ubuntu. Caso contrário, consulte [Personalização das configurações do CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517).


## Instruções

1. [Faça login em uma instância do Linux usando VNC](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute o seguinte comando para mudar para a conta "raiz".
```
sudo su root
```
3. Execute o seguinte comando para obter, e atualizar para, a versão mais recente.
```
apt-get update
```
4. Selecione e execute o comando abaixo de acordo com a versão do seu sistema para instalar o VNC.
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
apt-get install vnc4server
```
:::
::: Ubuntu\s20.04
```
apt-get install tightvncserver
```
:::
</dx-tabs>
5. <span id="step05"></span>Execute o seguinte comando para iniciar o VNC e definir uma senha.
```
vncserver
```
Se o resultado retornado for semelhante ao que segue, isso indica que o VNC foi iniciado com sucesso.
![](https://main.qcloudimg.com/raw/adad6ffbb0b1b722d1e429133060134b.png)
6. Execute o seguinte comando para instalar o pacote básico do X-window.
```
sudo apt-get install x-window-system-core
```
7. Execute o seguinte comando específico do sistema para instalar o gerenciador de login.
<dx-tabs>
::: Ubuntu\s16.04/18.04
```
sudo apt-get install gdm
```
:::
::: Ubuntu\s20.04
```
sudo apt-get install gdm3
```
:::
</dx-tabs>
8. Execute o seguinte comando para instalar a área de trabalho do Ubuntu.
```
sudo apt-get install ubuntu-desktop
```
Durante a instalação, escolha "gdm3" para `Default display manager:` (Gerenciador de exibição padrão).
9. Execute o seguinte comando para instalar o software de suporte GNOME.
```
sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
10. Execute o seguinte comando para acessar o arquivo de configuração do VNC.
```
vi ~/.vnc/xstartup
```
11. Pressione **i** para entrar no modo de edição e modifique o arquivo de configuração como segue.
```
#!/bin/sh
# Remova o comentário das duas linhas a seguir para uma área de trabalho normal:
export XKL_XMODMAP_DISABLE=1
 unset SESSION_MANAGER
# exec /etc/X11/xinit/xinitrc
unset DBUS_SESSION_BUS_ADDRESS
gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```
12. Pressione **Esc** e digite **:wq** para salvar e fechar o arquivo.
13. Execute os seguintes comandos para reiniciar o processo da área de trabalho.
```
vncserver -kill:1 # Digite o comando para encerrar o processo da área de trabalho original (em que :1 é o número da área de trabalho)
```
```
vncserver :1 # Gerar uma nova sessão
```
14. [Clique aqui](https://www.realvnc.com/en/connect/download/viewer/) para fazer o download e instalar o VNC Viewer. Selecione a versão que corresponde ao seu sistema operacional.
15. Digite `CVM IP address: 1` no VNC Viewer e pressione **Enter**.
![](https://main.qcloudimg.com/raw/df25e2085e9d27d53b1827ccf98a3618.png)
16. Clique em **Continue (Continuar)** na caixa de diálogo pop-up.
17. Digite a senha VNC definida na [Etapa 5](#step05) e clique em **OK**.
>? Em caso de tempo limite de conexão, verifique a conexão de rede e as configurações do grupo de segurança. Crie uma regra de entrada `TCP:5901` para o grupo de segurança para abrir a porta de escuta 5901 do VNC Server. Para obter instruções detalhadas, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).









