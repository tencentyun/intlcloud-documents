Após receber um pacote ACK de handshake triplo do soquete de escuta, o kernel do Linux entra no status TCP_ESTABLISHED de SYN_REVC. O kernel chama a função tcp_v4_syn_recv_sock.
A função de gancho tcp_v4_syn_recv_sock_toa chama a função tcp_v4_syn_recv_sock original primeiro, depois extrai TOA OPTION de TCP OPTION chamando a função get_toa_data e salva-a no campo sk_user_data.

Depois que a chamada acima for concluída, o kernel chama inet_getname_toa hook inet_getname para obter o IP de origem e a porta. Primeiro, ele chama o inet_getname original e verifica se o campo sk_user_data está vazio. Se o IP real e a porta puderem ser extraídos desse campo, os valores retornados de inet_getname serão substituídos por esses dois valores.

O programa do servidor chama getpeername no modo de usuário, e o IP original e a porta do cliente serão retornados.
