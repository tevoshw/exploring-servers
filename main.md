# 1. O que é

Servidores são basicamente computadores — a diferença não é o hardware em si, 
é o **papel**: uma máquina dedicada a ficar ligada o tempo todo, escutando 
requisições e entregando respostas/recursos pra outras máquinas (clientes).

- Pode ser um computador físico dedicado (data center, on-premise)
- Pode ser uma máquina virtual (VM) numa cloud (AWS EC2, GCP Compute Engine)
- Pode ser até seu próprio notebook rodando um `uvicorn` — tecnicamente, 
  nesse momento, ele é um servidor

O que define "servidor" não é o tamanho ou a marca, é a **função**: estar 
sempre disponível, escutando portas, esperando conexões.

# 2. Estrutura (Hardware)

- **Placa-mãe** — conecta todos os componentes entre si
- **CPU** — processa as instruções, lida com lógica geral e requisições
- **GPU** — processamento paralelo; essencial em servidores de ML/IA 
  (treino e inferência de modelos)
- **RAM** — memória volátil, guarda dados em uso ativo (quanto mais RAM, 
  mais conexões/processos simultâneos o servidor aguenta)
- **HD/SSD** — armazenamento persistente (SSD é padrão hoje em servidores 
  por velocidade de I/O)
- **Placa de rede (NIC)** É por ela que o servidor 
  literalmente se conecta à rede, envia/recebe pacotes (tem IP associado a ela)
- **Fonte de alimentação (PSU)** — em servidores reais, geralmente redundante 
  (duas fontes, caso uma falhe)

## Diferença de hardware servidor vs desktop comum

| Componente | Servidor | Desktop comum |
|------------|----------|----------------|
| CPU | Muitos núcleos, otimizado pra multitarefa | Poucos núcleos, otimizado pra tarefas únicas |
| RAM | ECC (correção de erro), grande volume | Comum, sem correção de erro |
| Disco | RAID (redundância), hot-swap | Único disco, sem redundância |
| Uptime esperado | 24/7, anos sem desligar | Liga/desliga normal |
# 3. Rede

- **IP**: É um endereço virtual de uma máquina, toda máquina possui, podendo ser:
    * **Público** = Roteável globalmente pela internet. Alcançável diretamente 
      de qualquer lugar (se não houver firewall bloqueando).
    * **Privado** = Só existe/é reconhecido dentro da própria rede local. 
      Não é roteável pela internet — pra sair, precisa de um intermediário 
      (roteador/NAT) que "empresta" um IP público.

    Todo IP possui uma versão, as mais famosas são:
    - **IPv4** = Um IP de 4 componentes (octetos), cada um de 0-255. Ex: `192.168.1.1`
    - **IPv6** = Um IP de 8 componentes (grupos hexadecimais). Ex: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

## Público vs Privado, na prática

- **Máquinas na mesma rede local** (mesmo range de IP privado) se comunicam 
  **direto**, sem precisar de IP público nem intermediário.
- **Máquinas em redes diferentes** (cidades/redes distintas) só se comunicam 
  através de **IPs públicos**, porque só eles são únicos e roteáveis no mundo todo.
- **IP privado não consegue "aparecer" sozinho na internet** — precisa de um 
  intermediário (roteador de casa, NAT Gateway na AWS) que faz a tradução 
  IP privado ↔ IP público (chamado **NAT**).
- **IP público não precisa de tradução** — só precisa de uma conexão com a 
  internet (ex: Internet Gateway, na AWS).

## DNS

DNS (Domain Name System) é o sistema responsável por traduzir nomes de domínio em endereços IP.

Computadores se comunicam usando endereços IP, mas nós normalmente usamos nomes como google.com. O DNS faz essa tradução.

google.com
    ↓

   DNS
   ↓

142.250.x.x

> Um exemplo de um provedor de DNS é o cloudfare

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
