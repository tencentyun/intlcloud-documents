## 1\. CONSIDERAÇÕES INICIAIS

Esse Módulo se aplica se você usar o recurso Cloud Streaming Services (“**Recurso**”). Esse módulo está incorporado ao Contrato de Segurança e Processamento de Dados localizado no [DPSA](https://intl.cloud.tencent.com/document/product/301/17347). Os termos utilizados, mas não definidos nesse Módulo, devem ter o significado dado a eles no DPSA. No caso de qualquer conflito entre o DPSA e esse Módulo, esse Módulo será aplicado conforme a inconsistência.

## 2\. PROCESSAMENTO

Processaremos os seguintes dados em conexão com o Recurso:

| **Informações Pessoais**                                     | **Uso**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Dados de configuração:**<li>Configuração de nome de domínio (configurar autenticação, configuração de limite de largura de banda, configuração https (incluindo certificado SSL), configuração de região, configurar modelo, configuração de servidor de origem);<br><li>Modelo de gravação \[nome do modelo, formato de arquivo de gravação, duração de arquivo único de gravação, período de retenção, tempo limite de retomada (somente para hls), subaplicativo Record to VOD (gravar no vídeo sob demanda)\];<br><li>Modelo de marca d'água (nome do modelo, imagem da marca d'água, local da marca d'água);<br><li>Modelo de transcodificação (nome do modelo, taxa de bits, altura da tela ao vivo, GOP, método de codificação);<br><li>Modelo de captura de tela (nome do modelo, frequência de captura de tela, localização do armazenamento de captura de tela, nome do arquivo de captura de tela, detecção inteligente de pornografia). | Apenas processamos esses dados com a finalidade de fornecer o Recurso a você e a seus usuários finais, conforme sua configuração específica.<br/>Observe que esses dados estão armazenados em nosso recurso TencentDB for MySQL. |
| **Gravação de vídeos ao vivo** (se você optar por gravar vídeos de transmissões ao vivo) | Apenas processamos esses dados com a finalidade de fornecer o Recurso para você.<br/>Observe que esses dados são armazenados em nosso recurso Video on Demand (VOD). |
| **Capturas de tela ao vivo** (se você optar por gravar capturas de tela ao vivo), incluindo as capturas de tela ao vivo resultantes após a detecção de pornografia (se você optar por ativar a função de configuração de detecção de pornografia) | Apenas processamos esses dados com a finalidade de fornecer o Recurso para você.<br/>Observe que esses dados são armazenados em nosso recurso Cloud Object Storage (COS) .<br/>Observe que se você habilitar a função de configuração de detecção de pornografia desse Recurso, esses dados armazenados no COS serão transmitidos para nosso recurso Image Moderation System (Sistema de Moderação de Imagem, IMS), a fim de fornecer esse Recurso conforme necessário (inclusive para revisar e identificar informações e retornar resultados sobre o mesmo). O IMS irá reter as capturas de tela ao vivo apenas pelo tempo necessário para concluir o processo de detecção de pornografia e retornar os resultados referentes ao mesmo para você. |


## 3\. REGIÃO DO SERVIÇO

Conforme especificado no DPSA.

## 4\. SUBPROCESSADORES

Como especificado no DPSA, incluindo Aceville Pte. Ltd.

## 5\. RETENÇÃO DE DADOS

Armazenaremos dados pessoais processados em conexão com o Recurso da seguinte forma:

| **Informações Pessoais**                                | **Política de Retenção**                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Dados de configuração Gravação de vídeos ao vivo Captura de tela ao vivo | Retemos os dados de acordo com o seu limite de tempo de retenção de dados escolhido. Caso contrário, quando você excluir sua conta ou encerrar o seu uso do Recurso, nós vamos excluir esses dados após 60 dias. |

Você pode solicitar a exclusão desses dados pessoais de acordo com o DPSA.

## 6\. CONDIÇÕES ESPECIAIS

Você deve garantir que este Recurso seja usado apenas por usuários finais que têm, pelo menos, a idade mínima para que um indivíduo possa consentir com o processamento de seus dados pessoais ou com o consentimento dos pais obtido para pessoas com idade inferior à mínima exigida. Pode haver diferenças dependendo da jurisdição em que o usuário final está localizado.

Você declara, garante e assume que deve obter e manter todos os consentimentos necessários dos Usuários Finais em relação ao processamento dos dados pessoais deles em relação ao Recurso, de acordo com as leis aplicáveis e de modo a nos permitir cumprir essas leis.  