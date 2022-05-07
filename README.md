# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

### EndPoint usado:

htttp://localhost:3001

### Cadastrar

POST /register

Formato do objeto em JSON:

{
"email": "meuEmail@gmail.com",
"password": "123456"
}

201 Created, retorna:

{
"accessToken": "Token de Acesso",
"user": {
"email": "meuEmail@gmail.com",
"id": 1
}
}

400 Bad Resquest, retorna:

{
"Email and password are required"
}

### Login

POST /login ou /signin

Formato:

{
"email": "meEmail@gmail.com",
"password": "123456"
}

200 OK, retorna:

{
"accessToken": "Token de Acesso",
"user": {
"email": "meuEmail@gmail.com",
"id": 1
}
}

400 Bad Request:

{"Email and password are required"}

### Ler os arquivos dos usuarios:

GET /archives

200 OK, retorna:

Se nao possuir nenhum arquivo do usuario:
[]

Do contrario:

[
{
"type": "cachorro",
"name": "Batata",
"id": 1
},
{
"type": "cachorro",
"name": "Batata",
"id": 2
},
{
"type": "cachorro",
"name": "Napoleao",
"id": 3
},
{
"type": "Lorem",
"name": "ipsum",
"id": 4
}
]

Salvar um arquivo:

POST /archives

Authorizacao requerida:

headers: {
Authorization: `Bearer ${seuToken}`
}

Formato do objeto vai do seu criteiro, exemplo:

{
"type": "Lorem",
"name": "ipsum",
}

200 OK, retona:

{
"type": "Lorem",
"name": "ipsum",
"id": 4
}

400 Bad Request, sem header de Autorizacao:

{
"Missing authorization header"
}

### Adicionar um Animal e velos:

POST /animals

Adicionar um animal para o usuario eh necessario estar logado:

Authorizacao requerida:

headers: {
Authorization: `Bearer ${seuToken}`
}

Formato do objeto fica a seu criterio

201 Created, retorna:

{
"Lorem": "ipsum",
"id": 1
}

Ver os animais do seu usuario eh necessario estar logado:

GET /animals

Authorizacao requerida:

headers: {
Authorization: `Bearer ${seuToken}`
}

200 OK, retorna:

[{
"Lorem": "ipsum",
"id": 1
}]

401 Unauthorized, retorna:

{"Missing token"}
