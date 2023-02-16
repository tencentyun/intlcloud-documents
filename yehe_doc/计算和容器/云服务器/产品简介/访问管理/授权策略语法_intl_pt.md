
<span id = "celueyufa"></span>
### Sintaxe da política
Política do CAM:

```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 

```
- a **version** (versão) é obrigatória. Atualmente, apenas a "2.0" é compatível.
- a **statement** descreve os detalhes de uma ou mais permissões. Esse elemento contém uma permissão ou conjunto de permissões que é composto por outros elementos, como efeito, ação, recurso e condição. Uma política contém apenas uma instrução.
 1. A **action** descreve as ações permitidas ou negadas. Uma ação pode ser uma API (descrita com o prefixo "name") ou um conjunto de funcionalidades (um conjunto de APIs específicas, descrito com o prefixo "permit"). Esse elemento é obrigatório.
 2. O **resource** descreve os detalhes da autorização. Um recurso é descrito em um formato de seis partes. As definições detalhadas dos recursos variam de acordo com o produto. Para obter mais informações sobre como definir um recurso, consulte a documentação do devido produto. Esse elemento é obrigatório.
 3. A **condition**  descreve a condição para que a política entre em vigor. Uma condição é composta por operador, chave da ação e valor da ação. Um valor da condição pode conter informações, como hora e endereço IP. Alguns serviços permitem que você especifique valores adicionais em uma condição. Esse elemento é opcional.
 4. O **effect** descreve se o resultado produzido pela instrução é "allowed" (permitido) ou "denied" (negado). Esse elemento é obrigatório.

<span id = "caozuo"></span>
### Operações do CVM

Uma política do CAM permite que você execute operações de API em qualquer serviço do Tencent Cloud que seja compatível com o CAM. Para o CVM, use o prefixo `name/cvm:` com qualquer API, como `name/cvm:RunInstances` ou `name/cvm:ResetInstancesPassword`.
Para especificar várias ações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo:
```
"action":["name/cvm:action1","name/cvm:action2"]
```
Você também pode especificar várias ações usando um caractere curinga. Por exemplo, você pode especificar todas as APIs cujos nomes começam com "Describe", conforme mostrado abaixo:
```
"action":["name/cvm:Describe*"]
```
Para especificar todas as operações do CVM, use o caractere curinga "*" da seguinte forma:
```
"action": ["name/cvm:*"]
```

<span id = "ziyuanlujing"></span> 
### Caminho de recursos do CVM
Cada política do CAM define seus próprios recursos.
O formato geral dos caminhos de recursos é o seguinte:
```
qcs:project_id:service_type:region:account:resource
```
**project_id**: informações do projeto, que são usadas apenas para fins de compatibilidade e podem ser deixadas em branco.
**service_type** : abreviatura de um produto, como CVM.
**region**: região do recurso, como bj.
- **account**: a conta raiz do proprietário do recurso, como uin/164256472.
**resource**: informações detalhadas dos recursos de cada produto, como instance/instance_id1 or instance/*.

Por exemplo, você pode definir uma instância específica (i-15931881scv4) na instrução da seguinte maneira:
```
"resource":[ "qcs::cvm:bj:uin/164256472:instance/i-15931881scv4"]
```
Você também pode usar o caractere curinga "*" para definir todas as instâncias que pertencem a uma conta específica, conforme mostrado abaixo:
```
"resource":[ "qcs::redis:bj:uin/164256472:instance/*"]
```

Se você quiser especificar todos os recursos ou se alguma operação de API não for compatível com permissões no nível do recurso, você poderá usar o caractere curinga "*" em `resource`, conforme mostrado abaixo:
```
"resource":["*"]
```
Para especificar vários recursos em uma instrução, separe-os com vírgulas. No exemplo a seguir, dois recursos foram especificados:
```
"resource":["resource1","resource2"]
```
A tabela a seguir descreve os recursos do CVM e os métodos de descrição dos recursos correspondentes.
<style>
table th:nth-of-type(1){
width:250px;
}
table th:nth-of-type(2){
width:500px;
}
</style>
Na tabela a seguir, os nomes com o prefixo $ são placeholders.
- $project é o ID do projeto.
- $region é a região do recurso.
- $account é o ID da conta.

| Recurso | Sintaxe |
|-------|-------|
| Instância | qcs::cvm:$region:$account:instance/$instanceId |
| Chave | qcs::cvm:$region:$account:keypair/$keyId |
| VPC | qcs::vpc:$region:$account:vpc/$vpcId |
| Sub-rede | qcs::vpc:$region:$account:subnet/$subnetId |
| Imagem | qcs::cvm:$region:$account:image/\* |
| CBS |  qcs::cvm:$region:$account:volume/$diskid|
| Grupo de segurança | qcs::cvm:$region:$account:sg/$sgId |
| EIP |  qcs::cvm:$region:$account:eip/*|

 

<span id = "tiaojianmiyue"></span>
### Chaves de condição do CVM
Você pode usar as condições para especificar sob quais condições as políticas entram em vigor. Cada condição é composta por um ou mais pares de chaves. Elas não diferenciam maiúsculas de minúsculas.

- Se você especificar várias condições ou várias chaves em uma condição, elas serão conectadas com o operador lógico "AND" (E).
- Se você especificar uma chave com vários valores em uma condição, eles serão conectados com o operador lógico "OR" (OU).
A tabela a seguir descreve as chaves de condição do CVM para serviços específicos.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 25%;">
<col style="width: 25%;">
<col style="width: 50%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Chave de condição</th>
<th class="tableblock halign-left valign-top">Tipo de referência</th>
<th class="tableblock halign-left valign-top">Par de chaves</th>
</tr>
</thead>
<tbody>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:instance_type=<code>instance_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>instance_type</code> é o modelo da instância do CVM, como S1.SMALL1.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:image_type=<code>image_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>image_type</code> é o tipo de imagem, como IMAGE_PUBLIC.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>vpc:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>region</code> é a região da instância do CVM, como ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>Integer</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_size=<code>disk_size</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>Disk_size</code> é o tamanho do disco, como 500</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:disk_type</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm_disk_type=<code>disk_type</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>Disk_type</code> é o tipo de disco, como CLOUD_BASIC.</p>
</li>
</ul>
</div></div></td>
</tr>
<tr>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>String</p>
</div></div></td>
<td class="tableblock halign-left valign-top"><div><div class="paragraph">
<p>cvm:region=<code>region</code></p>
</div>
<div class="ulist">
<ul>
<li>
<p><code>region</code> é a região da instância do CVM, como ap-guangzhou.</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
