Um ataque de XSS ocorre quando um atacante usa sites ligítimos para enviar scripts maliciosos a um usuário. Isso pode ocorrer por meio de campos de entrada sem validação ou codificação.
Uma forma de identificar é procurar por parâmtros na URL que são refletidos na página ou casos onde um dado inserido em um campo de entrada também é exibido dessa forma.

Um ataque de XSS pode adotar 3 formas:
	Reflected XSS ->	Pode ocorrer na exploração de parâmetros; um exemplo de uso seria quando um atacante cria um script malicioso que captura os cookies do usuário e os envia para um servidor de seu domínio. Quando o usuário clicar no link (onde o script foi injetado), seu navegador automaticamente irá executar o código.
	Stored XSS ->		Ocorre quando o script malicioso fica permanentemente salvo no servidor-alvo. Um exemplo bem comum é em fóruns, onde todos os usuários tem a possibilidade de escrever algo e salvar em servidores. Na prática, um atacante iria criar um script malicioso e inserir no campo de entrada. Quando fosse salvo, o código ficaria disponível na página inicial e, quando qualquer pessoa acessasse, ele seria executado pelo navegador.
	DOM based XSS ->	Ocorre quando não há interação com o servidor: o JavaScript do navegador da vítima faz o trabalho completo, pegando dados da URL e injetando no Document Object Model (DOM) do navegador sem sanitização. Não aparece em logs e pode causar um bypass de WAFs.

---------------------------------------------------------------------------------------------------------------------------
Exemplo de Stored XSS no Mutillidae

OWASP 2013 > Cross Site Scripting > Persistent > Add to your blog

A vulnerabilidade Stored XSS nos permite injetar códigos JavaScript maliciosos e armazená-los no sistema.
Isso é perigoso pois o código será executado pelo navegador de todas as pessoas que acessarem a página.
Exemplo:
	Vá no campo de entrada do site e digite:
	<script>alert("Hello World")</script>
	Isso fará com que o código fique armazenado no blog, sendo executado por todos que acessarem.

Veja a aba "Hints ans Videos" 
---------------------------------------------------------------------------------------------------------------------------

Alguns casos de XSS:
	eBay		Reflected XSS	Parâmetro "url" não validado permitiu redirecionamentos maliciosos, roubando sessões de usuários.
	WhatsApp	Reflected XSS 	XSS via link em chamadas instalou spyware (NSO Group), afetando 1,5 bilhão de usuários.
	Spotify		Reflected XSS	Redirecionamento via "javascript:" em URLs permitiu execução de JS, roubando sessões.
	eBay		Stored XSS		XSS em listagens de veículos permitiu roubo de credenciais, criando mais fraudes.
