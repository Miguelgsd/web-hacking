# Fundamentos de Redes
## A seguir, irei mostrar os principais fundamentos sobre Redes e Internet.

### Tipos de redes
* **LAN** (Local Area Network): imagine os dispositivos que estão conectados ao seu roteador. Todos eles formam uma LAN. Em uma LAN, cada dispositivo tem um IP privado, usado para a comunicação entre eles.  
* **WAN** (Wide Area Network): pense em redes LAN interligadas. Este conjunto de LANs formam uma WAN.  
* **PAN** (Personal Area Network): uma rede com alcance menor, mais usada em conexões Bluetooth.  
* **MAN** (Metropolitan Area Network): meio-termo entre LAN e WAN. Pense no caso em que uma prefeitura precisa interligar seus departamentos; a MAN é uma infraestrutura que une esses pontos.  

### Dispositivos de Rede
* **Repetidor**: É o dispositivo mais simples. Sua única função é receber um sinal elétrico ou óptico e regenerá-lo para que ele possa percorrer distâncias maiores sem perda de integridade.    
* **Hub**: Funciona como um repetidor com várias portas. Quando um dado chega em uma porta, o Hub o retransmite para todas as outras portas. Pode gerar problemas no tráfego (congestionamento) e de segurança (todos têm acesso aos dados enviados).  
* **Bridge**: A Bridge é usada para dividir uma rede grande em dois segmentos menores. Ela é mais inteligente que o Hub porque consegue ler o Endereço MAC dos dispositivos.  
* **Switch**: O Switch é, essencialmente, uma Bridge com várias portas. Ele é o "cérebro" da rede local (LAN).
* **Roteadores**: Enquanto o Switch conecta computadores, o Roteador conecta redes diferentes (ex: sua casa com a Internet). Trabalha com endereços IP e traduz o tráfego da rede privada para a rede pública.  

---

### Modelos Conceituais
Podemos dividir a comunicação entre dispositivos em camadas, e é isso que vemos nos modelos OSI e Kurose. Os dois tratam do mesmo assunto, mas possuem algumas diferenças, principalmente no número de camadas. Para este repositório, irei explorar o modelo de Kurose, por ser mais simples e prático.  
De acordo com esse modelo, podemos dividir a comunicação em 5 camadas: Físico, Enlace, Rede, Transporte e Aplicação:  

| Camada     | O que é                                                                             | Protocolos e Serviços            | Vulnerabilidades                                                                         |
|------------|-------------------------------------------------------------------------------------|----------------------------------|------------------------------------------------------------------------------------------|
| Aplicação  | É onde residem os protocolos que as aplicações usam para se comunicar pela rede.    | FTP, DNS, HTTP/HTTPS, SMTP, etc. | SQL Injection, XSS, XXE, SSRF, RFI, LFI, etc.                                            |
| Transporte | Responsável pela transferência de dados ponta a ponta entre processos de aplicação. | TCP e UDP                        | SYN Flood (DoS), TCP Session Hijacking e brute force.                                    |
| Rede       | Responsável por mover pacotes (datagramas) de um host de origem para um de destino. | IP.                              | IP Spoofing, ICMP Flooding e Poisoning de rota.                                          |
| Enlace     | Responsável por transferir dados entre nós vizinhos em um mesmo link.               | Enquadramento e MAC.             | ARP Spoofing, MAC Flooding e ataques contra o protocolo Spanning Tree (STP) em Switches. |
| Físico     | Lida com a transmissão bruta de bits pelo meio de comunicação.                      | Voltagens, transmissões e cabos  | Jamming, Sniffing físico e danos físicos à infraestrutura.                               |

---

### Protocolos de Rede
Sobre a comunicação, também temos diversos serviços que são executados em diferentes portas de um host. Veja os principais:

| Porta   | Protocolo         | Função                                                                                                          |
|---------|-------------------|-----------------------------------------------------------------------------------------------------------------|
| 80      | HTTP              | Protocolo base da web para transferência de hipertexto. Sem criptografia.                                       |
| 443     | HTTPS             | É o HTTP rodando sobre uma camada de criptografia (SSL/TLS). Padrão atual.                                     |
| 22      | SSH               | Protocolo para acesso a terminais remotos de forma criptografada. É o padrão para administrar servidores Linux. |
| 23      | Telnet            | Também serve para terminal remoto, mas não possui criptografia.                                                 |
| 21      | FTP               | Utilizado para transferência de arquivos.                                                                       |
| 53      | DNS               | Responsável por traduzir nomes de domínio (google.com) em endereços IP.                                         |
| 25      | SMTP              | Protocolo para o envio de e-mails entre servidores.                                                             |
| 135-139 | NetBIOS/Microsoft | Serviços de rede do Windows para descoberta e compartilhamento.                                                 |
| 3389    | RDP               | Protocolo da Microsoft para acesso à Área de Trabalho Remota do Windows.                                        |
| 143     | IMAP              | Protocolos para recebimento e sincronização de mensagens de e-mail no cliente do usuário.                       |
| 110     | POP3              | Mesmo que IMAP.                                                                                                 |
| 3306    | MySQL             | Um dos bancos de dados mais populares do mundo.                                                                 |

### Exemplos Práticos
Caso queira testar o que aprendeu, pode utilizar comandos de descoberta em rede, como o `nmap` e `wireshark`, ou acessar cursos com simuladores, como a [Cisco Networking Academy](https://www.netacad.com/about-networking-academy/packet-tracer/).
