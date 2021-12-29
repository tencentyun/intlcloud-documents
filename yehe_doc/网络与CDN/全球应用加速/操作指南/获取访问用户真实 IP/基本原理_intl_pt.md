## Obtenção de IPs reais de cliente por meio do TOA
Quando uma conexão de aceleração encaminha o pacote de dados, SNAT e DNAT serão executados no pacote; ou seja, os endereços de origem e destino do pacote de dados serão modificados. O endereço de origem do pacote visto pelo servidor de origem será o endereço IP de encaminhamento da conexão de aceleração, em vez do IP real do cliente. Para passar o IP do cliente ao servidor, a conexão de aceleração incluirá o IP do cliente e a porta no campo personalizado `tcp option` ao encaminhar o pacote, conforme mostrado abaixo:
```
#define TCPOPT_ADDR  200    
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

/*
 * insert client ip in tcp option, now only support IPV4,
 * must be 4 bytes alignment.
 */
struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
};
```

## Obtenção de IPs reais de cliente por meio do protocolo de proxy
O protocolo de proxy facilita a transmissão de informações do cliente (como pilha de protocolo, IP de origem, IP de destino, porta de origem e porta de destino etc.) adicionando um cabeçalho ao TCP, que é ideal para casos em que a condição da rede é complexa e os IPs do cliente são necessários. Durante esse processo, o proxy insere um pacote de dados contendo as informações quádruplas da conexão original na conexão após o handshake triplo.

Para obter os IPs do cliente usando o método do protocolo de proxy, primeiro é necessário configurá-lo no console. Ele só pode ser configurado para listeners com TCP. Após o serviço de aceleração ser conectado ao servidor de origem, o texto do protocolo de proxy será inserido no pacote `payload` transmitido pela primeira vez.

Atualmente, o Nginx e o HAProxy aceitam o protocolo de proxy. Para a configuração do protocolo de proxy no Nginx, basta adicionar `proxy_protocol` após o comando `listen` no trecho `server`.
```
http {
    #...
    server {
        listen 80   proxy_protocol;
        listen 443  ssl proxy_protocol;
        #...
    }
}
```

 Para programas que não aceitam o protocolo de proxy, após a configuração da conexão TCP, é necessário analisar a string de texto do protocolo de proxy da seguinte forma para obter os IPs do cliente:
 ```
 PROXY TCP4 1.1.1.2 2.2.2.2 12345 80\r\n
 ```
