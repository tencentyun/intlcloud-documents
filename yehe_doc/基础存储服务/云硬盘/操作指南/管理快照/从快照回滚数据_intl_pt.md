Reverter os dados do snapshot para um disco em nuvem pode recuperar os dados do disco para o estado em que o snapshot foi criado. Esse método é muito útil em caso de erros de dados ou perdas de dados causados por determinadas alterações.

Os snapshots só podem ser revertidos para o disco em nuvem em que foram criados. Se você precisar obter dados de snapshots de outros discos em nuvem, use o serviço de [Criação de um disco em nuvem de um snapshot](/doc/product/362/5757).

Observação:

- Quando você reverte um snapshot para um disco em nuvem elástico, o disco deve ser desmontado.
- Quando você reverte um snapshot para um disco em nuvem não elástico adquirido com um CVM, a instância do CVM deve ser encerrada.

## Reversão de um snapshot no console
1) Abra o [Console do CVM](https://console.cloud.tencent.com/cvm/).

2) Clique em "Snapshot" no painel de navegação.

3) Selecione o snapshot que precisa ser revertido para o disco na lista de snapshots e clique em "Rollback (Reverter)".

## Reversão de um snapshot por uma API
É possível usar a API [`ApplySnapshot`](https://intl.cloud.tencent.com/zh/document/product/362/15643) para reverter um snapshot.
