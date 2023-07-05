## Casos de uso
Quando você deseja acessar a internet por meio de um EIP, pode escolher o modo NAT ou o modo de conexão direta. O modo padrão é o NAT.
- No modo NAT, o EIP fica invisível na máquina local.
- No modo de conexão direta, o EIP fica visível na máquina local. Não é necessário adicionar manualmente um endereço EIP para cada configuração, o que pode minimizar o custo de desenvolvimento.
- O modo NAT pode atender à maioria dos requisitos. No entanto, se você deseja verificar o IP público no CVM, é necessário usar o modo de conexão direta com o EIP.

## Limites de uso
- No momento, a conexão direta com o EIP está em teste beta e disponível apenas para usuários autorizados. Só é compatível com dispositivos em um VPC. É possível [enviar um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar essa funcionalidade.
- Um NAT Gateway pode ser vinculado a EIPs habilitados com conexão direta, mas a conexão direta não pode ser implementada.
- No CVM, a conexão direta com o EIP não pode entrar em vigor ao mesmo tempo que um NAT Gateway. Se a tabela de roteamento associada à sub-rede em que seu CVM está localizado estiver configurada com uma política de roteamento de acesso à rede pública por meio do NAT Gateway, a conexão direta não pode ser implementada por meio do EIP no CVM. É possível permitir que o CVM acesse a rede pública por meio do seu EIP [ajustando as prioridades dos NAT Gateways e EIPs](https://intl.cloud.tencent.com/document/product/1015/32734). Nesse caso, a conexão direta com o EIP pode ser implementada.

## Instruções
Para usar a conexão direta com o EIP, é necessário habilitá-la no console e adicionar o IP ao ENI no sistema operacional. Também é necessário configurar o roteamento no sistema operacional com base em seu aplicativo. Portanto, fornecemos um script para configurar o IP de forma que o tráfego da rede privada passe pelo IP privado e o tráfego da rede pública passe pelo IP público.
>Para outros aplicativos, configure o roteamento de acordo.
>
### Configuração da conexão direta com o EIP no CVM do Linux
>
>- O script para Linux é compatível com o CentOS 6 e posterior e com o Ubuntu.
>- O script para Linux é compatível apenas com o ENI principal (eth0) e não é compatível com o ENI secundário.
>- Se o IP público vinculado ao ENI principal não for um EIP, será necessário converter o IP público em um EIP. Para obter mais informações, consulte [Conversão do IP público para EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Cenário
O script para Linux é aplicável ao seguinte cenário: tanto o IP privado quanto o IP público estão vinculados ao ENI principal (eth0), em que o endereço da rede pública é acessado pelo IP público e o endereço da rede privada é acessado pelo IP privado.

#### Etapa 1: baixe o script para a conexão direta com o EIP
A conexão direta com o EIP pode causar a interrupção da rede. Portanto, é necessário baixar o script para a conexão direta com o EIP e carregá-lo no CVM com antecedência. É possível obter o script usando um dos seguintes métodos:
- **Método 1: carregue o script para a conexão direta com o EIP**
 (1) Baixe o script de configuração para a conexão direta com o EIP em Download Script for Linux (Baixar o script para Linux)
 (2) Depois de baixar o script para Linux na máquina local, carregue-o no CVM que requer conexão direta com o EIP.
- **Método 2: use um comando diretamente**
Faça login no CVM e execute o seguinte comando no CVM para baixar o script:
```
wget https://network-data-1255486055.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

#### Etapa 2: execute o script para a conexão direta com o EIP
1. Faça login no CVM que requer a conexão direta com o EIP.
2. Execute o script para a conexão direta com o EIP da seguinte forma:
 (1) Execute o seguinte comando para adicionar a permissão de execução:
```
chmod +x eip_direct.sh
```
 (2) Execute o seguinte comando para executar o script:
```
./eip_direct.sh install XX.XX.XX.XX
```
Aqui, XX.XX.XX.XX indica o endereço EIP (opcional). É possível deixá-lo em branco e executar `./eip_direct.sh install` diretamente.

#### Etapa 3: habilite a conexão direta com o EIP
1. Faça login no [Console do EIP](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Encontre o EIP de destino e selecione **More (Mais)** -> **Direct connection (Conexão direta)** na coluna **Operation (Operação)** à direita.


### Configuração da conexão direta com o EIP no CVM do Windows
>
>- Para usar a conexão direta com o EIP no Windows, é necessário um ENI para o IP privado e outro para o IP público, e vincular o IP público ao ENI principal e o IP privado ao ENI secundário.
>- Durante a configuração da conexão direta com o EIP no Windows, a conexão com a internet pode ser interrompida. Portanto, recomendamos que você [faça login em uma instância do Windows pelo VNC](https://intl.cloud.tencent.com/document/product/213/32496).
- Se o IP público vinculado ao ENI principal não for um EIP, será necessário convertê-lo em um EIP. Para obter mais informações, consulte [Conversão do IP público para EIP](https://intl.cloud.tencent.com/document/product/213/16586#converting-public-ip-to-eip).

#### Cenários
O script para Windows é aplicável ao seguinte cenário: O tráfego da rede pública passa pelo ENI principal e o tráfego da rede privada passa pelo ENI secundário.

#### Etapa 1: baixe o script para a conexão direta com o EIP<span id="step1" />
Durante a configuração da conexão direta com o EIP, a conexão com a internet será interrompida. Portanto, é necessário baixar o script para a conexão direta com o EIP e carregá-lo no CVM com antecedência.
Abra o seguinte link no navegador do CVM para baixar o script para conexão direta com o EIP:
```
https://windows-1254277469.cos.ap-guangzhou.myqcloud.com/eip_windows_direct.bat
```

#### Etapa 2: configure o ENI secundário
1. Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/overview).
2. Na página **Instances (Instâncias)**, clique no ID do CVM configurado para ir para a página **Basic Information (Informações básicas)**.
3. Selecione a guia **ENI** e clique em **Bind ENI (Vincular ENI)** para criar um ENI que esteja na mesma sub-rede do principal.
![](https://main.qcloudimg.com/raw/2da530f15e824ff99858f08397687cf6.png)
4. Na janela pop-up, selecione **Create and Bind an ENI (Criar e vincular um ENI)**, insira as informações, selecione **Automatic Assignment (Atribuição automática)** na seção **Assign IP (Atribuir IP)** e clique em **OK**.
![](https://main.qcloudimg.com/raw/cb6fe49d3bbefd792355ade6e62f29f3.png)

#### Etapa 3: configure a conexão direta com o EIP para o ENI principal
1. Faça login no [Console do EIP](https://console.cloud.tencent.com/cvm/eip?rid=1).
2. Encontre o EIP que está vinculado ao ENI principal e selecione **More (Mais)** -> **Direct Connection (Conexão direta)** na coluna **Operation (Operação)** à direita.

#### Etapa 4: configure o IP no CVM
1. Faça login no CVM. Esta operação pode causar a interrupção da rede pública. Portanto, é necessário [fazer login em uma instância do Windows pelo VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Na página do sistema operacional, selecione <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width:25px"> no canto inferior esquerdo e clique em <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: -3px 0px;"> para abrir a janela **Windows PowerShell (PowerShell do Windows)**. Insira `firewall.cpl` e pressione Enter para abrir a página **Windows Firewall (Firewall do Windows)**.
3. Clique em **Turn Windows Firewall on or off (Ativar ou desativar o Firewall do Windows)** para ir para a página **Customize Settings (Personalizar configurações)**.
![](https://main.qcloudimg.com/raw/e6d6a44be911ec5f60a6205b6f47a2c7.png)
4. Selecione **Turn off Windows Firewall (Desativar o Firewall do Windows)** no painel **Private network settings (Configurações da rede privada)** e no painel **Public network settings (Configurações da rede pública)**.
![](https://main.qcloudimg.com/raw/cdb7703dec781e98101f7f3fd7ecf71f.png)
5. Clique duas vezes para executar o script baixado na [Etapa 1](#step1). Insira o endereço IP público e pressione Enter duas vezes.
6. Insira `ipconfig` na janela **Windows PowerShell (PowerShell do Windows)** e pressione Enter. É possível observar que o endereço IPv4 no ENI principal muda para o endereço da rede pública.

>Quando a conexão direta está habilitada, não é possível atribuir um IP privado ao ENI principal. Caso contrário, o CVM não consegue acessar a rede pública.
