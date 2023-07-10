## Cenário de operação
Com o Cloud Block Storage (CBS), é possível criar snapshots e salvar os dados do disco em nuvem em um momento específico. O Tencent Cloud cria snapshots de maneira incremental, o que significa que só cria os dados que foram alterados desde o último snapshot. Se o tamanho dos dados alterados for pequeno, a criação do snapshot é rápida. Como os snapshots são criados de forma incremental, a exclusão de snapshots não afeta o uso de nenhum dado do snapshot. Portanto, é possível restaurar seus discos em nuvem usando quaisquer snapshots restantes.
É possível criar um snapshot de um disco em nuvem em qualquer estado, mas o snapshot salvará apenas os dados que já estão gravados no disco em nuvem no momento atual. Quando algum aplicativo ou processo está gravando dados, os dados podem ainda não terem sido salvos no snapshot que está sendo criado. Nesse caso, você pode optar por suspender todas as gravações e criar o snapshot o mais rápido possível ou [desmontar](https://intl.cloud.tencent.com/document/product/362/32400) o disco em nuvem e [montá-lo](https://intl.cloud.tencent.com/document/product/362/32401) mais tarde para garantir a integridade dos dados do snapshot.

## Pré-requisitos
- Você [criou um disco em nuvem](https://intl.cloud.tencent.com/document/product/362/5744).
- Os limites superiores para a quantidade e tamanho total de snapshots na região atual não foram atingidos. Para obter mais informações, consulte os [Limites de uso de snapshots](https://intl.cloud.tencent.com/document/product/362/32406#use-limits-on-snapshot).

## Observações
Um snapshot contém apenas dados que já foram gravados no disco (mas não os dados que estão na memória e ainda não foram gravados no disco) no momento em que o snapshot foi criado. É altamente recomendável desligar a instância ou garantir que os dados da memória já estejam gravados no disco em nuvem e, em seguida, suspender todas as gravações no disco em nuvem antes de criar o snapshot. Para isso, é necessário fazer o seguinte.
### Nível do banco de dados
Para serviços de banco de dados, recomendamos que você bloqueie todas as tabelas em bancos de dados como somente leitura para evitar uma situação em que novos dados sejam gravados no disco em nuvem e não possam ser capturados pelo snapshot que está sendo criado. Usando o MySQL como exemplo, o procedimento é o seguinte:
1. Execute o comando `FLUSH TABLES WITH READ LOCK` para fechar todas as tabelas abertas e use o bloqueio de leitura global para bloquear todas as tabelas em cada banco de dados, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/287ad27cec557a52a3386a60b937dc9b.png)
2. Crie um snapshot para o disco em nuvem.
3. Execute `UNLOCK TABLES` para desbloquear as tabelas, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/8a5fdcb0df254f0f9afcf3ef86679fc0.png)

### Nível do sistema
Para melhor desempenho do sistema, os dados são armazenados no buffer de memória antes de serem gravados no disco em nuvem, quando apropriado. Portanto, ao criar o snapshot, os dados armazenados no buffer de memória e ainda não gravados no disco em nuvem não serão gravados no snapshot nem recuperados dele. Como resultado, ocorre inconsistência de dados.
Para resolver esse problema, execute o comando `sync` para forçar a gravação dos dados no buffer de memória do sistema de arquivos imediatamente no disco em nuvem e, em seguida, evitar que novos dados sejam gravados no disco em nuvem. Se nenhuma mensagem de erro for retornada após a execução do comando, os dados no buffer de memória foram gravados com êxito no disco em nuvem, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/e1b0ac245e325281a0693f7ae43946ff.png)


<span id="CreateSnapshot"></span>
## Procedimento
### Criação de um snapshot no console
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Clique em **Create Snapshot (Criar snapshot)** para o disco em nuvem de destino.
3. Na caixa de diálogo **Create Snapshot (Criar snapshot)** que é exibida, digite o nome do snapshot e clique em **Submit (Enviar)**.

### Criação de um snapshot por API
É possível usar a API CreateSnapshot para criar um snapshot. Para obter mais informações, consulte [CreateSnapshot](https://intl.cloud.tencent.com/document/product/362/15648).
