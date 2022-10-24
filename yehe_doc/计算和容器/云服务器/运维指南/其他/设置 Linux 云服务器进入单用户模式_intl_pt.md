## Visão geral
Para operações como gerenciamento de senha, correção de SSHD e manutenção antes da montagem do disco, os usuários do Linux precisam entrar no modo de usuário único. Este documento descreve como inicializar neste modo nas principais distribuições do Linux.

## Instruções
1. No console do CVM, escolha VNC para fazer login em um CVM. Para obter instruções detalhadas, consulte [Login em instâncias do Linux por VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Na janela de login do VNC, selecione **Send CtrlAltDel (Enviar CtrlAltDel)** no canto superior esquerdo, pressione **Ctrl-Alt-Delete** e clique em **OK** na caixa de prompt.
3. Quando uma mensagem de falha de conexão for exibida, pressione a seta para cima ou para baixo para atualizar a página e passe o cursor sobre o menu `grub`, conforme a seguir.
![](https://main.qcloudimg.com/raw/350187ce0a771d00e6d54e929291ebae.png)
4. Pressione **e** para entrar no modo de resgate do grub.
5. Execute as etapas adequadas à versão do seu sistema operacional.
<dx-tabs>
::: CentOS\s6.x
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/5abc9f57184cc74bba927513fb1c4a88.png)
2. Pressione **e** para acessar a página de edição do kernel, escolha a linha do **kernel** usando a seta para cima ou para baixo e pressione **e** novamente, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/1a596a48df87d1d619e415d8d5b0cb65.png)
3. Insira **single** no final da linha, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/e1f74a4ce211a34301c4f74ffcc790b8.png)
4. Pressione **Enter** e, em seguida, **b** para inicializar a linha de comando selecionada e entrar no modo de usuário único, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/b379937bfc15e93f0823ec50095d1dc6.png)
A figura a seguir indica que o sistema inicializa no modo de usuário único.
![](https://main.qcloudimg.com/raw/517c4d2c24864f3fc8f5002bd1e2c2a1.png)
<dx-alert infotype="explain" title="">
Você pode executar o comando `exec /sbin/init` para sair do modo de usuário único.
</dx-alert>
:::
::: CentOS\s7.x
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/2ddc7d1e4416d9fa763922e23b59d580.png)
2. Pressione **e** para acessar a página de edição do kernel. Localize a linha iniciada com "linux16" usando a seta para cima ou para baixo e substitua `ro` por `rw init=/bin/bash` ou `/usr/bin/bash`, como mostrado abaixo.
![](https://main.qcloudimg.com/raw/1b861ba0ecee1cd82da4364523e8a1c6.png)
3. Pressione **Ctrl+X** para inicializar no modo de usuário único, conforme mostrado abaixo:
A figura a seguir indica que o sistema inicializa no modo de usuário único.
![](https://main.qcloudimg.com/raw/fbe8cfcf43aa4c914882edc4c3ee5faf.png)
<dx-alert infotype="explain" title="">
 Você pode executar o comando `exec /sbin/init` para sair do modo de usuário único.
</dx-alert>
:::
::: CentOS\s8.0
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/a6ce701e5845141929d822635bd42b9a.png)
2. Pressione **e** para acessar a página de edição do kernel. Localize a linha iniciada com "linux" usando a seta para cima ou para baixo e substitua `ro` por `rw init=/sysroot/bin/bash`, como mostrado abaixo.
![](https://main.qcloudimg.com/raw/d06effc3cab12d545fd7bc92f4577b14.png)
3. Pressione **Ctrl+X** para inicializar no modo de usuário único, conforme mostrado abaixo:
A figura a seguir indica que o sistema inicializa no modo de usuário único.
![](https://main.qcloudimg.com/raw/126dcdb5916e57815c3632e9e4b24412.png)
:::
::: Ubuntu\sou\sDebian
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/c3c0be766481edf3f6521f7764f8d4cb.png)
2. Pressione **e** para acessar a página de edição do kernel. Localize a linha iniciada com "linux" usando a seta para cima ou para baixo e adicione `quiet splash rw init=/bin/bash` ao final da linha, como mostrado abaixo.
![](https://main.qcloudimg.com/raw/40882cf22d755c0338ea9d7c106bc280.png)
3. Pressione **Ctrl+X** para inicializar no modo de usuário único, conforme mostrado abaixo:
A figura a seguir indica que o sistema inicializa no modo de usuário único.
![](https://main.qcloudimg.com/raw/df55d20b7eb087744fb6283c5124e7fc.png)
:::
::: SUSE
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/4da4d0c5c98e4f0dbe4990e920a11daf.png)
2. Pressione **e** para acessar a página de edição do kernel. Localize a linha iniciada com "linux" usando a seta para cima ou para baixo, adicione `rw` no início e `1` no final do parâmetro `splash`, como mostrado abaixo.
![](https://main.qcloudimg.com/raw/013a0099ccb5c19d04441dd60ea7558b.png)
3. Pressione **Ctrl+X** para inicializar no modo de usuário único, conforme mostrado abaixo:
:::
::: tlinux
1. Selecione um kernel no modo grub, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/c497e63321b76e5cd1f0eea06f53cdb2.png)
2. Pressione **e** para acessar a página de edição do kernel, escolha a linha do **kernel** usando a seta para cima ou para baixo e pressione **e** novamente, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/06c66e0f30163e9fc7e6aafbf9463645.png)
3. Adicione um espaço e **1** ao final da linha (ou seja, após **256M**), conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/06efb32e3a2edb39f32e13be1ab8527f.png)
4. Pressione **Enter** para entrar no modo de usuário único.
:::
</dx-tabs>
