
A Indicação de Nome de Servidor (SNI, na sigla em inglês) foi criada para resolver o problema de que um servidor só pode usar um certificado para melhorar as extensões SSL/TLS do servidor e do cliente. Se um servidor aceita a SNI, significa que ele pode ser vinculado a vários certificados. Para usar a SNI para o cliente, o nome de domínio ao qual se conectar deve ser especificado antes que as conexões SSL/TLS com o servidor sejam estabelecidas. Depois, o servidor retornará um certificado apropriado com base no nome de domínio.

## Casos de uso
Um listener HTTPS da camada 7 do CLB aceita a SNI, ou seja, vincular vários certificados, que podem ser usados por nomes de domínio diferentes nas regras de escuta. Por exemplo, no mesmo listener `HTTPS:443` de uma instância do CLB, você pode usar o certificado 1 e o certificado 2 para `*.test.com` e `*.example.com` respectivamente, a fim de encaminhar solicitações desses nomes de domínio para dois conjuntos diferentes de servidores.

## Pré-requisitos
Você [adquiriu uma instância do CLB](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-k9gii1kb).
>O CLB da rede clássica não permite o encaminhamento com base no nome de domínio e URL; portanto, ele não aceita a SNI.

## Instruções
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. [Configure um listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8) e ative a SNI.
![](https://main.qcloudimg.com/raw/eb6958c5f3772c3b55ab3a2a1e92d341.png)
3. Ao adicionar uma regra de encaminhamento ao listener, configure certificados de servidor diferentes para nomes de domínio diferentes. Depois, clique em **Next (Avançar)** e configure a verificação de integridade e a persistência de sessão.
![](https://main.qcloudimg.com/raw/bf5150f1f263a133770f1ad5694f501c.png)
