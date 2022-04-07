### O que é uma imagem?
Uma imagem é o modelo para configuração de software da CVM (sistemas operacionais, programas pré-instalados etc.). A Tencent Cloud exige que os usuários usem imagens para iniciar instâncias. Uma imagem pode iniciar várias instâncias, e os usuários podem usá-la repetidamente. Para mais informações sobre as imagens, consulte a [Visão geral](https://intl.cloud.tencent.com/document/product/213/4940).

### O que preciso fazer antes de importar a imagem?
Antes de importar uma imagem, você precisa concluir duas etapas principais: solicitar permissões e preparar arquivos de imagem. Para mais informações, consulte a [Visão geral](https://intl.cloud.tencent.com/document/product/213/4945).

### Como faço para exportar uma imagem para teste local?
A migração de serviço da Tencent Cloud aceita imagens nos formatos qcow2, vhd, raw e vmdk.
Você pode usar as ferramentas de exportação de imagens de plataformas de virtualização, como o VMWare vCenter Convert ou o Citrix XenConvert. Para mais informações, consulte a documentação da ferramenta de exportação de cada plataforma. Você também pode exportar imagens [usando o Disk2vhd (Windows)](https://intl.cloud.tencent.com/document/product/213/17815) ou [executando comandos (Linux)](https://intl.cloud.tencent.com/document/product/213/17814).

### Posso excluir uma imagem personalizada que foi usada para criar uma instância da CVM?
Sim. Assim que uma imagem personalizada é excluída, ela não pode mais ser usada para iniciar uma nova instância da CVM. Isso não afetará as instâncias que já foram iniciadas. Caso deseje excluir todas as instâncias iniciadas a partir desta imagem, consulte [Recuperação de instâncias](https://intl.cloud.tencent.com/document/product/213/4931) ou [Encerramento de instâncias](https://intl.cloud.tencent.com/document/product/213/4930).

### Posso excluir uma imagem personalizada que foi compartilhada com outra conta?
Não. Você não pode excluir uma imagem personalizada que foi compartilhada com outra conta. Para excluí-la, primeiro é necessário cancelar o compartilhamento. Para mais informações, consulte [Cancelamento do compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148).


