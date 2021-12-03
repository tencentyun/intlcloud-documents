Este documento descreve como modificar o nome, o endereço DNS, o nome de domínio, a tag ou outras informações de um VPC.

## Informações gerais
O protocolo DHCP (Dynamic Host Configuration Protocol) é um protocolo de rede local que define o padrão da transferência de informações de configuração para servidores de rede TCP/IP. 
Os CVMs em um VPC do Tencent Cloud são compatíveis com o DHCP. As opções configuráveis do DHCP incluem o endereço DNS e o nome de domínio. Essas configurações entrarão em vigor em todos os CVMs no VPC.

>?
> - Por enquanto, os VPCs criados antes de 1º de abril de 2018 não são compatíveis com as funcionalidades do DHCP. Se você não conseguir modificar o endereço DNS e o nome de domínio no console, significa que seu VPC não é compatível com essas funcionalidades.
> - As novas configurações entrarão em vigor em todos os CVMs no VPC.
> - Para os CVMs recém-criados, as configurações modificadas entram em vigor imediatamente.
> - Para os CVMs existentes, as configurações modificadas entram em vigor após os CVMs ou os serviços de rede serem reiniciados.

## Instruções
1. Faça login no [Console do VPC](https://console.cloud.tencent.com/vpc).
2. Selecione a região do VPC na parte superior da página **VPC**.
3. Clique no ícone de edição ao lado de um nome de VPC para modificá-lo.
![](https://main.qcloudimg.com/raw/a0f96b51068c3c081fbcbd7abb586911.png)
4. Clique no ID do VPC para acessar a página **Basic Information (Informações básicas)**.
5. Clique no ícone de edição para modificar o DNS, o nome de domínio e a tag, respectivamente.
   + DNS: endereços do servidor DNS
     + O DNS padrão do Tencent Cloud é `183.60.83.19` e `183.60.82.98`. Se o DNS padrão não for usado, os serviços internos como a ativação do Windows, o NTP e o YUM não estarão disponíveis.
     + O DNS aceita no máximo quatro endereços IP. Separe os IPs com vírgulas.
     + Embora quatro IPs possam ser especificados para o DNS, alguns sistemas operacionais podem não conseguir aceitar quatro endereços DNS.
   + Nome de domínio: sufixo do nome do host do CVM, como `exemplo.com`. Você pode inserir até 60 caracteres ou manter a configuração padrão se não tiver requisitos especiais.
   + Tag: usada para identificar e gerenciar os recursos. Opcionalmente, você pode adicionar tags ou excluí-las.
![](https://main.qcloudimg.com/raw/50129c5b14c7c6d5923263719eec5bd2.png)
