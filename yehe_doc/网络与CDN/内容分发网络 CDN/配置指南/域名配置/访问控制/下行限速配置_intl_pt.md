
## Visão geral das configurações

O CDN do Tencent Cloud aceita a configuração de limite de velocidade downstream, para definir a velocidade máxima da taxa de transferência downstream em um único URL no servidor.
A configuração do limite de velocidade downstream pode controlar a largura de banda de pico do CDN até certo ponto. Ela costuma ser usada em cenários como promoções de comércio eletrônico e lançamentos e atualizações de versões novas de jogos.

>! Depois que o limite de velocidade downstream for configurado, a experiência de acesso do usuário e o efeito de aceleração do CDN serão afetados. Portanto, use-o com cuidado.

## Guia de configuração

### Limitações de configuração

- Quantidade máxima de regras de limite de velocidade downstream: 10
- Unidade: KB/s; faixa do valor: 1 a 1.000.000 (somente números inteiros)
- Tipos de regras aceitos: todo o conteúdo, tipo de arquivo especificado, pasta especificada e arquivo especificado. Atualmente, a correspondência regular não é aceita.
- As regras são executadas de baixo para cima. As regras no final têm prioridade mais alta.

### Instruções de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Selecione a guia **Access Control (Controle de acesso)** para localizar a configuração de limite de velocidade downstream, que fica desativado por padrão:
![](https://main.qcloudimg.com/raw/c9ea85be753b60096b8088b048ac626a.png)
Clique em **Add Speed Limit Rule (Adicionar regra de limite de velocidade)** para configurar uma regra:
![](https://main.qcloudimg.com/raw/02e033c829da553acc5eeb9bca864528.png)
A configuração geral será desativada após a adição de uma regra, para que os serviços em andamento não sejam afetados:
![](https://main.qcloudimg.com/raw/e0006ace8527cc13c381666b22f21790.png)
Você pode ativar o botão de alternância para implantar a regra de limite de velocidade configurada para os nós em toda a rede do CDN:
![](https://main.qcloudimg.com/raw/4b9685cb889210accb67d11f1b389ae8.png)

## Exemplos de configuração

A configuração do limite de velocidade downstream de `cloud.tencent.com` é a seguinte:
![](https://qcloudimg.tencent-cloud.cn/raw/814d50bbc8ca84e86bb5ac8c36dffc15.png)
Se um usuário acessar o recurso `http://cloud.tencent.com/test.mp4`, o servidor retornará o conteúdo na velocidade de downstream configurada de 200 KB/s.
Se um usuário acessar o recurso `http://cloud.tencent.com/test.flv`, o servidor retornará o conteúdo na velocidade de downstream configurada de 400 KB/s.
