Com base em seus ciclos de vida útil, os discos em nuvem podem ser usados como discos do sistema ou discos de dados de CVMs. Renovar os discos em nuvem no prazo adequado pode evitar a perda de dados causada pela expiração. Recomendamos que você configure lembretes de expiração para dados fundamentais.


## Renovação de discos de dados
- Apenas discos de dados do CBS com modo de faturamento de assinatura mensal permitem renovação.
- Antes da expiração de um disco de dados do CBS, você pode renová-lo para evitar a desmontagem do disco e falhas de leitura/gravação causadas pela expiração.
- Após a expiração de um disco de dados do CBS, mas antes de seu encerramento (dentro de 14 dias após a expiração), você ainda pode restaurá-lo. Se você não renovar o disco a tempo, ele será encerrado e isso poderá ocasionar perda de dados.

### Renovação via API
Você pode usar a API RenewDisk para renovar discos em nuvem elásticos.
