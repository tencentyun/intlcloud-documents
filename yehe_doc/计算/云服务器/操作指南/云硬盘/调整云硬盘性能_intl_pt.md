
O desempenho de um disco em nuvem depende da capacidade dele. É possível melhorar o desempenho ajustando a capacidade dele até atingir o teto. Quando o teto é atingido, é possível adquirir um desempenho extra para obter um desempenho ainda maior. Observe que o desempenho extra está disponível apenas para as instâncias de SSD aprimorado. Para obter mais informações, consulte [Desempenho do SSD aprimorado](https://intl.cloud.tencent.com/document/product/362/39611).
>!
>- Atualmente, apenas o **SSD aprimorado** é compatível com ajustes de desempenho independentes.
>- O [desempenho extra](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) pode ser ajustado de forma independente apenas depois que o [desempenho básico](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD) atingir o teto.
>- O ajuste de desempenho não afetará o funcionamento de seus discos em nuvem e seus negócios.



## Faturamento do ajuste de desempenho

### Upgrade

- Para discos em nuvem com pagamento conforme o uso, o upgrade de desempenho entra em vigor imediatamente e os discos em nuvem já começam a serem cobrados pela nova configuração.

### Downgrade


- Para discos em nuvem com pagamento conforme o uso, o upgrade de desempenho entra em vigor imediatamente e os discos em nuvem já começam a serem cobrados pela nova configuração.

## Upgrade de desempenho

#### Upgrade de um disco pelo console
Quando os pré-requisitos são atendidos, é possível fazer o upgrade de um disco conforme as instruções abaixo no console: 

1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Selecione a região e o disco em nuvem que requer ajuste de desempenho.
3. Clique em **More (Mais)** > **Adjust Performance (Ajustar desempenho)** na coluna **Operation (Operação)** do disco em nuvem selecionado.
4. Selecione uma configuração de destino na janela pop-up.
5. Leia e confirme as observações e inicie o ajuste.

#### Upgrade de um disco por API
Também é possível usar a API `ModifyDiskExtraPerformance` para fazer o upgrade de um disco em nuvem especificado. Para obter direções detalhadas, consulte [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).


## Downgrade de desempenho

#### Downgrade de um disco pelo console
Quando os pré-requisitos são atendidos, é possível fazer o downgrade de um disco conforme as instruções abaixo no console:

1. Faça login no [Console do CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Selecione a região e o disco em nuvem que requer ajuste de desempenho.
3. Clique em **More (Mais)** > **Adjust Performance (Ajustar desempenho)** na coluna **Operation (Operação)** do disco em nuvem selecionado.
4. Selecione uma configuração de destino na janela pop-up.
5. Leia e confirme as observações e inicie o ajuste.

#### Downgrade de um disco por API
Também é possível usar a API `ModifyDiskExtraPerformance` para fazer o downgrade de um disco em nuvem especificado. Para obter direções detalhadas, consulte [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).

