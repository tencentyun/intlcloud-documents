
Por padrão, você pode baixar arquivos de backup de instâncias do TencentDB for MySQL pela rede pública ou privada. Para limitar o download, você pode ajustar as configurações de download de backup.
>?
>- As configurações de download de backup são suportadas nas seguintes regiões:
>Guangzhou, Xangai, Pequim, Shenzhen, Chengdu, Chongqing, Nanjing, Hong Kong (China), centro financeiro de Pequim, centro financeiro de Xangai, centro financeiro de Shenzhen, Toronto, Singapura, Vale do Silício, Frankfurt, Seul, Mumbai, Bangkok, Moscou e Tóquio.
>- Como habilitar as configurações de download de backup:
> - Antes de 9 de novembro de 2021, você precisava [enviar um ticket](https://console.cloud.tencent.com/workorder/category) para ativar esse recurso.
> - A partir de 9 de novembro de 2021, esse recurso passou a ficar disponível no console.

## Definição das regras de download de backup
1. Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), selecione **Database Backup (Backup de banco de dados)** na barra lateral esquerda e selecione uma região na parte superior.
2. Na guia **Download Settings (Configurações de download)**, visualize as configurações de download de backup e clique em **Edit (Editar)** para modificá-las.
>?O download pela rede pública está habilitado por padrão e, quando habilitado, o download pela rede privada também é permitido.
>
![](https://qcloudimg.tencent-cloud.cn/raw/530fbf3e6c93eea06ff23e112cad84c0.png)
3. Na página exibida, defina as regras de download e clique em **OK**.
   - Download pela rede pública:
     - Habilitado: você não pode definir nenhuma regra de download.
     - Desabilitado: você pode definir as regras de download permitindo ou bloqueando IPs e VPCs específicos.
   - Definição de regras de download:
     - Se você não especificar nenhum valor, a condição não terá efeito.
     - Você deve separar os valores de uma condição de IP com vírgulas.
     - Você pode inserir IPs ou intervalos de IP como os valores de uma condição de IP.
     - Se nenhum requisito de IP e VPC for definido, não haverá limite de download pela rede privada.
![](https://qcloudimg.tencent-cloud.cn/raw/7e0a4a48af62fdd643259f8902fcd95f.png)
4. Depois que a configuração for concluída, retorne à guia **Download Settings (Configurações de download)** para ver as regras que entram em vigor.
![](https://qcloudimg.tencent-cloud.cn/raw/cb4ac45dcde8a57610b0eaec9075c6cb.png)

## Autorização de subcontas para definir regras de download de backup
Por padrão, as subcontas não têm permissão para definir regras de download de backup para instâncias do TencentDB for MySQL. Portanto, você precisa criar políticas de CAM para conceder a permissão a subcontas específicas.

O [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) é um serviço da Tencent Cloud baseado na web que ajuda a gerenciar e controlar com segurança as permissões de acesso aos recursos da sua conta da Tencent Cloud. Usando o CAM, você pode criar, gerenciar e encerrar usuários (ou grupos) e controlar quem pode usar os recursos da Tencent Cloud por meio do gerenciamento de identidade e política.

Ao usar o CAM, você pode associar uma política a um usuário ou grupo de usuários para permitir ou proibir que usem recursos especificados para concluir tarefas especificadas. Para obter mais informações sobre as políticas do CAM, consulte [Lógica da sintaxe](https://intl.cloud.tencent.com/document/product/598/10603).

### Autorização de subcontas
1. Faça login no [console do CAM](https://console.cloud.tencent.com/cam) com a conta raiz, localize o subusuário de destino na lista de usuários e clique em **Authorize (Autorizar)**.
![img](https://qcloudimg.tencent-cloud.cn/raw/89d7cf063bd376a0cc4f4db0c78e7e56.png)
2. Na janela pop-up, selecione a política predefinida **QcloudCDBFullAccess** e clique em **OK** para concluir a autorização.
![](https://qcloudimg.tencent-cloud.cn/raw/0819ca9a1a81fc00968f0a263dc7727e.png)

### Sintaxe da política
A seguinte sintaxe de política é usada para autorizar uma subconta a definir regras de download de backup para instâncias do TencentDB for MySQL:
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"effect",
             "action":["action"],
             "resource":["resource"]
            }
       ] 
}
```
- a **version (versão)** é obrigatória. Atualmente, apenas o valor "2.0" é permitido.
- a **statement (instrução)** descreve os detalhes de uma ou mais permissões. Esse elemento contém uma permissão ou conjunto de permissões que é composto por outros elementos, como efeito, ação e recurso. Cada política tem apenas uma instrução.
- O **effect (efeito)** é obrigatório. Ele descreve o resultado de uma instrução. O resultado pode ser "allow (permitir)" ou um "deny (negar)" explícito.
- A **action (ação)** é obrigatória. Ela descreve a operação permitida ou negada. Uma operação pode ser uma API (prefixada com "name") ou um conjunto de recursos (um conjunto de APIs específicas prefixadas com "permid").
- **resource (recurso)** é obrigatório. Ele descreve os detalhes da autorização.

### Operações de API
Em uma instrução de política do CAM, você pode especificar qualquer operação de API de qualquer serviço compatível com o CAM. APIs prefixadas com `name/cdb:` devem ser usadas para o TencentDB for MySQL. Para especificar várias operações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo:
```
"action":["name/cdb:action1","name/cdb:action2"]
```
Também é possível especificar várias operações usando um curinga. Por exemplo, você pode especificar todas as operações cujos nomes começam com "Describe (Descrever)", conforme mostrado abaixo:
```
"action":["name/cdb:Describe*"]
```

### Caminho do recurso
O formato geral dos caminhos de recursos é o seguinte:
```
qcs::service_type::account:resource
```
- service_type: descreve a abreviação do produto, como `cdb` aqui.
- conta: é a conta raiz do proprietário do recurso, como "uin/326xxx46".
- recurso: descreve as informações detalhadas de recursos do serviço específico. Cada instância do TencentDB for MySQL (instanceId) é um recurso.

O exemplo é o seguinte:
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kfxxh3"]
```
Aqui, `cdb-kfxxh3` é o ID do recurso de instância do TencentDB for MySQL, ou seja, o `resource` na instrução de política do CAM.

### Exemplo
O exemplo a seguir mostra apenas o uso do CAM. Para obter a lista completa de APIs usadas para definir as regras de download de backup do MySQL, consulte a [documentação da API](https://intl.cloud.tencent.com/document/product/236/43327).
```
{
       "version":"2.0",
       "statement":
       [
          {
             "effect":"allow",
             "action": ["name/cdb: ModifyBackupDownloadRestriction"],
             "resource": ["*"]
            }
       ]
}
```

### Personalização de uma política de CAM para definir regras de download de backup do MySQL
1. Faça login no  [console do CAM](https://console.cloud.tencent.com/cam/policy) com a conta raiz, selecione **Policies (Políticas)** na barra lateral esquerda e clique em **Create Custom Policy (Criar política personalizada)**.
![img](https://qcloudimg.tencent-cloud.cn/raw/4ddc463dc28ee48b9dd63d862fa41ea1.png)
2. Na caixa de diálogo pop-up, selecione **Create by Policy Generator (Criar pelo gerador de política)**.
3. Na página **Select Service and Action (Selecionar serviço e ação)**, selecione os itens de configuração, clique em **Add Statement (Adicionar instrução)** e clique em **Next (Próximo)**.
   - Serviço: selecione **TencentDB for MySQL**.
   - Ação: selecione todas as APIs de configuração das regras de download de backup do MySQL. Para obter mais informações, consulte a [documentação da API](https://intl.cloud.tencent.com/document/product/236/43327).
   - Recurso: para mais informações, consulte [Método de descrição do recurso](https://intl.cloud.tencent.com/document/product/598/10606). Você pode inserir `*` para indicar que as regras de download de backup das instâncias do TencentDB for MySQL na região especificada podem ser definidas.
![](https://qcloudimg.tencent-cloud.cn/raw/5372ae1d2ac16ff63b63fbf175f3fccf.png)
4. Na página **Edit Policy (Editar política)**, insira o **Policy Name (Nome da política)** (como `BackupDownloadRestriction`) conforme necessário e a **Description (Descrição)** e clique em **Done (Concluído)**.
![](https://qcloudimg.tencent-cloud.cn/raw/3c5454e0da412c0e12beebb4b045979d.png)
5. Retorne à lista de políticas e você poderá visualizar a política personalizada recém-criada.
![](https://qcloudimg.tencent-cloud.cn/raw/d242b34c0b9cad83d130444d84e205e0.png)

