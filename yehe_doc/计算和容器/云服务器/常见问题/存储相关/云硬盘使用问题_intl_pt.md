### Como posso exibir o disco de dados?
1. Faça login no [console da CVM](https://console.cloud.tencent.com/cvm).
2. Clique em **Cloud Block Storage** na barra lateral esquerda para acessar a página de gerenciamento dele.
3. Clique no ícone de filtro ao lado do título da coluna **Attribute (Atributo)**, selecione **Data disk (Disco de dados)** e clique em **OK** para exibir todos os discos de dados da região.

### Como ler e gravar o disco de dados NTFS original após a reinstalação do sistema operacional Windows no Linux?
O Windows emprega dois sistemas de arquivos principais, NTFS ou FAT32, já o EXT é o sistema de arquivos do Linux. Quando um sistema operacional é alterado de Windows para Linux após a reinstalação, o disco de dados permanece em seu formato original. Portanto, o sistema pode não conseguir acessar o sistema de arquivos do disco de dados. Nesses casos, será necessário usar um conversor de formato para ler o disco de dados. Para maisdetalhes, consulte [Leitura/gravação de discos de dados NTFS após reinstalar uma CVM do Windows para CVM do Linux](https://intl.cloud.tencent.com/document/product/213/3857).

### Como leio o disco de dados no formato EXT após a reinstalação do sistema operacional Linux no Windows?
O Windows emprega dois sistemas de arquivos principais, NTFS ou FAT32, já o EXT é o sistema de arquivos do Linux. Quando um sistema operacional é alterado de Linux para Windows após a reinstalação, o disco de dados permanece em seu formato original. Portanto, o sistema pode não conseguir acessar o sistema de arquivos do disco de dados. Nesses casos, será necessário usar um conversor de formato para ler o disco de dados. Para maisdetalhes, consulte [Leitura/gravação de discos de dados EXT após reinstalar uma CVM do Linux para CVM do Windows](https://intl.cloud.tencent.com/document/product/213/3856).

### Quais são as diferenças entre o Premium Cloud Storage, o SDD e o Enhanced SSD?

- Premium Cloud Storage: a Tencent Cloud Premium Cloud Storage é um tipo de armazenamento híbrido. Ele adota o mecanismo de cache para fornecer um armazenamento semelhante ao SSD de alto desempenho e emprega um mecanismo distribuído de três cópias para garantir a confiabilidade dos dados. O Premium Cloud Storage é adequado para aplicações de pequeno e médio porte com altos requisitos de confiabilidade de dados e requisitos padrão de desempenho.
- SSD: o SSD usa SSD NVMe como mídia de armazenamento e emprega um mecanismo distribuído de três cópias. Ele oferece armazenamento de alto desempenho com baixa latência, IOPS aleatório alto, E/S de alta taxa de transferência e segurança de dados de até 99,9999999%, tornando-o adequado para aplicações com altos requisitos de desempenho de E/S.
- Enhanced SSD: o Enhanced SSD conta com o mecanismo de armazenamento mais recente da Tencent Cloud, a mídia de armazenamento SSD NVMe e a infraestrutura de rede mais recente. Ele emprega um mecanismo distribuído de três cópias para fornecer armazenamento de alto desempenho com baixa latência, IOPS aleatório alto, E/S de alta taxa de transferência e segurança de dados de até 99,99999999%, tornando-o adequado para aplicações de E/S intensiva com altos requisitos para latência, como bancos de dados e NoSQL de grande porte.


Os preços dos três tipos de discos em nuvem variam de acordo com a região. Você pode escolher o disco em nuvem que melhor se adapta aos requisitos e ao orçamento da sua aplicação. Para mais detalhes de preços, consulte a [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).
Para mais informações sobre os tipos de disco e o desempenho, consulte [Tipos de disco em nuvem](https://intl.cloud.tencent.com/document/product/362/31636).

### Como testar o desempenho do disco?
Recomendamos usar o FIO para realizar teste de estresse e verificação em discos em nuvem. Para mais instruções, consulte [Medida do desempenho de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/6741).

### Quais são as operações mais comuns do disco em nuvem?
Para operações comuns de disco em nuvem, consulte [Visão geral de operação](https://intl.cloud.tencent.com/document/product/362/33140).

### Como verifico o espaço disponível e usado nos discos em nuvem?
Você pode fazer login na instância da CVM para verificar o espaço disponível e usado nos discos em nuvem. Essas informações também podem ser vistas no console da CVM da seguinte forma.
1. Faça login no [console da CVM](https://console.cloud.tencent.com/cvm/instance/index) e acesse a página **Instances (Instâncias)**.
2. Selecione o ID/Nome da instância em questão para acessar a página de detalhes.
3. Clique na guia **Monitoring (Monitoramento)** para exibir o uso de disco da instância:
![](https://main.qcloudimg.com/raw/25270ae80b513d497527a0e9f2af1bac.png)

### Por que o disco em nuvem que criei separadamente foi liberado junto com a minha instância?
Ao montar um disco em nuvem, você pode decidir se ele deve ser liberado com a instância automaticamente. Isso pode ser configurado pelo [console do CBS](https://console.cloud.tencent.com/cvm/cbs/index) ou pela API [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659).

### Como eu particiono e formato um disco em nuvem montado?
Para mais informações, consulte [Inicialização de discos em nuvem (menores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) ou [Inicialização de discos em nuvem (maiores que 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).




