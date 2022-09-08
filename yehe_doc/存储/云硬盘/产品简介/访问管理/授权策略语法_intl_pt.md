
<span id = "celueyufa"></span>
## Sintaxe da política
Política do CAM:
```json
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
- **version (versão)**: é obrigatório. Atualmente, o único valor válido é `"2.0"`.
- **statement (instrução)**: descreve detalhadamente as informações de uma ou mais permissões. Cada permissão é composta por um conjunto de elementos, inclusive efeito, ação, recurso e condição. Uma política contém apenas um elemento de instrução.
 1. **action (ação)**: é **obrigatório**. Descreve as operações a serem permitidas ou negadas, as quais podem ser APIs (descritas com o prefixo "name") ou um conjunto de funcionalidades (um conjunto de APIs específicas descritas com o prefixo "permid").
 2. **resource (recurso)**: é **obrigatório**. Descreve os dados específicos a serem autorizados em um formato de seis segmentos. As definições detalhadas dos recursos variam de acordo com o produto.
 3. **condition (condição)**: é opcional. Descreve as condições necessárias para que a política entre em vigor. Uma condição é composta por operador, chave de operação e valor de operação. Um valor de condição pode conter informações, como hora e endereço IP. Alguns serviços permitem que você especifique outras informações nas condições.
 4. **effect (efeito)**: é **obrigatório**. Descreve o resultado retornado pela instrução, ou seja, se a permissão é autorizada ("allow" – permitir) ou negada ("deny" – negar).


## Operações do CBS[](id:caozuo)

Em uma instrução de política do CAM, você pode especificar qualquer operação de API a partir de qualquer serviço compatível com CAM. Para o CBS, use as APIs com o prefixo `name/cvm:`, por exemplo, `name/cvm:CreateDisks` ou `name/cvm:DescribeDisks`.
Para especificar várias operações em uma única instrução, separe-as com vírgulas, conforme mostrado abaixo.
```
"action":["name/cvm:action1","name/cvm:action2"]
```
Você também pode usar um asterisco para especificar várias operações. Por exemplo, você pode especificar todas as operações cujos nomes comecem com "Describe (Descrever)", conforme mostrado abaixo.
```
"action":["name/cvm:Describe*"]
```
Para especificar todas as operações do CVM, use o asterisco `*` da seguinte forma.
```
"action":["name/cvm:*"]
```


### Caminhos de recursos do CBS[](id:ziyuanlujing)
Toda instrução de política do CAM contém os recursos a serem aplicados à política em si. O formato geral do caminho de um recurso é mostrado abaixo.
```
qcs:project_id:service_type:region:account:resource
```
- **project_id**: indica as informações do projeto, as quais são usadas apenas para habilitar a compatibilidade com a lógica anterior do CAM. Esse elemento pode ser deixado em branco.
- **service_type**: indica o nome abreviado de um produto, por exemplo, "CVM".
- **region**: indica as informações da região, por exemplo, "bj".
- **account**: indica a conta-raiz do proprietário de um recurso, por exemplo, "uin/164256472".
- **resource**: indica os recursos específicos de um produto, por exemplo, "volume/diskid1" ou "volume/*".

Você pode especificar um recurso do CBS na instrução, por exemplo "disk-abcdefg", conforme mostrado abaixo.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/disk-abcdefg"]
```
Você também pode usar o asterisco `*` para especificar todos os recursos do CBS presentes em uma conta, conforme mostrado abaixo.
```
"resource":[ "qcs::cvm:bj:uin/164256472:volume/*"]
```

Para especificar todos os recursos ou se uma operação de API não autorizar o controle de permissão no nível do recurso, você pode usar o asterisco `*` no elemento do recurso, conforme mostrado abaixo.
```
"resource": ["*"]
```
Para especificar vários recursos em uma instrução, separe-os com vírgulas. No exemplo a seguir, dois recursos foram especificados.
```
"resource":["resource1","resource2"]
```


## Chaves de condição do CBS[](id:tiaojianmiyue)
Em uma instrução de política, você pode especificar as condições necessárias para que a política entre em vigor. Cada condição contém um ou mais pares de chave-valor. As chaves de condição não diferenciam letras maiúsculas e minúsculas.

- Se você especificar várias condições ou várias chaves em uma mesma condição, a condição é avaliada com o operador lógico "AND".
- Se você especificar uma chave com vários valores em uma mesma condição, a condição será avaliada com o operador lógico "OR". A permissão só poderá ser concedida quando todas as condições forem satisfeitas.
A tabela a seguir descreve as chaves de condição do CBS que são usadas para serviços específicos.
<table class="tableblock frame-all grid-all spread">
<colgroup>
<col style="width: 15%;">
<col style="width: 15%;">
<col style="width: 70%;">
</colgroup>
<thead>
<tr>
<th class="tableblock halign-left valign-top">Chave de condição</th>
<th class="tableblock halign-left valign-top">Tipo de referência</th>
<th class="tableblock halign-left valign-top">Par de chave-valor</th>
</tr>
</thead>
<tbody>
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
em que <code>region</code> indica uma região (por exemplo, "ap-guangzhou").</p>
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
<p>em que <code>disk_type</code> indica um tipo de disco (por exemplo, "CLOUD_PREMIUM").</p>
</li>
</ul>
</div></div></td>
</tr>
</tbody>
</table>
