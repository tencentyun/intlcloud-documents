## Casos de uso de modelo de parâmetros
O modelo de parâmetros é uma maneira eficiente, rápida e de fácil manutenção para adicionar regras em grupos de segurança. Por exemplo, quando você precisa adicionar vários intervalos de IP, IPs especificados ou portas de protocolo de vários tipos, é possível definir um modelo de parâmetros. Você também pode usar o modelo de parâmetros posteriormente para manter as origens de IP e as portas de protocolo nas regras de grupo de segurança.
>?Todos os endereços IP e as portas de protocolo neste documento são exemplos. Substitua-os de acordo com as suas condições reais de negócios durante a configuração.
>


## Descrição do exemplo
Suponha que você queira configurar as seguintes regras de grupo de segurança e precise atualizar o intervalo de IP de origem de entrada e a porta de protocolo posteriormente:
+ Regras de entrada:
 + Intervalo de IP de origem permitido: 10.0.0.16-10.0.0.30; porta de protocolo: TCP:80,443
 + Bloco CIDR de origem permitido: 192.168.3.0/24; porta de protocolo: TCP:3600-15000

+ Regras de saída:
 Endereço IP de destino rejeitado: 192.168.10.4; porta de protocolo: TCP:800


## Solução
Como você tem a mesma política de grupo de segurança para vários intervalos de IP e portas de protocolo, e precisa atualizar o intervalo de IP de origem posteriormente, é possível usar um modelo de parâmetros para implementar a adição e manutenção de regras de grupo de segurança.



### Etapa 1. Criar um modelo de parâmetros
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Security (Segurança)** >**Parameter Template (Modelo de parâmetros)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na guia **IP Address (Endereço IP)**, clique em **+ New (+ Novo)** para criar um modelo de parâmetros de endereço IP para adicionar regras de entrada e de saída.
4. Na janela pop-up, insira o intervalo de IP de origem e clique em **Submit (Enviar)**.</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/581bf5c79ec186d05290c8ab73138338.png" width="45%" />
</br>
O modelo de parâmetros de endereço IP recém-criado é mostrado abaixo.
<img src="https://qcloudimg.tencent-cloud.cn/raw/67f474a18a1f4cca9001995700d80559.png" >
5. Na guia **Protocol Port (Porta de protocolo)**, clique em **+ New (+ Novo)** para criar um modelo de parâmetros de porta de protocolo para adicionar regras de entrada e de saída.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fa453b19c81e823dee3afc0e5b473d72.png" width="45%" /> 
</br>
O modelo de parâmetros de porta de protocolo recém-criado é mostrado abaixo:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce16cdc7fdbeec0f3117ca4c8e3a863.png" >

### Etapa 2. Adicionar uma regra de grupo de segurança
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc).
2. Selecione **Security (Segurança)** >**Security Group (Grupo de segurança)** na barra lateral esquerda, para acessar a página de gerenciamento.
3. Na lista, localize o grupo de segurança que precisa importar o modelo de parâmetros e clique em seu ID para acessar a página de detalhes.
4. Na guia **Inbound/Outbound Rules (Regras de entrada/saída)**, clique em **Add Rule (Adicionar regra)**.
5. Na janela pop-up, selecione o tipo “personalizada”, selecione o modelo de parâmetros de endereço IP correspondente da origem/destino, selecione o modelo de parâmetros de porta de protocolo correspondente da porta de protocolo e clique em **Complete (Concluir)**.
![](https://qcloudimg.tencent-cloud.cn/raw/9039d1de4a8a2891873faaec92627fee.png)

	
### Etapa 3. Atualizar o modelo de parâmetros
Suponha que você precise adicionar uma regra de entrada com a origem de IP sendo o intervalo de IP `10.0.1.0/27` e a porta de protocolo sendo `UDP:58`. Você pode atualizar diretamente os modelos de parâmetros do endereço IP `ipm-0ge3ob8e` e da porta de protocolo `ppm-4ty1ck3i`.
1. Na guia **IP Address (Endereço IP)** do modelo de parâmetros, localize o modelo de parâmetros `ipm-0ge3ob8e`.
2. Clique em **Edit (Editar)** à direita.
![](https://qcloudimg.tencent-cloud.cn/raw/f7f28bf7fdb77f25c6c1e2fbf5555809.png)
3. Na janela pop-up, adicione o intervalo de IP `10.0.1.0/27` em uma nova linha e clique em **Submit (Enviar)**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0be07de1ae0e9858ec94327cb0b3ba75.png" width="45%" />
4. Na guia **Protocol Port (Porta de protocolo)** do modelo de parâmetros, localize o modelo de parâmetros `ppm-4ty1ck3i`.
5. Clique em **Edit (Editar)** à direita.
![](https://qcloudimg.tencent-cloud.cn/raw/9ba28cdac71dbded7259eee9e74d128a.png)
6. Na janela pop-up, adicione a porta de protocolo de entrada `UDP:58` em uma nova linha e clique em **Submit (Enviar)**.</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b4f15b9ef711caae75920b2f70780667.png" width="45%" />
