<h1 id="title"> Conventional commits usando commitlint, husky e commitzen </h1>

<p align="center" id="badges">
    <img loading="lazy" src="http://img.shields.io/static/v1?label=STATUS&message=EM%20DESENVOLVIMENTO&color=GREEN&style=for-the-badge" alt="Status Badge"/>
</p>

🚀 Doc simples de instalação das bibliotecas: commitlint, husky e commitzen

<h3 id="indice">Índice</h3>

* [Título](#title)
* [Badges](#badges)
* [Índice](#indice)
* [Introdução](#intro)
* [Installing](#installing)
* [Commitlint](#commitlint)
* [Husky](#husky)
* [Commitzen](#commitzen)
* [Conclusão](#conclusion)
* [Referências](#references)

<h3 id="intro">Introdução</h3>

Trouxe uma forma simplificada de usar essas bibliotecas para facilitar nosso sistema de commits dentro da *The Alfred*

*"Beleza, fiz tudo o que eu tinha que fazer :white_check_mark: , mas como eu vou nomear esse commit para que os outros entendam o que eu fiz?"*

Além da nossa doc explicando quando usar os títulos e como descrever nossos commits, resolvi trazer uma ferramente para automatizar essa ação e torna-la mais simples.


<h3 id="installing">Installing</h3>
Com projeto já iniciado, precisamos initiar nosso repositório git:
```git
  git init
```

Feito isso, vamos às bibliotecas:

<h4 id="commitlint">:Sparkles: Instalando o commitlint</h4>
* [Link para o site da biblioteca](https://commitlint.js.org/#/guides-local-setup)

Primeiro, instalamos a versão *CLI do commitlint* e as configurações do *Conventional Commits* como
dependencias de desenvolvedor:

```javascript
  yarn add @commitlint/cli @commitlint/config-conventional -D
```

Feita a instalação, precisamos configurar o arquivo commitlint.config.js extendendo a configuração que instalamos no passo anterior:

```javascript
  echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
```

<h4 id="husky">:wolf: Instalando o husky</h4>
* [Link para o site da biblioteca](https://typicode.github.io/husky/)

Para instalarmos o Husky precisamos dos seguintes comandos:

```javascript
  // Install husky
  yarn add --dev husky

  // iniciar o husky
  npx husky init
```

Após a instalação e inicialização do husky, você terá que criar um arquivo chamado **commit-msg** na pasta **.husky** para dar lint com o hook da commit-msg afim de que o husky exiba a verificação de um commit correto ou errado.

É só usar esse comando:

```javascript
  echo "npx --no -- commitlint --edit \$1" > .husky/commit-msg
```

Na nova versão do Husky, quando instalamnos o mesmo, um arquivo chamado **pre-commit** é gerado e no nosso caso não precisamos dele, você pode simplesmente apaga-lo usando `rm pre-commit`, apagando diretamente ou adicionando esse comando em algum script.

E assim você será capaz de verificar o funcionamento testando os commits.

```git 
  # Primeiro precisamos adicionar os arquivos para serem commitados
  git add .

  # Vamos fazer o commit falhar para ver se tudo está funcionando
  # Se o commit passar, algum passo até aqui deu errado
  git commit -m "qualquer coisa"

  # Agora vamos fazer o commit corretamente, nesse caso eu vou usar o tipo chore
  # Por se tratar de uma configuração no ambiente de desenvolvimento
  git commit -m "chore: add commitlint e husky"
```

<h4 id="commitzen">:sparkles: instalando o commitzen</h4>
* [Link para o site da biblioteca](https://commitizen.github.io/cz-cli/)

Agora que temos todo o necessário para automatizar nosso sistema de commits
podemos adicionar o commitzen, uma biblioteca que vai automaticamente nos dar as opções
de construção do commit:

```javascript
  # Instalando o commitizen
  yarn add commitizen -D

  # Criando a configuração
  yarn commitizen init cz-conventional-changelog --yarn --dev --exact

  # Add um script no package.json para disparar o commitizen
  "scripts": {
    "commit": "git-cz"
  }
```

Com a biblioteca instalada e configurada, vamos fazer um commit para entender o passo a passo que ela traz na prática.

```git 
  # Primeiro, precisamos adicionar os arquivos para serem commitados
  git add .

  # Agora vamos executar o script para iniciar a biblioteca
  yarn commit
```

Ao iniciar a biblioteca ela vai mostrar um passo a passo:

1) Select the type of change that you're committing: (Use arrow keys)

Selecione o tipo de mudança que você está realizando: (Use as teclas de seta)

* É só usar as setas e enter para selecionar um tipo.
2) What is the scope of this change (e.g. component or file name): (press enter to skip)

Qual é o escopo desta mudança (por exemplo, componente ou nome do arquivo): (pressione Enter para pular)

* **Exemplo:** chore(eslint): obrigar o uso de aspas duplas no jsx.
Em vez de colocar na mensagem do commit onde estava sendo feita a modificação, eu passei essa informação no escopo e a mensagem ficou mais sucinta.

3) Write a short, imperative tense description of the change (max 82 chars):

Escreva uma descrição breve e imperativa da mudança (máx. 82 caracteres):

* Utilizando o exemplo a cima, essa é a mensagem que sucede o dois pontos: obrigar o uso de aspas duplas no jsx
4) Provide a longer description of the change: (press enter to skip)

Forneça uma descrição mais longa da mudança: (pressione Enter para pular)

* Essa opção é opcional e geralmente eu não preencho, mas você pode inserir um contexto mais amplo que descreve a modificação que foi feita.
5) Are there any breaking changes? (y/N)

Existem alterações importantes? (y/N)

* A tradução não descreve bem essa opção, ela está ligada a quebra de compatibilidade estipulada pelo Semantic Versioning, se tiver conhecimento sobre isso, vai saber a resposta, senão quer dizer que não está fazendo versionamento e pode pular sem medo.
OBS: Sempre que estiver trabalhando no terminal e ele mostrar duas opções, sendo uma delas maiúscula, se pressionar enter ele seleciona a maiúscula que no caso é o N, ou você pode digitar N e pressionar enter.

6) Does this change affect any open issues? (y/N)

Essa mudança afeta algum problema em aberto? (y/N)

* Essa opção está ligada as Issues do GitHub, é uma opção mais avançada e não vou abordá-la nesse artigo, é só pressionar enter.
E pronto, o commit vai ser realizado.

Podemos digitar o comando `git log` no terminal para ver a lista com os últimos commits, e em primeiro lugar vai estar o commit gerado pelo commitizen.

<h3 id="conclusion">Conclusão</h3>

Legal né?  
Achou difícil?

* [x] Claro que não, facinho
* [ ] Muita informação :skull::skull:
* [ ] Mó fome

Espero que essa documentação tenha sido útil e te ajuda a instalar essas ferramentas de forma simples!! Meu objetivo é que deixemos as coisas mais fáceis e organizadas para que nosso trabalho possa fluir da melhor forma possível :heart:

<h3 id="references">Referências</h3>

* <https://dev.to/vitordevsp/padronizacao-de-commit-com-commitlint-husky-e-commitizen-3g1n>
* <https://medium.com/@abpeter14/how-to-install-commitlint-husky-2024-f1157f14006f>
* <https://typicode.github.io/husky/get-started.html>
* <https://www.youtube.com/watch?v=TpgxD84MwS4>
* <https://www.youtube.com/watch?v=Kn8pyfOyweo>
* <https://typicode.github.io/husky/>
* <https://commitlint.js.org/#/guides-local-setup>
* <https://commitizen.github.io/cz-cli/>
  
