## Criação de listener TCP/UDP

1. Faça login no [Console do GAAP](https://console.cloud.tencent.com/gaap), acesse a página **Access Management (Gerenciamento de acesso)** e clique em **ID/Connection Name (ID/Nome da conexão)** da conexão especificada.
2. Na página exibida, selecione **TCP/UDP Listener Management (Gerenciamento de listener TCP/UDP)** > **Create (Criar)**. A configuração específica é mostrada abaixo:
   1. Configure as informações do listener para definir o mapeamento da porta do protocolo.
		![](https://qcloudimg.tencent-cloud.cn/raw/84cfd2802fbed4a46323e9e543aabcb6.png)
      
      - Origin Server Type (Tipo de servidor de origem): pode ser um endereço IP ou nome de domínio, mas apenas um tipo pode ser selecionado para um listener. (Observação: atualmente, o tipo de nome de domínio não é aceito em conexões IPv6).
      - Get Client IP (Obter IP do cliente): você pode selecionar TOA ou protocolo proxy para obter o IP real do usuário. Para obter mais informações, consulte [Princípio básico](https://intl.cloud.tencent.com/document/product/608/14429).
      - Listening Port (Porta de escuta): a porta de acesso do VIP da conexão de aceleração. Intervalo de portas válido: 1–64999 (a porta 21 está indisponível no momento). São aceitos uma única porta ou um intervalo de portas consecutivas. A porta deve ser exclusiva. É possível adicionar, no máximo, 20 portas consecutivas por vez, como 8000–8019.
   2. Configure a política de processamento do servidor de origem; ou seja, se um listener estiver vinculado a vários servidores de origem, será necessário selecionar uma política de programação para os servidores de origem.
      ![](https://qcloudimg.tencent-cloud.cn/raw/6da057ddde07681f3056153ad2bd3096.png)
      
      - RR: vários servidores de origem efetuam o pull de origem, de acordo com a política de RR.
      - Weighted RR (RR ponderado): vários servidores de origem efetuam o pull de origem, de acordo com a relação de peso (é possível definir o peso de cada servidor de origem ao vincular o listener).
      - Least Connections (Conexões mínimas): significa programar primeiro o servidor de origem com a menor quantidade de conexões.
      - Least Latency (Latência mínima): significa programar primeiro o servidor de origem com a latência mínima.
      - Secondary Origin Server (Servidor de origem secundário): você pode escolher se deseja ativar a alternância do servidor de origem principal/secundário (para isso, é necessário ativar a verificação de integridade do servidor de origem).
      <blockquote class="d-mod-notice">
      					<div class="d-mod-title d-notice-title">
      						<i class="d-icon-notice"></i>Observação:
      					</div>
             <p>Os listeners com servidores de origem do tipo nome de domínio aceitam apenas **RR** e **Least Connections (Conexões mínimas)** como política de programação e não aceitam servidores de origem secundários.</p>
      				</blockquote>
3. Se um listener TCP for usado, você pode optar por configurar o mecanismo de verificação de integridade para detectar e remover automaticamente servidores de origem excepcionais. Se o servidor de origem secundário estiver ativado, não será possível desativar a verificação de integridade.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b317846881f8cc41983077c44df92ff0.png)
   
      - Response Timeout (Tempo limite de resposta): tempo limite de resposta do servidor de origem.
      - Health Check Interval (Intervalo de verificações de integridade): o intervalo entre duas verificações de integridade consecutivas.
      - Unhealthy Threshold (Limite não íntegro): indica a quantidade de verificações com falha consecutivas realizadas pelo monitor antes que o servidor de origem seja considerado não íntegro. Se um servidor de origem for considerado não íntegro durante uma verificação, nenhum outro pacote de dados será encaminhado a ele até que retorne ao status normal. 
      - Healthy Threshold (Limite íntegro): indica a quantidade de verificações com êxito consecutivas realizadas pelo monitor antes que o servidor de origem seja considerado íntegro. Se um servidor de origem for considerado íntegro durante uma verificação, os pacotes de dados serão encaminhados a ele novamente.
4. Escolha se deseja ativar a persistência de sessão.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e2ee5834fc04cb1ef2d5ebda205a4193.png)
   
      - Session Persistence (Persistência de sessão): as solicitações de usuário do mesmo IP vão acessar o mesmo servidor de origem.
      - Hold Time (Tempo de espera): duração da persistência de sessão. Quando o listener não tem solicitações por um período maior do que o tempo de espera, a persistência de sessão será automaticamente desconectada.
3. Clique em **Complete (Concluir)**.

## Configuração de listener TCP/UDP

Clique na guia **TCP/UDP Listener Management (Gerenciamento de listener TCP/UDP)** e clique em **Settings (Configurações)** na coluna **Operation (Operação)** de um listener para renomeá-lo ou modificar sua política de programação e os parâmetros de verificação de integridade.

## Vinculação do servidor de origem

1. Selecione a guia **TCP/UDP Listener Management (Gerenciamento de listener TCP/UDP)** e clique em **Bind Origin Server (Vincular servidor de origem)** na coluna **Operation (Operação)** de um "listener TCP/UDP" criado, para vincular ou desvincular um ou mais servidores de origem. Se nenhuma informação do servidor de origem for encontrada conforme exibido no console, pode ser que o tipo de servidor de origem seja inválido ou que ele não tenha sido adicionado ao [Gerenciamento de servidores de origem](https://console.cloud.tencent.com/gaap/listrs).
![](https://qcloudimg.tencent-cloud.cn/raw/2db94f9d3b3aae697dcfbb719fc44f40.png)
2. Selecione um servidor de origem e configure uma porta de pull de origem.
   - Se o RR principal/secundário estiver ativado para um listener, será necessário definir o **Primary Origin Server (Servidor de origem principal)** e o **Secondary Origin Server (Servidor de origem secundário)** na página **Bind Origin Server (Vincular servidor de origem)**.
   - Se você deseja definir as portas de vários servidores de origem, pode usar as funcionalidades de **Cover Port/Complement Port (Porta de cobertura/Porta de complemento)** no canto superior direito. Independentemente das portas do servidor de origem que você configurou anteriormente, a funcionalidade **Cover Port (Porta de cobertura)** definirá os servidores de origem de destino que você selecionar para o número da porta que você inseriu. Se nenhuma porta tiver sido configurada para os servidores de origem de destino selecionados, você pode usar a funcionalidade **Complement Port (Porta de complemento)** para configuração unificada, a fim de reduzir a carga de trabalho repetitiva.
   - Se a política do listener for **Weighted RR (RR ponderado)**, você pode definir o peso (1–100) de um servidor de origem ao vinculá-lo. O servidor de origem é programado com base na proporção de seu peso em relação ao peso total. Por exemplo, se o peso do servidor de origem 1 for 60 e o do servidor de origem 2 for 80, a taxa de programação será 60/(60 + 80) = 42,8% para o servidor de origem 1 ou 57,2% para o servidor de origem 2.
     ![](https://qcloudimg.tencent-cloud.cn/raw/d278faea3ac7a20e8a41b0a6f4dedbb0.png)
   - Se estiver ativada, a verificação de integridade começará quando o servidor de origem for vinculado. Você pode determinar se o servidor de origem está normal verificando o status do listener. Uma conexão de aceleração somente encaminhará pacotes para servidores de origem com o status normal. Os pacotes não serão encaminhados para servidores de origem excepcionais até que retornem ao status normal durante a verificação de integridade.
   - Se você não ativar a verificação de integridade ou se usar um listener UDP, a conexão de aceleração sempre encaminhará pacotes, independentemente do status do servidor de origem.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ed13a74bd6a1187caeb2969f4f471ade.png)
3. Confirme a configuração.
   Após concluir a configuração do servidor de origem, clique em **Next (Avançar)** para acessar a página de confirmação da configuração, na qual é possível exibir as informações de conexão configuradas atualmente e os detalhes do listener.
![](https://qcloudimg.tencent-cloud.cn/raw/04e81f74564fc1604ef7f154afb1b383.png)
4. Clique em **Complete (Concluir)**.

## Exclusão do listener TCP/UDP

Abra a guia **TCP/UDP Listener Management (Gerenciamento de listener TCP/UDP)** e clique em **Delete (Excluir)** na coluna **Operation (Operação)** do listener especificado a ser excluído. Se o listener estiver vinculado a um servidor de origem, primeiro será necessário marcar **Allow force deletion of listeners with bound origin servers (Permitir exclusão forçada de listeners com servidores de origem vinculados)**. Após a exclusão, o serviço de aceleração da porta do listener será interrompido.
 ![](https://qcloudimg.tencent-cloud.cn/raw/200902ee0a9b4533825cae99a5050c94.png)