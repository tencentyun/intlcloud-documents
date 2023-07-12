Atualmente, a replicação de snapshots entre regiões está na versão beta. Com essa funcionalidade, é possível migrar dados e serviços para outras regiões ou criar um sistema de recuperação de desastre entre regiões para sua empresa com facilidade.
Você pode **enviar uma solicitação** para usar essa funcionalidade.

## Limites de uso
- **Solicitar beta**: atualmente, a replicação de snapshots entre regiões está na versão beta. É necessário **enviar uma solicitação**.
- **Regiões compatíveis**: para obter mais informações, consulte [Regiões e zonas de disponibilidade](https://intl.cloud.tencent.com/document/product/362/32396)。


## Instruções

1. Faça login na página [Lista de snapshots](https://console.cloud.tencent.com/cvm/snapshot).
2. Clique em **Cross-Region Replication (Replicação entre regiões)** para o snapshot de destino.
3. Configure os seguintes parâmetros:
  - **Novo nome do snapshot**: (opcional) insira o novo nome do snapshot com até 60 caracteres.
    Por padrão, um novo nome de snapshot contém o ID do snapshot de origem e as informações da região e está no seguinte formato: `Copied <Source snapshot ID> from <Source snapshot region>`, por exemplo, `Copied snap-oi5spwt2 from ap-shanghai`.
  - **Região**: (obrigatório) uma região de destino para a qual um snapshot é copiado
    Verifique a cota de snapshots e a restrição geográfica ao selecionar a região.
4. Clique em **OK** para iniciar a replicação. Passe o mouse sobre o ícone de informações para exibir o status do snapshot de origem. O novo snapshot é adicionado à região de destino.  
5. Assim que a replicação for concluída, é possível exibir o novo snapshot na lista de snapshots da região de destino.
> O snapshot de origem não pode ser excluído durante a replicação entre regiões desse snapshot.
>
 Durante o processo de replicação entre regiões:
 - Status do snapshot de origem: é possível exibi-lo acessando a **snapshot list (lista de snapshots)** da região de origem e observando a coluna de status na linha do snapshot de origem.
 - Status do snapshot de destino: é possível exibi-lo acessando a página da lista de snapshots da região de destino.
