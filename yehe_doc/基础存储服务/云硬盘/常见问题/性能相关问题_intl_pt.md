### Como medir o desempenho de um disco em nuvem?
As métricas a seguir costumam ser usadas para descrever o desempenho de um dispositivo de armazenamento:
- IOPS: contagem de leitura/gravação por segundo. O IOPS varia de acordo com o tipo de unidade subjacente do dispositivo de armazenamento.
- Taxa de transferência: volume de dados lidos/gravados por segundo, com unidade em MB/s.
- Latência: tempo decorrido desde o envio de uma operação de E/S até o recebimento da confirmação (em segundos).

### Como testar o desempenho do disco?
Nós recomendamos que você use FIO para realizar a verificação e o teste de pressão no disco em nuvem. Para obter mais informações, consulte [Medição do desempenho de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/6741).

### O tamanho da E/S da leitura-gravação do aplicativo afeta o desempenho de IOPS?
Sim. Para um determinado recurso, o IOPS apresentado é determinado pelo tamanho da E/S das operações de leitura e gravação do aplicativo. Normalmente, quando a leitura e a gravação são feitas em pequenos blocos (por exemplo, tamanho de E/S de 256 KB), o desempenho de IOPS do disco pode ser usado totalmente.

### O tamanho da E/S da leitura-gravação do aplicativo afeta o desempenho da taxa de transferência?
Sim. Para um determinado recurso, a taxa de transferência apresentada é determinada pelo tamanho da E/S das operações de leitura e gravação do aplicativo. Normalmente, quando a leitura e a gravação são feitas em grandes blocos (por exemplo, tamanho de E/S de 1 MB), o desempenho da taxa de transferência do disco pode ser usado totalmente.

### É possível combinar logicamente vários discos em um só disco para ter um desempenho melhor?
Sim. Você pode unir esses vários discos em nuvem que estão montados no CVM para equilibrar a carga de E/S em vários discos, aumentando a capacidade de E/S em paralelo para implementar um desempenho melhor em um único disco. Para obter mais informações, consulte [Criação de volumes lógicos de LVM para vários discos em nuvem elásticos](https://intl.cloud.tencent.com/document/product/362/2933).

