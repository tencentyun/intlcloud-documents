
Este documento descreve como definir o período de retenção do binlog para uma instância do TencentDB for MySQL no console.

## Descrição do binlog
O binlog cresce rapidamente quando uma instância do TencentDB for MySQL executa grandes transações ou muitas operações DML. O binlog é dividido a cada 256 MB e carregado na COS. Você pode ver os arquivos de binlog carregados na lista de logs no console.
![](https://main.qcloudimg.com/raw/bcf3d0d2ac291ccebbcfebea05fd11f1.png)

## Visão geral
Antes de serem carregados na COS, os arquivos de binlog são armazenados no disco da instância (ou seja, localmente). Você pode definir o período de retenção do binlog local, controlar a porcentagem máxima de espaço em disco que o binlog pode ocupar ou expandir o espaço de disco no console. Recomendamos que você limpe os dados que não são mais usados ​​para manter a utilização do disco abaixo de 80%.
- A sincronização de dados do MySQL é baseada no binlog. Para garantir a capacidade de restauração, estabilidade e alta disponibilidade do banco de dados, o binlog não pode ser desabilitado no TencentDB for MySQL.
- Os arquivos binlog gerados são automaticamente copiados para COS através do [recurso de backup automático](https://intl.cloud.tencent.com/document/product/236/37796) fornecido pelo TencentDB for MySQL. Os arquivos binlog cujos backups já foram carregados na COS serão limpos de acordo com a política de retenção do binlog local. Para evitar exceções, os arquivos binlog em uso não podem ser limpos, mesmo que expirem. Portanto, a limpeza do binlog local tem um atraso.
>?Regra para limpeza de arquivos binlog expirados:
>Os arquivos binlog locais são verificados uma vez a cada 60 segundos. Se a hora de início de um arquivo binlog ou o uso de espaço não atender à regra de retenção definida, ele será adicionado à fila de arquivos a serem excluídos. Os arquivos binlog na fila serão classificados por hora e excluídos, um por um, começando pelo arquivo mais antigo, até que a fila seja limpa.

## Instruções
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb) e clique em um ID de instância, na lista de instâncias, para entrar na página de gerenciamento de instâncias.
2. Na página de gerenciamento de instâncias, selecione a guia **Backup and Restoration (Backup e restauração)** e clique em **Configure Local Binlog (Configurar binlog local)**.
3. Na janela pop-up, especifique o período de retenção e o limite de utilização do espaço e clique em **OK**.

## Perguntas frequentes
#### A restauração do banco de dados será afetada se o período de retenção do binlog local for muito curto?
Não, porque os arquivos binlog gerados serão carregados para a COS através do recurso de backup automático o mais rápido possível, e aqueles que ainda não foram carregados não podem ser apagados. No entanto, um período de retenção muito curto afetará a velocidade da reversão.

#### Qual é a política de retenção padrão para o binlog local?
Por padrão, o período de retenção do binlog local é de 120 horas e a utilização máxima do espaço de binlog é de 30%.

#### Os arquivos de binlog ocuparão o espaço em disco da instância?
Sim. Antes que os arquivos de binlog sejam carregados na COS e limpos de acordo com a política de retenção, eles serão armazenados no disco da instância.
