Com base na experiência do cliente em testes de estresse, este documento resume problemas comuns de desempenho em testes de estresse e oferece resolução de problemas, bem como sugestões.

## Perguntas frequentes sobre testes de estresse

### 1. O acesso à rede pública não está habilitado no servidor de back-end
Se o acesso à rede pública não estiver habilitado quando você comprar o CVM, o encaminhamento pode falhar quando um CLB de rede pública for montado na instância do CVM.
### 2. A largura de banda de um servidor de back-end é insuficiente
Se o servidor de back-end tiver uma largura de banda baixa, ele não poderá retornar pacotes ao CLB quando o limite for excedido. O CLB retornará um erro 504 ou 502 ao cliente.
### 3. As portas do cliente são insuficientes 
Se o número de clientes for muito pequeno ou o intervalo de portas do cliente for muito estreito, as portas do cliente se tornarão insuficientes e as conexões não serão estabelecidas. Além disso, se o valor `keep_alive` for maior que 0 quando uma conexão persistente for estabelecida, a conexão usará permanentemente a porta, o que reduz o número de portas de cliente disponíveis.
### 4. Os aplicativos usados por servidores de back-end têm problemas de desempenho
Depois que uma solicitação chega a um servidor de back-end por meio do CLB, a carga no servidor de back-end é normal. No entanto, como os aplicativos em servidores de back-end também dependem de outros aplicativos, como banco de dados, problemas de desempenho no banco de dados também podem afetar o desempenho do teste de estresse.
### 5. Um servidor de back-end não está íntegro
O status de integridade de servidores de back-end pode ser ignorado em testes de estresse. Se o servidor de back-end tiver uma falha na verificação de integridade ou um status de verificação de integridade instável (às vezes bom e às vezes ruim com mudanças rápidas), o teste de estresse pode ter um desempenho ruim.
### 6. Persistência de sessão habilitada para resultados CLB em distribuição de tráfego irregular entre servidores de back-end
Depois que a persistência da sessão é habilitada para CLB, as solicitações podem ser distribuídas para servidores de back-end fixos. A distribuição do tráfego torna-se irregular, afetando o desempenho dos testes de estresse. Recomendamos que seja desativada a persistência da sessão durante o teste de estresse.

## Sugestões para teste de estresse
> As configurações a seguir são usadas apenas para teste de estresse do CLB. Você não precisa tê-las em seu ambiente de produção.

- Recomendamos que seja usada uma conexão não persistente ao efetuar teste de estresse na capacidade de encaminhamento do CLB.
Exceto para verificação dos recursos de persistência da sessão, o teste de estresse geralmente é projetado para verificar a capacidade de encaminhamento do CLB. Portanto, a conexão não persistente pode ser usada para testar a capacidade de processamento do CLB e dos servidores de back-end.
- Recomendamos que seja usada a conexão persistente para efetuar teste de estresse na carga do CLB, como o limite superior de largura de banda e serviços de conexão persistentes.
Recomendamos que o período de tempo limite da ferramenta de teste de estresse seja ajustado para um valor baixo. Caso contrário, o tempo médio de resposta aumentará quando o período de tempo limite aumentar, fazendo com que você não consiga avaliar rapidamente se o nível de estresse foi atingido.
- Recomendamos que seja usado um site estático fornecido pelo servidor de back-end para teste de estresse para evitar perdas causadas pela lógica do aplicativo, como E/S e DB.
- Desative a persistência da sessão para os listeners. Caso contrário, o estresse será concentrado em certos servidores de back-end. Se o desempenho da pressão não for satisfatório, é possível identificar se o tráfego está distribuído uniformemente através da verificação dos dados de monitoramento de servidores de back-end em CLB.
- Desative a verificação de integridade para listeners para reduzir as solicitações de acesso a servidores de back-end geradas durante a verificação de integridade.
- Use vários clientes (> 5) para o teste de estresse. Os IPs de fonte dispersa podem simular melhor as condições online reais.
