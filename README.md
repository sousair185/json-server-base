Endpoints

A Api tem um total de 7 endpoints o principal é o de cadastro de usuário, assim posibilitando cadastrar animais, foto, seus hobbies e mensagens.
O url base da API é https://sousateste.herokuapp.com

Rotas que não precisa de autenticação
GET/animals
formato da resposta - STATUS 200
{
"type": "Cachorro",
"name": "Agnes",
"userId": 2,
"id": 1
},
{
"type": "Galinha",
"name": "Carijó",
"userId": 2,
"id": 2
},
{
"type": "Gato",
"name": "Derua",
"userId": 2,
"id": 3
}
GET/hobbies
formato da resposta - STATUS 200
{
"description": ""
}

Criação de usuário
POST/register - formato da requisição
{ "email": "emailvalido@mail.com",
"password": "melhorsenha",
"name": "Nome do usuario",
"age": 99
}

Os únicos campos obrigatórios para criação de usuário são, email e password

Caso dê tudo certo a resposta será assim:
POST/register - formato da resposta - STATUS 201
{
"accessToken": "token criado automaticamente",
"user": {
"email": "emailvalido@mail.com",
"name": "Nome do usuario",
"age": 99,
"id": 99
}
}

Login
POST/login - Formato da requisição
{
"email": "emailvalido@mail.com",
"password": "melhorsenha"
}

Caso dê tudo certo a resposta será assim:
POST/login - Formato da resposta - STATUS 200
{
"accessToken": "token criado automaticamente",
"user": {
"email": "emailvalido@mail.com",
"name": "Nome do usuario",
"age": 99,
"id": 99
}
}
Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

Rotas que necessitam de autorização
Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}
Caso dê tudo certo a resposta será assim:
POST/animals Formato da requisição
{
"type": "Pássaro",
"name": "Pica Pau",
"userId": 2
}
Caso dê tudo certo a resposta será assim:
POST/animals Formato da resposta - STATUS 201
{
"type": "Pássaro",
"name": "Pica Pau",
"userId": 2,
"id": 5
}
POST/photo Formato da requisição
{
"url": "#",
"userId": 2
}
POST/hobbies Formato da requisição
{
"description": "descrição dos hobbies",
"userId": 2
}
POST/messages Formato da requisição
{
"messages": "mensagem de lembrete",
"userId": 2
}

O Formato de resposta para sucesso seguirá o padrão de STATUS 201

Possíveis erros
O corpos da requisição precisa conter o id correspondente ao token utilizado
POST/photo
POST/animals
POST/hobbies
POST/messages - FORMATO DA RESPOSTA - STATUS 403
{
"status": "Forbidden",
"message": [
"Private resource creation: request body must have a reference to the owner id"
]
}

Email já cadastrado
POST/register - FORMATO DA RESPOSTA - STATUS 400
{
"status": "error",
"message": "Email already exists"
}
