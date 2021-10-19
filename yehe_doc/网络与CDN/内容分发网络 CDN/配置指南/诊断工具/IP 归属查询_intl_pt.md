## Visão geral da funcionalidade
O CDN fornece uma ferramenta para consultar a propriedade de IPs. Essa ferramenta pode ser usada para verificar se um IP especificado é de um nó de cache global do CDN e verificar a região do serviço de aceleração do IP, distrito e ISP.
## Visão geral
Essa ferramenta pode ser usada para a solução de problemas. Quando há uma exceção de acesso, é possível consultar o IP acessado das seguintes maneiras:
- Se o IP não for de um nó do CDN do Tencent Cloud, o problema pode ter sido causado por uma exceção de resolução de nome de domínio. Acesse seu provedor de serviços de DNS e verifique se a configuração do CNAME está correta;
- Se o IP for de um nó do CDN do Tencent Cloud, é possível verificar o status do serviço do nó para conferir se as solicitações foram interrompidas pela ativação/desativação do nó.

## Guia de operação
### Método de consulta
Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Inspect Tool (Ferramenta de inspeção)** -> **Verify Tencent Cloud CDN IP (Verificar IP do CDN do Tencent Cloud)** na barra lateral esquerda.
![](https://main.qcloudimg.com/raw/7c72a39a1c0f33e633057d02af9c3a6f.png)
### Limites de uso
- Insira os endereços IP a serem verificados na caixa de texto (um endereço por linha).
- Até 20 endereços IP podem ser verificados por vez.
- A verificação de endereços IPv4 e IPv6 é aceita.
- A verificação é aceita para os nós de cache globais. Para os nós na China Continental, os dados do ISP no distrito correspondente serão retornados; para os nós fora da China Continental, os dados do país/da região correspondente serão retornados.
- É possível exibir o status do serviço do nó **nas últimas 3 horas**. Se houver mudanças de status de ativação/desativação, o tempo de operação correspondente será exibido.

## Casos de uso
### Nós na China Continental
![](https://main.qcloudimg.com/raw/92a04bfdc0905c9be0465d3dc4825dd3.png)
### Nós fora da China Continental
![](https://main.qcloudimg.com/raw/6a2e1b6f94362d5508ed98a52bd2d125.png)







