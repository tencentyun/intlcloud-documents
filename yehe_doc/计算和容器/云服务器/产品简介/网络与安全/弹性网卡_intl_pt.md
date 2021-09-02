[Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/product/eni?from_cn_redirect=1) é uma interface elástica para acesso à rede, que vincula servidores do Cloud Virtual Machine (CVM) em um Virtual Private Cloud (VPC) para migração perfeita entre vários servidores do CVM. Vários ENIs podem ser vinculados a um servidor do CVM para criar uma rede de alta disponibilidade. 

Um ENI faz parte de uma sub-rede, que integra a um VPC, que por sua vez está inserido em uma zona de disponibilidade. Um ENI só pode ser associado à uma instância do CVM na mesma zona de disponibilidade. Vários ENIs podem ser associados à mesma instância do CVM. A quantidade específica depende da especificação do CVM.

## Conceitos

 - **ENI principal e ENI secundário**: ao criar uma instância do CVM, um ENI é criado automaticamente no processo. Esse é o ENI principal. Os ENIs subsequentes que você criar são ENIs secundários. Você não pode vincular ou desvincular um ENI principal. Os ENIs secundários permitem vinculação e desvinculação.
 - **IP privado principal:** o IP privado principal de um ENI é atribuído pelo sistema ou especificado pelo usuário ao criar o ENI. Você pode modificar o IP privado principal do ENI principal, mas não os dos ENIs secundários.
  **IP privado secundário:** diferente do IP privado principal, todos os endereços IP vinculados ao ENI são IPs privados secundários. Você pode vincular/desvincular esses IPs.
 - **EIP**: os EIPs são mapeados um a um para os IPs privados de um ENI.
 - **Grupo de segurança**: um ENI pode ser associado a um ou mais grupos de segurança.
 - **Endereço MAC**: cada ENI tem um endereço MAC global exclusivo.

## Casos de uso
- **Isolamento entre rede privada, rede pública e rede de gerenciamento**:
Segmentos de negócio críticos geralmente exigem políticas de roteamento e grupos de segurança diferentes para redes privadas e redes públicas, além de gerenciamento para garantir a segurança dos dados e o isolamento da rede. Você pode usar o CVM para atingir o mesmo nível de isolamento que os diferentes servidores físicos. Basta atribuir diferentes ENIs a diferentes sub-redes.
**Implantação de aplicativos altamente confiáveis:**
Os componentes críticos do sistema exigem vários backups dinâmicos para garantir alta disponibilidade. A vinculação e a desvinculação flexível dos ENIs e dos IPs privados são a base da arquitetura de alta disponibilidade do Tencent Cloud. Utilize o Keepalived (mensagens enviadas entre dispositivos) para implementar essa funcionalidade.

## Limites de uso

A quantidade de ENIs a que uma instância do CVM pode ser associada e a quantidade de IPs privados a que um ENI pode ser associado dependem das configurações da CPU e da memória. Veja na tabela a seguir:
> A quantidade de endereços IP vinculados a um único ENI representa apenas o limite superior de endereços IP aos quais os ENIs podem estar vinculados, e não à cota de EIP disponível. Para saber a cota de EIP da sua conta, consulte EIP [limites de uso](https://intl.cloud.tencent.com/document/product/213/5733).

| Especificação do CVM | Quantidade de ENIs | Quantidade de IPs privados |
| ------------------- | :---- | :------ |
| CPU: 1 núcleo </br>Memória: 1 GB | 2 | 2 |
| CPU: 1 núcleo </br>Memória: > 1 GB | 2 | 6 |
| CPU: 2 núcleos | 2 | 10 |
| CPU: 4 núcleos </br>Memória: < 16 GB | 4 | 10 |
| CPU: 4 núcleos </br>Memória: > 16 GB | 4 | 20 |
| CPU: 8 - 12 núcleos | 6 | 20 |
| CPU: > 12 núcleos | 8 | 30 |


## Visão geral das APIs
Na tabela abaixo, temos uma lista das APIs relacionadas ao ENI e ao CVM. Para obter mais informações, consulte a [Visão geral das APIs do ENI](https://intl.cloud.tencent.com/document/product/215/15755?from_cn_redirect=1#.E5.BC.B9.E6.80.A7.E7.BD.91.E5.8D.A1.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3).

| Funcionalidade | ID da ação | Descrição |
|---------|---------|---------|
| Criar um ENI | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818?from_cn_redirect=1) | Cria um ENI |
| Solicitar IPs privados | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813?from_cn_redirect=1) | Solicita IPs privados para um ENI |
| Vincular um ENI à uma instância do CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819?from_cn_redirect=1) | Vincula um ENI à uma instância do CVM |
