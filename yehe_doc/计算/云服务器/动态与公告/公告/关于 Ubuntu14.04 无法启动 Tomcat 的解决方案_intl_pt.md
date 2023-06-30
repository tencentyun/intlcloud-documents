Foi detectado que quando o Tomcat ou o Hadoop é instalado através do comando apt-get em um CVM com Ubuntu14.04 adquirido da Tencent Cloud, ele consegue ouvir a porta, mas não consegue responder às solicitações. Já temos a solução. Recomendamos seguir as instruções abaixo para solucionar esse problema. 

### Causas
Esse problema é causado por um [problema conhecido do Java Runtime Environment](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6202721).

### Análise
Tanto o Tomcat quanto o Hadoop são desenvolvidos usando a API Java `java.security.SecureRandom`.
Por padrão, essa API usa o `/dev/random` como um gerador de números aleatórios em alguns JREs. O `/dev/random` processa ruídos ambientais detectados de dispositivos, tais como temperatura da CPU ou tempo do teclado para gerar entropia. No entanto, o ambiente virtual dos CVMs dificulta o acesso a tais ruídos e a geração de entropia, fazendo com que o `cat /dev/random` bloqueie a inicialização do Tomcat e o Hadoop.

### Solução
#### Modificação da configuração do JRE
Altere o `securerandom.source=file:/dev/urandom` no original `/etc/java-7-openjdk/security/java.security` (use a URL real) para `securerandom.source=file:/dev/./urandom`, para resolver esse problema.




