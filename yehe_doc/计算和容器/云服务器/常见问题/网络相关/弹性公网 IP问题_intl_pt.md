### Para que são usados os EIPs?
Os ElPs são aplicáveis aos seguintes cenários:
- Recuperação de desastres. É altamente recomendável que você use EIPs para recuperação de desastres. Por exemplo, quando um de seus servidores falha, você pode desvincular o EIP desse servidor e vinculá-lo a um servidor íntegro para retomar os serviços rapidamente.
- Retenção de um IP público específico. Se você precisar reter um IP público específico em sua conta, poderá convertê-lo em um EIP, que pode ser vinculado ou desvinculado do dispositivo e usado para acessar a rede pública. Esse EIP será retido na sua conta até que você o “libere”.
- Outros casos especiais. Quando você precisa alterar um IP em alguns casos, é possível converter o IP público em um EIP e, em seguida, vincular ou desvincular o EIP do seu dispositivo. Mas os recursos de EIP em uma conta são limitados em cada região, planeje e use EIPs de acordo.

### Como um EIP é faturado?

1. A taxa exibida no console se aplica a EIPs que ficaram ociosos por mais de 1 hora. Os EIPs podem ser faturados com precisão de segundos. Os EIPs que foram vinculados/desvinculados várias vezes são faturados com base na duração total (em segundos) que estavam desassociados.
2. Os EIPs que ficaram ociosos por menos de 1 hora são faturados pela taxa de ocupação de recursos proporcionalmente.

### Quando um EIP é faturado?
Você pode solicitar, vincular, desvincular ou liberar EIPs. Pelos recursos de EIP disponíveis serem limitados, um EIP é faturado por uma pequena taxa de ocupação de recursos somente quando não está vinculado.

### Como interromper o faturamento do EIP?
- Quando você não precisar mais de um EIP, poderá liberá-lo para interromper o faturamento.
Para mais informações sobre as operações específicas, consulte [Liberação de EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- Se você precisar reter um EIP, mas quiser interromper o faturamento, vincule-o a um dispositivo (como CVM ou NAT). Um EIP vinculado não será faturado.

### É possível converter um EIP novamente em um IP público?

Não é possível converter um EIP novamente em um IP público.

### É possível recuperar um EIP?
Você pode recuperar IPs públicos que não foram atribuídos a outros usuários. Para mais detalhes, consulte [Recuperar o endereço IP da rede pública](https://intl.cloud.tencent.com/document/product/213/32719).

