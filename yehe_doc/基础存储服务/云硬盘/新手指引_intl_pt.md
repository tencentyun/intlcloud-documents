## 1. Princípios básicos do CBS
- [Visão geral](https://intl.cloud.tencent.com/document/product/362/2345)
- [Vantagens do produto](https://intl.cloud.tencent.com/document/product/362/3039)
- [Tipos de disco em nuvem](https://intl.cloud.tencent.com/document/product/362/31636)
- [Casos de uso](https://intl.cloud.tencent.com/document/product/362/3065)
- [Limites de uso](https://intl.cloud.tencent.com/document/product/362/32406)

## 2. Modos de faturamento do CBS
O Tencent Cloud CBS permite os modos de faturamento de **assinatura mensal** e **pagamento conforme o uso**. Você precisa conhecer esses dois modos de faturamento para selecionar a solução de faturamento ideal. Para obter mais informações, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/362/32415).

## 3. Snapshots
Snapshots são métodos práticos e eficientes de proteção dos dados. Recomendamos que você crie snapshots para os discos em nuvem antes de realizar grandes alterações empresariais. Se ocorrer algum erro com uma alteração empresarial, os snapshots poderão ser usados para restaurar os dados rapidamente. Para obter mais informações, consulte [Visão geral de snapshots](https://intl.cloud.tencent.com/document/product/362/31638).


## 4. Introdução
#### 4.1 Registro e autenticação.
Antes de usar o Tencent Cloud CBS, crie uma [conta do Tencent Cloud](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) e conclua a [verificação de identidade](https://intl.cloud.tencent.com/document/product/378/3629).

#### 4.2 Criação de disco em nuvem
Após o registro e a verificação de identidade, você pode selecionar um tipo de disco em nuvem, a capacidade, o modo de faturamento, o período de retenção, a renovação automática e a expiração ou proteção contra atrasos com base nos requisitos da zona de disponibilidade, na qual seu CVM está localizado, para criar discos em nuvem. Para obter mais informações, consulte [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31647).

#### 4.3 Uso de discos em nuvem
Após criar discos em nuvem, você precisa montar os discos em nuvem adquiridos separadamente nos CVMs na mesma zona de disponibilidade e inicializar os discos. Para obter mais informações, consulte os documentos a seguir:
- [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/39991)
- [Inicialização de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31645)

#### 4.4 Criação de snapshots (opcional)
Após criar discos em nuvem, você pode usar snapshots para fazer backup manualmente ou periodicamente de dados de negócios importantes, para evitar perda de dados ou danos causados por falhas operacionais, ataques, vírus etc. Para obter mais informações, consulte [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755) e [Snapshot agendado](https://intl.cloud.tencent.com/document/product/362/35238).



## 5. Visão geral das funcionalidades do console

| Funcionalidades | Referência |
|---------|---------|
| Criar discos em nuvem usando diferentes métodos. | [Criação de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/5744) |
| Montar um disco em nuvem em um CVM que esteja na mesma zona de disponibilidade e configurar a montagem automática do disco em nuvem. | [Montagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32401) |
| Inicializar discos em nuvem com base nos requisitos reais. | [Cenários de inicialização](https://intl.cloud.tencent.com/document/product/362/31596) |
| Expandir discos em nuvem para adicionar espaço de armazenamento. | [Cenários de expansão de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/31600) |
| Desmontar discos em nuvem e montá-los em outros CVMs. | [Desmontagem de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32400) |
| Encerrar ou devolver um disco em nuvem. | [Encerramento de discos em nuvem](https://intl.cloud.tencent.com/document/product/362/32399) |
| Criar o snapshot de um disco em nuvem em um determinado ponto temporal para salvar os dados do disco em nuvem existentes naquele momento. | [Criação de snapshots](https://intl.cloud.tencent.com/document/product/362/5755) |
| Usar uma política de snapshot agendado para fazer backup dos dados de forma flexível. | [Snapshots agendados](https://intl.cloud.tencent.com/document/product/362/35238) |
| Excluir snapshots desnecessários. | [Exclusão de snapshots](https://intl.cloud.tencent.com/document/product/362/5758) |
| Reverter o estado de um disco em nuvem usando um snapshot para restaurar os dados existentes no momento da criação do snapshot. | [Reversão usando snapshots](https://intl.cloud.tencent.com/document/product/362/5756) |

## 6. Perguntas frequentes
#### Uso do CBS
- [Quais são os cenários aplicáveis a diferentes tipos de discos em nuvem?](https://intl.cloud.tencent.com/document/product/362/32409)
- [Como eu posso ver os detalhes de um disco em nuvem?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.A6.82.E4.BD.95.E6.9F.A5.E7.9C.8B.E4.BA.91.E7.A1.AC.E7.9B.98.E8.AF.A6.E7.BB.86.E4.BF.A1.E6.81.AF.EF.BC.9F)
- [É possível acessar um disco em nuvem por meio de CVMs?](https://intl.cloud.tencent.com/document/product/362/32409#.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E5.A4.9A.E4.B8.AA.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.AE.BF.E9.97.AE.E5.90.8C.E4.B8.80.E5.9D.97.E4.BA.91.E7.A1.AC.E7.9B.98.EF.BC.9F)
- [Por que o disco em nuvem separado que eu criei foi liberado junto com minha instância?](https://intl.cloud.tencent.com/document/product/362/32409#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.88.91.E5.8D.95.E7.8B.AC.E5.88.9B.E5.BB.BA.E7.9A.84.E4.BA.91.E7.A1.AC.E7.9B.98.E5.92.8C.E6.88.91.E7.9A.84.E5.AE.9E.E4.BE.8B.E4.B8.80.E8.B5.B7.E9.87.8A.E6.94.BE.E4.BA.86.EF.BC.9F)
- [Eu posso alterar o tipo de disco em nuvem após a aquisição?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.9C.A8.E6.88.90.E5.8A.9F.E8.B4.AD.E4.B9.B0.E5.90.8E.EF.BC.8C.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E6.9B.B4.E6.8D.A2.E4.BA.91.E7.A1.AC.E7.9B.98.E7.9A.84.E7.B1.BB.E5.9E.8B.EF.BC.9F)
- [Posso particionar meu disco do sistema?](https://intl.cloud.tencent.com/document/product/362/32409#.E7.B3.BB.E7.BB.9F.E7.9B.98.E8.83.BD.E5.90.A6.E8.BF.9B.E8.A1.8C.E5.88.86.E5.8C.BA.E6.93.8D.E4.BD.9C.EF.BC.9F)


#### Perguntas frequentes sobre snapshots
- [Quais são as diferenças entre snapshots e imagens?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Por que eu não posso excluir um snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Eu preciso desligar o CVM para fazer a reversão usando um snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Quando eu encerrar um disco em nuvem, os respectivos snapshots também serão excluídos?](https://intl.cloud.tencent.com/document/product/362/17820)


## 7. Feedback e sugestões
Se você tiver dúvidas ou sugestões ao utilizar os produtos e serviços do Tencent Cloud CBS, envie seu feedback pelos canais a seguir. Uma equipe especializada entrará em contato com você para resolver seus problemas.

- Se você encontrar problemas na documentação de um produto, como links, conteúdo ou erros de API, clique em **Send Feedback (Enviar feedback)** na parte inferior do documento para selecionar o conteúdo que apresenta problemas.
- Se você encontrar problemas relacionados ao produto, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar ajuda.
