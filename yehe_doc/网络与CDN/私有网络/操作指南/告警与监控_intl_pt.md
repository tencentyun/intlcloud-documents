Ao configurar as políticas de alarme, você pode monitorar o status dos recursos em uma VPC, como o NAT Gateway, o gateway do VPN, o gateway do Direct Connect, o EIP etc., para descobrir a execução anormal dos recursos da nuvem a tempo, localizar e resolver os problemas ASSIM QUE POSSÍVEL.

## Configuração de uma política de alarme
1. Faça login no [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview).
2. Selecione **Alarm Configuration (Configuração de alarmes)** > **Alarm Policy (Política de alarmes)** na barra lateral esquerda, para acessar a página de configuração da política de alarmes.
3. Clique em **Create (Criar)**, insira um nome de política, selecione um recurso de nuvem da VPC a ser configurada para o tipo de política, como **VPC** > **EIP**, e configure as regras de alarme e as notificações de alarme.
![]()
4. Clique em **Complete (Concluir)**. Você pode conferir a política de alarme definida na lista de políticas de alarme.
>? Para excluir uma política de alarme, primeiro é necessário desvincular todos os recursos dela.
>
5. Quando um alarme for acionado, você receberá a notificação de alarme por meio do canal de alarme selecionado (SMS/e-mail/Centro de mensagens etc.).

As configurações de política de alarme para diferentes recursos de nuvem estão detalhadas abaixo:
- Direct Connect: [Configuração de políticas de alarme](https://intl.cloud.tencent.com/document/product/216/38402) 
- NAT Gateway: [Configuração de alarmes](https://intl.cloud.tencent.com/document/product/1015/30242) 
- Conexão VPN: [Configuração de alarmes](https://intl.cloud.tencent.com/document/product/1037/32699) 

## Exibição de informações de monitoramento
Você pode exibir as informações de monitoramento dos recursos de nuvem correspondentes no console da VPC, para ajudar a solucionar as falhas de rede. Consulte:
- Direct Connect: [Exibição de dados de monitoramento](https://intl.cloud.tencent.com/document/product/216/38401) 
- CCN: [Exibição de informações de monitoramento](https://intl.cloud.tencent.com/document/product/1003/30071) 
- NAT Gateway: [Exibição de informações de monitoramento](https://intl.cloud.tencent.com/document/product/1015/30241) 
- Peering Connection: [Exibição de dados de monitoramento do tráfego de rede em um Peering Connection entre regiões](https://intl.cloud.tencent.com/document/product/553/18842) 
- Conexão VPN: [Exibição de dados de monitoramento](https://intl.cloud.tencent.com/document/product/1037/32698) 
