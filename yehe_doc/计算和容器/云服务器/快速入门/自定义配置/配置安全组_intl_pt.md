Este documento descreve como criar e configurar um grupo de segurança para uma instância. Para obter mais informações, consulte o [Grupo de segurança](https://intl.cloud.tencent.com/document/product/213/12452).


## Configuração de um grupo de segurança
1. Selecione **New security group (Novo grupo de segurança)**.
> Se você tiver grupos de segurança disponíveis, poderá selecionar **Existing Security Groups (Grupos de segurança atuais)**.
>
![](https://main.qcloudimg.com/raw/c08ca9a0262f4911fdac90925762e4a6.png)
2. Selecione os endereços IP ou as portas para abrir, com base em seus requisitos reais.
As regras para um novo grupo de segurança são as seguintes:<ul>
<li><b>ICMP</b>: abre para o protocolo ICMP e permite o ping do servidor na rede pública.</li>
<li><b>TCP:80</b>: abre a porta 80 e permite o acesso a serviços Web em HTTP.</li></li>
<li><b>TCP:22</b>: abre a porta 22 e permite uma conexão remota com os CVMs do Linux em SSH.</li>
<li><b>TCP:443</b>: abre a porta 443 e permite o acesso a serviços Web em HTTPS.</li>
<li><b>TCP:3389</b>: abre a porta 3389 e permite uma conexão remota com os CVMs do Windows em RDP.</li>
<li><b>Rede privada</b>: abre para a rede privada e permite o acesso à rede privada entre diferentes recursos de nuvem (IPv4).</li></ul>
<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Observação:
</div>
<ul><li> Depois de selecionar os endereços IP ou as portas a serem abertas, as regras detalhadas de entrada e saída são exibidas na página da guia <b>Security Group Rule (Regra do grupo de segurança)</b>.</li><li>Para abrir outras portas para a sua empresa, consulte os <a href="https://intl.cloud.tencent.com/document/product/213/32369">Casos de uso de grupos de segurança</a> para <a href="https://intl.cloud.tencent.com/document/product/213/34271">criar grupos de segurança</a>. Por motivos de segurança, recomendamos que você abra portas apenas quando for realmente necessário, para evitar riscos de segurança desnecessários.
</li></ul>
</blockquote>
3. Configure outras informações conforme solicitado.

## Regras de grupos de segurança

**Regras de entrada**: permite o tráfego para os CVMs associados a um grupo de segurança.
**Regras de saída**: indica o tráfego de saída dos CVMs.

- As regras em um grupo de segurança são **priorizadas de cima para baixo**.
- Quando um CVM está vinculado a um grupo de segurança sem regras, todo o tráfego de entrada e de saída é rejeitado por padrão. Se uma regra estiver disponível, ela prevalece.
- Quando um CVM está vinculado a vários grupos de segurança, os com **números menores têm prioridade mais alta**.
- Por padrão, quando um CVM está vinculado a vários grupos de segurança, a regra de rejeição tem efeito para o grupo de segurança com a prioridade mais baixa.

## Limites de grupos de segurança

Para obter mais informações, consulte os [Limites de grupos de segurança](https://intl.cloud.tencent.com/document/product/213/15379).
