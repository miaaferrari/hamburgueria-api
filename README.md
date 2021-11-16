HAMBURGUERIA API


ENDPOINTS
A API tem um total de 8 endpoints, sendo eles: user, products e preferences.

O url base da API é https://hamburgueria-api-maria.herokuapp.com/


# ROTAS QUE NÃO PRECISAM DE AUTENTICAÇÃO #

Nessa aplicação o usuário, sem fazer login ou se cadastrar, consegue ver a lista de produtos cadastrados, se registrar e logar.

## LISTANDO PRODUTOS

GET /products - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "id": 1,
    "img": "https://i.ibb.co/fpVHnZL/hamburguer.png",
    "title": "Hamburguer",
    "category": "Sanduiches",
    "price": 14
  }
]

## CRIAÇÃO DE USUÁRIO

POST /register - FORMATO DA REQUISIÇÃO

{
	"email": "dri1@mail.com",
	"password": "12345Aa@",
	"name": "Dri"
}

FORMATO DA RESPOSTA - STATUS 201

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRyaTFAbWFpbC5jb20iLCJpYXQiOjE2MzcwMjA0MjYsImV4cCI6MTYzNzAyNDAyNiwic3ViIjoiNCJ9.4G9T34_Inv0Fsn6jh8926kd2LbPHh7Fl7lndnps6Noc",
  "user": {
    "email": "dri1@mail.com",
    "name": "Dri",
    "id": 4
  }
}

## LOGIN 

POST /signin - FORMATO DA REQUISIÇÃO

{
	"email": "dri@mail.com",
	"password": "12345Aa@"
}

FORMATO DA RESPOSTA - STATUS 201

{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRyaUBtYWlsLmNvbSIsImlhdCI6MTYzNjgyNjg2NCwiZXhwIjoxNjM2ODMwNDY0LCJzdWIiOiI1In0.YQ2EodKUkqkdJnpSIbMM9Cdq9F3C9Ifp2RJ3bSSZ1sQ",
  "user": {
    "email": "dri1@mail.com",
    "name": "Dri",
    "id": 5
  }
}

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.


# ROTAS QUE NECESSITAM DE AUTENTICAÇÃO #

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

    Authorization: Bearer {token}

Já registrado e logado, o usuário consegue ver a lista de usuários; capturar um usuário específico; capturar um usuário específico, adicionar e deletar preferências.

## ACESSAR USUÁRIO ESPECÍFICO

GET /users/userId - FORMATO DA RESPOSTA - STATUS 200

{
  "email": "mia1@mail.com",
  "password": "$2a$10$QIJlsBausH9xUECj9CYXauJN4j9EokFUJHeYZhaTcv8w.6neowYx2",
  "name": "Mia",
  "id": 3
}

## LISTAR PREFERÊNCIAS

GET /preferences - FORMATO DA RESPOSTA - STATUS 200

[
  {
    "title": "orange juice",
    "userId": 3,
    "id": 1
  }
]

## ACESSAR AS PREFERÊNCIAS DE UM USUÁRIO ESPECÍFICO

GET /users/userId?_embed=preferences - FORMATO DA RESPOSTA - STATUS 200

{
  "email": "miaa@mail.com",
  "password": "$2a$10$.LWmH2eWeYbFggZ19zoD3e2vJg4OWNkiY.NLyzWqrGKUkfZb8jRVW",
  "name": "Mia",
  "id": 4,
  "preferences": [
    {
      "title": "orange juice",
      "userId": 4,
      "id": 3
    }
  ]
}

## ADICIONAR PREFERÊNCIAS

POST /preferences - FORMATO DA REQUISIÇÃO

{
	"title": "Sunday",
	"userId": 4
}

FORMATO DA RESPOSTA - STATUS 201 

{
  "title": "Sunday",
  "userId": 4,
  "id": 2
}

## DELETAR PREFERÊNCIAS

DELETE /preferences/preferenceId - FORMATO DA RESPOSTA - STATUS 200

{}








