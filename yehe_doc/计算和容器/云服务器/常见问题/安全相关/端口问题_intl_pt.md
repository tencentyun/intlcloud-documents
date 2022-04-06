### Quais portas devem ser abertas para a Internet antes de fazer login em uma instância?
Geralmente, você precisa abrir a porta 22 para uma instância do Linux ou a porta 3389 para uma instância do Windows. Para mais informações sobre as portas aplicáveis a outros tipos de instâncias, consulte [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/32369).

### Quais portas são frequentemente usadas na CVM?

Para mais informações, consulte [Porta comum do servidor](https://intl.cloud.tencent.com/document/product/213/12451).

### Por que uma porta deve ser aberta para a Internet? Como abrir uma porta específica?

Você pode usar o serviço somente após abrir a porta para a Internet no grupo de segurança. Por exemplo:
Se você deseja acessar páginas da Web usando a porta 8080, a porta deve ser habilitada e aberta para a Internet no grupo de segurança.
Para abrir uma porta para a Internet, siga as etapas abaixo:
1. Acesse a página do [grupo de segurança](https://console.cloud.tencent.com/vpc/securitygroup) e clique no ID/nome do grupo de segurança vinculado a essa instância para acessar sua página de detalhes.
2. Selecione **Inbound/Outbound rule (Regra de entrada/saída)** e clique em **Add a Rule (Adicionar uma regra)**.
3. Digite o intervalo de endereços IP e a porta a ser aberta, e selecione **Allow (Permitir)** para abrir a porta.
Para mais informações, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).

### Como altero a porta remota padrão de uma instância da CVM?

Para mais informações, consulte [Modificação da porta remota padrão de uma CVM](https://intl.cloud.tencent.com/document/product/213/35376).


### Por que o serviço não pode ser usado após alterar a porta?

Após modificar a porta de serviço, também é necessário abrir a porta correspondente para a Internet no grupo de segurança.

### Quais portas não são permitidas pela Tencent Cloud?

- Por padrão, a porta TCP 25 é bloqueada pela Tencent Cloud. Se você precisar desbloquear essa porta, consulte [Desbloqueio da porta 25](https://intl.cloud.tencent.com/document/product/213/34833).
- Algumas portas apresentam riscos de segurança. Embora essas portas não sejam bloqueadas pela Tencent Cloud, elas serão bloqueadas pelos ISPs e não poderão ser acessadas. Para evitar o bloqueio, recomendamos que você altere as portas e não use as seguintes portas para o listening (estado de espera):
<table>
<tr><th>Protocolo</th><th>Porta bloqueada</th></tr>
<tr><td>TCP</td><td>42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, 9996</td></tr>
<tr><td>UDP</td><td>1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, 135 - 139</td></tr>
</table>


### Por que não posso usar a porta 25 do TCP?
A porta 25 do TCP é a porta de serviço de e-mail padrão. Por motivos de segurança, a porta 25 das instâncias da CVM fica bloqueada por padrão. Se precisar usá-la, consulte [Desbloqueio da porta 25](https://intl.cloud.tencent.com/document/product/213/34833).

