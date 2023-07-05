## Limites da conta para a aquisição de instâncias do CVM

- Você precisa criar uma conta do Tencent Cloud. Para obter mais informações, consulte a [Criação de conta do Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985).
- Se você criar um CVM com pagamento conforme o uso, o sistema vai congelar o custo de uma hora de uso do CVM. Certifique-se de que sua conta tenha saldo suficiente para o pedido.

## Limites de uso de instâncias do CVM

- O software virtualizado não pode ser instalado ou virtualizado novamente (como a instalação de VMware ou Hyper-V).
- Não é possível usar placas de som ou montar dispositivos de hardware externos (como unidades flash USB, discos externos e U-keys).
- O gateway público do CVM está disponível apenas no sistema operacional Linux.

## Limites de aquisição de instâncias do CVM

- Para cada usuário, a **cota** de instâncias do CVM com pagamento conforme o uso em cada zona de disponibilidade é 30.
- Para obter mais informações, consulte os [Limites de aquisição](https://intl.cloud.tencent.com/document/product/213/2664).


## Limites de imagens

- Imagens públicas: sem limites de uso.
- Imagens personalizadas: cada região aceita no máximo 10 imagens personalizadas.
- Imagens compartilhadas: cada imagem personalizada pode ser compartilhada com no máximo 50 usuários do Tencent Cloud. As imagens personalizadas só podem ser compartilhadas com contas na mesma região que a conta de origem.
- Para obter mais informações, consulte os [Tipos de imagens](https://intl.cloud.tencent.com/document/product/213/4941).

## Limites de EIP

#### Limites de cota

| Recursos | Limite |
|---------|:---------:|
| Quantidade de EIPs para cada conta do Tencent Cloud em cada região | 20 |
| Quantidade de aquisições diárias de aplicativos de cada conta do Tencent Cloud em cada região | Cota * 2 |
| Quantidade de vezes que os endereços IPs públicos podem ser reatribuídos gratuitamente a cada conta por dia quando um EIP é desvinculado | 10 |

#### Limites de IPs públicos atribuídos ao CVM

Com início em 18 de setembro de 2019, a quantidade máxima de IPs públicos que pode ser vinculada a um único CVM foi alterada com base na configuração da CPU. As cotas são mostradas abaixo:
>? Esse limite não se aplica a instâncias do CVM adquiridas antes das 00:00 de 18 de setembro de 2019. Para essas instâncias, a quantidade de IPs públicos que podem ser associados a cada instância é igual à [quantidade de IPs privados](https://intl.cloud.tencent.com/document/product/576/18527) aceita pelo seu servidor.
>

| Quantidade de CPUs em um CVM | Quantidade máxima de IPs públicos que pode ser vinculada (incluindo IPs públicos e elásticos) |
|---------|---------|
| 1-5 | 2 |
| 6-11 | 3 |
| 12-17 | 4 |
| 18-23 | 5 |
| 24-29 | 6 |
| 30-35 | 7 |
| 36-41 | 8 |
| 42-47 | 9 |
| ≥ 48 | 10 |

## Limites de ENI

Com base nas configurações de CPU e memória, a quantidade de ENIs vinculados a um CVM difere da quantidade de IPs privados vinculados a um ENI. As cotas são mostradas abaixo:
>! A quantidade de endereços IP vinculados a um único ENI indica a quantidade máxima permitida. A cota de EIP não é fornecida com base nesse limite superior, mas com base nos [limites de uso](https://intl.cloud.tencent.com/document/product/213/5733) do EIP.

<dx-tabs>
::: Number\sof\sENIs\sbound\sto\sa\sCVM\sinstance
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Modelo</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Tipo de instância</th>
    <th width="86%" colspan="10" style = "text-align:center;">Quantidade de ENIs</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 núcleo</th>
    <th style = "text-align:center;">CPU: 2 núcleos</th>
    <th style = "text-align:center;">CPU: 4 núcleos</th>
    <th style = "text-align:center;">CPU: 6 núcleos</th>
    <th style = "text-align:center;">CPU: 8 núcleos</th>
    <th style = "text-align:center;">CPU: 10 núcleos</th>
    <th style = "text-align:center;">CPU: 12 núcleos</th>
    <th style = "text-align:center;">CPU: 14 núcleos</th>
    <th style = "text-align:center;">CPU: 16 núcleos</th>
    <th style = "text-align:center;">CPU: &gt;16 núcleos</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Padrão</th>
    <th style="text-align:center">Padrão S5</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão com armazenamento otimizado S5se</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão SA2</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S4</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">Padrão com rede otimizada SN3ne</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S3</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão SA1</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S2</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">Alta E/S</th>
    <th style = "text-align:center;">Alta E/S IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Alta E/S IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">Memória otimizada</th>
    <th  style = "text-align:center;">Memória otimizada M5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Memória otimizada M4</th>
    <td >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Computação</th>
    <th  style = "text-align:center;">Computação otimizada C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação com rede otimizada CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Computação C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Computação C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">Com base na GPU</th>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">Computação de GPU GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Computação de GPU GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">Computação de GPU GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big data</th>
    <th  style = "text-align:center;">Big data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td>8</td>
    <td>8</td>
   </tr>
  </table>
:::
::: Number\sof\sprivate\sIPs\sbound\sto\sa\ssingle\sENI\son\sCVM\sinstances
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">Modelo</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">Tipo de instância</th>
    <th width="86%" colspan="10" style = "text-align:center;">Quantidade de IPs privados vinculados a um único ENI</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU: 1 núcleo</th>
    <th style = "text-align:center;">CPU: 2 núcleos</th>
    <th style = "text-align:center;">CPU: 4 núcleos</th>
    <th style = "text-align:center;">CPU: 6 núcleos</th>
    <th style = "text-align:center;">CPU: 8 núcleos</th>
    <th style = "text-align:center;">CPU: 10 núcleos</th>
    <th style = "text-align:center;">CPU: 12 núcleos</th>
    <th style = "text-align:center;">CPU: 14 núcleos</th>
    <th style = "text-align:center;">CPU: 16 núcleos</th>
    <th style = "text-align:center;">CPU: &gt;16 núcleos</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">Padrão</th>
    <th style="text-align:center">Padrão S5</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão com armazenamento otimizado S5se</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão SA2</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S4</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">Padrão com rede otimizada SN3ne</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S3</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão SA1</th>
    <td >1 GB de memória: 2<br/>&gt;1 GB de memória: 6</td>
    <td >10</td>
    <td >8 GB de memória: 10<br/>16 GB de memória: 20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S2</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Padrão S1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">Alta E/S</th>
    <th style = "text-align:center;">Alta E/S IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Alta E/S IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">Memória otimizada</th>
    <th  style = "text-align:center;">Memória otimizada M5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Memória otimizada M4</th>
    <td >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Memória otimizada M1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">Computação</th>
    <th  style = "text-align:center;">Computação otimizada C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação com rede otimizada CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">Computação C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >Computação C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">Com base na GPU</th>
    <th  style = "text-align:center;">Computação de GPU GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">Computação de GPU GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Computação de GPU GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">Computação de GPU GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Computação de GPU GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">Com base em FPGA</th>
    <th style = "text-align:center;">FPGA acelerado FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">Big data</th>
    <th  style = "text-align:center;">Big data D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big data D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">Big data D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">Máquina física na nuvem 2.0</th>
    <td colspan="10" style = "text-align:center;">Não compatível</td>
   </tr>
  </table>
:::
</dx-tabs>


## Limites de largura de banda

- Largura de banda máxima de saída (largura de banda downstream)
 - As seguintes regras se aplicam a instâncias criadas antes das 00:00 de 24 de fevereiro de 2020: 
<table>
<tr><th rowspan="2">Método de faturamento da rede</th><th colspan="2">Instância</th><th rowspan="2">Intervalo máximo de largura de banda (Mbps)</th></tr>
<tr><th>Método de faturamento da instância</th><th>Configuração da instância</th></tr>
<tr><td>Faturamento por tráfego</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Faturamento por largura de banda</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Pacote de largura de banda</td><td colspan="2">Todas</td><td>0-2000</td></tr>
</table>

 - As seguintes regras se aplicam a instâncias criadas após as 00:00 de 24 de fevereiro de 2020:
<table>
<tr><th rowspan="2">Método de faturamento da rede</th><th colspan="2">Instância</th><th rowspan="2">Intervalo máximo de largura de banda (Mbps)</th></tr>
<tr><th style="width: 18.5607%;">Método de faturamento da instância</th><th style="width: 24.5814%;">Configuração da instância</th></tr>
<tr><td>Faturamento por tráfego</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Faturamento por largura de banda</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Pacote de largura de banda</td><td colspan="2">Todas</td><td>0-2000</td></tr>
</table>

- Largura de banda máxima de entrada (largura de banda upstream)
	- Se a largura de banda fixa que você adquiriu for superior a 10 Mbps, o Tencent Cloud atribuirá uma largura de banda de entrada da rede pública igual à largura de banda adquirida.
	- Se a largura de banda fixa que você adquiriu for inferior a 10 Mbps, o Tencent Cloud atribuirá uma largura de banda de entrada da rede pública de 10 Mbps.

## Limites de disco

<table>
	<tr><th>Limitações</th><th>Descrição</th></tr>
	<tr><td>Capacidade de disco em nuvem elástico</td><td>A partir de maio de 2018, todos os discos de dados adquiridos com CVMs são discos em nuvem elásticos, que podem ser desmontados e remontados nos CVMs. Essa funcionalidade é compatível com todas as <a href="https://intl.cloud.tencent.com/document/product/213/35071">zonas de disponibilidade</a>.</td></tr>
	<tr><td>Desempenho do disco em nuvem elástico</td><td>A especificação de E/S se aplica ao desempenho de entrada e saída ao mesmo tempo.<br/>Por exemplo, se um SSD de 1 TB tiver um IOPS aleatório máximo de 26.000, isso significa que seu desempenho de leitura e gravação pode atingir esse valor. Devido aos limites de desempenho, se o tamanho do bloco nesse exemplo for 4 KB ou 8 KB, o IOPS máximo pode ser atingido. Se o tamanho do bloco for 16 KB, o IOPS máximo não pode ser atingido (a taxa de transferência já atingiu o limite de 260 MB/s.)</td></tr>
	<tr><td>Quantidade de discos em nuvem elásticos montados em um CVM</td><td>Um máximo de 20</td></tr>
	<tr><td>Quantidade de snapshots em uma região</td><td>64 + Quantidade de discos em nuvem na região x 64</td></tr>
	<tr><td>Discos em nuvem montados em um CVM</td><td>O CVM e os discos em nuvem devem estar na mesma zona de disponibilidade.</td></tr>
	<tr><td>Reversão do snapshot</td><td>Os dados do snapshot só podem ser revertidos para o disco em nuvem onde o snapshot foi criado.</td></tr>
	<tr><td>Tipo de discos em nuvem que pode ser criado usando snapshots</td><td>Apenas snapshots de discos de dados podem ser usados para criar discos em nuvem elásticos.</td></tr>
	<tr><td>Tamanho dos discos em nuvem criados usando snapshots</td><td>O tamanho dos discos em nuvem criados usando snapshots deve ser maior ou igual ao do disco em nuvem de origem.</td></tr>
</table>


## Limites de grupos de segurança

- Os grupos de segurança são específicos da região. Um CVM só pode ser vinculado a grupos de segurança na mesma região.
- Os grupos de segurança são aplicáveis a instâncias do CVM em todos os [ambientes de rede](https://intl.cloud.tencent.com/document/product/213/5227).
- Cada usuário pode configurar no máximo 50 grupos de segurança para cada projeto em uma região.
- É possível configurar, no máximo, 100 regras de entrada ou saída para um grupo de segurança.
- Um CVM pode ser associado a vários grupos de segurança e um grupo de segurança pode ser associado a várias instâncias do CVM.
- Os grupos de segurança associados a CVMs na **rede clássica** não podem filtrar pacotes de ou para bancos de dados TencentDB (MySQL, MariaDB, SQL Server ou PostgreSQL) e NoSQL (Redis ou Memcached). Em vez disso, é possível usar iptables para filtrar o tráfego para tais instâncias.
- As cotas são mostradas abaixo:
<table>
<tr><th>Item</th><th>Limite</th></tr>
<tr><td>Quantidade de grupos de segurança</td><td>50 por região</td></tr>
<tr><td>Quantidade de regras em um grupo de segurança</td><td>100 para regras de entrada e 100 para regras de saída</td></tr>
<tr><td>Quantidade de instâncias do CVM associadas a um grupo de segurança</td><td>2.000</td></tr>
<tr><td>Quantidade de grupos de segurança associados a uma instância do CVM</td><td>5</td></tr>
<tr><td>Quantidade de grupos de segurança que podem ser referenciados por um grupo de segurança</td><td>10</td></tr>
</table>

## Limites de VPC

| Recurso | Limite |
|---------|---------|
| Quantidade de VPCs por região para cada conta | 20 |
| Quantidade de sub-redes por VPC | 100 |
| Quantidade de CVMs baseados na rede clássica que podem ser associados a cada instância do VPC | 100 |
| Quantidade de tabelas de rotas por VPC | 10 |
| Quantidade de tabelas de rotas associadas a cada sub-rede | 1 |
| Quantidade de políticas de roteamento por tabela de rotas | 50 |
| Quantidade de HAVIPs padrão por VPC | 10 |

