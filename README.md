# Node.js

## Conceitos gerais

- Plataforma (não é uma linguagem)
- Permite usar Javascript no Back ends
    - Não lida com eventos do usuário final
    - Rotas e integrações

## O que é npm/yarn?

- gerenciador de pacotes
- instala bibliotecas de terceiros
- equiparável ao pip do Python

## Características

- Arquitetura Event-loop
    - Call Stack (pilha de eventos)
    - Last IN, First OUT (LIFO)
- Node single-thread (processo fica alocado em apenas um core do precessamento)
    - C++ por trás com libuv
    - Background threads
- Non-blocking I/O
    - Não necessita dar toda a resposta de uma requisição de uma vez
    - Dar uma resposta não gera perda de conexão como em outras linguagens
    - Possibilita aplicações em tempo real

## Frameworks

- ExpressJS como base
    - sem opinião
        - não possui uma estrutura fechada
    - ótimo para iniciar
        - microframework
    - micro-serviços
        - possibilita dividir a aplicação

### Frameworks opinados

- AdonisJS
- NestJS

---

# Conceitos API Rest

## Funcionamento

- do tipo requisição e resposta
- requisição feita por um cliente
- resposta retorna através de uma estrutura de dados
- cliente recebe resposta e processa resultado

## As rotas utilizam métodos HTTP

- GET
- POST
- PUT
- DELETE

## Benefíficos

- múltiplos clientes front-end e até mesmo back-end
- protocolo de comunicação padronizado
    - mesma estrutura para web / mobile / API pública
    - comunicação com serviços externos

## JSON

- JavaScript Object Notation
- objetos que podem contem arrays e outros objetos

## Alguns tipos de Requisições

- GET:
    - utiliza Query Params
    - vai na própria **URL**
    - inicia-se após o nome do recurso, com o sinal de interrogação **?**

    ```jsx
    http://api.com/company/1/users?page=2
    ```

- POST:
    - utiliza-se **Body** para não poluir a URL e não mostrar campos sensíveis

    ```jsx
    {
    	"user": {
    		"name": "Arlucio Nunes",
    		"email": "arlucionunes@gmail.com",
    		"techs": ["ReactJS", "NodeJS", "Reactive Native"]
    	}
    }
    ```

## HTTP Codes

- 1xx: Informational
- 2xx: Success
    - 200: SUCCESS
    - 201: CREATED
- 3xx: Redirection
    - 301: MOVED PERMANENTLY
    - 302: MOVED
- 4xx: Client Error
    - 400: BAD REQUEST
    - 401: UNAUTHORIZED
    - 404: NOT FOUND
- 5xx: Server Error
    - 500: INTERNAL SERVER ERROR

---

# Criando Projeto Node

- criar uma pasta

```jsx
mkdir nome_da_pasta
```

- iniciar um projeto javascript

```jsx
yarn init -y
```

- abrir pasta com o VScode

```jsx
code .
```

- criar uma pasta **src** no vscode
- criar um arquivo index.js
- importar uma dependência, **express**: é um microframework

```jsx
yarn add express
```

- criar uma aplicação

```jsx
const express = require('express');

const app = express();
```

## Acessar a aplicação pelo navegador

- necessário ouvir uma porta
- acessar via localhost: **porta** (qualquer porta acima de 80)
    - bastante utilizado 3333 e acima, caso tenha mais aplicações node

```jsx
app.listen(3333)
```

- fazer o express monitorar a rota e retornar uma resposta

```jsx
app.get('/projects', (request, response) => {
  return response.send('Hello World');
});
```

- executando a aplicação

```jsx
node src/index.js
```

- ir no navegador e buscar endereço **localhost:3333/projects**
- não é necessário ir para um endereço como no exemplo **projects**. Pode ser usado apenas "/", então será acessado direto o **localhost:3333**
- retornando dados do tipo JSON

```jsx
app.get('/', (resquest, response) => {
  return response.json({message: 'Hello World'});
});
```

- o node não faz a reinicialização automática do servidor quando há uma alteração, portanto é necessário **CTRL + C**, para cancelar a execução e executá-lo de novo.

---

# Configurando Node

## Instalação Nodemon

- ferramenta usada por toda comunidade node
- atualização automática do servidor, toda vez que o node detecta uma alteração

```jsx
yarn add nodemon -D
```

- executando...

```jsx
yarn nodemon src/index.js
```

- criando atalho para execução
    - no arquivo **package.json**

```jsx
"main": "src/index.js",
"scripts": {
    "dev": "nodemon"
  },
```

## Retornando um feedback no terminal sobre a aplicação

- alterar o método **app.listen**, que pode receber uma função como segundo parâmetro

```jsx
app.listen(3333, () => {
	console.log('=> Back-end started!');
});
```

---

# Métodos HTTP

## Get

- buscar informações do back-end
- rota usada para retornar alguma informação

⇒ Nem toda rota retorna uma informação. Se o usuário for deletar alguma coisa do back-end, por exemplo, essa ação não retornará uma informação.

## Post

- criar uma informação no back-end

## Put/Patch

- alterar uma informação no back-end
- ambos atualizam informações
- put serve para atualizar um recurso por completo
    - Ex: usuário altera todos os dados do seu perfil na aplicação de uma vez
- patch serve para atualizar uma informação específica
    - Ex: alterar a foto de avatar do usuário

## Delete

- deleta uma informação no back-end

---

# Utilizando o Insomnia

- programa baixado em **[insomnia.rest](http://insomnia.rest)** automaticamente
- instalado tema dracula automático também
- criar uma pasta para requisições do mesmo recurso
    - no caso criaremos uma folder chamada **Projects**
- adicionamos novas **requests**
    - damos um nome. Ex: **List**
    - escolhemos o método. Ex: **Get**
    - depois colocamos o caminho da rota
    - clicar em **Send** para finalmente testar a rota

⇒ Lembrando que para as rotas **put e delete**, deve-se colocar um **/id** depois do caminho

## Adicionando um environment

- serve para criar atalhos que são muito usados
- Manage Environments
- adicionar um novo sub environment
- colocar um nome
- adicionar uma cor
- colocar um código padrão json, Ex:

```jsx
{
  "base_url": "http://localhost:3333"
}
```

- clicar em **Done**
- selecionamos o **Environment** desejado
- alteramos o caminho da rota e adicionamos o objeto criado com o código
    - **Ctrl + Espaço**
    - selecionar **base_url**
- manter o caminho restante do recurso **/projects**

⇒ Lembrando que para as rotas **put e delete**, deve-se colocar um **/id** depois do caminho

---

# Tipos de  Parâmetros

***Parâmetros**: Formas do Front-end enviar algum tipo de informação

## Query Params

- usado principalmente para filtros e paginação
- enviar parâmetros **Query:**
    - adicionar um ponto de interrogação **?** após o recurso
    - **nome_do_parâmetro**=**valor_do_parâmetro**
    - para adicionar mais parâmetros, usar o 'E' comercial **&**
    - Ex:

    ```jsx
    http://localhost:3333/projects?title=React&owner=Elton
    ```

- no **Insomnia** pode ser usado a aba **Query**
- no código da aplicação adicionamos:

```jsx
const query = request.query;

  console.log(query);
```

- que deverá retornar:

```jsx
{ title: 'React', owner: 'Elton' }
```

- desmembrando a variável **query**, podemos deixar da seguinte forma:

```jsx
const {title, owner} = request.query;

  console.log(title);
  console.log(owner);
```

- que deverá retornar:

```jsx
React
Elton
```

## Route Params

- identificar recursos na hora de **Atualizar/Deletar**
- solicitamos com o identificador depois do caminho e identificamos no código conforme a seguir, respectivamente:

```jsx
http://localhost:3333/projects/1

app.put('/projects/:id', (request, response) => {...
```

- para nosso back-end identificar o **id** adiconamos ao código:

```jsx
const params = request.params;

  console.log(params);
```

- que deverá retornar:

```jsx
{ id: '1' }
```

- da mesma forma que na **Query**, podemos desestruturar conforme a seguir:

```jsx
const {id} = request.params;

  console.log(id);
```

## Request Body

- conteúdo na hora de criar ou editar um recurso
- esse conteúdo, ou seja, essas informações, chegam para o front-end através de **JSON**
- na requisição feita pelo **Insomnia**
    - no campo **Body**, selecionar **JSON**
    - criar um objeto com as informações desejadas. Ex:

    ```jsx
    {
    	"title": "Aplicativo React Native",
    	"owner": "Elton Possidonio"
    }
    ```

- no código da aplicação:

```jsx
const body = request.body;

  console.log(body);
```

- para o **Express** interpretar a requisição acima:

```jsx
app.use(express.json());
```

- retornando então:

```jsx
{ title: 'Aplicativo React Native', owner: 'Elton Possidonio' }
```

- desmembrando mais uma vez:

```jsx
const {title, owner} = request.body;

  console.log(title);
  console.log(owner);
```

- retornando:

```jsx
Aplicativo React Native
Elton Possidonio
```

---

# Aplicação Funcional

- criar API, armazenando projetos
    - listar
    - criar
    - deletar
- por enquanto sem uso de **Banco de Dados**
- criar uma variável **projects,** antes das rotas, que vai ser um array vazio

```jsx
const projects = [];
```

- fechando / reiniciando a aplicação, a variável retorna para o valor dela, que é um array vazio

## Rota de listagem de projetos GET

- rota após deixar os filtros comentados e retornar o array

```jsx
app.get('/projects', (request, response) => {
  // const {title, owner} = request.query;

  // console.log(title);
  // console.log(owner);

  return response.json(projects);
});
```

## Rota de criação dos projetos POST

- apago os console logs da rota post onde foram marcados como comentário

```jsx
app.post('/projects', (request, response) => {
  const {title, owner} = request.body;

/*
  console.log(title); 
  console.log(owner);
*/

  return response.json([
    'Projeto 1',
    'Projeto 2',
    'Projeto 3',
  ])
})
```

- criar uma variável que contenha um **title**, um **owner** e um **id**
- para a criação do **id**, instalar uma biblioteca chamada **uuidv4**

```jsx
yarn add uuidv4
```

- importar apenas a função **uuid** do módulo **uuidv4**

```jsx
const { uuid } = require('uuidv4');
```

- criando a variável **project**, conforme descrito acima

```jsx
const project = { id: uuid(), title, owner };
```

- criar um **push**, que irá enviar o que foi criado para o array

```jsx
projects.push(project);
```

- retornar o projeto que foi criado

```jsx
return response.json(project);
```

- ao rodar no **Insomnia**

```jsx
DeprecationWarning: uuidv4() is deprecated. Use v4() from the uuid module instead.
```

- como a biblioteca **uuidv4** está defasada, foi instalada a biblioteca **uuid** e usada a função **v4**, conforme orientação da notificação, ficando os comandos e códigos da seguinte forma:

```jsx
yarn add uuid // para instalar o módulo
const { v4 } = require('uuid'); // para importar universal unique id
const project = { id: v4(), title, owner }; // usando a função na variável
```

### No Insomnia

- a rota GET deve estar vazia, caso tenha reiniciado a aplicação
- na rota POST, dando um Send com o que já estava criado anteriormente

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-18-53.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-18-53.png)

- deve gerar uma resposta do tipo

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-20-29.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-20-29.png)

Repare no id único gerado. Caso aperte Send novamente, será criado um novo projeto, apenas com o id único diferente

## Rota de update PUT

- nessa rota, repare que recebo um **id** como parâmetro

```jsx
app.put('/projects/:id', (request, response) => {
  const {id} = request.params; // aqui recebo id como parâmetro

  console.log(id);

  return response.json([
    'Projeto 4',
    'Projeto 2',
    'Projeto 3',
  ])
})
```

- percorremos então o array **projects**, em busca do projeto que queremos atualizar, utilizando a função find() do JS

```jsx
const project = projects.find(project => project.id === id);
```

- porém, para facilitar a atualização, procuramos a posição do projeto no array, ou seja, o índice:

```jsx
const projectIndex = projects.findIndex(project => project.id === id);
```

- colocamos uma condição também caso não encontremos o projeto

```jsx
if (projectIndex < 0) { // caso não encontre, retorna uma resposta -1
    return response.json({ error: 'Project not found.' })
  }
```

- testando a rota PUT no **Insomnia**:

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-49-35.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-49-35.png)

repare que retornou um status code de sucesso 200

- para setar esse status code mudamos o código para:

```jsx
return response.status(400).json({ error: 'Project not found.' })
```

- retornando a resposta:

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-53-02.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_18-53-02.png)

### Atualizando o projeto

- com o projeto encontrado, criamos uma nova informação do projeto
- pegamos a informação de dentro do body

```jsx
const { title, owner } = request.body;
```

- recriamos o projeto

```jsx
const project = {
    id,
    title,
    owner,
  }
```

- substituímos no array na mesma posição

```jsx
projects[projectIndex] = projects;
```

- retornamos o projeto atualizado

```jsx
return response.json(project);
```

- código final

```jsx
app.put('/projects/:id', (request, response) => {
  const { id } = request.params;
  const { title, owner } = request.body;

  const projectIndex = projects.findIndex(project => project.id === id);

  if (projectIndex < 0) { // caso não encontre, retorna uma resposta -1
    return response.status(400).json({ error: 'Project not found.' })
  }

  const project = {
    id,
    title,
    owner,
  }

  projects[projectIndex] = projects;

  return response.json(project);
})
```

### Testando no **Insomnia**

- em Post, criamos um novo projeto e copiamos seu id
- em Put, colocamos o id do projeto após projects
- copiamos o conteúdo da rota de criação em Post
- colamos em Put, selecionamos o formato json, alteramos alguma coisa e damos um send

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_19-40-12.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_19-40-12.png)

- podemos encontrar o projeto na rota de List

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_19-42-04.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_19-42-04.png)

## Rota de Delete

- identificamos o id do projeto com base no parâmetro passado na URL
- localizamos dentro do array
- caso ele exista, utilizamos a função splice(), que retira uma informação de dentro de um array, passando como parâmetro o índice e quantas posições quero remover a partir desse índice, no caso apenas a informação contida nele, então no caso **1**

```jsx
projects.splice(projectIndex, 1);
```

- nesse caso retornamos apenas um valor em branco, usando o send()
- recomenda-se enviar com o status code 204, quando for uma resposta vazia

```jsx
return response.status(204).send();
```

### Testando no Insomnia

- basta copiar o id, colocar na URL após projects e apertar send

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-00-21.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-00-21.png)

- voltado na listagem, não encontra-se mais o projeto

## Filtrando Rota List

- utilizando apenas filtro **title**, com valor **React**, por exemplo
- será encontrado todos os projetos que o título contenha React
- criamos uma constante chama **results**, observando se o título foi preenchido pelo usuário
- caso tenha sido preenchido
    - usamos função filter() e includes()
- caso não tenha sido preenchido, retorna todos os projetos
- código final:

```jsx
app.get('/projects', (request, response) => {
  const { title } = request.query;

  const results = title
    ? projects.filter(project => project.title.includes(title))
    : projects;

  return response.json(results);
});
```

### Testando no Insomnia

- criando 2 projetos e desabilitando o filtro e buscando em List

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-23-40.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-23-40.png)

- habilitando o filtro em Query

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-24-43.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-24-43.png)

- resultado:

![Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-25-43.png](Aplicac%CC%A7a%CC%83o%20Funcional%204e91aad2dc384e6abf53bfc76bf25ef3/Captura_de_tela_de_2020-12-21_20-25-43.png)