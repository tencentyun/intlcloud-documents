## Instâncias do CVM com pagamento conforme o uso

![](https://main.qcloudimg.com/raw/463d6b815dcf2677ebe28f9683d14430.jpg)

### Observações
- Depois de parar de usar recursos com pagamento conforme o uso, **encerre-os assim que possível** para evitar a dedução de taxas.
- Depois que uma instância do CVM for encerrada ou reavida, seus dados serão apagados e não poderão ser recuperados.
- Como seu consumo real de recursos muda constantemente, algumas pequenas discrepâncias podem existir para o saldo declarado no alerta de saldo baixo.

### Alertas

<table>
	<tr><th>Tipo de alerta</th><th>Descrição</th></tr>
	<tr><td><b>Lembrete de pagamento em atraso</b></td><td>Os recursos com pagamento conforme o uso são faturados por hora. Quando o saldo da sua conta ficar negativo, o criador, os colaboradores de recursos globais e os colaboradores financeiros da sua conta do Tencent Cloud serão notificados por e-mail e SMS.</td></tr>
	<tr><td><b>Alerta de pagamento em atraso</b></td><td>Esta funcionalidade está desabilitada por padrão.</td></tr>
</table>

### Política de pagamentos em atraso
Quando o saldo da sua conta ficar negativo, você pode continuar a usar as instâncias do CVM pelas próximas 2 horas. Também continuaremos a faturar esse uso. Após 2 horas, se o saldo da sua conta permanecer negativo, as instâncias do CVM serão encerradas automaticamente e o faturamento será interrompido.
Após o desligamento automático, suas instâncias do CVM passam pelos seguintes estágios:
<table>
	<tr><th>Tempo desde o desligamento</th><th>Descrição</th></tr>
	<tr><td rowspan=2><b>≤ 15 dias</b></td><td>Se sua conta for carregada com um saldo positivo, o faturamento é retomado e você pode continuar a usar suas instâncias do CVM.</td></tr>
	<tr><td>Se o saldo da sua conta permanecer negativo, você não conseguirá iniciar as instâncias do CVM.</td></tr>
	<tr><td><b>> 15 dias</b></td><td>Se sua conta não for carregada com um saldo positivo, seus CVMs com pagamento conforme o uso serão reavidos. Todos os dados serão apagados e não podem ser recuperados. Quando o seu CVM for reavido, o criador e todos os colaboradores da conta do Tencent Cloud serão notificados por e-mail e SMS.</td></tr>
</table>

## Rede com faturamento por tráfego
<table>
	<tr><th>Tipo de alerta</th><th>Descrição</th></tr>
	<tr><td><b>Alerta de saldo</b></td><td>O consumo de tráfego da rede tende a flutuar significativamente e é difícil de prever. Portanto, não oferecemos alertas de saldo.</td></tr>
	<tr><td><b>Alerta de pagamento em atraso</b></td><td>Quando seu saldo ficar negativo, você pode continuar a usar a rede com faturamento por tráfego durante <b>as próximas 2 horas</b>. Também continuaremos a faturar esse uso. Após 2 horas, se o saldo da sua conta permanecer negativo, o serviço da rede com faturamento por tráfego será interrompido automaticamente. </br>Depois que sua conta for carregada com um saldo positivo, o serviço será retomado. Verifique as instâncias do CVM e as instâncias do CLB afetadas e certifique-se de que todas as configurações anteriores foram restauradas.</td></tr>
</table>

>! Para obter informações sobre as taxas de tráfego, consulte o [Faturamento da rede pública](https://intl.cloud.tencent.com/document/product/213/10578).
>
