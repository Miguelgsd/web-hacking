Com o Reverse DNS Lookup, é possível checar se há domínios ou subdomínios relacionados com o site alvo.

Tabela DNS:
Também é possível ver a tabela de servidores DNS do domínio alvo:
whois:
whois google.com
   Domain Name: GOOGLE.COM
   Name Server: NS1.GOOGLE.COM
   Name Server: NS2.GOOGLE.COM
   Name Server: NS3.GOOGLE.COM
   Name Server: NS4.GOOGLE.COM

dig @8.8.8.8 globo.com ANY
	|       |       |
        |       |  <Tipo de entrada (qualquer uma)>
	|      <alvo>
<servidor DNS do Google>

AA/AAAA - Hosts e IPs reais
MX - fornecedores de email ou IPs de email
NS/SOA - onde tentar transferir zona (AXFR) e saber o master.
PTR - pode revelar nomes associados a IPs (reverso).
TXT - chaves, políticas, verificações (às vezes credenciais/leads acidentais).
SRV - serviços internos (VoIP, XMPP, LDAP, etc.).
AXFR - se permitido, lista completa de registros da zona — ouro puro para recon.
ANY - tentativa rápida de listar, mas pouco confiável hoje; muitos servidores retornam resposta limitada ou REFUSED.

