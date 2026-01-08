mutillidae

OWASP 2013 > Insecure Direct Object Reference > Text File Viewer

O site se trata de uma página que lê um determinado arquivo fornecido pelo usuário.
Para inspecionarmos, vamos utilizar o Burp Suite.

Assim, vemos que a página possui o parâmetro "textfile=" na requisição, passando um endereço logo em seguida.
Temos a possibilidade de modificar essa requisição, passando qualquer página desejada.
	textfile=http://google.com

Também podemos visualizar arquivos do sistema:
	textfile=../../../../../../etc/passwd

É importante lembrar que, por se tratar de um Directory Traversal, a página apenas visualiza o conteúdo de determinado arquivo.
Na prática, isso significa que não é possível executar códigos como no RFI ou LFI.
