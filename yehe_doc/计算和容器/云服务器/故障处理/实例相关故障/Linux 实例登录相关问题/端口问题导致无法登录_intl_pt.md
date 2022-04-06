Este documento descreve como diagnosticar e solucionar falhas de login remoto causadas por problemas de porta.
>?As operações a seguir usam uma instância do CVM com o sistema operacional CentOS 7.8 como exemplo.
>

## Ferramentas
Você pode usar as seguintes ferramentas para verificar se os problemas de login estão relacionados à configuração de portas ou de grupos de segurança:
- [Autodiagnóstico](https://console.cloud.tencent.com/workorder/check)
- [Verificação de portas](https://console.cloud.tencent.com/vpc/helper)

Se o problema for realmente causado por configurações de grupos de segurança, clique em **Open all ports (Abrir todas as portas)** em [Verificação de portas](https://console.cloud.tencent.com/vpc/helper) e tente fazer login novamente. Se você ainda não conseguir fazer login após abrir as portas, consulte o guia de solução de problemas abaixo.

## Solução de problemas
### Verificação da conectividade de rede
Você pode usar o comando `Ping` para testar a conectividade de rede do seu PC. Você deve executar o teste em computadores em diferentes ambientes de rede (como diferentes intervalos de IP ou ISPs) para verificar se é um problema de rede local ou de servidor.
1. Abra a ferramenta de linha de comando em seu computador local.
	- **Windows**: clique em **Start (Iniciar)** > **Run (Executar)** e insira `cmd`. Uma janela de prompt de comando será exibida.
	- **MacOS**: abra uma janela do Terminal.
2. Execute o comando a seguir para testar a conexão de rede.
```
ping [CVM instance’s public IP address]
```
Primeiro, você deve [obter o endereço IP público](https://intl.cloud.tencent.com/document/product/213/17940) da instância do CVM. Por exemplo, `ping 81.71.XXX.XXX`.
 - Se um resultado semelhante ao seguinte for retornado, sua conexão de rede com a instância do CVM está normal.
![](https://main.qcloudimg.com/raw/796dd285720755d7b5dc9e0bee492c83.png)
 - Se a mensagem **Request Timeout (Tempo limite da solicitação)** for exibida, a conexão entre a rede e a instância do CVM não está funcionando corretamente. Nesse caso, consulte [Falha no ping do endereço IP da instância](https://intl.cloud.tencent.com/document/product/213/14639) para mais alternativas de solução de problemas.

### Verificação da conectividade de porta
1. [Faça login em uma instância do Linux pelo VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Execute o comando a seguir e pressione **Enter** para verificar se a porta remota está aberta e acessível.
```
telnet [CVM instance’s public IP address] [Port number]
```
Por exemplo, execute o comando `telnet 119.XX.XXX.67 22` para verificar se a porta 22 está aberta.
 - Se forem retornadas informações semelhantes às mostradas abaixo, a porta 22 está acessível.
![](https://main.qcloudimg.com/raw/246134de6829323457dc1d51f85589b8.png)
 - Se forem retornadas informações semelhantes às mostradas abaixo, a porta 22 está inacessível. Verifique a configuração de rede correspondente. Por exemplo, verifique se a porta 22 está aberta no firewall ou no grupo de segurança da instância.
 ![](https://main.qcloudimg.com/raw/d6eadfe7638046f0b0c1f15261ea74ab.png)


### Verificação do serviço SSHD
Se você não conseguir [fazer login em uma instância do Linux pela chave SSH](https://intl.cloud.tencent.com/document/product/213/32501) devido a falhas de conexão, pode ser porque a porta SSHD não está sendo escutada ou o serviço SSHD não foi iniciado. Nesse caso, consulte [Não é possível fazer login em uma instância do Linux via SSH](https://intl.cloud.tencent.com/document/product/213/32486) para mais instruções de solução de problemas.
