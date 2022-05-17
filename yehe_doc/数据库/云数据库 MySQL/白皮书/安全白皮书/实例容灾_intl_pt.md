
Para aplicações com altos requisitos de continuidade de serviço, confiabilidade de dados e conformidade, o TencentDB for MySQL fornece soluções de recuperação de desastres entre zonas de disponibilidade (AZ, na sigla em inglês) e regiões diferentes, Isso ajuda a aprimorar sua capacidade de fornecer serviços contínuos a custos baixos e melhorar a confiabilidade dos dados.

### Recuperação de desastres na mesma região
Você pode criar instâncias do TencentDB for MySQL de [dois nós](https://intl.cloud.tencent.com/document/product/236/38328) e [três nós](https://intl.cloud.tencent.com/document/product/236/38328) para permitir a implantação multi-AZ. Os servidores físicos de uma instância multi-AZ são implantados em AZs diferentes na mesma região. Quando uma AZ falha, o tráfego de atividades será alternado para outra AZ rapidamente, o que é imperceptível para os negócios e não requer alterações na camada de aplicação para obter a recuperação de desastres na mesma região.
>?Como os nós de uma instância multi-AZ estão em AZs diferentes, pode haver um atraso de sincronização de rede adicional de 2 a 3 ms.

Para mais informações sobre recuperação de desastres na mesma região, consulte [Alta disponibilidade (várias AZs)](https://intl.cloud.tencent.com/document/product/236/8459).

### Recuperação de desastres entre regiões diferentes
O recurso de recuperação de desastres na mesma região do TencentDB for MySQL é limitado a AZs diferentes na mesma região. Para melhorar ainda mais a disponibilidade, o TencentDB for MySQL também permite a recuperação de desastres de dados entre regiões diferentes.

Você pode replicar dados de forma assíncrona em uma instância do TencentDB for MySQL na região A para outra instância (instância de recuperação de desastres) na região B por meio do DTS. A instância de recuperação de desastres tem um endereço de conexão, conta e permissões independentes. Se ocorrer uma falha grave na região A e ela não puder ser corrigida em pouco tempo, você poderá executar o failover sempre que necessário. Especificamente, você pode encaminhar rapidamente solicitações de aplicações para a instância de recuperação de desastres; basta modificar a configuração de conexão de banco de dados na aplicação, fornecendo assim uma disponibilidade de banco de dados de nível financeiro.

Para mais informações sobre a recuperação de desastres entre regiões diferentes, consulte [Instância de recuperação de desastres](https://intl.cloud.tencent.com/document/product/236/7272).

