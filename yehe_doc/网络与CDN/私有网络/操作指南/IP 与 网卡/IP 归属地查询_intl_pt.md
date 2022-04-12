A funcionalidade de consulta de localização de IP te ajuda a obter informações sobre a localização geográfica e o ISP de um endereço IP público.
Por exemplo, a consulta mostra que o endereço IP `123.123.123.123` está localizado em Pequim e é fornecido pela China Unicom.
>?  
>- Atualmente, a funcionalidade de consulta de localização de IP está em teste beta. Para testá-la, inscreva-se para a elegibilidade beta.
>- No momento, essa funcionalidade está disponível gratuitamente, e nenhum SLA pode ser fornecido. Ela será faturada após a comercialização.

## Casos de uso
- Você pode consultar a localização e o ISP de um endereço IP da CVM de destino e escolher a CVM de origem para se conectar. 
- Você pode consultar a localização real de um IP público que você adquiriu da Tencent Cloud ou de outras plataformas de nuvem.

## Restrições
Atualmente, a consulta de localização de IP está disponível apenas para os endereços IPv4.

## Instruções
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Clique **IP and Interface (IP e interface)** > **IP Location Query (Consulta de localização de IP)** na barra lateral esquerda.
3. Insira um endereço IP para ser consultado e clique em <img src="https://main.qcloudimg.com/raw/38242f38a7e37d681899fe37dfbc6423.png" style="margin:-3px 0px">.
>? Você também pode chamar a API [`DescribeIpGeolocationInfos`](https://intl.cloud.tencent.com/document/product/215/39094) ou [`DescribeIpGeolocationDatabaseUrl`](https://intl.cloud.tencent.com/document/product/215/38901) para consultar a localização do IP.

