O Global Application Acceleration Platform (GAAP) fornece um plano básico de proteção de segurança por padrão (2 Gbps de largura de banda para usuários gerais e 10 Gpbs para usuários VIP). Para um nível mais alto de proteção, acesse **Assets on Cloud (Ativos na nuvem)** para fazer o upgrade no console do Anti-DDoS Pro.

O console do GAAP também permite configurar uma lista de bloqueio/lista de permissões. Você pode configurá-la da seguinte forma:
1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** da conexão selecionada.
2. Selecione **Attack Defense (Defesa de ataque)** > **Add Rule (Adicionar regra)** e execute as seguintes etapas de configuração:
	1. Adicione uma regra de acesso e escolha permitir ou negar todo o tráfego que acessa a conexão, por padrão.
	 ![](https://main.qcloudimg.com/raw/db45ecb4382cfc75b632f086caba4d2a.png)
	2. Adicione um IP de origem, selecione um protocolo e adicione uma porta de protocolo. Em seguida, escolha **Allow (Permitir)** ou **Reject (Rejeitar)** para processar o acesso do IP.
<img src="https://main.qcloudimg.com/raw/435c2ede3aa58b20060e828cad9db856.png" width="50%">
>? i. É possível adicionar um máximo de 100 regras de acesso.
>
3. Clique em **Confirm (Confirmar)**.
