## Tipos de recursos do CLB autorizáveis no CAM
| Tipo de recurso | Descrição do recurso na política de autorização |
| :-------- | -------------- |
| Instância do CLB | ` qcs::clb:$region::clb/$loadbalancerid` |
| Servidor de back-end do CLB | `qcs::cvm:$region:$account:instance/$cvminstanceid` |

Aqui:
- `$region` deve ser sempre o ID de uma região e pode estar vazio.
- `$account` deve sempre ser o `AccountId` do dono do recurso ou `*`.
- `$loadbalancerid` deve ser sempre o ID de uma instância do CLB ou `*`.

E assim por diante...

## APIs autorizáveis para o CLB no CAM
Você pode autorizar as seguintes ações para um recurso do CLB no CAM.
### Instância

Operação da API | Descrição do recurso | Descrição da API |
| :-------- | :--------| :------ |
| DescribeLoadBalancers | Consulta a lista de instâncias do CLB | `*` indica que apenas a API deve ser autenticada |
| CreateLoadBalancer | Compra instância do CLB | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers | Exclui instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes | Modifica os atributos da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName | Renomeia a instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### Listener

Operação da API | Descrição do recurso | Descrição da API |
| :-------- | :---------| :------ |
| DeleteLoadBalancerListeners | Exclui listener do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DescribeLoadBalancerListeners | Obtém a lista de listeners do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerListener | Modifica os atributos do listener do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateLoadBalancerListeners | Cria listener do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteForwardLBListener | Exclui listener do CLB (camada 4 e camada 7) | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBSeventhListener | Modifica os atributos do listener do CLB de camada 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
ModifyForwardLBFourthListener | Modifica os atributos do listener do CLB de camada 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DescribeForwardLBListeners | Consulta lista de listeners do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBSeventhLayerListeners | Cria listener do CLB de camada 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBFourthLayerListeners | Cria listener do CLB de camada 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### URL e nome de domínio do CLB

Operação da API | Descrição do recurso | Descrição da API |
| :-------- | --------| :------ |
| ModifyForwardLBRulesDomain | Modifica o nome de domínio da regra de encaminhamento do listener do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| CreateForwardLBListenerRules | Cria regra de encaminhamento do listener do CLB | 
`qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteForwardLBListenerRules | Exclui regra do listener do CLB de camada 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeleteRewrite | Exclui o relacionamento de redirecionamento da regra de encaminhamento da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ManualRewrite | Adiciona, manualmente, o relacionamento de redirecionamento da regra de encaminhamento da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| AutoRewrite | Gera, automaticamente, o relacionamento de redirecionamento da regra de encaminhamento da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### Servidor de back-end

Operação da API | Descrição do recurso | Descrição da API |
| :-------- | :--------| :------ |
| ModifyLoadBalancerBackends | Modifica o peso do servidor de back-end da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DescribeLoadBalancerBackends | Obtém a lista de servidores de back-end vinculados à instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| DeregisterInstancesFromLoadBalancer | Desvincula o servidor de back-end | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithLoadBalancer | Vincula o servidor de back-end à instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeLBHealthStatus | Consulta o status de integridade do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardFourthBackendsPort | Modifica a porta da instância do CVM na regra de encaminhamento do listener de camada 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
ModifyForwardFourthBackendsWeight | Modifica o peso da instância do CVM na regra de encaminhamento do listener de camada 4 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBSeventhListener | Vincula a instância do CVM à regra de encaminhamento do listener de camada 7 do CLB |`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| RegisterInstancesWithForwardLBFourthListener | Vincula a instância do CVM à regra de encaminhamento do listener de camada 4 do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLBFourthListener | Desvincula a instância do CVM da regra de encaminhamento do listener de camada 4 do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DeregisterInstancesFromForwardLB | Desvincula a instância do CVM da regra de encaminhamento do listener de camada 7 do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| ModifyForwardSeventhBackends | Modifica o peso da instância do CVM na regra de encaminhamento do listener de camada 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
ModifyForwardSeventhBackendsPort | Modifica a porta da instância do CVM na regra de encaminhamento do listener de camada 7 | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
| DescribeForwardLBBackends | Consulta a lista de instâncias do CVM da instância do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*` |
| DescribeForwardLBHealthStatus | Consulta o status da verificação de integridade do CLB | `qcs::clb:$region:$account:clb/*` |
| ModifyLoadBalancerRulesProbe | Modifica a verificação de integridade e o caminho de encaminhamento da regra de encaminhamento do listener do CLB | `qcs::clb:$region:$account:clb/$loadbalancerid` |


