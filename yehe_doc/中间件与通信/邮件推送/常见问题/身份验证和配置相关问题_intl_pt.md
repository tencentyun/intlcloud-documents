[](id:que1) 

### Quais mecanismos de autenticação são aceitos pelo SES?
O SES aceita todos os mecanismos de autenticação padrão do setor, incluindo o DomainKeys Identified Mail (DKIM), o Sender Policy Framework (SPF) e o Domain-Based Message Authentication, Reporting and Conformance (DMARC).

[](id:que2) 
### Como configuro um domínio de remetente?
<dx-tabs>
::: Etapa 1. Configurar na página DNS
1. Na página de configuração de [Domínio de remetente](https://console.cloud.tencent.com/ses/domain), clique em **Create (Criar)**, insira o nome do domínio e envie.
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. Configure as informações de verificação no [console do DNSPod](https://console.cloud.tencent.com/cns).
3. [](id:step2)Retorne à página de configuração de [Domínio de remetente](https://console.cloud.tencent.com/ses/domain) e clique em **Verify (Verificar)**.
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
4. Clique no endereço do domínio de remetente para acessar a página de detalhes da configuração, onde você pode conferir o valor do domínio.
5. Cole o endereço do domínio de remetente na [etapa 3](#step3) na página [DNSPod](https://console.cloud.tencent.com/cns) para adicionar um registro. Evite espaços.
 - Autenticação DKIM:
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - Autenticação SPF:
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - _dmarc record:
Insira `v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;` como o valor do registro.
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
 <dx-alert infotype="explain"> `xxx@163.com` é apenas um exemplo. Aqui você precisa substituir o exemplo pelo seu endereço de remetente.</dx-alert>
6. Retorne à página de detalhes da configuração do [Domínio de remetente](https://console.cloud.tencent.com/ses/domain) e clique em **Submit (Enviar)**.
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: Etapa 2. Verificar o resultado
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: Suplemento: quando o domínio de remetente é um domínio de terceiro nível
1. Na página de configuração de [Domínio de remetente](https://console.cloud.tencent.com/ses/domain), clique em **Create (Criar)**, insira o nome do domínio e envie.
2. Configure as informações de verificação no [console do DNSPod](https://console.cloud.tencent.com/cns).
:::
</dx-tabs>

>?
>- Após a configuração e verificação acima, se o problema persistir, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para obter ajuda.
>- Se a resolução DNSPod estiver registrada, mas não for possível encontrá-la pelo comando `dig`, o motivo pode ser que a verificação de identidade não foi concluída para o domínio (portanto, o registro interrompeu a resolução).
