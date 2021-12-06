>?Não é possível excluir as instâncias com assinatura mensal, mas você pode parar de renová-las após a expiração.

Após confirmar que uma instância do CLB não tem tráfego e não é mais necessária, é possível excluí-la por meio do console ou da API do CLB.
Depois de excluída, a instância do CLB será encerrada totalmente e não poderá ser recuperada. É altamente recomendável desvincular todos os servidores de back-end e observar por um tempo antes de excluir alguma instância.

#### Exclusão de uma instância do CLB pelo console
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Localize a instância do CLB que deseja excluir e clique em **More (Mais)** -> **Delete (Excluir)** na coluna **Operation (Operação)** à direita.
 ![](https://main.qcloudimg.com/raw/693acd714a4335920aea91b3ec4888f9.png)
3. A caixa de diálogo de confirmação será exibida. Após ler o prompt de segurança da operação, clique em **Submit (Enviar)** para confirmar a exclusão.
A caixa de diálogo é conforme mostrado abaixo. É recomendável confirmar a exclusão quando houver **0** regras vinculadas, **nenhuma** instância do CVM vinculada e uma marca verde na coluna **Notes About Operation Security (Observações sobre a segurança da operação)**.                              ![](https://main.qcloudimg.com/raw/e3f3e2f08b4b9c4f61c478762de4b33a.png)

#### Exclusão de uma instância do CLB pela API
Para obter mais informações, consulte [ExcluirBalanceadoresCarga](https://intl.cloud.tencent.com/document/api/214/1257).
