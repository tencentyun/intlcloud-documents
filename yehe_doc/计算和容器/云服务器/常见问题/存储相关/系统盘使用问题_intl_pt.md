### Qual é a capacidade padrão de um disco de sistema da CVM?

O disco de sistema de uma nova CVM tem 50 GB de espaço livre por padrão.

### Posso alterar o disco de sistema local de uma CVM para um disco em nuvem?

- Ao adquirir uma instância da CVM,
você pode escolher o tipo de disco desejado para o disco de sistema da CVM.
- Para uma instância da CVM já adquirida,
se a zona de disponibilidade onde a CVM adquirido estiver localizado tiver discos em nuvem disponíveis, você poderá usar a funcionalidade [alterar tipo de mídia do disco](https://intl.cloud.tencent.com/document/product/213/32365) para alterar o disco do sistema local para um disco em nuvem.

### Quais regiões e zonas de disponibilidade permitem a expansão da capacidade do disco de sistema para mais de 50 GB?

Se o disco de sistema for um disco em nuvem, a capacidade do disco poderá ser ajustada para mais de 50 GB em todas as regiões que permitirem snapshots.

### Posso expandir a capacidade do disco de sistema de uma CVM ao reinstalar o sistema operacional?

Depende do tipo de disco de sistema.
**Se o disco de sistema for um disco em nuvem,**
  a capacidade do disco de sistema pode ser aumentada, mas não pode ser diminuída.
**Se o disco de sistema for um disco local,**
  depende do tamanho do disco de sistema.
  - Se a capacidade padrão do disco de sistema da instância adquirida for de 50 GB, não será possível expandir o disco.
  - Para instâncias já adquiridas: se a capacidade do disco de sistema for de 20 GB ou menos, por padrão, será possível expandir o disco em mais 20 GB. Se a capacidade do disco de sistema for superior a 20 GB, por padrão, será possível expandir o disco em mais 50 GB.

### Posso aumentar a capacidade do disco de sistema e reinstalar o sistema operacional para diminuir a capacidade do disco?

A capacidade de um disco de sistema não pode ser reduzida.

### Como posso salvar os dados na instância da CVM e depois expandir a capacidade do disco de sistema?

Para expandir a capacidade do disco de sistema, você pode criar uma imagem e usá-la para reinstalar o sistema operacional.

### Qual é a capacidade do disco de sistema se eu usar uma imagem com menos de 50 GB para criar ou reinstalar a CVM?

A capacidade da imagem não afeta a capacidade do disco de sistema. A capacidade mínima do disco de sistema é de 50 GB.
