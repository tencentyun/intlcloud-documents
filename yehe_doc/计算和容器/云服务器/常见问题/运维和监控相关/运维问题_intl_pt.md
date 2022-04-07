### Há alguma orientação sobre operações de sites de pequeno porte hospedados na CVM?
Para manter as aplicativos do site, você pode:
- Fazer backup dos dados no disco em nuvem diariamente. Para mais informações, consulte [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Usar o [SSL Certificates Service](https://intl.cloud.tencent.com/document/product/1007/30152) para verificação de identidade e conexões criptografadas. 
- Instalar plugins antivírus ou serviços anti-DDoS ou adquirir o Cloud Workload Protection.
- Monitorar o tráfego "de" e "para o site", e identificar erros na faixa de tráfego. Adicione as regras de grupo de segurança de acesso negado para controlar temporariamente a solicitação de exceção de um único ponto. Para mais informações, consulte [Obtenção de estatísticas de monitoramento](https://intl.cloud.tencent.com/document/product/213/5178) e [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
- Monitorar o desempenho das instâncias da CVM e do disco em nuvem, e marcar o período de pico de tráfego/acesso. Familiarize-se com antecedência com o upgrade/downgrade, o Auto Scaling ou a expansão de disco em nuvem para responder a picos de solicitações. Para mais informações, consulte [Alteração da configuração da instância](https://intl.cloud.tencent.com/document/product/213/2178), [O que é o Auto Scaling (AS)?](https://intl.cloud.tencent.com/document/product/377/3154) ou [Cenários de expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31600).
- Atualizar a senha de administrador regularmente para os cenários em que você faz login em instâncias da CVM com o nome de usuário e a senha de administrador/raiz. Para mais informações, consulte [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
- Atualizar os patches de software regularmente.

