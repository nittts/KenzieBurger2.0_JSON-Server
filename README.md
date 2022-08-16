# KenzieBurger2.0_JSON-Server

Está aplicação foi construida com o propósito para alimentar e controlar a entrada de usuários como também a aquisição de arquivos da entrega 5C28 - Hamburgueria 2.0 - com TypeScript e JSON Server.

A fake-API possui as seguintes rotas com dois principais endpoints:

- user
- products

Como também é baseada na seguinte URL base:

```
https://hamburgueria-kenzie-api-nittts.herokuapp.com
```

---

<sub>Lembrete: Todas as rotas da API requerem autenticação!</sub>

## **USER**

O endpoint de users serve para controlar o fluxo dos usuários realizando login, registo e listagem dos próprios.

> A API é volátil, então registros são apagados após 24hrs necessitando um novo registro.

<h2 align ='center'> Listando usuários </h2>

### USERS:

`GET /users - FORMATO DA RESPOSTA - STATUS 200`

Esta rota serve primariamente para listagem de todos os usuários registrados na API, respondendo todos em um formato de JSON:

```JSON
{
      "email": "kenzinho@mail.com",
      "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
      "name": "Kenzinho",
      "age": 38,
      "id": 1
    }
```

Esta rota também está protegida contra acessos não autorizados, necessitando o envio do ID do usuário para verificação e acesso, caso não seja provido a API irá retornar:

`GET /users - FORMATO DA RESPOSTA - STATUS 403`

```JSON
"Private resource access: entity must have a reference to the owner id"
```

<h2 align ='center'> Criação de usuário </h2>

### **REGISTER**

A rota de registro é usada primariamente para o registro de um novo usuario requerindo as seguintes informações:

```JSON
"email": "superEmail@mail.com",
"password": "senhaSuperSecreta123",
```

Caso o registro seja bem sucedido será respondido com a resposta:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```JSON
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvYUBtYWlsLmNvbSIsImlhdCI6MTY2MDY4ODc1MiwiZXhwIjoxNjYwNjkyMzUyLCJzdWIiOiIzIn0.01HegRe_ewNT4AVjqwyaOyJL5ZyafwJ0Gf7p1vjlWv4",
	"user": {
		"email": "kenzinhoa@mail.com",
		"id": 3
	}
}
```

A API possui a proteção para senhas curtas, requirindo uma senha de no minimo 4 caractéres, como também possuindo a proteção contra email já registrados:

Caso já esteja registrado:

```JSON
"Email already exists"
```

Caso a senha seja menor que 6 caractéres:

```JSON
"Password is too short"
```

<h2 align ='center'> Login de usuário </h2>

### **LOGIN**

A rota de login possui o mesmo endpoint para o uso de acessar as outras rotas da API, podemos realizar o login enviando uma requisição POST com email e senha para a rota:

`POST /login - FORMATO DE REQUISIÇÃO - STATUS 200`

```JSON
{
	"email": "kenzinhodsa@mail.com",
	"password": "146d"
}
```

Caso tudo ocorra como esperado a API irá responder com:

`POST /login - FORMATO DE REQUISIÇÃO - STATUS 200`

```JSON
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvZHNhQG1haWwuY29tIiwiaWF0IjoxNjYwNjg5MDc5LCJleHAiOjE2NjA2OTI2NzksInN1YiI6IjUifQ.DpNxS-T4QXzLFS0Won5VQklES9_hq4KT9Kesc5K2D3I",
	"user": {
		"email": "kenzinhodsa@mail.com",
		"id": 5
	}
}
```

---

## PRODUCTS

A rota de produtos requer autenticação e existe primariamente apenas para a listagem de produtos registrados na Hamburgueria.
Usuários registrados e logados na aplicação podem acessar os dados pela seguinte rota:

<h2 align="center">Listando Produtos</h2>

`GET /products - FORMATO DE RESPOSTA - STATUS 200`

```JSON
[
	{
		"image": "https://i.ibb.co/g6BJRBc/202109090436-skn5yx754p-1.png",
		"title": "Hamburguer",
		"category": "Sanduíches",
		"price": 14,
		"id": 1
	},
	{
		"image": "https://i.ibb.co/NxBxpX1/202109200440-8fcy91zr6le-1.png",
		"title": "X-Burguer",
		"category": "Sanduíches",
		"price": 16,
		"id": 2
	},
	{
		"image": "https://i.ibb.co/XFpqRvC/202109200440-749eet5vy86-1.png",
		"title": "Big Kenzie",
		"category": "Sanduíches",
		"price": 18,
		"id": 3
	},
	{
		"image": "https://i.ibb.co/BPBXgVv/202110050424-xijoowz172-1.png",
		"title": "Combo Kenzie",
		"category": "Combos",
		"price": 26,
		"id": 4
	},
	{
		"image": "https://i.ibb.co/NKkgFpM/202108180426-tbwjnwcd1zq-1.png",
		"title": "Fanta Guaraná",
		"category": "Bebidas",
		"price": 5,
		"id": 5
	},
	{
		"image": "https://i.ibb.co/sQgskc7/202108180426-861zezb4bh-1.png",
		"title": "Coca-Cola",
		"category": "Bebidas",
		"price": 7,
		"id": 6
	},
	{
		"image": "https://i.ibb.co/9p11S7P/202108250455-4498m9wq98e-1.png",
		"title": "McShake Ovomaltine",
		"category": "Sobremesas",
		"price": 10,
		"id": 7
	},
	{
		"image": "https://i.ibb.co/NsSZLwr/202110110503-g22mtz565td-1.png",
		"title": "McShake Nutella",
		"category": "Sobremesas",
		"price": 10,
		"id": 8
	}
]
```

---

<h6>Made with ♥ by Nittts :3 </h6>
