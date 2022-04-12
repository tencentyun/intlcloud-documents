A funcionalidade Classiclink permite que os recursos baseados na VPC se comuniquem com as CVMs baseadas na rede clássica.  Por exemplo:
+ As CVMs baseadas na rede clássica podem se comunicar com os recursos da VPC, como a CVM, o TencentDB, o CLB da rede privada, o Redis/CMEM etc.
+ Os recursos da VPC só podem acessar as CVMs baseadas na rede clássica, mas não outros recursos na rede clássica, como o TencentDB e o CLB. 
![](https://main.qcloudimg.com/raw/5c4c66605c6ecd04591dfff5236231df.png) 

## Limites de uso
- Uma VPC só pode ser interconectada com a rede clássica **na mesma região**.
- O intervalo de IP da VPC deve estar dentro de `10.0.0.0/16-10.47.0.0/16` (incluindo os subconjuntos); caso contrário, pode haver conflitos de IP que podem causar falha durante a associação e comunicação com as CVMs baseadas na rede clássica.
- Uma CVM baseada na rede clássica só pode ser associado a uma VPC por vez.
- Uma VPC aceita a associação com até 100 CVMs baseadas na rede clássica.
- Depois que as CVMs baseadas na rede clássica são associadas a uma VPC, elas só conseguem se comunicar com os recursos no bloco CIDR principal, e não com os do bloco CIDR secundário da VPC.
- As instâncias do CLB em uma VPC não podem ser vinculadas a da CVM baseado na rede clássica que se interconecta com o mesmo VPC.
- Em situações com o Classiclink, o tráfego da CVM só pode ser roteado para endereços IP privados dentro da VPC, mas não para destinos fora da VPC.
>? O CVM baseado na rede clássica não consegue acessar os recursos de rede pública ou privada fora da VPC atual por meio de dispositivos de rede, como o gateway do VPN, o gateway do Direct Connect, o gateway público, o Peering Connection e o NAT Gateway. Da mesma forma, o par de um gateway do VPN, do gateway do Direct Connect e do Peering Connection não consegue acessar as CVMs baseadas na rede clássica.



## Observações
- Alterar o IP privado de da CVM baseado na rede clássica invalidará sua associação com a VPC, e fará com que as configurações se tornem inválidas. Para associá-los, é necessário adicionar um Classiclink novamente no console da VPC.
- O Classiclink não será afetado por ações tomadas em relação ao CVM, como o isolamento devido a pagamentos em atraso, o isolamento de segurança, a migração a frio, o failover, a modificação de configuração e a troca de sistema operacional.
- O CVM será desassociado automaticamente da VPC se a CVM for retornado.


## Referência
Para mais informações sobre o Classiclink, consulte [Gerenciamento do Classiclink](https://intl.cloud.tencent.com/document/product/215/41419).

