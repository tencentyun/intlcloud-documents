
## Cenários
Para criar uma melhor experiência do usuário, é possível configurar regras de alarme no Cloud Monitor. Um alarme é acionado imediatamente quando a condição de alarme configurada para a conexão de aceleração acontece.

## Instruções

Faça login no [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) antes de realizar os procedimentos a seguir.

### Monitoramento de conexão

1. Clique em **Alarm Policy (Política de alarme)** na barra lateral esquerda. Clique em **Create (Criar)** para acessar a página **Create Alarm Policy (Criar política de alarme)**.
2. Para **Policy Type (Tipo de política)**, selecione **GAAP** > **Channel (Canal)**.
![](https://qcloudimg.tencent-cloud.cn/raw/f951241047178c919b8bfef1a3894133.png)
3. Na seção **Alarm Policy (Política de alarme)**, adicione canais conforme necessário para **Policy Object (Objeto da política)**.
   Você pode escolher **Select template (Selecionar modelo)** ou **Configure manually (Configurar manualmente)** para **Trigger Condition (Condição de disparo)**.
   Se você escolher **Select template (Selecionar modelo)**, poderá usar as políticas de alarme configuradas anteriormente. Se não houver modelos, você pode criar e configurar um novo conforme abaixo. O modelo será salvo no console para uso posterior.
	1. Clique em **Add Trigger Condition Template (Adicionar modelo de condição de disparo)** para acessar a página de configuração do modelo.
![](https://qcloudimg.tencent-cloud.cn/raw/121bf297151fd5d14463d2a9f39a5989.png)
	2. Clique em **Create (Criar)**. Na janela pop-up, configure as seguintes condições de disparo:
		- **Template Name (Nome do modelo)**: insira um nome para o modelo.
		- **Remarks (Observações)**: insira observações para o modelo.
		- **Policy Type (Tipo de política)**: selecione um serviço de monitoramento, como **GAAP** > **Channel (Canal)**.
		- Use preset trigger conditions (Usar condições de disparo predefinidas): selecione esta opção para ativar as condições de disparo predefinidas para o produto monitorado correspondente.
		- Trigger condition (Condição de disparo): inclui alarme indicador e alarme de evento. Você pode clicar em **Add (Adicionar)** para definir vários alarmes.
	Se você escolher **Configure manually (Configurar manualmente)**, poderá adicionar várias condições de trigger de alarme, conforme necessário.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce5c2222f27a23a50e29b7d6e675a61.png)
4. Na seção **Configure Alarm Notification (Configurar notificação de alarme)**, clique em **Create Template (Criar modelo)**, insira um nome para o modelo e selecione um objeto e canal destinatário.
>!O objeto destinatário precisa ser vinculado a um canal. Caso contrário, você não receberá uma notificação de alarme.
>
![](https://qcloudimg.tencent-cloud.cn/raw/96bc43097aed1a331162305ef08a6c61.png)
Clique em **Select template (Selecionar modelo)** para escolher o modelo de que você precisa.
![](https://qcloudimg.tencent-cloud.cn/raw/4362a734429b1aadce77fd7b219358cb.png)

### Monitoramento de listener

1. Selecione **Alarm Policy (Política de alarme)** na barra lateral esquerda. Clique em **Create (Criar)** para acessar a página **Create Alarm Policy (Criar política de alarme)**.
2. Para **Policy Type (Tipo de política)**, selecione **GAAP** > **L4 Listener Origin Server Status (Status do servidor de origem do listener da camada 4)**/**L7 Listener Origin Server Status (Status do servidor de origem do listener da camada 7)**.
![](https://qcloudimg.tencent-cloud.cn/raw/31a0c004e5b18e3715f4b197791dc20f.png)
3. Na seção **Alarm Policy (Política de alarme)**, selecione um objeto para **Policy Object (Objeto da política)** e escolha ***Select template (Selecionar modelo)** ou **Configure manually (Configurar manualmente)** para **Trigger Condition (Condição de disparo)**. Se você escolher **Configure manually (Configurar manualmente)**, poderá definir uma condição de disparo para notificá-lo de que um servidor de origem é considerado excepcional.
![](https://qcloudimg.tencent-cloud.cn/raw/d75fdfe6dc7394fb9bdcdcbd6672915f.png)
4. Na seção **Configure Alarm Notification (Configurar notificação de alarme)**, clique em **Create Template (Criar modelo)**, insira um nome para o modelo e selecione um objeto e canal destinatário.
>!O objeto destinatário precisa ser vinculado a um canal. Caso contrário, você não receberá uma notificação de alarme.
>
![](https://qcloudimg.tencent-cloud.cn/raw/242dedea0ea3fb500e2c5cbf33ec449e.png)
Clique em **Select template (Selecionar modelo)** para escolher o modelo de que você precisa.
![](https://qcloudimg.tencent-cloud.cn/raw/16a460eea88e69afbc2a3ca4e97f2d10.png)
