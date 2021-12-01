O espelho de tráfego fornece um serviço de coleta de tráfego que filtra e copia o tráfego desejado da interface de rede especificada para instâncias do CVM no mesmo VPC. Essa funcionalidade é aplicável a casos de uso, incluindo auditoria de segurança, monitoramento de risco, solução de problemas e análise empresarial.
> ?No entanto, o espelho de tráfego consome recursos do CVM como CPU, memória e largura de banda proporcionalmente. Considere como exemplo você espelhar uma interface de rede que tem 1 Gbps de tráfego de entrada e 1 Gbps de tráfego de saída. Nesse caso, a instância precisa lidar com 1 Gbps de tráfego de entrada e 3 Gbps de tráfego de saída (1 Gbps para o tráfego de saída, 1 Gbps para o tráfego de entrada espelhado e 1 Gbps para o tráfego de saída espelhado).

## Procedimento
Veja abaixo os principais componentes de um espelho de tráfego, junto com seu fluxo de trabalho.
- Source (Origem): o ENI especificado no VPC que aplica as regras de filtro, como rede, intervalo de coleta, tipo de coleta e filtragem de tráfego.
- Target (Destino): os IPs de recebimento que obtêm o tráfego coletado.
![](https://main.qcloudimg.com/raw/37ff00d3d5021bb7340d2b233a3182dc.png)

## Casos de uso
### Auditoria de segurança
Um sistema em execução pode acarretar tráfego de rede não íntegro ou gerar uma mensagem de erro devido a exceção de software, falha de hardware, vírus de computador ou uso impróprio. Para localizar as causas desses problemas, é possível usar o espelho de tráfego para analisar as mensagens da rede.

### Verificação de intrusão
Para garantir a confidencialidade, integridade e disponibilidade dos recursos do sistema de rede, é possível usar o espelho de tráfego para copiar o tráfego para clusters do CVM, para análise em tempo real.

### Análise empresarial
Use o espelho de tráfego para apresentar o modo de tráfego da empresa de forma clara e visual.
