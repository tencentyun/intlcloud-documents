As instâncias do CLB determinam a disponibilidade de servidores de back-end por meio de verificações de integridade, evitando que negócios de front-end sejam afetados por exceções de servidores de back-end e melhorando a disponibilidade geral dos negócios.
- Se a verificação de integridade estiver ativada, a instância do CLB sempre executará verificações de integridade nas instâncias do CVM de back-end, independentemente de seus pesos (incluindo 0).
 - Se uma instância do CVM de back-end estiver anormal, a instância do CLB encaminhará automaticamente novas solicitações para outras instâncias normais do CVM, ignorando a que não estiver íntegra.
 - Uma vez recuperada a instância anormal do CVM, ela voltará a ser utilizada no serviço CLB e receberá novas solicitações.
 - Se todos os servidores de back-end estiverem anormais, as solicitações serão encaminhadas para todas as instâncias de back-end do CVM.
- Se a verificação de integridade estiver desabilitada, a instância do CLB encaminhará o tráfego para todos os servidores de back-end, incluindo aqueles anormais. Portanto, é altamente recomendável ativar a verificação de integridade da instância do CLB para verificar automaticamente os servidores de back-end e remover os anormais.

## Status da verificação de integridade
A descrição do status de verificação de integridade das instâncias do CVM de back-end é a seguinte:

| Status | Descrição | Se deve encaminhar o tráfego |
| ------- | ----------- | ---------------- |
| Detecção | O status de uma nova instância do CVM de back-end durante o período de intervalo de verificação × limite de integridade. Por exemplo, suponha que o intervalo de verificação seja de 2 segundos e o limite de integridade seja de 3 vezes, a instância do CVM de back-end permanece neste status por 6 segundos. | Não. |
| Íntegro | O servidor de back-end está normal. | Sim. |
| Anormal | O servidor de back-end está anormal. | <li>Não.</li><li> De acordo com o listener da camada 4 ou regra de URL da camada 7, se uma instância do CLB detectar que nenhum dos servidores de back-end está íntegro, ela encaminhará as solicitações para todos os servidores de back-end.</li>|
| Desativado | A verificação de integridade está desativada. | Sim. |

## Verificação de integridade do TCP
Para listeners TCP da camada 4, você pode configurar a verificação de integridade do TCP para obter o status das instâncias do CVM de back-end por meio de pacotes SYN, ou seja, handshake TCP de três vias. Além disso, para este fim, é possível personalizar a solicitação e retornar o conteúdo do protocolo.
![](https://main.qcloudimg.com/raw/5f30ebbb5e061affeff6eb031facaf28.png)
O mecanismo de verificação de integridade do TCP é o seguinte:
1. Uma instância do CLB envia um pacote de solicitação de conexão SYN para (o IP privado e a porta de verificação de integridade de) uma instância do CVM de back-end.
2. Depois de receber o pacote de solicitação SYN, a instância do CVM de back-end retornará um pacote de resposta SYN-ACK se a porta estiver escutando normalmente.
3. Se a instância do CLB receber o pacote de resposta SYN-ACK retornado dentro do tempo limite de resposta, isso indica que o servidor de back-end está normal e o resultado da verificação de integridade foi bem-sucedido. Em seguida, a instância do CLB enviará à instância do CVM de back-end um pacote TCP Reset (RST) para cortar a conexão TCP.
4. Se a instância do CLB não receber o pacote de resposta SYN-ACK retornado dentro do tempo limite de resposta, isso indica que o servidor de back-end está anormal e o resultado da verificação de integridade falhou. Em seguida, a instância do CLB enviará à instância do CVM de back-end um pacote TCP Reset (RST) para cortar a conexão TCP.

## Verificação de integridade do UDP
Para listeners UDP da camada 4, é possível configurar a verificação de integridade do UDP para obter o status das instâncias do CVM de back-end executando o comando Ping e enviando pacotes de detecção UDP para a porta de verificação de integridade. Além disso, para este fim, é possível personalizar a solicitação e retornar o conteúdo do protocolo.
![](https://main.qcloudimg.com/raw/97127e438782907e02e183e9258e652c.png)
O mecanismo de verificação de integridade do UDP é o seguinte:
1. Uma instância do CLB envia um comando Ping ao IP privado de uma instância do CVM de back-end.
2. Em seguida, a instância do CLB envia um pacote de detecção UDP para (IP privado e porta de verificação de integridade da) instância do CVM de back-end.
3. Se o comando Ping for bem-sucedido e a instância do CVM de back-end não retornar o erro `port XX unreachable` dentro do tempo limite de resposta, isso indica que o servidor de back-end está normal e o resultado da verificação de integridade foi bem-sucedido.
4. Se o comando Ping falhar ou a instância do CVM de back-end retornar o erro `port XX unreachable` dentro do tempo limite de resposta, isso indica que o servidor de back-end está anormal e o resultado da verificação de integridade falhou.

>!
1. As verificações de integridade do UDP são baseadas em ICMP, portanto, as instâncias CVM de back-end precisam ter permissão para responder pacotes ICMP (ou seja, o comando Ping é compatível) e pacotes ICMP de "porta inacessível" (ou seja, a porta pode ser detectada).
2. Se um servidor Linux for usado como instância do CVM de back-end, a velocidade do servidor para enviar pacotes ICMP será limitada durante a alta simultaneidade, pois o servidor Linux tem um mecanismo de defesa contra ataques ICMP. Neste caso, embora o servidor de back-end seja anormal, ele não pode retornar o erro `port XX unreachable` para a instância do CLB. Em seguida, a instância do CLB determinará se o resultado da verificação de integridade foi bem-sucedido, de modo que o status real do servidor de back-end não pode ser retornado.
Solução: Você pode configurar a verificação de integridade do UDP com strings de entrada e saída personalizadas. Portanto, em uma verificação de integridade, a string de entrada personalizada será enviada ao servidor de back-end e o resultado será determinado como bem-sucedido somente depois que a instância do CLB receber a string de resposta personalizada. Este método é baseado no servidor de back-end, que precisa processar a string de entrada da verificação de integridade e retornar a string de saída personalizada.

## <span id="http"></span>Verificação de integridade HTTP
Para listeners TCP da camada 4 e listeners HTTP/HTTPS da camada 7, você pode configurar a verificação de integridade HTTP para obter o status das instâncias CVM de back-end enviando solicitações HTTP.
![](https://main.qcloudimg.com/raw/94d491d305eca2c6b891912fc1a62ffe.png)
O mecanismo de verificação de integridade do HTTP é o seguinte:
1. De acordo com a configuração de verificação de integridade, uma instância do CLB pode enviar solicitações HTTP (com o nome de domínio de destino especificado) para (o IP privado, porta de verificação de integridade e caminho de verificação de) uma instância do CVM de back-end.
2. Depois de receber a solicitação, a instância do CVM de back-end retornará o código de status HTTP correspondente.
3. Se a instância do CLB receber o código de status HTTP retornado dentro do tempo limite de resposta e o código de status HTTP corresponder ao definido, isso indicará que a verificação de integridade foi bem-sucedida, caso contrário, terá falhado.
4. Se a instância do CLB não receber a resposta da instância do CVM de back-end dentro do tempo limite de resposta, isso indicará falha no resultado da verificação de integridade.

>? Para listeners HTTPS da camada 7, se HTTP for selecionado como o protocolo de back-end das regras de encaminhamento do listener HTTPS, a verificação de integridade de HTTP será conduzida; se HTTPS for selecionado, a verificação de integridade de HTTPS será conduzida.
As verificações de integridade de HTTPS são basicamente as mesmas que as <a href="#http">verificações de integridade de HTTP</a>. A diferença é que nas verificações de integridade HTTPS, as solicitações HTTPS são enviadas e o status da instância do CVM de back-end é determinado pelo código de status HTTPS retornado.
## Intervalo de tempo de verificação de integridade
O mecanismo de verificação de integridade do CLB melhora a disponibilidade dos negócios, mas as falhas frequentes de verificação de integridade podem causar trocas desnecessárias de servidor, comprometendo a disponibilidade do sistema. Portanto, o status da verificação de integridade pode ser alternado entre íntegro e anormal apenas se os resultados em um intervalo de tempo de verificação de integridade se repetirem várias vezes. O intervalo de tempo de verificação de integridade é baseado nos fatores abaixo:
<table>
<tr>
<th>Configuração de verificação de integridade</th>
<th>Observações</th>
<th>Valor padrão</th>
</tr>
<tr>
<td>Tempo limite de resposta</td>
<td><ul><li>Tempo limite máximo de resposta para uma verificação de integridade.</li><li>Se um servidor de back-end não responder dentro do tempo limite, será considerado anormal.</li><li>Intervalo de valores: 2 a 60 segundos.</li></ul></td>
<td>2 segundos.</td>
</tr>
<tr>
<td>Intervalo de verificação</td>
<td><ul><li>Intervalo entre duas verificações de integridade.</li><li>Intervalo de valores: 5 a 300 segundos.</li></ul></td>
<td>5 segundos</td>
</tr>
<tr>
<td>Limite de não integridade</td>
<td><ul><li>Se o resultado da verificação de integridade falhar por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end não está íntegra e o status exibido no console é **Abnormal (Anormal)**.</li><li>Intervalo de valores: 2 a 10 vezes.</li></ul></td>
<td>3 vezes</td>
</tr>
<tr>
<td>Limite de integridade</td>
<td><ul><li>Se o resultado da verificação de integridade for satisfatório por n (um valor personalizável) vezes, considera-se que a instância do CVM de back-end está íntegra e o status exibido no console é **Healthy (Íntegro)**.</li><li>Intervalo de valores: 2 a 10 vezes.</li></ul></td>
<td>3 vezes</td>
</tr>
</table>

Os cálculos do **intervalo de tempo de verificação de integridade da camada 4** são os seguintes:
>?Verificação de integridade da camada 4, ou seja, verificação de integridade de TCP ou verificação de integridade de UDP, o intervalo de tempo entre duas verificações é o valor definido, não importa se o resultado foi bem-sucedido ou se o tempo de resposta expirou.
- Intervalo de tempo de uma verificação de integridade com um resultado de falha = Intervalo de verificação × (Limite de não integridade - 1)
No exemplo abaixo, o tempo limite de resposta da verificação de integridade é de 2 segundos, o intervalo de verificação é de 5 segundos e o limite de não integridade é de 3 vezes, portanto, o intervalo de tempo de uma verificação de integridade com resultado de falha = 5 x (3-1) = 10 segundos.
![](https://main.qcloudimg.com/raw/63ee9657f3bb44c31c8e271484a67729.png)
- Intervalo de tempo de uma verificação de integridade com um resultado bem-sucedido = Intervalo de verificação × (Limite de integridade - 1)
No exemplo abaixo, o período de uma resposta de verificação de integridade bem-sucedida é de 1 segundo, o intervalo de verificação é de 5 segundos e o limite de integridade é de 3 vezes, portanto, o intervalo de tempo de uma verificação de integridade com um resultado bem-sucedido = 5 x (3-1 ) = 10 segundos.
![](https://main.qcloudimg.com/raw/9f147597b7eb8879c4460ec6eadea3cb.png)

Os cálculos do **intervalo de tempo de verificação de integridade da camada 7** são os seguintes:
- Intervalo de tempo de uma verificação de integridade com um resultado com falha = Tempo limite de resposta × Limite de não integridade + Intervalo de verificação × (Limite de não integridade - 1)
No exemplo abaixo, o tempo limite de resposta da verificação de integridade é de 2 segundos, o intervalo de verificação é de 5 segundos e o limite de não integridade é de 3 vezes, portanto, o intervalo de tempo de uma verificação de integridade com resultado de falha = 2 x 3 + 5 x (3-1) = 16 segundos.
![](https://main.qcloudimg.com/raw/8ddafd2348fd071942752dc24f5c5c2c.png)
- Intervalo de tempo de uma verificação de integridade com um resultado bem-sucedido = Período de uma resposta de verificação de integridade bem-sucedida × Limite de integridade + Intervalo de verificação × (Limite de integridade -1)
No exemplo abaixo, o período de uma resposta de verificação de integridade bem-sucedida é de 1 segundo, o intervalo de verificação é de 5 segundos e o limite de integridade é de 3 vezes, portanto, o intervalo de tempo de uma verificação de integridade com um resultado bem-sucedido = 1 x 3 + 5 x (3-1) = 13 segundos.
![](https://main.qcloudimg.com/raw/a6afea17bf2767081c2fcd66913233d0.png)


## Identificadores de verificação de integridade
Após o início das verificações de integridade do CLB, o servidor de back-end receberá solicitações de verificação de integridade além das solicitações normais de negócios. Uma solicitação de verificação de integridade pode ter as seguintes propriedades:
- O IP de origem da verificação de integridade é o VIP do CLB.
- Uma solicitação de verificação de integridade dos listeners da camada 4 (TCP, UDP e TCP SSL) será marcada com "HEALTH CHECK".
- Para uma solicitação de verificação de integridade dos listeners da camada 7 (HTTP e HTTPS), o `user-agent` no cabeçalho é `clb-healthcheck`.
>?
> - Para uma solicitação de verificação de integridade de instâncias do CLB clássico de rede privada, o IP de origem da verificação de integridade é `169.254.128.0/17`.
> - Para uma solicitação de verificação de integridade de instâncias do CLB de rede clássica, o IP de origem da verificação de integridade é o IP físico.

## Referência
- [Configuração da verificação de integridade](https://intl.cloud.tencent.com/document/product/214/39251)
- [Configuração dos logs de verificação de integridade](https://cloud.tencent.com/document/product/214/55139)
