# Local File Inclusion (LFI)
## Semelhante ao RFI, mas com algumas diferenças importantes
Enquanto no RFI o servidor busca algo fora, no LFI o atacante manipula a aplicação para expor segredos que já estão guardados dentro do próprio servidor. O LFI ocorre quando uma aplicação web utiliza o input do usuário para montar o caminho de um arquivo que será carregado e lido localmente pelo servidor. Diferente do RFI, aqui o atacante não precisa de allow_url_include ativado, pois o alvo são os arquivos internos da própria máquina onde a aplicação está rodando.

### Cenários de Ataque
O LFI é extremamente comum em aplicações que implementam sistemas de "template" ou troca de idiomas via URL. Alguns exemplos de brechas são:
* **Falha na lógica**: O desenvolvedor usa `include($_GET['page']);` esperando que o usuário digite apenas home.php ou contato.php.
* **Falta de Sanitização**: A aplicação não filtra caracteres de navegação de diretório, como o `../`.
* **Permissões de Arquivo**: O servidor web (ex: usuário www-data) tem permissão de leitura em arquivos sensíveis do sistema.

### Exploração
1. **Directory Traversal**
   Por meio dessa técnica, é possível acessar arquivos do sistema alterando o diretório até chegar na pasta raiz. Exemplo:
   `?page=../../../../etc/passwd`
2. **PHP Wrappers**
   Muitas vezes, a aplicação força uma extensão no final (ex: adiciona .php). Para ler o código fonte de um arquivo sem que ele seja executado, usamos o filtro de conversão para Base64:  
   `page=php://filter/convert.base64-encode/resource=config.php`
   Dessa forma, o servidor retorna o código em Base64. Basta decodificar para ver as senhas do banco de dados em texto claro.

### RFI x LFI
Por mais que sejam parecidas, não confunda:
* **LFI**: O atacante inclui arquivos que já existem no servidor da vítima (ex: /etc/passwd).
* **RFI**: O atacante inclui arquivos de um servidor externo controlado por ele.

### Exemplos Práticos
Para colocar em prática os conhecimentos adquiridos, acesse os seguintes laboratórios:  
* [PortSwigger Labs](https://portswigger.net/web-security/all-labs#path-traversal)
* [TryHackMe](https://tryhackme.com/room/fileinc)
