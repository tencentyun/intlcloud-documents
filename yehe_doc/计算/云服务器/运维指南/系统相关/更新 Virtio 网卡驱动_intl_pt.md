## Visão geral

Os CVMs do Windows Server 2008 R2 Enterprise SP1 e do Windows Server 2012 R2 do Tencent Cloud usam os drivers ENI Virtio para otimizar o desempenho da rede do hardware de virtualização. O Tencent Cloud continuará aprimorando os ENIs para um melhor desempenho e fácil solução de problemas. Este documento descreve como atualizar o driver ENI Virtio e verificar a sua versão.

## Pré-requisitos

Você fez login em um CVM do Tencent Cloud.

## Instruções

### Exibição das informações da versão do sistema

Realize as etapas a seguir para exibir a versão do sistema.
1. Faça login em um CVM e acesse a janela **System (Sistema)** de acordo com o sistema operacional:
 - **Window Server 2008 R2 Enterprise SP1**: clique com o botão direito do mouse em **This PC (Esse computador)** > **Properties (Propriedades)** na área de trabalho.
 - **Windows Server 2012 R2**: abra o **Control Panel (Painel de controle)** e selecione **System (Sistema)**.
2. Na seção **View basic information about your computer (Exibir informações básicas sobre o computador)**, você pode exibir as informações da versão do sistema.   

### Atualização do driver ENI Virtio
>! O CVM será desconectado brevemente durante a atualização. Certifique-se de que essa operação não afetará seu serviço antes de continuar. O CVM precisa ser reiniciado após a atualização.
>
1. Abra o navegador e digite o endereço a seguir para baixar o instalador do driver ENI Virtio para o Window Server 2008 R2 e o Windows Server 2012 R2. 
Escolha o endereço de download com base no ambiente de rede:
 - Endereço de download da rede pública: `http://mirrors.tencent.com/install/windows/virtio_64_10003.msi`
 - Endereço de download da rede privada: `http://mirrors.tencentyun.com/install/windows/virtio_64_10003.msi`
2. Após a conclusão do download, clique duas vezes no instalador, escolha o modo de instalação **Classic (Clássico)** e clique em **Next (Avançar)**.
3. Na janela pop-up Windows Security (Segurança do Windows), marque **Always trust the software from Tencent Technology (Shenzhen) Company Limited (Sempre confiar no software da Tencent Technology (Shenzhen) Company Limited)** e clique em **Install (Instalar)**. 
Durante o processo de instalação, escolha **Install this driver software anyway (Instalar este software de driver mesmo assim)** quando solicitado.      
4. Reinicie o computador conforme solicitado.


### Verificação da versão do driver

1. Clique em <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"  style="margin:0;">, digite **ncpa.cpl** na caixa Run (Execução), e pressione **Enter**.
2. Na janela **Network Connection (Conexão de rede)**, clique com o botão direito do mouse no ícone "Ethernet" e selecione **Properties (Propriedades)**.
3. Na janela **Ethernet Properties (Propriedades da Ethernet)**, clique em **Configure (Configurar)**.
4. Na janela **Tencent Virtio Ethernet Adapter Properties (Propriedades do adaptador de Ethernet Virtio da Tencent)**, selecione a guia **Driver** para exibir a versão atual do driver.


