Este artigo tem como objetivo ajudar os usuários a melhorarem a segurança e a confiabilidade de suas instâncias de CVM.

## Segurança e rede

- **Acesso limitado**: restrinja o acesso usando um firewall ([Grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452) para permitir que apenas os endereços confiáveis ​​acessem as instâncias. O grupo de segurança também deve ter regras rígidas, como limitar o acesso a portas, e por endereços IP.
- **Nível de segurança**: diferentes regras de grupo de segurança podem ser criadas para grupos de instâncias de diferentes níveis de segurança para garantir que instâncias que executam negócios importantes não sejam facilmente acessadas por fontes externas.
- **Isolamento lógico de rede**: use [VPC](https://intl.cloud.tencent.com/document/product/213/5227) para dividir os recursos em zonas lógicas.
- **Gerenciamento de permissão de conta:** quando é necessário permitir que várias contas diferentes acessem o mesmo conjunto de recursos de nuvem, você pode gerenciar permissões para recursos de nuvem usando o [mecanismo de política](https://intl.cloud.tencent.com/document/product/598/10601).
- **Login seguro:** faça login em suas instâncias do Linux usando a [chave SSH]
(https://intl.cloud.tencent.com/document/product/213/6092), sempre que possível. Para as instâncias nas quais você [usa senha para fazer login](https://intl.cloud.tencent.com/document/product/213/6093), tal senha precisa ser alterada regularmente.

## Armazenamento

- **Armazenamento de hardware:** para dados que requerem alta confiabilidade, use os discos em nuvem do Tencent Cloud para garantir o armazenamento persistente e a confiabilidade dos dados. Tente não usar [Discos locais](https://intl.cloud.tencent.com/document/product/213/5798) para armazenamento. Para obter mais informações, consulte a [Documentação do produto Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362).
- **Banco de dados:** para bancos de dados que são muito acessados e cuja capacidade muda com frequência, use o TencentDB do Tencent Cloud.

## Backup e recuperação

- **Backup de instância intra-regional**: você pode fazer backup de suas instâncias e dados de negócios usando **imagens personalizadas** e **instantâneos CBS**. Para obter mais informações, consulte [Instantâneo CBS](https://intl.cloud.tencent.com/document/product/362/31638) e [Criação de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4942).
- **Backup de instância entre regiões**: você pode copiar e fazer backup de instâncias entre regiões [Cópia de imagens](https://intl.cloud.tencent.com/document/product/213/4943).
- **Bloqueio de falhas de instância**: você pode usar [EIPs](https://intl.cloud.tencent.com/document/product/213/5733) para mapear o nome de domínio e garantir que o servidor possa redirecionar rapidamente o endereço IP do serviço para outra instância do CVM quando estiver indisponível, protegendo assim as falhas de instância.

## Monitoramento e alarmes
- **Monitoramento e resposta a eventos**: verifique periodicamente os dados de monitoramento e defina os alarmes adequados. Para obter mais informações, consulte a [Documentação do produto Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- **Tratamento de picos de solicitação**: com [Auto Scaling](https://intl.cloud.tencent.com/document/product/377), a estabilidade dos CVMs durante os horários de pico pode ser garantida e as instâncias não íntegras podem ser substituídas automaticamente.
