# React + Express

## Introdução

Esse repositório visa demonstrar uma forma fácil de 'integrar' uma aplicação frontend usando React.js com um back end (bem simples, sem banco de dados) usando node.js (com Express, Nodemon e Concurrently).

## Tecnologias

| Tecnologia   | Uso      | Download                                              | Documentação                                                            |
| ------------ | -------- | ----------------------------------------------------- | ----------------------------------------------------------------------- |
| React.js     | Frontend | [npm](https://www.npmjs.com/package/create-react-app) | [reactjs.org](https://pt-br.reactjs.org/)                               |
| node.js      | Backend  | [nodejs](https://nodejs.org/en/download/)             | [nodejs.org](https://nodejs.org/)                                       |
| Express.js   | Backend  | [npm](https://www.npmjs.com/package/express)          | [expressjs.com](https://expressjs.com/)                                 |
| Nodemon      | Terminal | [npm](https://www.npmjs.com/package/nodemon)          | [nodemon.io](https://nodemon.io/)                                       |
| Concurrently | Terminal | [npm](https://www.npmjs.com/package/concurrently)     | [concurrently @ github](https://github.com/kimmobrunfeldt/concurrently) |

## Passo a Passo

Aqui vamos entender como replicar a solução, ao invés de simplesmente usar esse repositório. Para isso, dividiremos esse tutorial num passo a passo simples. O fluxo do projeto - _giitflow_ - também respeitará esses mesmos passos através da criação de _branches_, _commits_ e _pull requests_ (PRs).

### Passo 1 | Criando o Projeto

_Branch: [feature/01-init-projeto]_

Após criarmos o diretório (pasta) do nosso projeto, executaremos o código `npm init` para criarmos um arquivo _package.json_, no qual salvaremos nossos _scripts_, dependências e outras informações acerca do projeto. Isso pode ser feito através da sua IDE de prefência, do terminal ou do próprio sistema operacional que estiver usando (como Explorer do usuário Windows ou Finder no caso do usuário Mac).

Vamos ver como faríamos via terminal (a partir da pasta onde quer criar o projeto):

**1.1. Criando a pasta do nosso projeto**

``` sh
mkdir NomeDoProjeto
```

**1.2. Acessando essa pasta com o comando '_change directory_', o famoso `cd`**

``` sh
cd NomeDoProjeto
```

**1.3. Abrindo o projeto na nossa IDE de preferência**

``` sh
code .
```

**1.4. Iniciando nosso projeto**

``` sh
npm init
```

**1.5. Definindo parâmetros iniciais do nosso _package.json_**

Nesse caso basta preencher as informações solicitadas ou apertar 'Enter' para acatar as sugestões exibidas. No tópico _entry point_, podemos definir o nome `server.js` . No mais, fique à vontade para definir seus próprios valores.

Nosso arquivo _package.json_ final ficará semelhante ao seguinte:

``` json
{
  "name": "react-express",
  "version": "1.0.0",
  "description": "Integração simples do React.js com o node.js",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/Marcelo-Diament/react-express.git"
  },
  "keywords": [
    "reactjs",
    "nodejs",
    "expressjs",
    "concurrently",
    "nodemon",
    "frontend",
    "backend"
  ],
  "author": "Marcelo Diament",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/Marcelo-Diament/react-express/issues"
  },
  "homepage": "https://github.com/Marcelo-Diament/react-express#readme"
}

```

### Passo 2 | Instalando as Dependências

_Branch: [feature/01-init-projeto]_

Agora vamos deixar nossas dependências instaladas, no caso o Express e o Concurrently (e o Nodemon como uma dependência de desenvolvimento).

**2.1. Instalando dependências**

Vamos instalar tanto o Express quanto o Concurrently com um só comando:

```sh
npm i express concurrently
```

_Não se preocupe se perceber que seu repositório/projeto tem uma pasta a mais em relação ao repositório. Isso é por que a pasta `node_modules` está sendo ignorada, através do arquivo `.gitignore` (e assim deve ser, pois nela estão de fato as dependências do projeto - mas já deixamos o registro das mesmas no `package.json`, logo não precisamos incluí-las no repositório)._

**2.2 Instalando dependências de desenvolvimento**

Agora instalaremos o _nodemon_, que nos poupa de derrubarmos e levantarmos o servidor a todo momento (pois ele fica 'olhando', 'observando' as atualizações do código e já dá um _refresh_ automaticamente no _server_). Para isso, basta rodar o seguinte código no terminal:

```sh
npm i nodemon --save-dev
```

O trecho `--save-dev` é quem instrui que essa dependência seja salva em `devDependencies` no nosso _package.json_.

### Passo 3 | Definindo Scripts

_Branch: [feature/01-init-projeto]_

**3.1. Definindo _scripts_**

Por fim, vamos definir alguns _scripts_ em nosso _package.json_ (e remover o _script_ de testes):

``` json
"start": "node server.js",
"server": "nodemon server.js"
```

Usaremos esses scripts mais adiante. Com isso finalizamos mais um passo do nosso tutorial! Veja como ficou nosso _package.json_ ao final desses passos:

``` json
{
  "name": "react-express",
  "version": "1.0.0",
  "description": "Integração simples do React.js com o node.js",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "server": "nodemon server.js"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/Marcelo-Diament/react-express.git"
  },
  "keywords": [
    "reactjs",
    "nodejs",
    "expressjs",
    "concurrently",
    "nodemon",
    "frontend",
    "backend"
  ],
  "author": "Marcelo Diament",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/Marcelo-Diament/react-express/issues"
  },
  "homepage": "https://github.com/Marcelo-Diament/react-express#readme",
  "dependencies": {
    "concurrently": "^5.3.0",
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.6"
  }
}

```

### Passo 4 | Criando o 'Backend'

_Branch: [feature/02-backend]_

Chegou a hora de criarmos nosso 'backend'. Repare que será um 'backend' muito simples (mesmo), afinal a intenção dessa prática é apenas mostrar como podemos integrar o React.js com o node.js. Para criarmos nosso 'backend' usaremos o Express, um _mini-framework_ que nos ajuda a configurar nosso servidor de maneira mais simples. Vamos lá!

**4.1. Criando o _server.js_**

Basicamente vamos criar um arquivo chamado `server.js` (que indicamos como `entry-point` no momento de iniciarmos o projeto). Podemos fazer isso através da IDE, pelo próprio computador (Explorer/Finder) ou pelo terminal, executando o seguinte comando:

```sh
touch server.js && code server.js
```
