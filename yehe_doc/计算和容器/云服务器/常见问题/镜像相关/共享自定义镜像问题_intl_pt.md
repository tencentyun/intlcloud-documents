### Qual é a quantidade máxima de usuários com os quais uma imagem pode ser compartilhada?

50 usuários.

### O nome e a descrição de uma imagem compartilhada podem ser alterados?

Não.

### Uma imagem compartilhada é considerada na minha cota de imagens?

Não.

### Existem limitações de região para uma imagem compartilhada na criação e reinstalação de uma instância da CVM?

Sim. A imagem compartilhada deve estar na mesma região que a imagem de origem. A instância da CVM só pode ser criada e reinstalada na mesma região.

### Uma imagem compartilhada pode ser copiada para outras regiões?

Não.

### Uma imagem personalizada que foi compartilhada com outros usuários pode ser excluída?

Sim, mas primeiro você precisa cancelar todos os compartilhamentos dessa imagem personalizada.

### Uma imagem compartilhada por outros usuários pode ser excluída?

Não.

### Quais são os riscos de usar uma imagem personalizada compartilhada por outros usuários?

A Tencent Cloud não garante a integridade e segurança das imagens compartilhadas por outros usuários. Escolha imagens compartilhadas por uma conta confiável.

### Posso compartilhar com outros uma imagem que um usuário compartilhou comigo?

Não.

### Quais são os riscos de compartilhar uma imagem personalizada com outra conta?

Podem ocorrer vazamentos de dados e software. Antes de compartilhar uma imagem personalizada com outra conta, verifique se a imagem não contém dados ou software confidenciais. Esteja ciente de que a conta com a qual você compartilha a imagem pode criar instâncias da CVM da imagem compartilhada para criar outras imagens personalizadas. A transferência constante de dados aumentará o risco de vazamento.

### Posso criar uma instância usando uma imagem que compartilhei com outros usuários?

Sim. Você pode criar uma instância da CVM usando a imagem que compartilhou com outra conta. Você também pode criar uma imagem personalizada com base na instância da CVM.

### Uma imagem criada no servidor A no Norte da China pode ser compartilhada com o servidor B no Leste da China?

- Se ambos os servidores estiverem na mesma conta, você poderá copiar diretamente a imagem para o Servidor B no Leste da China. Para  instruções mais detalhadas, consulte [Cópias de imagens](https://intl.cloud.tencent.com/document/product/213/4943)
- Se os dois servidores estiverem em contas diferentes, você precisará copiar a imagem para a região do Leste da China e compartilhá-la com a conta do Servidor B. Para instruções mais detalhadas, consulte [Cópias de imagens](https://intl.cloud.tencent.com/document/product/213/4943), [Compartilhamento de imagens personalizadas](https://intl.cloud.tencent.com/document/product/213/4944) e [Cancelamento do compartilhamento de imagens](https://intl.cloud.tencent.com/document/product/213/7148).

