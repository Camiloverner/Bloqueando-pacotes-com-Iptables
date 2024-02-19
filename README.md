# Bloqueando pacotes invalidos com Iptables
Abaixo esão alguns comandos da ferramenta Iptables. Estou colocando-os aqui para sempre lembrar de usa-los quando necessário.

<h3>👾  O código</h3>

~~~shellscript
iptables -t mangle -A PREROUTING -m conntrack --ctstate INVALID -j DROP
~~~

Resumindo, esse comando descarta pacotes com estado de conexão inválido antes mesmo de serem roteados para dentro do sistema. Isso pode ser útil para filtrar pacotes suspeitos ou malformados que podem representar uma ameaça à segurança do sistema.

~~~shellscript
iptables -t mangle -A PREROUTING -p tcp  ! --syn -m conntrack --ctstate NEW -j DROP
~~~

Esta regra do iptables descarta pacotes TCP que não estão iniciando uma nova conexão (ou seja, que não possuem o flag SYN), aplicando-se a pacotes que estão no estágio inicial da conexão TCP. Isso pode ser usado como uma medida de segurança para proteger contra certos tipos de ataques, como ataques de inundação SYN.

É importante ressaltar que, ao bloquear pacotes inválidos, é possível que alguns pacotes legítimos sejam bloqueados por engano. Por isso, é recomendável monitorar os logs do sistema e ajustar as regras do iptables conforme necessário.
