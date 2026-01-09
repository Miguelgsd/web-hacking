# Server-Side Request Forgery
### O SSRF é uma vulnerabilidade que permite a um atacante forçar o servidor a realizar requisições HTTP para destinos que o atacante escolher. Geralmente, o alvo são sistemas internos que estão atrás de um firewall e não podem ser acessados diretamente pela internet.

## Cenários e Tipos
A falha surge quando uma aplicação precisa buscar recursos externos (como uma foto de perfil de outro site, integração com APIs ou validação de URLs) e confia no input do usuário sem validar se o destino é seguro.  

**Tipos:**  
1. **SSRF contra o próprio servidor (localhost)**  
   Neste cenário, o atacante força o servidor a requisitar serviços rodando em loopback. Um exemplo é:  
   `stockApi=http://stock.weliketoshop.net:8080/check` -> realiza uma requisição a uma API.  
   `stockApi=http://localhost/admin` -> hacker altera a requisição e acessa o painel administrativo, burlando controles de acesso.

2. **SSRF contra outros sistemas internos**
   Neste outro cenário, o atacante irá utilizar o servidor vulnerável para descobrir e interagir com outros sistemas dentro da rede que não deveriam estar acessíveis externamente. Exemplo:
   `stockApi=http://192.168.0.15:5432` -> utiliza a mesma requisição de antes, mas tentando atingir outro alvo dentro da rede.

## Bypass de Filtros
Em alguns casos, os servidores podem bloquear certas palavras ou IPs, como "admin" ou "127.0.0.1". Para te dar uma possibilidade de escapar disso, listarei algumas formas representativas:

* **127.0.0.1**
  
  | Forma       | Representação |
  |-------------|---------------|
  | Abreviado   | 127.1         |
  | Decimal     | 2130706433    |
  | Hexadecimal | 0x7f000001    |
  | Octal       | 0177.0.0.1    |

* **Admin**
  | admin | %2561dmin                                |
  |-------|------------------------------------------|
  | admin | %2561%2564%256d%2569%256e (duplo encode) |
  | admin | ad%6din                                  |

---
## Exemplos Práticos
Para praticar a exploração dessa vulnerabilidade em ambientes autorizados, irei listar alguns sites:
* [Laboratórios do PortSwigger](https://portswigger.net/web-security/all-labs#server-side-request-forgery-ssrf)
* [Juice Shop](https://juice-shop.herokuapp.com/#/)
