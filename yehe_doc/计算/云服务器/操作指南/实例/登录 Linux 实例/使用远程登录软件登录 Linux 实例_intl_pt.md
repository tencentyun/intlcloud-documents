## Visão geral

Este documento usa o PuTTY como um exemplo para descrever como fazer login em uma instância do Linux a partir do Windows usando o software de login remoto.


## Sistema operacional aplicável

Windows

## Método de autenticação

**Senha** ou **Chave**

## Pré-requisitos
- Você já deve ter a conta de administrador e a senha (ou chave) para fazer login na instância.
 - Se você usar uma senha padrão do sistema para fazer login na instância, vá primeiro para [Centro de mensagens](https://console.cloud.tencent.com/message) para obtê-la.
 - Se você esqueceu sua senha, [redefina sua senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Um IP público foi adquirido e obtido para sua instância do CVM e a porta 22 está aberta. (Ela fica aberta por padrão para o CVM adquirido com a configuração rápida).


## Direções
<dx-tabs>
::: Logging\sin\swith\sa\spassword[](id:passwordLogin)
1. Baixe o software de login remoto do Windows, PuTTY.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">Clique aqui para baixar o PuTTY</a></div>
2. Clique duas vezes em **putty.exe** para abrir o cliente do PuTTY.
3. Na janela **PuTTY Configuration (Configuração do PuTTY)**, insira o seguinte conteúdo, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
Configure os parâmetros da seguinte forma:
 - **Host Name (or IP address) (Nome do host (ou endereço IP))**: o IP público do CVM. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index) para obter o IP público da lista de instâncias e das páginas de detalhes.
 - **Port (Porta)**: a porta do CVM, que deve ser “22”.
 - **Connection type (Tipo de conexão)**: selecione **SSH**.
 - **Saved Sessions (Sessões salvas)**: insira o nome da sessão, como `test`.
 Depois de configurar o **Host Name (Nome do host)**, configure e salve as **Saved Sessions (Sessões salvas)**. Você pode clicar duas vezes no nome da sessão salva em **Saved Sessions (Sessões salvas)** para fazer login no CVM.
4. Clique em **Open (Abrir)** para entrar na interface do **PuTTY**. O prompt de comando **login as: (login como:)** é exibido.
5. Digite o nome de usuário após **login as: (login como:)** e pressione **Enter**.
6. Digite a senha após **Password (Senha)** e pressione **Enter**.
A senha inserida não é exibida por padrão, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
Uma vez conectado, você pode ver as informações sobre o CVM ao qual você está conectado no momento à esquerda do prompt de comando.
:::
::: Logging\sin\swith\sa\skey[](id:keyLogin)
1. Baixe o software de login remoto do Windows, PuTTY. O putty.exe e o puttygen.exe são obrigatórios.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe" target="_blank" style="color: white; font-size:16px;">Baixar PuTTY</a></div><div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;margin:5px;"><a href="https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe" target="_blank" style="color: white; font-size:16px;">Baixar PuTTYgen</a></div>
2. Clique duas vezes em **puttygen.exe** para abrir o cliente da chave do PuTTY.
3. Clique em **Load (Carregar)**, selecione e acesse o caminho onde a chave privada baixada foi salva. Você deve baixar e manter sua chave privada depois de criar um par de chaves. Para obter mais informações, consulte [Gerenciamento de chaves SSH](https://intl.cloud.tencent.com/document/product/213/16691)
Por exemplo, selecione e abra o arquivo de chave privada `david`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>Na janela **PuTTY Key Generator (Gerador de chaves PuTTY)**, insira o nome da chave e a senha da chave privada criptografada (opcional) e clique em **Save private key (Salvar chave privada)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. Na janela pop-up, selecione o caminho onde a chave será salva. No campo **File name (Nome do arquivo)**, digite “Key Name.ppk” e clique em **Save (Salvar)**. Por exemplo, salve o arquivo de chave privada `david` como `david.ppk`, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/fad925e85923ac1d41afacde4a9c690c.png)
6. Clique duas vezes em **putty.exe** para abrir o cliente do PuTTY.
7. Na barra lateral esquerda, vá para **Connection (Conexão)** > **SSH** > **Auth (Autenticação)** e entre na interface de configuração da **Auth (Autenticação)**.
8. Clique em **Browse (Pesquisar)**, selecione e acesse o caminho onde a chave foi salva, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
9. Mude para a interface de configuração da **Session (Sessão)**. Configure o IP, a porta e o tipo de conexão do CVM, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - **Host Name (or IP address) (Nome do host (ou endereço IP))**: o IP público do CVM. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm/index) para obter o IP público da lista de instâncias e das páginas de detalhes.
 - **Port (Porta)**: a porta do CVM, que deve ser “22”.
 - **Connection type (Tipo de conexão)**: selecione **SSH**.
 - **Saved Sessions (Sessões salvas)**: insira o nome da sessão, como `test`.
 Depois de configurar o **Host Name (Nome do host)**, configure e salve as **Saved Sessions (Sessões salvas)**. Você pode clicar duas vezes no nome da sessão salva em **Saved Sessions (Sessões salvas)** para fazer login no CVM.
9. Clique em **Open (Abrir)** para entrar na interface do **PuTTY**. O prompt de comando **login as: (login como:)** é exibido.
10. Digite o nome de usuário após **login as: (login como:)** e pressione **Enter**.
11. Digite a senha configurada na [Etapa 4](#Step4) depois de **Passphrase for key "imported-openssh-key": (Frase secreta para chave "imported-openssh-key":)** e pressione **Enter**.
A senha inserida não é exibida por padrão, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
Uma vez conectado, você pode ver as informações sobre o CVM ao qual você está conectado no momento à esquerda do prompt de comando.
:::
</dx-tabs>

## Operações subsequentes

Depois de fazer o login no CVM, você pode criar um site pessoal ou fórum ou realizar outras operações. Para obter mais informações, consulte:
- [Configuração do WordPress](https://intl.cloud.tencent.com/document/product/213/33469)
- [Criação de fórum no Discuz!](https://intl.cloud.tencent.com/document/product/213/34278)

