Este documento descreve como migrar sem interrupções o seu serviço do CLB da rede pública da rede clássica para uma VPC.
>? Este exemplo é apenas para referência. Na migração real, avalie cuidadosamente o impacto e elabore o plano de migração com antecedência.

### Cenário
Configuração de recursos de negócios baseados na rede clássica: 
+ O nome de domínio DNS é resolvido para o VIP do CLB da rede pública na rede clássica.
+ O CLB da rede pública está vinculado à duas CVMs (CVM 1 e CVM 2) como servidores de back-end.
+ As aplicações implantadas na CVM 1 e na CVM 2 podem acessar os serviços de back-end do TencentDB for Redis e do TencentDB for MySQL.


### Processo de migração
<dx-steps>
- Criar uma VPC
- Migrar os serviços do TencentDB
- Criar instâncias da CVM e implantar aplicações
- Criar um CLB da rede pública e associá-lo às CVMs
- Alterar o endereço IP do nome de domínio DNS
- Liberar os recursos da rede clássica
</dx-steps>

### Instruções para a migração
1.  Crie uma VPC conforme instruído em [Criação de VPCs](https://intl.cloud.tencent.com/document/product/215/31805).
![]()
2.  Migre as instâncias do [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/31915) e do [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/31944) para a VPC.
>? Durante a migração, as instâncias do TencentDB ainda permanecem conectadas. Tanto o IP original da rede clássica quanto os endereços IP da VPC permanecem válidos por um determinado período após a migração, mantendo assim a disponibilidade do serviço. Conclua a migração dos demais recursos dentro desse período.
>
![]()
3.  Crie imagens para a CVM 1 e a CVM 2 baseadas na rede clássica conforme instruído em [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942) e [use as imagens](https://intl.cloud.tencent.com/document/product/213/36304) para criar duas instâncias da CVM na VPC. Depois, teste se as CVMs conseguem acessar as instâncias do TencentDB.
 >? Se a reinicialização das instâncias da CVM durante a migração for aceitável para os seus negócios, você poderá alternar diretamente para a VPC fora do horário de pico. Para obter instruções detalhadas, consulte [Alternância para a VPC](https://intl.cloud.tencent.com/document/product/213/20278).
 >
![]()
4.  Crie um CLB da rede pública na VPC, e associe-a às duas CVMs criadas na etapa anterior. Para mais informações, consulte [Introdução ao CLB](https://intl.cloud.tencent.com/document/product/214/8975). Execute uma verificação de integridade para evitar a interrupção do serviço devido a uma exceção.
![]()
5.  Resolva o nome de domínio DNS para o VIP do CLB da rede pública na VPC.
![]()
6.  Verifique se a VPC está funcionando corretamente. Se estiver, libere os recursos originais do CLB e da CVM da rede pública na rede clássica para concluir a migração.
 >? O IP original da rede clássica de uma instância do TencentDB será liberado automaticamente após a expiração.
 >
![]()
