## Visão geral

O IP público elástico, ou EIP, é um IP estático projetado para computação em nuvem dinâmica e um IP público fixo em uma determinada região. Com o EIP, é possível mapear rapidamente um endereço para outra instância (ou instância do NAT Gateway) da sua conta para evitar falhas de instância.

Você pode manter o EIP na sua conta até que seja liberado. Embora o IP público só possa ser liberado com o CVM, o EIP pode ser dissociado do ciclo de vida do CVM e operar de forma independente como um recurso em nuvem. Por exemplo, caso precise manter um IP público que esteja fortemente relacionado à sua empresa, você pode convertê-lo em um EIP e mantê-lo em sua conta.

## Regras e limites

### Regras de uso

- Um endereço EIP é aplicado simultaneamente a instâncias em redes básicas e VPCs, bem como a instâncias do [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) em VPCs.
- Quando um EIP estiver vinculado à uma instância do CVM, o IP público vigente da instância será liberado.
- Quando uma instância do NAT Gateway/CVM for encerrada, ocorrerá a desassociação entre a instância e o EIP.
- Para obter mais detalhes acerca das regras de faturamento do EIP, consulte [Faturamento do IP público elástico](https://intl.cloud.tencent.com/document/product/213/17156).
- Para obter os procedimentos detalhados dos EIPs, consulte [IP público elástico](https://intl.cloud.tencent.com/document/product/213/16586).
 
### Limites de cota

| Recurso            | Limite         |
|---------|:---------:|
| Cota do EIP para cada conta do Tencent Cloud em cada região | 20 |
| Quantidade de aquisições diárias de aplicativos de cada conta do Tencent Cloud em cada região | Cota \* 2 vezes |
| Quantidade de vezes que os IPs públicos podem ser reatribuídos gratuitamente a cada conta por dia quando um EIP é desvinculado | 10 vezes |

> O ajuste da cota do EIP não é permitido por padrão. É possível realizar a convergência de IP por meio do [NAT Gateway](https://intl.cloud.tencent.com/product/nat) e do [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
> - Caso precise ajustar a cota de EIP, sua conta deverá ter a quantidade correspondente de recursos do CVM disponíveis para uso.
> - Se for necessária uma cota maior, poderá ter a incidência de taxas.
> - Caso altere o IP com frequência ou viole as leis aplicáveis após o ajuste, o Tencent Cloud tem o direito de revogar a cota.
>


### Limites de IPs públicos atribuídos ao CVM

Desde 18 de setembro de 2019 (inclusive), a quantidade máxima de IPs públicos que pode ser vinculada a um único CVM foi alterada com base na configuração da CPU.
> Esse limite não se aplica aos CVMs adquiridos antes da 0h de 18 de setembro de 2019.
>
| Quantidade de CPUs do CVM | Quantidade máxima de IPs públicos que pode ser vinculada a um CVM (incluindo IPs públicos e EIPs) |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



