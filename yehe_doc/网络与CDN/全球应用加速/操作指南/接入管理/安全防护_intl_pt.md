O Global Application Acceleration Platform (GAAP) fornece um plano básico de proteção de segurança por padrão (2 Gbps de largura de banda para usuários gerais e 10 Gpbs para usuários VIP). Para um nível mais alto de proteção, acesse **Assets on Cloud (Ativos na nuvem)** para fazer o upgrade no console do Anti-DDoS Pro.

O console do GAAP também permite configurar uma lista de bloqueio/lista de permissões. Você pode configurá-la da seguinte forma:
1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** da conexão selecionada.
2. Selecione **Attack Defense (Defesa de ataque)** > **Add Rule (Adicionar regra)** e execute as seguintes etapas de configuração:
	1. Adicione uma regra de acesso e escolha permitir ou negar todo o tráfego que acessa a conexão, por padrão.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/e53fc82cbd2e9b9dd40237c796990f56.jpg)
	2. Adicione um IP de origem, selecione um protocolo e adicione uma porta de protocolo. Em seguida, escolha **Allow (Permitir)** ou **Reject (Rejeitar)** para processar o acesso do IP.
        ![](https://qcloudimg.tencent-cloud.cn/raw/0cf0464e39a7b802e81dd0e23141eb7f.jpg)

>?  i. É possível adicionar um máximo de 100 regras de acesso.
>

3. Clique em **Confirm (Confirmar)**.
