# WHOIS
## O Whois é uma ferramenta para os primeiros passos de um reconhecimento passivo.  

Por meio dele, é possível descobrir informações interessantes sobre o alvo; entre elas, vale destacar:  
* **Nameservers (NS)**: Revelam onde o site está hospedado (ex: AWS, Cloudflare, DigitalOcean).
* **Registrant Email**: Útil para identificar outros domínios da mesma pessoa (através de Reverse WHOIS) ou para ataques de engenharia social (phishing).
* **Datas (Created/Updated/Expires)**: Domínios criados muito recentemente podem indicar sites temporários ou infraestruturas de ataque, enquanto domínios antigos mostram maturidade.
* **NetRange (Consultando o IP)**: Se você fizer um WHOIS no IP em vez do domínio, descobrirá o tamanho do bloco de rede (CIDR) da empresa (ex: /24), o que expande seu escopo de ataque.

### Redacted for Privacy
Por causa da LGPD e GDPR, muitos dados do Whois são ocultos com `REDACTED FOR PRIVACY`. Quando isso acontece, é necessário o uso de outras ferramentas para descobrir novas informações sobre o alvo.

---
Exemplo de uso no bancocn.com (alguns textos foram excluídos para não "poluir", mantendo apenas o essencial):  

```txt
	Domain Name: BANCOCN.COM
	   Registry Domain ID: 2109524495_DOMAIN_COM-VRSN
	   Registrar WHOIS Server: whois.registrar.amazon
	   Registrar URL: http://registrar.amazon.com
	   Updated Date: 2025-02-23T22:05:34Z
	   Creation Date: 2017-03-29T21:16:53Z
	   Registry Expiry Date: 2026-03-29T21:16:53Z
	   Registrar: Amazon Registrar, Inc.
	   Registrar IANA ID: 468
	   Registrar Abuse Contact Email: trustandsafety@support.aws.com
	   Registrar Abuse Contact Phone: +1.2024422253
	   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
	   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
	   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
	   Name Server: MEGAN.NS.CLOUDFLARE.COM
	   Name Server: NOEL.NS.CLOUDFLARE.COM
	   DNSSEC: unsigned
	   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
	>>> Last update of whois database: 2026-01-09T12:02:13Z <<<
	
	Domain Name: bancocn.com
	Registry Domain ID: 2109524495_DOMAIN_COM-VRSN
	Registrar WHOIS Server: whois.registrar.amazon
	Registrar URL: https://registrar.amazon.com
	Updated Date: 2025-02-23T22:05:34Z
	Creation Date: 2017-03-29T21:16:53Z
	Registrar Registration Expiration Date: 2026-03-29T21:16:53Z
	Registrar: Amazon Registrar, Inc.
	Registrar IANA ID: 468
	Registrar Abuse Contact Email: trustandsafety@support.aws.com
	Registrar Abuse Contact Phone: +1.2024422253
	Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
	Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
	Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
	Registry Registrant ID: Not Available From Registry
	Registrant Name: On behalf of bancocn.com owner
	Registrant Organization: Identity Protection Service
	Registrant Street: PO Box 786
	Registrant City: Hayes
	Registrant State/Province: Middlesex
	Registrant Postal Code: UB3 9TR
	Registrant Country: GB
	Registrant Phone: +44.1483307527
	Registrant Phone Ext:
	Registrant Fax: +44.1483304031
	Registrant Fax Ext:
	Registrant Email: 25b89f28-0af5-4973-89ae-677aa309f5cd@identity-protect.org
	Registry Tech ID: Not Available From Registry
	Tech Name: On behalf of bancocn.com owner
	Tech Organization: Identity Protection Service
	Tech Street: PO Box 786
	Tech City: Hayes
	Tech State/Province: Middlesex
	Tech Postal Code: UB3 9TR
	Tech Country: GB
	Tech Phone: +44.1483307527
	Tech Phone Ext:
	Tech Fax: +44.1483304031
	Tech Fax Ext:
	Tech Email: 25b89f28-0af5-4973-89ae-677aa309f5cd@identity-protect.org
	Name Server: NOEL.NS.CLOUDFLARE.COM
	Name Server: MEGAN.NS.CLOUDFLARE.COM
	DNSSEC: unsigned
	>>> Last update of WHOIS database: 2026-01-09T12:02:22Z <<<
```

### Analisando os resultados, notamos que:  
* O uso de NS.CLOUDFLARE.COM indica que o site provavelmente está atrás de um firewall de aplicação web (WAF) e CDN.
* O domínio foi registrado via Amazon (AWS), sugerindo que a aplicação pode estar hospedada em instâncias EC2 ou S3.
* O e-mail e a organização estão sob um serviço de proteção (Identity Protection Service), o que impede a descoberta direta do dono real, exigindo técnicas de reconhecimento mais avançadas.
