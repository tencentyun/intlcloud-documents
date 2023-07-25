>!If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

## Política de atraso do CBS
<dx-tabs>

::: Discos em nuvem com pagamento conforme o uso

- Depois de parar de usar recursos com pagamento conforme o uso, **encerre-os assim que possível** para evitar a dedução de taxas.
- Como seu consumo real de recursos muda constantemente, poderá haver algumas diferenças no seu saldo definido.

![](https://main.qcloudimg.com/raw/becc841c9f150f7ad781da71278fbed3.png)

### Alertas
<table>
<tr>
<th>Tipo</th><th>Descrição</th>
</tr>
<tr>
<td><b>Alerta de saldo baixo</b></td>
<td>O sistema estima quando o saldo da sua conta ficará zerado com base no valor do saldo atual e no uso dos recursos nas últimas 24 horas. Quando é estimado que o saldo ficará zerado em 5 dias ou menos, um alerta de saldo baixo é enviado ao criador da sua conta do Tencent Cloud e aos colaboradores que habilitaram o envio de mensagens por e-mail, SMS e Message Center.</td>
</tr>
<tr>
<td><b>Alerta de pagamento em atraso</b></td>
<td>Os recursos com pagamento conforme o uso são faturados por hora. Quando o saldo da sua conta ficar negativo (conforme o Ponto 1 na figura acima), um alerta será enviado ao criador da sua conta do Tencent Cloud e aos colaboradores que habilitaram o envio de mensagens por e-mail, SMS e Message Center.</td>
</tr>
</table>

Processamento de pagamento em atraso

- Você pode continuar a usar um disco em nuvem com pagamento conforme o uso por 2 horas a partir do momento em que o saldo da sua conta ficou negativo. Você será cobrado por esse período. Após 2 horas (Ponto 2 na figura acima), os serviços serão suspensos (o disco em nuvem ficará indisponível e apenas armazenará os dados). A cobrança ainda será feita de acordo com o padrão de faturamento (mesmo que o saldo da conta fique negativo) até que os dados sejam completamente apagados.
- Se sua conta do Tencent Cloud apresentar um saldo positivo dentro de 15 dias após os serviços do disco em nuvem terem sido suspensos, ainda será possível restaurar o disco.
- Se o saldo continuar negativo por 15 dias após a suspensão dos discos em nuvem (Ponto 3 na figura acima), nós reaveremos o disco com pagamento conforme o uso. Todos os dados serão apagados e **não poderão ser recuperados**. O criador da conta do Tencent Cloud e todos os colaboradores serão notificados por e-mail, SMS e Message Center.
:::
</dx-tabs>

## [Política de atraso para snapshots](id:SnapshotArrears)
### Congelamento
Após sua conta do Tencent Cloud entrar em débito, os snapshots apresentarão o status **Isolated (Isolado)**. As operações relacionadas a snapshots não serão permitidas, inclusive a criação e reversão de snapshots, replicação intrarregional, políticas de snapshots agendados etc.
- Os snapshots isolados serão mantidos por 30 dias. Se o saldo da sua conta permanecer negativo, todos os snapshots (exceto snapshots de imagem) serão excluídos após esse período.


### Observações
- Mesmo após sua conta entrar em débito, o **tamanho do armazenamento do snapshot que exceder o nível gratuito ainda será cobrado** até ser excluído.
- Após os snapshots serem encerrados, os dados não poderão ser restaurados.
- Quando o pagamento em atraso for efetuado, as operações de snapshots serão automaticamente retomadas.
- Se você não precisar mais de um snapshot, exclua-o para evitar a cobrança de taxas. Para obter mais informações, consulte [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758).


