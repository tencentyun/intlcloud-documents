## Política de acesso total para todas as instâncias do CLB
- Conceda acesso total ao serviço do CLB (criação, gerenciamento, etc.) a uma subconta.
- Nome da política: CLBResourceFullAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## Política somente leitura para todas as instâncias do CLB
- Conceda a uma subconta acesso somente leitura ao CLB (ou seja, a permissão para visualizar, mas não para criar, atualizar ou excluir todos os recursos do CLB). No console, o pré-requisito para manipular um recurso é a capacidade de visualizar o recurso; portanto, é recomendável conceder à subconta acesso de leitura total ao CLB.
- Nome da política: CLBResourceReadOnlyAccess
```
{
	"version": "2.0",
	"statement": [{
		"action": [
			"name/clb:Describe*"
		],
		"resource": "*",
		"effect": "allow"
	}]
}
```

## Política de acesso total para serviço CLB sob uma etiqueta especificada
- Conceda a uma subconta acesso total ao serviço CLB (criação de instâncias, gerenciamento de listeners, etc.) sob uma tag especificada (chave de tag: tagkey; valor de tag: tagvalue).
- As instâncias do CLB oferecem suporte à configuração de tags e ao uso de tags para autenticação.

```
{
    "version":"2.0",
    "statement":[
        {
            "effect":"allow",
            "action":"*",
            "resource":"*",
            "condition":{
                "for_any_value:string_equal":{
                    "qcs:tag":[
                        "tagkey&tagvalue"
                    ]
                }
            }
        }
    ]
}  
```
   
