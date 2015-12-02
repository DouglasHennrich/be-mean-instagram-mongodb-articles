# MongoDb - Artigo sobre Autenticação no MongoDb
**Autor:** Douglas Hennrich
**Data** Date.now() //em timestamp

## Qual a diferença entre Autenticação e Autorização?
- Autenticação:

    Verifica a identidade, credenciais, de um usuário.

- Autorização:

    Determina o acesso do usuário, ocorre após uma autenticação bem-sucedida.

---
---

## Descreva aqui o passo-a-passo como criar um usuário administrador e um usuário comum.

#### Usuário Administrador:

- Devemos conectar ao `mongo` na DataBase chamada `admin`.
```js
mongo admin
MongoDB shell version: 3.0.7
connecting to: admin
Odin(mongod-3.0.7) admin>
```

- Utilize o comando `db.createUser` ou `db.runCommand()` para criar um usuário. Esse usuário deve ter a regra chamada `userAdminAnyDatabase`.
```js
// Usando db.createUser
db.createUser({     
    user: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
})

// Usando db.runCommand
db.runCommand({
    createUser: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , customData: { qualquerCampo: "Valor desse campo" }
})
```

---
---

## Explique cada papel listado em Cluster Administration Roles.

---
---

## Explique todas as ações de privilégio listadas em Privilege Actions.
