加速チャネルがデータパケットを転送する際、データパケットは同時にSNATとDNATを行い、データパケットのソースアドレスと宛先アドレスのどちらも変更されます。オリジンサーバから見たデータパケットのソースアドレスは、クライアントの実IPではなく、加速チャネル転送IPアドレスです。クライアントIPをサーバーに転送するために、加速チャネルは転送時にクライアントのIPとPortをカスタムのtcp optionフィールドに入れます。以下に示すとおりです。
```
#define TCPOPT_ADDR  200    
#define TCPOLEN_ADDR 8      /* |opcode|size|ip+port| = 1 + 1 + 6 */

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
