A funcionalidade Sem Cobranças Quando Desligada significa que você não será cobrado pelas instâncias (CPU, memória) depois de **selecionar a opção Sem Cobranças Quando Desligada** para **desligar** instâncias com pagamento conforme o uso. Componentes como [discos em nuvem](https://intl.cloud.tencent.com/document/product/213/2255) (discos do sistema e discos de dados), largura de banda da rede pública (faturamento por largura de banda) e imagens ainda serão cobrados.

## Limites de uso

A funcionalidade **Sem Cobranças Quando Desligada** se aplica apenas a **instâncias com pagamento conforme o uso** usando **discos em nuvem como disco do sistema e disco de dados**.
Essa funcionalidade **não está disponível** para os seguintes cenários:
- Você desliga a instância após fazer o login nela, em vez de desligá-la no console.
- Montagem de instâncias de disco local.
- Instâncias spot.
- Instâncias que são desligadas devido a uma conta em atraso: quando uma instância é desligada devido a um pagamento em atraso, o faturamento da instância e seus recursos associados param. Os recursos de computação e os IPs públicos são liberados. O faturamento é retomado após o pagamento em atraso.

Se a operação de desligamento em lote incluir instâncias que são elegíveis para a funcionalidade Sem Cobranças Quando Desligada e outras que não são, então:
- Para as instâncias elegíveis, **a CPU e a memória não serão cobradas** após o desligamento;
- As instâncias inelegíveis **ainda serão cobradas** após o desligamento.

## Impactos

Quando a funcionalidade Sem Cobranças Quando Desligada estiver ativada, ela causará os seguintes impactos depois que as instâncias forem desligadas.
1. Após o desligamento, a CPU e a memória da instância **não serão mantidas**, portanto, **podem falhar** ao serem reiniciadas. Se for o caso, tente reiniciar mais uma vez ou espere um pouco antes de tentar novamente.
2. Se a instância foi atribuída a um endereço IP público, ele será **automaticamente liberado** após o desligamento. Um novo IP público será atribuído quando você reiniciar a instância. O IP privado permanece o mesmo. 
 **Para manter o IP público, você pode converter o IP público em um EIP antes do desligamento da instância**. O EIP será mantido após o desligamento da instância, bem como durante a reinicialização, e nenhuma taxa de inatividade será cobrada.
3. Quando a instância é desligada, a maioria das operações **exceto a inicialização da instância** não estará disponível, incluindo ajustar as configurações, os discos e as redes; reinstalar sistemas; reiniciar instâncias, redefinir senhas; renomear, etc. **Você precisará iniciar a instância para realizar essas operações**.
4. A funcionalidade Sem Cobranças Quando Desligada **não se aplica ao** desligamento da instância como resultado da reinicialização da instância para ajustes de configuração/disco, reinstalação do sistema e outras operações OPS.

## Guia de operações

Consulte os [Detalhes da Funcionalidade Sem Cobranças Quando Desligada para as instâncias com pagamento conforme o uso](https://intl.cloud.tencent.com/document/product/213/19922).
