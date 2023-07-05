## Cenário

O login pelo VNC fornecido pelo Tencent Cloud permite que os usuários se conectem remotamente ao CVM por meio de um navegador da web. Se um cliente não tiver o login remoto instalado ou ele não puder ser usado ou conectado por algum outro meio, os usuários podem se conectar a um CVM usando o login pelo VNC para observar o status do CVM e realizar operações básicas de gerenciamento do CVM usando a conta do CVM.

## Limites de uso

- Atualmente, as funcionalidades como copiar/colar, entrada em chinês e upload/download de arquivos não são aceitas em CVMs usando o login do VNC.
- Deve-se usar os navegadores convencionais ao usar o login pelo VNC em um CVM, como Chrome, Firefox e IE 10 ou superior.
- Um login pelo VNC é um terminal dedicado, o que significa que apenas um usuário pode usar um login pelo VNC por vez.

## Sistema operacional aplicável

Windows, Linux ou macOS.

## Pré-requisitos

Você já deve ter a conta de administrador e a senha para fazer login em uma instância do Windows remotamente.
- Se você usar uma senha padrão do sistema para fazer login na instância, obtenha-a visitando [Mensagem interna](https://console.cloud.tencent.com/message).
Se você esqueceu sua senha, [redefina a senha da instância](http://intl.cloud.tencent.com/document/product/213/16566).

## Etapas

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento da instância, selecione o CVM do Windows no qual deseja fazer login e clique em **Log In (Login)** conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. Na janela pop-up **Log into Windows instance (Login na instância do Windows)**, selecione **Alternative login methods (VNC) (Métodos alternativos de login (VNC))** e clique em **Log In Now (Fazer login agora)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. Na janela de login, selecione “Send Remote Command (Enviar comando remoto)” no canto superior esquerdo e pressione **Ctrl-Alt-Delete** para entrar na interface de login do sistema conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)



