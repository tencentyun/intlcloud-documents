## Visão geral

Este documento descreve como usar uma chave SSH para fazer login em uma instância do Linux a partir de um Linux, Mac OS ou Windows local.

## Sistemas compatíveis

Linux, Mac OS ou Windows (incluindo Windows 10 e Windows Server 2019)

## Método de autenticação

**Senha** ou **Chave**

## Pré-requisitos
- Você já deve ter a conta de administrador e a senha (ou chave) para fazer login na instância.
 - Se você usar uma senha padrão do sistema para fazer login na instância, vá primeiro para o [Centro de mensagens](https://console.cloud.tencent.com/message) para obtê-la.
 - Se você [usar uma chave](#LoginWithKey) para fazer o login, deve ter criado uma chave e vinculado a este CVM. Para obter mais informações, consulte [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691).
 - Se você esqueceu sua senha, [redefina sua senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Um IP público foi adquirido para sua instância do CVM e a porta 22 está aberta. (Ela fica aberta por padrão para um CVM adquirido com a configuração rápida).

## Direções

### Uso da senha

1. Execute o seguinte comando para se conectar ao CVM do Linux.
>? Se o seu computador local usa o Mac OS, você deve abrir o terminal fornecido pelo sistema e, em seguida, executar o seguinte comando.
> Se o seu computador local usa o Linux, você pode executar diretamente o seguinte comando.
> Se o seu computador local usa o Windows 10 ou o Windows Server 2019, você deve primeiro abrir o prompt de comando CMD e depois executar o seguinte comando.
>
```
ssh <username>@<hostname or IP address>
```
 - `username` refere-se ao nome da conta padrão obtido como um pré-requisito.
 - `hostname or IP address` refere-se ao endereço IP público ou nome de domínio personalizado da sua instância do Linux.
2. Digite a senha que você já obteve e pressione **Enter** para fazer login.

<span id="LoginWithKey"></span>
### Uso da chave

1. Execute o seguinte comando para definir o arquivo de chave privada que pode ser lido apenas por você.
 - Se o seu computador local usa o Mac OS, primeiro você deve abrir o terminal fornecido pelo sistema e, em seguida, executar o seguinte comando.
 - Se o seu computador local usa o Linux, você pode executar diretamente o seguinte comando.
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
 - Se o seu computador local usa o Windows 10, você deve primeiro abrir o prompt de comando CMD e depois executar os seguintes comandos.
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /grant <Windows user account>:F
```
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /inheritancelevel:r
```
2. Execute o seguinte comando para login remoto.
```
ssh -i <The absolute path of the private key downloaded to be associated with the CVM> <username>@<hostname or IP address>
```
 - `username` refere-se ao nome da conta padrão obtido como um pré-requisito.
 - `hostname or IP address` refere-se ao endereço IP público ou nome de domínio personalizado da sua instância do Linux.

 Por exemplo, execute o comando `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` para fazer login remotamente no CVM do Linux.

## Operações subsequentes

Depois de fazer o login no CVM, você pode criar um site pessoal ou fórum ou realizar outras operações. Para obter mais informações, consulte:
- [Criação manual de um site no WordPress](https://intl.cloud.tencent.com/document/product/213/8044)


