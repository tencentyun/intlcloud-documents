## O que é o Tencent Cloud Block Storage?
O Cloud Block Storage (CBS) é um dispositivo de armazenamento em blocos altamente disponível, confiável, de baixo custo e personalizável. Ele pode ser usado como um disco autônomo e expansível para o CVM, fornecendo dispositivos de [armazenamento](https://intl.cloud.tencent.com/document/product/213/4952) eficientes e confiáveis. O CBS fornece armazenamento de longo prazo no nível dos blocos de dados. Normalmente é usado como o dispositivo de armazenamento principal para os dados que requerem atualizações frequentes e refinadas (como sistema de arquivos e banco de dados), apresentando alta disponibilidade, confiabilidade e desempenho. O CBS usa um mecanismo distribuído de três cópias para fazer backup dos seus dados em diferentes máquinas físicas para evitar a perda de dados causada por um ponto único de falha, melhorando a confiabilidade dos dados.
É possível adquirir, ajustar e gerenciar facilmente seus dispositivos de disco em nuvem por meio do console e desenvolver um sistema de arquivos para criar um espaço de armazenamento maior do que um único disco em nuvem. Os discos em nuvem podem ser classificados de acordo com ciclos de vida diferentes da seguinte maneira:
- O ciclo de vida do disco em nuvem não elástico segue completamente o do CVM. Ele é adquirido com o CVM e usado como um disco do sistema. Não é compatível com a montagem e a desmontagem.
- O ciclo de vida do disco em nuvem elástico é independente do CVM. Ele pode ser adquirido separadamente e montado manualmente no CVM. Ele também pode ser adquirido com o CVM e montado automaticamente no CVM como um disco de dados. O disco em nuvem elástico é compatível com a montagem e a desmontagem do CVM na mesma zona de disponibilidade a qualquer momento. É possível montar vários discos em nuvem elástico no mesmo CVM ou desmontar um disco em nuvem do CVM A e montá-lo no CVM B.

O Tencent Cloud impõe limites de cota aos discos em nuvem dos usuários. Para obter mais informações, consulte os [Limites de uso](https://intl.cloud.tencent.com/document/product/362/32406).

## Casos de uso comuns
- É possível adquirir e montar um ou mais discos em nuvem para atender aos requisitos de capacidade de armazenamento quando o espaço em disco do seu CVM for insuficiente.
- Ao adquirir o CVM, não é necessário espaço de armazenamento adicional. Quando você tem requisitos de armazenamento, pode expandir a capacidade de armazenamento do CVM adquirindo um disco em nuvem.
- Quando houver uma solicitação de troca de dados entre vários CVMs, é possível desmontar os discos em nuvem (discos de dados) e remontá-los em outros CVMs.
- É possível expandir a capacidade máxima de armazenamento de um único disco em nuvem adquirindo vários discos em nuvem e configurando um Gerenciamento de volume lógico (LVM, do inglês "Logical Volume Manager").
- É possível expandir a capacidade máxima de E/S de um único disco em nuvem adquirindo vários discos em nuvem e configurando uma política de Matriz Redundante de Discos Independentes (RAID, do inglês "Redundant Array of Independent Disks").

## Funcionalidades
O Tencent Cloud fornece uma variedade de dispositivos de armazenamento de longo prazo, permitindo ao usuário escolher um tipo apropriado de disco em nuvem para armazenar arquivos, criar bancos de dados, etc.
- O CBS do Tencent Cloud vem com quatro tipos de disco: Premium Cloud Storage, SSD, Enhanced SSD e Tremendous SSD.
- Montagem e desmontagem elástica: todos os tipos de discos em nuvem elásticos são compatíveis com a montagem e desmontagem elástica. É possível montar vários discos em nuvem em um CVM para criar um sistema de arquivos com alta capacidade.
- Expansão elástica: um único disco aceita uma capacidade máxima de 32 TB. Você pode expandir o disco a qualquer momento.
- Backup por snapshot: é possível criar e reverter um snapshot para fazer backup dos dados. Também é possível criar um disco em nuvem a partir do snapshot para acelerar a implantação da sua empresa.
