### Conexões simultâneas
| Conexões simultâneas    | PPS     | HTTP-QPS | HTTPS-QPS |
|-------|---------|----------|-----------|
| 20.000   | 80.000   | 14.000    | 900       |
| 50.000   | 120.000  | 21.000    | 1.350      |
| 100.000  | 200.000  | 35.000    | 2.250      |
| 200.000  | 400.000  | 70.000    | 4.500      |
| 300.000  | 600.000  | 105.000   | 6.750      |
| 400.000  | 800.000  | 140.000   | 9.000      |
| 500.000  | 1.000.000 | 175.000   | 11.250     |
| 600.000  | 1.200.000 | 210.000   | 13.500     |
| 700.000  | 1.400.000 | 245.000   | 15.750     |
| 800.000  | 1.600.000 | 280.000   | 18.000     |
| 900.000  | 1.800.000 | 315.000   | 20.250     |
| 1.000.000 | 2.000.000 | 350.000   | 22.500     |


## Quantidade de listeners
- Para regiões de aceleração com nós da Tencent Cloud implantados, é possível adicionar no máximo 200 listeners. Para aumentar o limite superior, você pode enviar um tíquete para entrar em contato conosco.
- Para regiões de aceleração com nós de parceiros implantados, é possível adicionar no máximo 20 listeners. Para aumentar o limite superior, você pode enviar um tíquete para entrar em contato conosco.
- É possível criar um máximo de 20 listeners TCP/UDP por vez.
- É possível criar apenas um listener HTTP/HTTPS por vez.

## Intervalo de portas do listener
O intervalo de portas válido é de 1 a 64999 (a porta 21 não está disponível no momento).

## Quantidade de conexões
É possível criar até 20 conexões em um grupo de conexões.

## Listener TCP/UDP
É possível vincular um máximo de 100 servidores de origem a um listener.

## Listener HTTP/HTTPS
- É possível adicionar até 100 nomes de domínio a um listener.
- É possível adicionar até 20 regras a um nome de domínio.
É possível vincular até 100 servidores de origem a uma regra.

## Quantidade de nomes de domínio unificado
É possível criar até 5 nomes de domínio, por padrão. Para aumentar o limite superior, você pode enviar um tíquete para entrar em contato conosco.

## Quantidade de regras de segurança
É possível criar até 100 regras de segurança, por padrão. Para aumentar o limite superior, você pode enviar um tíquete para entrar em contato conosco.
