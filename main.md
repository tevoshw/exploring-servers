# 1. O que é

Servidores são básicamente computadores


# 2. Estrutura (Hardware)
- PLACA-MÃE
- CPU
- GPU
- RAM
- HD/SSD

# 3. Rede
- IP: Ip é um endereço virtual de uma máquina, toda máquina possui, podendo ser:
    * Público = Pode ser acessado diretamente pela internet
    * Privado = Não pode ser acessado diretamente pela internet
    Todo IP Possui uma versão, as mais famosas são:
    - IPv4 = Um IP de 4 componentes (octetos), cada um de 0-255Ex: 192.168.1.1
    - IPv6 = Um IP de 8 componentes (grupos hexadecimais) Ex: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

- Gateway
- DNS

# 4. Portas

## O que são portas?
Imagine que uma máquina queira mandar/receber dados de outras máquinas. Apenas com o IP, seria tudo desorganizado — o sistema não saberia para qual aplicação/processo entregar os dados (não necessariamente "travamento", mas ambiguidade de destino). As portas existem para organizar isso: identificam qual processo específico deve receber os dados dentro da máquina.

Para melhor entendimento, imagine que um prédio é uma máquina, e seu endereço é o IP. Caso não houvesse portas, apenas 1 pessoa receberia tudo nesse caso, o porteiro e ele não saberia para qual morador entregar cada correspondência. Então as portas se tornam o número do apartamento,onde cada apartamento é uma aplicação/serviço diferente rodando na máquina.

Em resumo, as máquinas (IPs) trocam dados por meio de protocolos, e para os dados 
chegarem até a aplicação certa é preciso uma porta — senão viraria bagunça, 
já que a máquina não saberia pra qual processo entregar cada coisa.


- Portas abertas: São aquelas onde existe um processo/aplicação rodando e escutando (listening) — ou seja, aquela porta está pronta para aceitar conexões e receber dados que a aplicação vai interpretar segundo um protocolo.
- Portas fechadas: São aquelas onde não há nenhum processo escutando (a máquina recusa a conexão), OU onde existe um processo rodando mas o firewall está bloqueando o acesso externo a ela.


## Serviços escutando em portas
Nosso IP tem as 65 e poucas mil portas disponíveis para uso. Elas existem todas o tempo todo — mas ficam "fechadas"/inativas até que um serviço comece a escutar (listen) em uma delas. Quando isso acontece, a porta fica "aberta"e pronta pra receber conexões. Alguns exemplos de serviços
| Linguagem | Serviços comuns              |
|-----------|-------------------------------|
| Python    | Uvicorn, Gunicorn, Flask, Django, Jupyter |
| Java      | Tomcat, Jetty, Spring Boot, Kafka |
| C / C++   | Nginx, Apache, Redis, MySQL, PostgreSQL |
| Node.js   | Express, Fastify |
| Go        | net/http, Docker, Kubernetes |
| Rust      | Actix-web, Axum |

## Portas Conhecidas
Aqui vai alguns exemplos de portas conhecidas e famosas
| Porta | Serviço                  |
|-------|----------------------------|
| 20/21 | FTP                       |
| 22    | SSH                       |
| 23    | Telnet                    |
| 25    | SMTP (envio de e-mail)    |
| 53    | DNS                       |
| 80    | HTTP                      |
| 443   | HTTPS                     |
| 3306  | MySQL                     |
| 5432  | PostgreSQL                |
| 6379  | Redis                     |
| 8000  | APIs (FastAPI, dev comum) |
| 8080  | HTTP alternativa / proxies|
| 27017 | MongoDB                   |
