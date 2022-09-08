## Canais de aquisição de discos em nuvem

O Tencent Cloud disponibiliza duas formas de aquisição de discos em nuvem, por meio do console ou via API. 


### Aquisição diretamente pelo console[](id:CreateDisk)
1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs), selecione uma região e clique em **Create (Criar)**.
2. Configure o tipo e a capacidade do disco em nuvem.
3. Selecione um método de faturamento.
4. Confirme o pedido e efetue o pagamento.
5. O disco em nuvem é criado imediatamente após o pagamento do pedido. O disco em nuvem pode ser usado logo após ter sido montado e inicializado.

### Uso de snapshots para comprar pelo console
Se você quiser salvar os dados do snapshot de um disco de dados em um novo disco por padrão, use o snapshot para criar um disco em nuvem na [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot). Você também pode configurar o parâmetro **Snapshot** para especificar o snapshot de destino para criar um disco quando você [comprá-lo separadamente pelo console](#CreateDisk).
1. Acesse a [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot) no console.
2. Na linha do snapshot de destino, selecione **More (Mais)**>**Create new disk (Criar novo disco)**.
<dx-alert infotype="explain" title="">
3. Configure o tipo e a capacidade do disco em nuvem.
Quando você usa snapshots para criar um disco em nuvem, o tamanho da capacidade não deve ser inferior ao tamanho do snapshot. Se você não especificar a capacidade do disco em nuvem, por padrão, a capacidade será igual à do snapshot.
</dx-alert>
4. Selecione um método de faturamento.
5. Confirme o pedido e efetue o pagamento.
6. O disco em nuvem é criado imediatamente após o pagamento do pedido. O disco em nuvem pode ser usado logo após ter sido montado e inicializado.

### Aquisição junto com um CVM
- Ao comprar um CVM do Tencent Cloud, você também pode adquirir um disco em nuvem não elástico definindo **System Disk (Disco do sistema)** no disco em nuvem. Para obter mais informações, consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855).
- Você pode adquirir um disco em nuvem elástico definindo o parâmetro **Data Disk (Disco de dados)** ao comprar um CVM. Para obter mais informações, consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855).

### Aquisição por API
Você pode usar a API `CreateDisks` para criar um disco em nuvem. Para obter mais informações, consulte [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/16312).

### Canais de aquisição de discos locais
Atualmente, os discos locais podem ser adquiridos apenas quando você compra uma instância do CVM High-IO ou Big-Data, e não podem ser comprados separadamente. Para obter mais informações, consulte [Criação de instâncias](https://intl.cloud.tencent.com/document/product/213/4855).

