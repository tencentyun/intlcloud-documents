O Tencent Cloud oferece dois ambientes de rede: o [Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc) (VPC) e a rede básica.
Depois de 13 de junho de 2017, a rede básica não será mais compatível com as contas recém-registradas. Recomendamos que você use um VPC pelos seguintes motivos:
- Funcionalidades completas: o VPC abrange todas as funcionalidades básicas de rede, fornecendo serviços de rede mais flexíveis, como intervalo de IP personalizado, roteamento, Direct Connect, VPN, NAT etc.
- Migração fácil: não existe uma solução de migração sem nenhum tipo de complicação no setor (há necessidade de desligar, alterar o IP privado etc.). Se você precisar usar um VPC para desenvolvimento posterior da empresa, o processo de migração poderá afetar seus negócios.

## VPC e rede básica

### VPC

Com o [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215) do Tencent Cloud, você pode personalizar uma rede virtual isolada logicamente na nuvem. Ainda que na mesma região, diferentes VPCs não conseguem se comunicar entre si por padrão. Semelhante à rede tradicional que você executa em seu data center, seus recursos do Tencent Cloud, como o [CVM](https://intl.cloud.tencent.com/document/product/213/495), o [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524) e o [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147), estão hospedados no VPC do Tencent Cloud para proporcionar a você controle total sobre o ambiente. Para obter mais informações sobre cenários de configurações e aplicação, consulte [VPC](https://intl.cloud.tencent.com/document/product/215/535). O VPC ajuda a criar uma arquitetura de rede mais complexa e é adequado para aqueles que estão familiarizados com o gerenciamento de redes.

![](https://main.qcloudimg.com/raw/b86b2e3af8e21354d317bb2b4739b47d.jpg)

### Rede básica

A rede básica é o pool de recursos de rede pública para todos os usuários do Tencent Cloud. Todos os seus recursos do Tencent Cloud serão gerenciados centralmente pelo Tencent Cloud.

### Diferenças nas funcionalidades

| **Funcionalidade**| **Rede básica**| **VPC** |
|---------|---------|---------|
| Associação de locatários | Associação de locatários | Rede isolada logicamente baseada em encapsulamento GRE |
| Personalização de rede | Não compatível | Compatível |
| Personalização de roteamento | Não compatível | Compatível |
| IP personalizado | Não compatível | Compatível |
| Regras de interconexão | A interconexão é permitida para o mesmo locatário na mesma região | A interconexão entre regiões e contas é compatível |
| Controle de segurança　| [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452)| [Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452) e [ACL à rede](https://intl.cloud.tencent.com/document/product/215/5132) |

## Compartilhamento e acesso de recursos entre a rede básica e o VPC

Alguns recursos e funcionalidades do Tencent Cloud são compatíveis com a rede básica e o VPC, e podem ser compartilhados ou acessados por meio dessas duas redes.

|**Recurso**|**Descrição**|
|--|--|
|[Imagem](https://intl.cloud.tencent.com/document/product/213/4940)|Uma imagem pode ser usada para iniciar uma instância do CVM em qualquer ambiente de rede|
|[IP público elástico](https://intl.cloud.tencent.com/document/product/213/5733)|Os IPs públicos elásticos podem ser vinculados a uma instância do CVM em qualquer ambiente de rede|
|Instâncias|As instâncias da rede básica e do VPC podem se comunicar entre si por meio do [IP público](https://intl.cloud.tencent.com/document/product/213/5224) ou do [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807)|
|[Chaves SSH](https://intl.cloud.tencent.com/document/product/213/6092)|A chave SSH é compatível com o carregamento de uma instância do CVM em qualquer ambiente de rede|
|[Grupos de segurança](https://intl.cloud.tencent.com/document/product/213/12452)|Os grupos de segurança são compatíveis com as instâncias do CVM em qualquer ambiente de rede|

> O [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) não pode ser compartilhado entre a rede básica e o VPC. Mesmo quando o VPC e a rede básica estão interconectados, o Cloud Load Balancer não permite a vinculação de instâncias nos VPCs e nas redes básicas ao mesmo tempo.

## Migração de instâncias da rede básica para o VPC

Consulte [Mudar paro VPC](https://intl.cloud.tencent.com/document/product/213/20278) para migrar instâncias dentro da rede básica para o VPC.
