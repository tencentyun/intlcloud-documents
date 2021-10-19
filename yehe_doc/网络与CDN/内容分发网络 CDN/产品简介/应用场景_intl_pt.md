## Casos de uso
A tabela a seguir lista os casos de uso do CDN. Clique para exibir os detalhes.

<table  style="width:890">
<thead>
	<tr>
		<th scope="col" style="width: 100px;">Caso de uso</th>
		<th scope="col">Descrição</th>
	</tr>
</thead>
<tbody>
	<tr>
	<td><a href = "#m1">Aceleração de sites</a></td>
		<td >O CDN fornece recursos de entrega acelerada para conteúdo estático, como páginas da web, imagens e arquivos pequenos em cenários de negócios como portais da Web, comércio eletrônico e comunidades de UGC, melhorando significativamente a experiência do usuário. </td>
	</tr>
	<tr>
		<td><a href = "#m2">Aceleração de download</a></td>
		<td >O CDN fornece aceleração de download estável e de alta qualidade para jogos, aplicativos ou pacotes de instalação de ROM.</td>
	</tr>
	<tr>
		<td><a href = "#m3">Aceleração de áudio/vídeo</a></td>
		<td>Com o suporte da profunda experiência da Tencent em operação de vídeo online, o CDN consegue sustentar grandes volumes de solicitações simultâneas para reprodução de áudio e vídeo online durante os horários de pico, garantindo de forma eficaz a alta disponibilidade de serviço e velocidade de transferência de mídia, ao mesmo tempo em que fornece uma experiência de visualização estável, perfeita e aprimorada. </td>
	</tr>
	<tr>
		<td><a href = "#m4">ECDN</a></td>
		<td >O Enterprise Content Delivery Network (ECDN) é um produto autônomo do Tencent Cloud para aceleração completa de recursos dinâmicos ou dinâmico-estáticos. Ele consegue identificar recursos dinâmicos e estáticos automaticamente enquanto implementa a aceleração simultânea para todos os tipos de recursos em uma única plataforma. </td>
	</tr>
	<tr>
		<td><a href = "#m5">SCDN</a></td>
		<td >O SCDN do Tencent Cloud fornece recursos avançados de proteção de segurança, além de todas as vantagens de aceleração do CDN. Ele pode proteger contra ataques DDoS de alto tráfego e ataques CC em grande escala e fornecer WAF contra invasões de sites. Você pode conectar-se rapidamente e habilitar o SCDN no CDN.</td>
	</tr>
</tbody>
</table>
## Descrições dos casos de uso
<span ID = "m1"></span>
### Aceleração de sites
A aceleração de sites é adequada para todos os tipos de sites, como portais da Web, plataformas de comércio eletrônico e comunidades UGC. O CDN pode armazenar em cache e acelerar a entrega de conteúdo estático em seus sites. Para acelerar o conteúdo dinâmico, use o [ECDN](https://intl.cloud.tencent.com/product/ecdn).

<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>O que são conteúdos estático e dinâmico?
</div>
<p></p>	
<ul>	
<li>O conteúdo estático refere-se ao conteúdo que permanece o mesmo quando solicitado. <br>Exemplos: arquivos .html, .css e .js, imagens, vídeos, pacotes de instalação de software, arquivos APK e arquivos compactados.</li>
<li>O conteúdo dinâmico refere-se ao conteúdo que varia quando solicitado. <br>Exemplos: APIs e arquivos .jsp, .asp, .php, .perl e .cgi.</li>
</ul>	
</blockquote>
O CDN fornece recursos avançados de entrega de conteúdo estático, acelerando significativamente o carregamento de páginas e oferecendo uma experiência de navegação fácil e rápida para os usuários finais em localizações diferentes. Durante os picos de serviço, quando há uma grande quantidade de usuários simultâneos, ele pode aliviar a pressão sobre os servidores de origem para garantir acesso estável e sem problemas a serviços e páginas da Web.
![](https://main.qcloudimg.com/raw/c2291b131ce33d1eb39ec35167453437.png)


<span ID = "m2"></span>
### Aceleração de download
A aceleração de download é adequada para acelerar o download de vários arquivos, como jogos, aplicativos e pacotes de instalação de ROM

Apoiado por uma enorme quantidade de largura de banda elástica reservada, o CDN consegue sustentar picos de tráfego e acelerar o download de arquivos grandes, garantindo a estabilidade do serviço e fornecendo uma experiência de download eficiente para todos os usuários finais.
![](https://main.qcloudimg.com/raw/ada400d5a04d58fb73662e6bc028232c.png)


<span ID = "m3"></span>
### Aceleração de áudio/vídeo
A aceleração de áudio/vídeo é adequada para diferentes tipos de sites e aplicações de áudio/vídeo sob demanda, como aplicativos de áudio/vídeo, plataformas de áudio/vídeo online e IPTV. Com recursos aprimorados de entrega de conteúdo e apoiado pela profunda experiência da Tencent em operação de vídeo online, o CDN do Tencent Cloud consegue efetivamente garantir uma reprodução de áudio/vídeo perfeita para todos os usuários finais durante os horários de pico com grandes volumes de solicitações simultâneas.
![](https://main.qcloudimg.com/raw/0e852cfff1cd2f131f3ab1256a5b3a51.png)


<span ID = "m4"></span>
### ECDN
O [ECDN](https://intl.cloud.tencent.com/product/ecdn) é adequado para sites e aplicações com recursos híbridos dinâmicos/estáticos ou uma grande quantidade de recursos dinâmicos, como arquivos .asp, .jsp, .php, .cgi. e .perl, APIs e solicitações de interação de banco de dados.

Ao integrar o cache de borda estático com a otimização dinâmica de rotas de pull de origem, programando de forma inteligente as solicitações para os nós de serviço ideais, identificando automaticamente recursos estáticos e dinâmicos e utilizando o algoritmo de cálculo de rotas ideais proprietário da Tencent e a tecnologia de otimização de TCP, o ECDN, atualmente um produto autônomo, consegue fornecer aos usuários finais uma experiência de aceleração completa e de alto desempenho.
![](https://main.qcloudimg.com/raw/a6f7d54e98720a3d4a18d673fc1f9b4c.png)

<span ID = "m5"></span>

### SCDN
Ao integrar o cache de borda estático com a otimização de rotas de pull de origem dinâmica, programando de forma inteligente as solicitações para os nós de serviço ideais, identificando automaticamente recursos estáticos e dinâmicos e utilizando o algoritmo de cálculo de rotas ideais proprietário da Tencent e a tecnologia de otimização de TCP, o SCDN, atualmente um produto autônomo, consegue fornecer aos usuários finais uma experiência de aceleração completa e de alto desempenho.
O SCDN é baseado no CDN e não é necessário refazer a configuração de DNS. A proteção de segurança de rede pode ser ativada rapidamente para nomes de domínio acelerados pelo CDN. 
![](https://main.qcloudimg.com/raw/164d28b237eb5dbe05a57b631d98616e.png)



​	