# XSS
### O XSS é uma vulnerabilidade que ocorre quando um atacante consegue injetar scripts maliciosos (geralmente JavaScript) em páginas web visualizadas por outros usuários. Diferente de outros ataques, o alvo principal aqui não é o banco de dados, mas a sessão e os dados do navegador da vítima.

## Como identificar?
A forma mais comum de identificar o XSS é buscar por pontos de entrada (inputs, parâmetros de URL, formulários) cujos dados são refletidos na página sem a devida sanitização ou codificação (encoding).

## Tipos
Um ataque de XSS pode adotar 3 formas:  
* **Reflected XSS** ->	Permite ao atacante inserir scripts maliciosos em Javascript em um parâmetro vulnerável do site. Precisa de interação direta com o usuário, envolvendo um pouco de engenharia social. Ao clicar no link com o script malicioso, o navegador da vítima executa o código sem que ela perceba, podendo ocasionar em roubos de sessão.  
* **Stored XSS** ->		Sendo relativamente mais perigoso que o Reflected, o Stored XSS consiste em armazenar o script malicioso na página vulnerável. Desta vez, não é necessário uma interação direta com o usuário. Alguns dos cenários possíveis são fóruns vulneráveis ou sistemas de avaliações de produtos, onde o atacante pode inserir um determinado texto que será mostrado para todos que visitarem a página. Injetando um payload Javascript, o navegador de qualquer usuário irá executá-lo automaticamente ao carregar a página.  
* **DOM based XSS** ->	Diferente dos anteriores, este ocorre inteiramente no lado do cliente (client-side). O script malicioso é executado quando o JavaScript legítimo da página lê dados de uma fonte controlada pelo usuário (como a fragmentação da URL após o #) e os escreve de forma insegura no DOM. Para a vantagem do atacante, como os dados após o # muitas vezes não são enviados ao servidor, o ataque pode passar despercebido por logs de servidor e WAFs (Web Application Firewalls).

---
**Exemplos**  
Alguns exemplos de scripts que podem ser usados, dependendo do contexto, são:  
```html
	1. <script>alert('XSS!')</script>  
	2. <script>print()</script>
	3. <script>alert(document.domain)</script>  
	4. <img src="x" onerror="alert(1)">
	5. <input autofocus onfocus="alert(1)">  
	6. <video><source onerror="alert(1)">
	7. <a href="javascript:alert(1)">Teste</a>  
```
Apenas se lembre de que, como pentester, você deve avaliar o contexto e descobrir o que irá se encaixar melhor em sua situação. Não é garantido que eles irão funcionar sempre.

## Prevenção

Algumas formas de prevenção são:  
1. **Output Encoding**: Converter caracteres especiais (como < para &lt;) antes de exibir no HTML.  
2. **Content Security Policy (CSP)**: Uma camada de segurança extra que ajuda a detectar e mitigar ataques XSS, restringindo de onde os scripts podem ser carregados.  
3. **HttpOnly Flags**: Configurar cookies com a flag HttpOnly impede que o JavaScript acesse os cookies, anulando ataques de roubo de sessão via XSS.  

---
## Exemplos práticos
Para se ter um pouco de prática, irei listar alguns sites interessantes onde é possível (e autorizado) explorar essas falhas:  
* [Laboratórios do PortSwigger](https://portswigger.net/web-security/all-labs#cross-site-scripting)
* [Google XSS Game](https://xss-game.appspot.com/)
* [Juice Shop](http://juice-shop.herokuapp.com/#/)
