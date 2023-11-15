## Visão geral
A Tencent Cloud aceita [rede clássica e VPC](https://intl.cloud.tencent.com/document/product/215/31807), que oferecem uma diversidade de serviços suaves. Com base nisso, fornecemos serviços mais flexíveis, conforme mostrado abaixo, para ajudá-lo a gerenciar a conectividade de rede com facilidade.
- **Alternância de rede**
  - Alternar da rede clássica para VPC: uma única instância de origem do TencentDB pode ser alternada da rede clássica para VPC.
  - Alternar de VPC A para VPC B: uma única instância de origem do TencentDB pode ser alternada de VPC A para VPC B.
- **IP e porta personalizados)**
  - IP e porta da instância de origem personalizados: o IP e a porta de uma instância de origem podem ser personalizados na página de detalhes da instância no console.
  - IP e porta da instância somente leitura personalizados: o IP e a porta de uma instância somente leitura podem ser personalizados na página de detalhes da instância no console.

## Observações
- A troca de rede pode causar a alteração do IP privado da instância. O IP original se tornará inválido após o término do tempo de tomada de posse. Modifique o IP da instância no cliente imediatamente.
O tempo padrão de tomada de posse para o IP original é de 24 horas e o tempo de tomada de posse mais longo pode ser de 168 horas. Se "Valid Hours of Old IPs (Horas válidas de IPs antigos)" estiver definido como 0 horas, o IP será liberado imediatamente após a alteração da rede.
- A alternância da rede clássica para VPC é irreversível. Após a mudança para VPC, a instância do TencentDB não pode se comunicar com os serviços da Tencent Cloud em outra rede clássica ou VPC.
- Depois de alternar a rede de uma instância de origem, as redes de instâncias somente leitura associadas à instância de origem não serão alternadas automaticamente, ou seja, você precisará alterná-las manualmente.

## Instruções
### Alternância de rede
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para acessar a página de detalhes da instância.
2. Clique em **Switch to VPC (Alternar para VPC)** ou **Change Network (Alterar rede)** após **Network (Rede)** na seção **Basic Info (Informações básicas)**.
3. Na janela pop-up, selecione a sub-rede, a VPC e clique em **OK**.
>?
>- Se não houver um endereço IP especificado, este será atribuído automaticamente pelo sistema.
>- Você só pode selecionar uma VPC na região da instância.
Recomendamos que a VPC onde reside a instância da CVM seja selecionada; caso contrário, a instância da CVM não poderá acessar o TencentDB for MySQL pela rede privada, a menos que uma instância de[conexão pareada](https://intl.cloud.tencent.com/document/product/553/18827) ou de [CCN](https://intl.cloud.tencent.com/document/product/1003/30049) seja criada entre ambas as VPCs.
>
   - **Alternar da rede clássica para VPC**
![](https://main.qcloudimg.com/raw/ba78ed608b83c2f553cb72350b726491.png)
   - **Alternar de VPC A para VPC B)**
![](https://main.qcloudimg.com/raw/d0df57066adb8398e599a6206db7cd56.png)
4. Retorne à página de detalhes da instância, na qual você pode visualizar a rede da instância.
![](https://main.qcloudimg.com/raw/5342a64814664fa784e256ecbd6f934f.png)

### IP e porta personalizados
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Na lista de instâncias, clique em um ID de instância ou em **Manage (Gerenciar)** na coluna **Operation (Operação)** para entrar na página de detalhes da instância.
2. Clique em <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> após **Private Network Address (Endereço de rede privada)** e **Private Port (Porta privada)** na seção **Basic Info (Informações básicas)**.
>!Modificar o endereço e a porta da rede privada afeta os negócios do banco de dados que está sendo acessado.
3. Na janela pop-up, determine o IP, a porta e clique em **OK**.
