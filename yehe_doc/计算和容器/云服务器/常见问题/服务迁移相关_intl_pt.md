## Migração offline

### Por que o upload e a migração do COS demoram tanto?

A duração do upload está relacionada ao tamanho do arquivo de imagem e à largura de banda. Recomendamos que você use formatos de imagem compactados (qcow2 ou vhd) para reduzir o tempo de transferência e migração.

### Por que a tarefa de migração falhou?

 - Atualmente, a migração de serviço da Tencent Cloud aceita os seguintes formatos de imagem: qcow2, vpc, vmdk e raw. Verifique se a imagem está em um desses formatos.
 - Verifique se o arquivo de imagem já foi carregado no COS e certifique-se de que o arquivo não esteja danificado ou corrompido.
 - Certifique-se de que o disco em nuvem/CVM para o qual deseja migrar esteja em uso normal. Não é possível migrar dispositivos expirados.
 
### Como solucionar a causa do erro gerado por uma tarefa de migração?
 
 - Se a mensagem “image file verification failed (falha na verificação do arquivo de imagem)” for exibida, geralmente é porque a capacidade do disco do sistema ou do disco de dados para o qual você deseja migrar é menor que a capacidade do disco de origem ou o tamanho do arquivo de imagem. Ajuste a capacidade do disco do sistema ou disco de dados e tente novamente.
 - Se a mensagem “failed to obtain the metadata of the image file (falha ao obter os metadados do arquivo de imagem)” for exibida, geralmente é porque o arquivo de imagem está danificado ou o formato do arquivo de imagem não é aceito. Verifique se há erros no processo de criação, exportação e upload da imagem. Você também pode usar o arquivo de imagem no formato qcow2, vpc, vmdk ou raw e tentar novamente.
 - Se forem exibidas mensagens como “task timeout (tempo limite da tarefa)”, “system error (erro do sistema)” e “other reasons (outros motivos)”, ou se você tentou novamente a tarefa de migração, mas ela falhou mais uma vez, você pode [entre em contato conosco](https://cloud.tencent.com/document/product/213/39047) para obter ajuda.
 

## Migração online

### Quais sistemas operacionais e tipos de disco são compatíveis?

- Os sistemas operacionais Linux convencionais, como o CentOS e o Ubuntu, são compatíveis.
- A migração não está relacionada ao tipo e uso do disco.

### Onde baixar a ferramenta de migração online?

Atualmente, não é possível baixar a ferramenta de migração online. Se necessário, entre em contato com um representante de vendas ou envie um tíquete para solicitar permissão e obter a documentação relacionada.

### Como usar a ferramenta de migração online?

A ferramenta de migração online deve ser copiada para o servidor de origem. Você precisa modificar os arquivos de configuração dependendo do estado da máquina. Você pode escrever um script para executar o processamento em lotes.

### Preciso manter a ferramenta após a conclusão da migração?

Não, você não precisa manter a ferramenta. Quando a migração for concluída, você poderá excluir a ferramenta no servidor de origem.

### E quanto à velocidade e custo da migração?

- Velocidade: depende principalmente da largura de banda da CVM. Testamos uma CVM com pagamento conforme o uso de 1u1g com 100 mbps de largura de banda, e a taxa de migração ficou em torno de 12 MB/s. A taxa de migração real será de cerca de 9 MB/s.
- Custo: a ferramenta de migração é gratuita. No entanto, como os dados são transferidos pela Internet pública, você será cobrado pela pequena quantidade de recursos usados durante a migração. Para mais detalhes, consulte os preços listados no site da Tencent Cloud.
  
### Posso migrar várias CVMs ao mesmo tempo?

Sim, é possível migrar várias CVMs ao mesmo tempo. Como são migrados para CVMs diferentes, eles não são relacionados.
