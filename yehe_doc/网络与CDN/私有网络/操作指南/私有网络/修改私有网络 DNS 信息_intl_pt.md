As CVMs em uma VPC da Tencent Cloud são compatíveis com o DHCP. As opções configuráveis do DHCP incluem o endereço DNS e o nome de domínio. Este documento descreve como modificar o endereço DNS e o nome de domínio de uma VPC.
>?
>+ O protocolo DHCP (Dynamic Host Configuration Protocol) é um protocolo de rede local que define o padrão da transferência de informações de configuração para servidores de rede TCP/IP. 
>+ Por enquanto, as VPCs criadas antes de 1º de abril de 2018 não são compatíveis com as funcionalidades do DHCP. Se você não conseguir modificar o endereço DNS e o nome de domínio no console, significa que seu VPC não é compatível com essas funcionalidades.

## Observações
As novas configurações entrarão em vigor em todos as CVMs na VPC.
 + Para as CVMs recém-criadas, as configurações modificadas entram em vigor imediatamente.
 + Para as CVMs existentes, as configurações modificadas entram em vigor após as CVMs ou os serviços de rede serem reiniciados.

## Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região da VPC na parte superior da página **VPC**.
3. Clique no ID da VPC para acessar a página **Basic Information (Informações básicas)**.
4. Clique no ícone de edição para modificar o DNS e o nome de domínio, respectivamente.
   + DNS: endereços do servidor DNS
     >?
     >+ O DNS padrão da Tencent Cloud é “183.60.83.19” e “183.60.82.98”. Se o DNS padrão não for usado, os serviços internos como a ativação do Windows, o NTP e o YUM não estarão disponíveis.
     >+ O DNS aceita no máximo quatro endereços IP. Separe os IPs com vírgulas. Observe que alguns sistemas operacionais podem não aceitar quatro endereços DNS.
   + Nome de domínio: sufixo do nome do host da CVM, como “exemplo.com”. Você pode inserir até 60 caracteres ou manter a configuração padrão se não tiver requisitos especiais.
    ![](https://main.qcloudimg.com/raw/50129c5b14c7c6d5923263719eec5bd2.png)
