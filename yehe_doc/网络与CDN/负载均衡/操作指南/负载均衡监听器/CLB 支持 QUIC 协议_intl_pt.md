O protocolo QUIC ajuda você a acessar aplicativos com mais rapidez e atinge a multiplexação sem a necessidade de reconexão em cenários como rede fraca ou alternância frequente entre Wi-Fi e 4G. Este documento apresenta como configurar o protocolo QUIC no console do CLB.
## Visão geral do QUIC
O Quick UDP Internet Connection ([QUIC](https://www.chromium.org/quic) é um protocolo de rede da camada de transporte desenvolvido pelo Google, multiplexando fluxos de dados simultâneos usando UDP. Comparado com o protocolo TCP+TLS+HTTP2 mais conhecido, o QUIC tem as seguintes vantagens:
- Reduz o tempo para estabelecer uma conexão.
- Melhora o controle de congestionamento.
- Multiplexa sem bloqueio de início de linha (HOL, na sigla em inglês).
- Realiza migração de conexão.

Após ativar o QUIC, o cliente poderá estabelecer uma conexão QUIC com uma instância do CLB. Se a conexão QUIC falhar devido à negociação entre o cliente e a instância do CLB, o HTTPS ou HTTP/2 será usado. No entanto, a instância do CLB e o servidor de back-end ainda usam o protocolo HTTP1.x.
>?Atualmente, o CLB aceita o QUIC Q044 e versões anteriores.

## Limites de uso
- Atualmente, o protocolo QUIC no CLB está em teste beta. Para usá-lo, envie uma solicitação.
- O protocolo QUIC já está disponível em Pequim, Xangai e Mumbai.
- Atualmente, apenas o CLB de rede pública com listeners HTTPS da camada 7 aceita o protocolo QUIC.
- O protocolo QUIC atual só aceita instâncias do CLB de uma única zona de disponibilidade.

## Instruções[](id:making)
1. Para obter mais informações sobre como criar uma instância do CLB, consulte [Criação de instâncias do CLB](https://intl.cloud.tencent.com/document/product/214/6149).
>?Ao criar uma instância do CLB, selecione “Beijing (Pequim)”, “Shanghai (Xangai)” ou “Mumbai” para **Region (Região)** e “Public Network (Rede pública)” para **Network Type (Tipo de rede)**.
2. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb) e clique em **Instance Management (Gerenciamento de instâncias)** na barra lateral esquerda.
2. Na página **Instance Management (Gerenciamento de instâncias)**, selecione a guia **Cloud Load Balancer**.
3. Localize a instância do CLB da rede pública criada na região de Pequim, Xangai ou Mumbai e clique em **Configure Listener (Configurar listener)** na coluna **Operation (Operação)**.
4. Na página **Listener Management (Gerenciamento de listener)**, clique em **Create (Criar)** em **HTTP/HTTPS Listener (Listener HTTP/HTTPS)**.
5. Na página **Create Listener (Criar listener)**, escolha “HTTPS” como o protocolo da porta de escuta. Conclua as demais configurações e clique em **Submit (Enviar)**.
6. Na página **Listener Management (Gerenciamento de listener)**, clique no símbolo **+** ao lado do listener recém-criado.
7. Na página **CreateForwarding rules (Criar regras de encaminhamento)**, ative o **QUIC** e crie uma regra da camada 7. Preencha os campos relevantes e clique em **Next (Avançar)** para concluir a configuração básica.
>?
>- Se você ativou o protocolo QUIC ao criar uma regra de encaminhamento HTTPS, poderá ativar ou desativá-lo posteriormente, conforme necessário. Se você não ativou o protocolo QUIC ao criar uma regra de encaminhamento HTTPS, não poderá ativá-lo mais tarde.
>- Com base no protocolo UDP, o QUIC usará a porta UDP de uma instância do CLB. Se você ativar o QUIC para um listener HTTPS, as portas UDP e TCP serão usadas. Por exemplo, você ativa o QUIC para o listener HTTPS:443, as portas TCP:443 e UDP:443 são usadas e não é possível criar o listener TCP:443 ou UDP:443.
>

## Operações subsequentes
Após concluir a configuração básica, você pode configurar a [verificação de integridade](https://intl.cloud.tencent.com/document/product/214/6097) e a [persistência de sessão](https://intl.cloud.tencent.com/document/product/214/6154).

