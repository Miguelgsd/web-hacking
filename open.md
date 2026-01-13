# Open Redirect
## Uma vulnerabilidade que não afeta tanto o servidor, mas pode ser usada para phishing e engenharia social.
O Open Redirect ocorre quando uma aplicação web aceita um input do usuário (geralmente via parâmetro na URL) para determinar para onde o usuário deve ser redirecionado após uma ação (como fazer login ou mudar o idioma), sem validar se o destino é um domínio confiável.  

### Cenários de Ataque
A falha surge quando a aplicação confia cegamente no parâmetro de redirecionamento. O desenvolvedor utiliza funções como `header("Location: " . $_GET['redirect']);` em PHP ou `redirect(params[:url])` em Rails.  
Exemplos comuns:  
1. **Login**: `site.com/login?forward=dashboard`
2. **Idioma**: `site.com/setlang?url=/en/home`
3. **Links Externos**`site.com/out?url=http://google.com`

### Exploração
O objetivo do Open Redirect não é roubar dados do servidor, mas usar o nome do site para enganar uma vítima. Um exemplo disso é:  
1. O atacante cria uma página de login falsa idêntica à do site original;
2. Explorando o parâmetro vulnerável, ele adiciona sua própria URL, ficando assim:  
   `https://banco.com/login?redirect=https://atacante.com/login`
   
   Perceba que o domínio original do "banco" ainda é o mesmo, mas o usuário será redirecionado para uma página falsa por causa do `?redirect=`. Por isso, é importante verificar não apenas o domínio, mas o link inteiro.  
   Essa falha também pode ser usada para redirecionar o usuário para o download automático de um malware.

### Exemplos Práticos
Para praticar os conhecimentos adquiridos, veja os seguintes laboratórios:  
* [Juice Shop](https://juice-shop.herokuapp.com/)
* [PortSwigger](https://portswigger.net/web-security/dom-based/open-redirection)
