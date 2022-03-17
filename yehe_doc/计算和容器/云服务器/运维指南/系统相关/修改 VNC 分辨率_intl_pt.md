## Visão geral

Por padrão, algumas imagens do sistema Linux possuem resoluções de exibição do VNC mais baixas. Por exemplo, a resolução do VNC para CentOS é apenas 720 \* 400. Você pode definir a resolução do VNC para 1024 \* 768 modificando o parâmetro `grub`.
Se as imagens do sistema Windows tiverem resoluções do VNC muito baixas, alguns aplicativos podem não ser exibidos ou abertos corretamente. Para evitar esses problemas, é necessário modificar as resoluções das imagens do sistema Windows.

Este documento descreve como ajustar a resolução de exibição do VNC de um CVM.

## Instruções

### Modificação da resolução do VNC de uma instância do CVM do Windows

>? As etapas abaixo descrevem como modificar a resolução do VNC de uma instância do Windows no sistema operacional Windows Server 2012.

1. [Login em uma instância do Windows por VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Clique com o botão direito do mouse na área de trabalho e selecione **Screen resolution (Resolução da tela)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b8ec8e8ec22002532a4a517150079d2d.png)
3. Na janela "Screen resolution (Resolução da tela)", defina **Resolution (Resolução)** com o valor desejado e clique em **Apply (Aplicar)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/b90a33fa0600846888a15154f1e656dc.png)
4. Na janela pop-up, clique em **Keep changes (Manter as alterações)**.
5. Clique em **OK** para fechar a janela "Screen resolution (Resolução da tela)".

### Modificação da resolução do VNC de uma instância do CVM do Linux

Imagens mais recentes do Linux, como CentOS 7, CentOS 8, Ubuntu e Debian 9.0, adotam uma resolução do VNC padrão de 1024 \* 768, que pode ser usada sem nenhuma modificação. O guia abaixo apresenta como modificar as resoluções do VNC de instâncias do Linux nos sistemas operacionais CentOS 6 e Debian 7.8.

#### CentOS 6

Por padrão, uma imagem do CentOS 6 tem uma resolução do VNC de 720 \* 400. Para definir sua resolução para 1024 \* 768, modifique o parâmetro de inicialização `grub` da seguinte forma:
- [Login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais esteja mais familiarizado:
 - [Login em uma instância do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Login em uma instância do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Login em uma instância do Linux por VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Execute o comando a seguir para abrir o arquivo `/etc/grub.conf`.
```
vi /etc/grub.conf
```
3. Pressione **i** para mudar para o modo de edição e adicione `vga=792` ao parâmetro `grub`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/3c2193fa370c48a7af149c63720da077.png)
4. Pressione **Esc**, digite **:wq** e salve e feche o arquivo.
5. Execute o comando a seguir para reinicializar o CVM.
```
reboot
```

#### Debian 7.8

Por padrão, ambas as imagens do Debian 7.8 e Debian 8.2 têm resoluções do VNC de 720 \* 400. Para definir sua resolução para 1024 \* 768, modifique o parâmetro de inicialização `grub` da seguinte forma:
- [Login em uma instância do Linux usando o método de login padrão](https://intl.cloud.tencent.com/document/product/213/5436). Você também pode usar outros métodos de login com os quais esteja mais familiarizado:
 - [Login em uma instância do Linux por meio de ferramentas de login remoto](https://intl.cloud.tencent.com/document/product/213/32502).
 - [Login em uma instância do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501)
 - [Login em uma instância do Linux por VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Execute o comando a seguir para abrir o arquivo `grub`.
```
vi /etc/default/grub
```
3. Pressione **i** para mudar para o modo de edição e adicione `vga=792` ao final do valor do parâmetro `GRUB_CMDLINE_LINUX_DEFAULT`.
![](https://main.qcloudimg.com/raw/f8e275c35b65b7b2d26cfbd7a8ae4dd6.png)
4. Pressione **Esc**, digite **:wq** e salve e feche o arquivo.
5. Execute o comando a seguir para atualizar o arquivo `grub.cfg`.
```
grub-mkconfig -o /boot/grub/grub.cfg
```
6. Execute o comando a seguir para reinicializar o CVM.
```
reboot
```


## Apêndice

A tabela abaixo compara a resolução da instância do Linux e os parâmetros do VGA:
<table>
	<tr><th>Resolução</th><td>640 * 480</td><td>800 * 600</td><td>1024 * 768</td></tr>
	<tr><th>VGA</th><td>786</td><td>789</td><td>792</td></tr>
</table>
