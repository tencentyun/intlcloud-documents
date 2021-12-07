Ao configurar um listener HTTPS de uma instância do CLB, você pode usar diretamente um certificado do Serviço de Certificado SSL ou fazer upload de um certificado de servidor e um [Certificado SSL](https://intl.cloud.tencent.com/document/product/1007/30152) emitido por uma AC de terceiros para o CLB.

## Requisitos de certificado
O CLB é compatível apenas com certificados no formato PEM. Antes de fazer upload de um certificado, certifique-se de que seu certificado, cadeia de certificados e chave privada atendam aos requisitos de formato. Para obter os requisitos de certificado, consulte [Formato do certificado SSL](https://intl.cloud.tencent.com/document/product/214/5369).

### Configuração de certificado
A configuração de certificado para um listener HTTPS pode ser feita de duas formas:
- Se o SNI não estiver habilitado, um certificado pode ser configurado no nível do listener, sob o qual todos os nomes de domínio usam o mesmo certificado. Para obter mais informações, consulte [Configuração de um listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).
- Se o SNI estiver habilitado, um certificado pode ser configurado no nível do nome de domínio e diferentes certificados podem ser configurados para diferentes nomes de domínio no listener. Para obter mais informações, consulte [Suporte SNI para vincular vários certificados a uma instância do CLB](https://intl.cloud.tencent.com/document/product/214/19048).

## Atualização de certificados em lotes
Para evitar que a expiração do certificado afete o seu serviço, atualize o certificado antes que expire.
Após a atualização de um certificado, o sistema não excluirá o certificado legado; em vez disso, ele irá gerar um novo. O certificado será atualizado automaticamente para todas as instâncias do CLB que o utilizam.

1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Clique em **Certificate Management (Gerenciamento de certificados)** na barra lateral esquerda.
3. Na lista de certificados na página **Certificate Management (Gerenciamento de certificados)**, clique em **Update (Atualizar)** na coluna "Operation (Operação)" à direita do certificado de destino.
4. Na caixa de diálogo "Create Certificate (Criar certificado)" que aparece, insira o conteúdo do certificado e o conteúdo da chave do novo certificado e clique em **Submit (Enviar)**.
![](https://main.qcloudimg.com/raw/d6534b57f4a33fab69b98fca4d1023f3.png)

## Visualização da instância do CLB associada ao certificado
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb).
2. Clique em **Certificate Management (Gerenciamento de certificados)** na barra lateral esquerda.
3. Na lista de certificados na página **Certificate Management (Gerenciamento de certificados)**, clique no ID do certificado de destino.
4. Na página "Basic Info (Informações básicas)", visualize as instâncias do CLB associadas ao certificado.
![](https://main.qcloudimg.com/raw/b3670e111ec8b9e1a43b9c7d2e870be3.png)
