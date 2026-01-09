# Reverse DNS Lookup
### O Reverse DNS Lookup é o processo inverso da consulta DNS comum.  
Enquanto o DNS padrão traduz um nome de domínio em um endereço IP, o reverso traduz um endereço IP em um nome de host.

### Registros
Para realizar consultas reversas de DNS, é necessário entender os registros:  

| Registro | O que revela          | Valor                                                                             |
|----------|-----------------------|-----------------------------------------------------------------------------------|
| A/AAAA   | Endereços IPv4 e IPv6 | Identifica o IP direto do servidor (alvo para scans de porta).                    |
| MX       | Servidores de email   | Revela o provedor (ex: Outlook, Google) e possíveis vetores de phishing.          |
| NS       | Name Servers          | Indica quem gerencia a zona e é o alvo para tentativas de AXFR.                   |
| TXT      | Politicas             | Muitas vezes contém informações de serviços (AWS, Azure) e até chaves esquecidas. |
| SRV      | Servicos especificos  | Revela serviços internos como LDAP ou SIP que podem estar expostos.               |
| PTR      | Registro Reverso      | Oposto do registro 'A'; resolve um IP para um nome de host.                       |
