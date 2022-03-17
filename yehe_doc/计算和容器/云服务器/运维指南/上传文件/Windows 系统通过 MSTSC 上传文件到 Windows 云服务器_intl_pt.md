## Cenário

O método comum para upload de arquivo para o CVM do Windows é usar o Cliente dos serviços de terminal da Microsoft. Este documento descreve como fazer upload de arquivos para o CVM do Windows usando a conexão de área de trabalho remota em um computador Windows local.

## Pré-requisitos

Certifique-se de que o CVM do Windows pode acessar a rede pública.

## Instruções
> O exemplo a seguir usa o computador local com sistema operacional Windows 7. As etapas específicas podem variar de acordo com os sistemas operacionais.
>
### Obtenção de um IP público
Faça login no [Console do CVM](https://console.cloud.tencent.com/cvm/index). Na página da lista de instâncias, registre o IP público do CVM para o qual deseja fazer upload dos arquivos.

### Upload de arquivo
1. Use a tecla de atalho **Windows + R** no computador local para abrir a janela **Run (Executar)**.
2. Na janela pop-up **Run (Executar)**, digite **mstsc** e clique em **OK** para abrir a caixa **Remote Desktop Connection (Conexão de área de trabalho remota)**.
3. Na caixa **Remote Desktop Connection (Conexão de área de trabalho remota)**, digite o endereço IP público do CVM e clique em **Show Options (Mostrar opções)**.
4. Na guia **General (Geral)**, insira o endereço IP da rede pública do CVM e o nome de usuário do administrador.
5. Selecione a guia **Local Resources (Recursos locais)** e clique em **More (Mais)**.
6. Na janela pop-up **Local devices and resources (Dispositivos e recursos locais)**, selecione o módulo **Drives (Unidades)**, verifique os discos locais onde os arquivos a serem carregados no CVM do Windows estão localizados e clique em **OK**.
7. Após a configuração local for concluída, clique em **Connect (Conectar)** para fazer login no CVM do Windows remotamente.
8. Clique em **Start (Iniciar)** > **Computer (Computador)** no CVM do Windows e você poderá ver os discos locais montados no CVM.
9. Clique duas vezes para abrir os discos locais montados e copie os arquivos locais para outros discos rígidos do CVM do Windows para concluir o upload dos arquivos.
Por exemplo, copie o arquivo A do disco local (E) para o disco C do CVM do Windows.

### Download de um arquivo
Para baixar arquivos do CVM do Windows para o computador local, consulte as operações de upload de arquivo acima e copie os arquivos necessários do CVM do Windows para os discos locais montados para concluir o download dos arquivos.
