## Visão geral
A porta 53 é a porta aberta do Domain Name Server (DNS). Ele é usado principalmente para definição de nomes de domínio. O DNS atua como um conversor entre o nome de domínio e o endereço IP; portanto, os usuários precisam apenas lembrar o nome do domínio para acessar o site de forma rápida.

O “Classified Catalogue of Telecommunications Businesses (Catálogo classificado de empresas de telecomunicações)” (Edição de 2015) classificou os serviços de definição recursiva de nomes de domínio da Internet como serviços de telecomunicações (Número do código: B26-1). Para gerenciar serviços de nomes de domínio recursivos, é necessário obter a licença de serviços de telecomunicações.

## Políticas e regulamentos relacionados

**1. Os serviços de definição de domínio da Internet não são permitidos sem uma licença comercial.**
Se você ou a sua empresa trabalhar com essa área, deverá solicitar uma “Code and Protocol Conversion License (Licença de conversão de código e protocolo)”. Para detalhes específicos, entre em contato com a administração de telecomunicações local.
**Artigo 46 das “Medidas administrativas para o licenciamento de operações comerciais de telecomunicações”:** quem violar o disposto no parágrafo 1 do artigo 16 e no parágrafo 1 do artigo 28, mediante o qual indiretamente preste serviços de telecomunicações ou preste serviços de telecomunicações para além do âmbito permitido, é punido nos termos do artigo 69 dos “Telecommunications Regulations of the People's Republic of China (Regulamentos das telecomunicações da República Popular da China)”. Em casos de infrações graves, será emitida ordem de suspensão da empresa para retificação, que será incluída na lista de prestadores de serviços de telecomunicações não confiáveis.
**Artigo 36 dos “Regulamentos de nomes de domínio na Internet” do Ministério da Indústria e Tecnologia da Informação”:** para fornecer serviços de definição de nomes de domínio, as empresas devem cumprir as leis, os regulamentos e as normas vigentes, além de possuírem as capacidades técnicas, de serviços, de segurança de rede e informações pertinentes. As empresas devem implementar medidas de segurança de rede e informações, registrar e armazenar logs de definição de nomes de domínio, logs de operação e manutenção, e alterar os registros de acordo com a lei, para garantir a qualidade do serviço de definição e a segurança do sistema de definição. Quando os serviços de telecomunicações estiverem em pauta, as empresas deverão tirar as licenças de operação de telecomunicações de acordo com a lei.
**2. A Tencent Cloud não fornecerá serviços, como acesso ou faturamento, para indivíduos ou entidades que não possuírem licenças comerciais ou declarações ICP para serviços não comerciais de informações da Internet na China Continental.**
**Artigo 24 das “Medidas administrativas para o licenciamento de operações comerciais de telecomunicações”, as empresas de telecomunicações de alto valor agregado e que prestam serviços de acesso devem cumprir o seguinte regulamento:** (Três) Não é permitida a prestação de serviços, como acesso ou faturamento, para entidades ou indivíduos que não obtiveram licenças comerciais ou declarações ICP para serviços não comerciais de informações da Internet na China Continental de acordo com a lei.
Caso você ou sua empresa não trabalhar com **serviços de definição de nomes de domínio da Internet**, recomendamos que você adeque a política do grupo de segurança do seu servidor, e desative a porta 53 por meio de regras de entrada.

## Desativação da porta 53 por meio de regras de entrada

1. Faça login no [console do CVM da Tencent Cloud](https://console.cloud.tencent.com/cvm/index).
2. Na página de gerenciamento de instâncias, selecione a instância em que a porta 53 deve ser desativada e clique em **ID/Name (ID/Nome)**. Observe o exemplo abaixo:
![](https://main.qcloudimg.com/raw/186bd6ec5c69b12b3ea9645ff1dbb22b.png)
3. Na página de detalhes da instância, selecione a guia **Security Groups (Grupos de segurança)** para acessar a página de gerenciamento do grupo de segurança dessa instância. Observe o exemplo abaixo:
![](https://main.qcloudimg.com/raw/7eb1b0b56520701fc8d28a14cfecd7f1.png)
4. No campo **Bound to security group (Vinculada ao grupo de segurança)**, selecione o **Security Group ID/Name (ID/Nome do grupo de segurança)** da regra de entrada que deve ser modificada.
5. Na página **Security Group Rule (Regra do grupo de segurança)**, selecione a guia **Inbound Rule (Regra de entrada)**. Clique em **Add a Rule (Adicionar uma regra)**. Observe o exemplo abaixo.
![](https://main.qcloudimg.com/raw/f1f7f9ce6d3e259e06542bf19d797022.png)
6. Na janela **Add Inbound Rule (Adicionar regra de entrada)**, insira as informações a seguir. Observer o exemplo abaixo:
![Add inbound rules-disable port 53](https://main.qcloudimg.com/raw/f3890575ef22f31f67c0c6902f6df55a.png)
 - Type (Tipo): selecione “Custom (Personalizada)”.
 - Source (Origem): insira “0.0.0.0/0”.
 - Protocol port (Porta de protocolo): insira “UDP:53”.
 - Policy (Política): selecione “Reject (Rejeitar)”.
7. Clique em **Complete (Concluir)** para desativar a porta 53.

## Perguntas frequentes

### O que é o serviço de definição de nomes de domínio da Internet?
A **Definição de nomes de domínio da Internet** estabelece a relação entre um nome de domínio da Internet e seu endereço IP correspondente.
O **Serviço de definição de nomes de domínio da Internet** cria servidores de definições de nomes de domínio e software relacionado na Internet para converter nomes de domínio da Internet em seus endereços IP correspondentes. Existem dois tipos de serviços de definição de nomes de domínio: serviços de definição autoritativa e recursiva.
- Definição autoritativa: esse serviço fornece definição para nomes de domínio raiz, nomes de domínio de nível superior e outros níveis de nomes de domínio.
- Definição recursiva: esse serviço estabelece a correspondência entre os nomes de domínio e os endereços IP consultando o cache local ou o sistema de serviço de definição autoritativa.

O serviço de definição de nomes de domínio da Internet aqui se refere especificamente ao serviço de definição recursiva. Para mais informações, consulte o “Classified Catalogue of Telecommunications Businesses (Catálogo classificado de empresas de telecomunicações)” (Edição 2015): B26-1 Serviços de definição de nomes de domínio da Internet.

 
### Como a desativação da porta 53 por meio de regras de entrada afetará meu servidor?
Se você não trabalha com serviços de definição de nomes de domínio da Internet, desativar a porta 53 por meio de regras de entrada não afetará seu servidor ou seus negócios.

### Uma pessoa pode trabalhar com serviços de definição de nomes de domínio?
Os provedores de serviços de telecomunicações devem ter empresas estabelecidas de acordo com a lei. Uma pessoa não pode trabalhar com esse tipo de serviço. Você deve obter uma “Code and Protocol Conversion License (Licença de conversão de código e protocolo)” antes de trabalhar com serviços de definição de nomes de domínio da Internet. Para mais informações sobre como obter uma licença, entre em contato com o escritório de administração de telecomunicações local.

### Quais são os impactos ao fornecer serviços de definição de nomes de domínio na Internet sem autorização?
De acordo com o artigo 69 dos “Telecommunications Regulations of the People's Republic of China (Regulamentos das telecomunicações da República Popular da China)”: (Um) Quem infringir o artigo 7, parágrafo 3, ou praticar os atos previstos no artigo 58, item 1, em que opere negócios de telecomunicações sem autorização ou opere fora do âmbito permitido, estará sujeito a retificação pelo Ministério da Indústria e Tecnologia da Informação, agência reguladora de telecomunicações da província, região autônoma ou município, incluindo o confisco de renda ilegal e multa entre três a cinco vezes a renda ilegal. Caso não haja prática de renda ilegal ou essa não exceder 50.000 RMB, a penalidade será entre 100.000 RMB e 1.000.000 RMB. Em caso de infração grave, será emitida uma ordem para suspender a empresa para retificação.
