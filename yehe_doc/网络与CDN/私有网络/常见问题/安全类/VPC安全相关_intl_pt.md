### Como posso garantir a segurança de instâncias da CVM no VPC?
O próprio VPC é um ambiente de rede logicamente isolado, e o tráfego pode ser controlado configurando grupos de segurança e ACLs de rede:
- Grupo de segurança: fornece controle de tráfego de rede para CVMs no nível da instância. O tráfego que não tem permissão para entrar ou sair da instância é automaticamente rejeitado.
- [ACL de rede](https://intl.cloud.tencent.com/document/product/215/31850): fornece controle de tráfego de rede no nível da sub-rede.
