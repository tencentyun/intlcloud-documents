### Limites de uso
- A ocupação de um HAVIP pode ser declarada pelo back-end do CVM, mas você não pode vincular os HAVIPs manualmente a um servidor especificado no console (a experiência é consistente com a de uma máquina física tradicional).
- O RS de back-end, mas não o HAVIP, determina se a migração deve ser feita com base na negociação do arquivo de configuração.
- Apenas as instâncias do VPC são compatíveis, e a rede básica não é compatível.
- A detecção de pulsação deve ser feita por um aplicativo no CVM, mas não pelo HAVIP, que serve apenas como um endereço IP flutuante declarado pelo ARP (a experiência é a mesma de uma máquina física tradicional).

### Limites de cota
<table style="width:450px !important">
<thead>
<tr>
<th width="70%">Recurso</th>
<th>Limite</th>
</tr>
</thead>
<tbody><tr>
<td>Cota HAVIP padrão em cada VPC</td>
<td>10</td>
</tr>
</tbody></table>
