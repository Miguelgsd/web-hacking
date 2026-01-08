mutillidae

Parecido com o RFI, o Local File Inclusion é possível por causa da mesma vulnerabilidade na URL.
A diferença é que agora vamos acessar arquivos do próprio sistema do alvo. Ou seja, vamos acessar arquivos locais.

	?page=../../../../../../../../../../../../etc/passwd

Isso retornará as senhas salvas no sistema.
