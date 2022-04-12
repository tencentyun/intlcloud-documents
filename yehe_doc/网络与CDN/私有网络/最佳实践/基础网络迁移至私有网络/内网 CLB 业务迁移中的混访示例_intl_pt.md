Este documento fornece uma configuração de exemplo para o cenário em que a VPC e a rede clássica são necessárias durante a migração de negócios.


### Cenário
Configuração de recursos de negócios baseados na rede clássica:
+ O cliente da CVM acessa um CLB da rede privada.
+ O CLB da rede privada está vinculado às duas CVMs (CVM 1 e CVM 2) como servidores reais.
+ As aplicações implantadas na CVM 1 e na CVM 2 podem acessar os serviços de back-end do TencentDB for MySQL.

Solicitações:
+ Migra os recursos da rede clássica para uma VPC
+ Os clientes baseados na VPC têm acesso prioritário ao serviço do CLB da rede privada na rede clássica.
+ O acesso à rede clássica permanece disponível por um mês após a migração.

### Processo de migração
<dx-steps>
- Criar uma VPC
- Migrar os serviços do TencentDB
- Configurar uma conexão de terminal
- Criar um CLB da rede privada e configurar seu serviço de back-end
- Configurar um Classiclink
- Liberar os recursos da rede clássica
</dx-steps>


### Etapas
1.  Crie uma VPC conforme instruído em [Criação de VPCs](https://intl.cloud.tencent.com/document/product/215/31805).
2.  Migre os serviços do TencentDB for MySQL para a VPC conforme instruído em [Alternância de rede](https://intl.cloud.tencent.com/document/product/236/31915).
    >? Durante a migração, as instâncias do TencentDB ainda permanecem conectadas. Tanto o IP original da rede clássica quanto os endereços IP da VPC permanecem válidos após a migração, mantendo assim a disponibilidade do serviço.
    >
    ![]()
3.  Configure um serviço de conexão de terminal para permitir que o cliente da CVM na VPC acesse o serviço do CLB da rede pública na rede clássica.
     ![]()
4.  Crie uma instância do CLB da rede privada e seu servidor real na VPC, e configure os serviços relacionados.
   ![]()
5.  Configure um Classiclink para permitir que a CVM baseado na rede clássica acesse a instância do CLB da rede privada na VPC. Teste se a VPC está fornecendo serviços normalmente.
    ![]()
6.  Após o serviço da VPC estiver normal, e a CVM baseada na VPC começar a acessar o CLB da rede privada na VPC, exclua a conexão de terminal, mantenha o Classiclink e libere os recursos na rede clássica.
    ![]()

