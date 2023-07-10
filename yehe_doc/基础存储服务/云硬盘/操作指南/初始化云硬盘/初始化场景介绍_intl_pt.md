Os discos em nuvem criados pelo console são montados manualmente em seu CVM e usados como discos de dados com o status Online por padrão. Para usar os discos, primeiro é preciso inicializá-los, incluindo a formatação, o particionamento e a criação de sistemas de arquivos. O método de inicialização varia de acordo com o cenário de uso real, conforme mostrado abaixo:
- Se todo o disco for apresentado como uma partição independente (ou seja, não houver vários discos lógicos, como D disk/vdb1 e E disk/vdb2), recomendamos fortemente que você não use partições e crie diretamente o sistema de arquivos em dispositivos vazios.
- Se todo o disco precisar ser apresentado como várias partições lógicas (ou seja, há vários discos lógicos), primeiro é preciso executar o particionamento e, em seguida, criar o sistema de arquivos em uma partição. 

Os estilos comuns de partição de disco são Main Boot Record (MBR) e Guid Partition Table (GPT). Se o formato da partição do disco for alterado após o disco ser colocado em uso, os dados originais do disco serão apagados. Portanto, selecione um estilo de partição apropriado de acordo com as necessidades reais.
Os fundamentos dos dois estilos de partição são mostrados na tabela a seguir:

| Estilo de partição | Capacidade máxima de disco suportada | Quantidade de partições suportadas | Ferramenta de partição |
|---------|---------|---------|---------|
|MBR | 2 TB |<li>4 partições principais</li><li>3 partições principais e 1 partição estendida</li>|Sistema operacional Windows: Gerenciamento do disco</br>Sistema operacional Linux:<ul><li>ferramenta fdisk</li><li>ferramenta parted</li></ul> |
|GPT | 18 EB</br>Atualmente, o disco em nuvem suporta uma capacidade máxima de 32 TB | Sem limite de quantidade de partições | Sistema operacional Windows: Gerenciamento do disco</br>Sistema operacional Linux: ferramenta parted|

Selecione o guia de operações adequado de acordo com a capacidade do disco e o tipo do sistema operacional do CVM:
- Para capacidade de disco inferior a 2 TB:
 - [Inicialização de discos em nuvem (Windows)](https://intl.cloud.tencent.com/document/product/362/31597#Steps)
 - [Inicialização de discos em nuvem (Linux)](https://intl.cloud.tencent.com/document/product/362/31597#Steps)
- Para capacidade de disco maior ou igual a 2 TB:
 - [Inicialização de discos em nuvem (Windows)](https://intl.cloud.tencent.com/document/product/362/31598#Steps)
 - [Inicialização de discos em nuvem (Linux)](https://intl.cloud.tencent.com/document/product/362/31598#Steps)









