Com vigência em janeiro de 2021, o desempenho de um único disco Enhanced SSD consiste no **desempenho básico** e no **desempenho extra**:
- O desempenho básico varia linearmente com a capacidade do disco em nuvem e atinge o valor máximo no ponto crítico.
- Se você tiver um requisito de desempenho superior, poderá ativar e configurar o desempenho extra.

Este documento apresenta o desempenho básico e o desempenho extra.

## Desempenho geral

Para um único disco Enhanced SSD, seu desempenho consiste em duas partes: o **desempenho básico** e o **desempenho extra**. A tabela a seguir especifica o desempenho máximo, independentemente da proporção de desempenho.

| Métrica de desempenho | Valor máximo |
| --------------------- | ------ |
| IOPS aleatório            | 100.000 |
| Taxa de transferência máx. (MB/s)    | 1.000   |



## Desempenho básico

Para o Enhanced SSD, seu desempenho básico varia linearmente com a capacidade do disco. O desempenho básico não pode ser ajustado independentemente, o que é calculado pela seguinte fórmula.

| Métrica de desempenho básico    | Fórmula de cálculo         | Valor máximo |
| ---------------------------- | --------------------------- | -------------- |
| IOPS aleatório         | mín. {1.800 + capacidade (GB) × 50, 50.000} | 50.000          |
| Taxa de transferência máx. (MB/s) | mín. {120 + capacidade (GB) × 0,5, 350}   | 350            |

De acordo com a fórmula,

- Se a capacidade do disco for 460 GB, a taxa de transferência atinge o valor máximo e seu desempenho básico é: IOPS aleatório: 24.800; taxa de transferência máxima: 350 MB/s.
- Se a capacidade do disco for 964 GB, o IOPS aleatório atinge o valor máximo e seu desempenho básico é: IOPS aleatório: 50.000; taxa de transferência máxima: 350 MB/s.



## Desempenho extra

Se você tiver um requisito de desempenho superior, poderá ativar o desempenho extra.

### Pré-requisitos

Os seguintes requisitos devem ser atendidos para permitir o desempenho extra:

- Atualmente, essa funcionalidade está disponível apenas para os discos **Enhanced SSD** e **Tremendous SSD**.
- O desempenho extra pode ser configurado somente depois que uma das métricas básicas de desempenho atingir seu valor máximo. Em outras palavras, a capacidade do disco deve ser maior que 460 GB de acordo com a fórmula de desempenho básico.

### Fórmula de desempenho extra

Consulte a fórmula a seguir para configurar o desempenho extra.

| Métrica de desempenho extra  | Fórmula de cálculo      | Valor máximo |
| ---------------------------- | --------------------- | -------------- |
| IOPS aleatório         | mín. {valor configurado × 128, 50.000} | 50.000          |
| Taxa de transferência máx. (MB/s) | mín. {valor configurado × 1, 650}     | 650            |

### Preço do desempenho extra
Para obter mais informações sobre os preços de desempenho extra, consulte a [Visão geral de preços](https://intl.cloud.tencent.com/document/product/362/2413).

## Exemplos

**Amostra 1: um disco Enhanced SDD requer uma capacidade de 2.000 GB e uma taxa de transferência de 500 MB/s**

Essa configuração de capacidade atinge o limite da taxa de transferência do desempenho básico e precisa configurar o desempenho de taxa de transferência extra: (500-350)/1 = 150. Portanto, basta adquirir um disco Enhanced SSD com capacidade de 2.000 GB e desempenho de taxa de transferência extra de 150 MB/s.

**Amostra 2: um disco Enhanced SDD requer uma capacidade de 1.000 GB e IOPS de 50.000**
Essa configuração de capacidade atinge o limite de IOPS aleatório de desempenho básico e o IOPS necessário é atendido. Portanto, basta adquirir um disco Enhanced SSD com capacidade de 1.000 GB.
