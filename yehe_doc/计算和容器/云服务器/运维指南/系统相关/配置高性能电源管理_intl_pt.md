## Visão geral

O gerenciamento de energia de alto desempenho é necessário para que o sistema operacional (SO) Windows Server permita o desligamento normal de instâncias do CVM. Caso contrário, você só pode desligar à força as instâncias do CVM no console do CVM. Este documento usa o Windows Server 2012 como exemplo para descrever como configurar o gerenciamento de energia.

## Observações

Para modificar o gerenciamento de energia, não é necessário reiniciar o computador.

### Instruções

1. Faça login em uma instância do Windows usando [o arquivo RDP (recomendado)](https://intl.cloud.tencent.com/document/product/213/5435) ou [a área de trabalho remota](https://intl.cloud.tencent.com/document/product/213/32498).
2. Abra o Internet Explorer no CVM do Windows, acesse a rede privada do Tencent Cloud e baixe a ferramenta de modificação e configuração de energia do Tencent Cloud.
O endereço de download é `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`.
Por exemplo, baixe a ferramenta de configuração e modificação de energia do Tencent Cloud (power-set-win.bat) na unidade C:.
3. Use a ferramenta de linha de comando (CMD) como administrador para abrir power-set-win.bat, conforme mostrado na seguinte figura:
![](https://main.qcloudimg.com/raw/22f81122e1188fc83ed4b1100a7469bc.png)
4. Execute o seguinte comando para exibir o plano de gerenciamento de energia atual:
```
powercfg -L
```
O resultado retornado é o seguinte:
 ![](https://main.qcloudimg.com/raw/54ceb4faddc8745b30556621268ac318.png)

4. Na área de trabalho do sistema operacional, clique em <img src = "https://main.qcloudimg.com/raw/87d894e564b7e83 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Control Panel (Painel de controle)** > **System and Security (Sistema e segurança)** > **Power Options (Opções de energia)**.
5. Na janela **Power Options (Opções de energia)**, clique em **Change plan settings (Alterar configurações do plano)**, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/54183c1f9d914789b986781b8a4da6ec.png)
6. Na janela **Edit Plan Settings (Editar configurações do plano)**, modifique os tempos de desligamento por inatividade do monitor e do disco, conforme mostrado abaixo:
 ![](https://main.qcloudimg.com/raw/f0b7f447d90fe50ef829a10dab0029c6.png)

