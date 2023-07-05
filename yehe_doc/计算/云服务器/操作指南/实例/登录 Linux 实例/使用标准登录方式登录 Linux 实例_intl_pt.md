### Cenário

O WebShell é o método de login recomendado pelo Tencent Cloud. Não importa se seu sistema operacional local é Windows, Linux ou Mac OS, contanto que você tenha adquirido IPs públicos para suas instâncias, você pode fazer login por Web Shell. Este documento descreve como fazer login em uma instância do Linux por Web Shell.
Benefícios do Web Shell:
- Aceita operações de copiar e colar com teclas de atalho.
- Aceita rolagem com o botão de rolagem do mouse.
- Aceita entrada chinesa.
- Possui alta segurança (é necessária senha ou chave para cada login).

## Sistema operacional local aplicável

Windows, Linux ou Mac OS.

## Método de autenticação

**Senha** ou **Chave**

## Pré-requisitos

- Você já deve ter a conta de administrador e a senha (ou chave) da instância para fazer login.
 - Se você escolher **Random Password (Senha aleatória)** ao criar a instância, vá para [Mensagem interna](https://console.cloud.tencent.com/message) para verificar a senha.
 - Se você esqueceu sua senha, [redefina a senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Certifique-se de que a instância do CVM tenha um IP público e a porta 22 esteja aberta. (Se o CVM for adquirido com a “Configuração rápida”, esta porta fica aberta por padrão.)

### Direções

1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento da instância, selecione o CVM do Linux no qual deseja fazer login e clique em **Log In (Login)** conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3. Na janela pop-up **Log in Linux instance (Login na instância do Linux)**, selecione **Standard login method (Método padrão de login)** e clique em **Log In Now (Fazer login agora)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/87ba7e511f8d0ffe48f220cecaa7b057.png)
4. Na janela **Log into Instance (Login na instância)**, selecione **Password Login (Login com senha)** ou **Key Login (Login com chave)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
Se o login for bem-sucedido, a mensagem “Socket connection established (Conexão de soquete estabelecida)” será exibida conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## Operações subsequentes

Depois de fazer o login no CVM, você pode criar um site pessoal ou fórum no CVM do Tencent Cloud ou realizar outras operações. Para obter mais informações, consulte os documentos a seguir:
- [Criar um site pessoal no WordPress](https://intl.cloud.tencent.com/document/product/213/8044)

