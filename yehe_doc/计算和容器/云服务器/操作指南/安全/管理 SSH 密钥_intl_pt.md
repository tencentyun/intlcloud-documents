## Visão geral
Este documento descreve as operações comuns relacionadas ao uso do par de chaves SSH para fazer login em uma instância. Por exemplo, é possível criar, vincular, desvincular, modificar ou excluir um par de chaves SSH.
>!Para vincular uma chave SSH ou desvinculá-la de uma instância, desligue a instância primeiro. Consulte [Desligar instâncias](https://intl.cloud.tencent.com/document/product/213/4929).
>

## Instruções

<span id="creatSSH"></span>
### Criação de uma chave SSH
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Clique em **[SSH Key (Chave SSH)](https://console.cloud.tencent.com/cvm/sshkey)** na barra lateral esquerda.
 3. Clique em **New (Nova)** na página **SSH Key (Chave SSH)**.
>! Depois de clicar em **OK**, a chave privada será baixada automaticamente. O Tencent Cloud não reterá a sua chave privada. Certifique-se de mantê-la segura.
 > 
![](https://main.qcloudimg.com/raw/a6675ade459e6bf236ff7301995a35f2.png)
  - Se você selecionar **Create a new key pair (Criar um novo par de chaves)**, insira o nome da chave.
  - Se você selecionar **Use an existing public key (Usar uma chave pública existente)**, insira o nome da chave e as informações da chave pública original.


<span id="bindingSSH"></span>
### Vinculação de uma chave a uma instância
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Clique em **[SSH Key (Chave SSH)](https://console.cloud.tencent.com/cvm/sshkey)** na barra lateral esquerda.
 3. Na página de gerenciamento de chaves SSH, selecione a chave SSH de destino e clique em **Bind with instances (Vincular às instâncias)**.
![](https://main.qcloudimg.com/raw/7419df720863aa9463e0dcf478580bbd.png)
 4. Na janela pop-up, selecione a região de destino e as instâncias e clique em **Bind (Vincular)**.


### Desvinculação de uma chave da instância
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Clique em **[SSH Key (Chave SSH)](https://console.cloud.tencent.com/cvm/sshkey)** na barra lateral esquerda.
 3. Na página de gerenciamento de chaves SSH, selecione a chave SSH de destino e clique em **Unbind from instances (Desvincular das instâncias)**.
![](https://main.qcloudimg.com/raw/263f344c4bea3cdff4e422996821cb5d.png)
 4. Na janela pop-up, selecione a região e as instâncias para desvincular da chave e clique em **Unbind (Desvincular)**.


### Modificação do nome ou da descrição da chave SSH
 1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
 2. Clique em **[SSH Key (Chave SSH)](https://console.cloud.tencent.com/cvm/sshkey)** na barra lateral esquerda.
 3. Na página de gerenciamento de chaves SSH, selecione a chave a ser modificada e clique em <img  style="margin:-3px 0px" src="https://main.qcloudimg.com/raw/9db81482f9242417d94a04f314b42b19.png"/> ao lado do nome da chave, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/e4c46354bafa78daa7efa24064eafea9.png)
 4. Na janela pop-up, insira o novo nome ou a nova descrição da chave e clique em **OK**.

### Exclusão de chaves SSH
>! Não é possível excluir uma chave SSH quando está vinculada a instâncias do CVM ou imagens personalizadas.
>
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/).
2. Clique em **[SSH Key (Chave SSH)](https://console.cloud.tencent.com/cvm/sshkey)** na barra lateral esquerda. É possível excluir uma ou várias chaves SSH conforme necessário.
 - **Exclusão de uma única chave**
    1. Na página de gerenciamento de chaves SSH, selecione a chave SSH a ser excluída e clique em **Delete (Excluir)** na coluna **Operation (Operação)**, conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/96d57d5beb3d73c0978cc1464bc73c7e.png)
    2. Na janela pop-up, clique em **OK**.
 - **Exclusão de chaves em lote**
    1. Na página de gerenciamento de chaves SSH, selecione as chaves SSH a serem excluídas e clique em **Delete (Excluir)** acima da lista para excluí-las em lote.
    2. Na janela pop-up, clique em **OK**, conforme mostrado abaixo.
    Apenas as que podem ser excluídas dos pares de chaves selecionados serão excluídas.
		![](https://main.qcloudimg.com/raw/bfcdfb401f8906834b02372d3e50dbe0.png)


### Uso de uma chave SSH para fazer login em um CVM do Linux

1. [Criação de uma chave SSH](#creatSSH).
2. [Vinculação de uma chave SSH a uma instância do CVM](#bindingSSH).
3. [Login em uma instância do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
