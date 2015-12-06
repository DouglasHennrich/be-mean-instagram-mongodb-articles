# MongoDb - Artigo sobre Autenticação no MongoDb
**Autor:** Douglas Hennrich
**Data** Date.now() //em timestamp

## Qual a diferença entre Autenticação e Autorização?
- Autenticação:

    Verifica a identidade, credenciais, de um usuário.

- Autorização:

    Determina o acesso do usuário, ocorre após uma autenticação bem-sucedida.

---

## Descreva aqui o passo-a-passo como criar um usuário administrador e um usuário comum.

#### Usuário Administrador:

- Utilize o comando `db.createUser` ou `db.runCommand()` para criar um usuário. Esse usuário deve ter a regra chamada `userAdminAnyDatabase`.
```js
// Usando db.createUser
db.createUser({     
    user: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , roles: [ { role: "userAdminAnyDatabase", db: "be-mean-pokemons" } ]
})

// Usando db.runCommand
db.runCommand({
    createUser: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , customData: { qualquerCampo: "Valor desse campo" }
  , roles: [ { role: "userAdminAnyDatabase", db: "be-mean-pokemons" } ]
})
```

#### Usuário Comum:

- Utilize o comando `db.createUser` ou `db.runCommand()` para criar um usuário. Para criarmos um usuário comum, sem nenhum papel, devemos deixar o campo `roles` vazio.
```js
// Usando db.createUser
db.createUser({     
    user: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , roles: []
})

// Usando db.runCommand
db.runCommand({
    createUser: "Nome do Usuário"
  , pwd: "Senha do Usuário"
  , customData: { qualquerCampo: "Valor desse campo" }
  , roles: []
})
```

---

## Explique cada papel listado em [Cluster Administration Roles](https://docs.mongodb.org/manual/reference/built-in-roles/#cluster-administration-roles).

- clusterAdmin
    - Fornece o maior acesso de gerenciamento de clusters. Essa regra combina os privilégios concedidos pelas regras `clusterManager`, `clusterMonitor` e `hostManager`. Além disso, essa regra proporciona a ação de `dropDatabase`.

- clusterManager
    - Fornece gerenciamento e monitoramento das ações no cluster. Um usuário com essa função pode acessar a configuração e bancos de dados locais, que são usados em `sharding` e `replication`, respectivamente.

    * Fornece as seguintes ações no cluster como um todo:
        - addShard
            - Usuário pode executar o comando `addShard`, o qual adiciona um `Shard` ao servidor.

        - applicationMessage
            - Usuário pode executar o comando `logApplicationMessage`, o qual permite postar uma mensagem customizada ao `audit` log.

        - cleanupOrphaned
            - Usuário pode executar o comando `cleanupOrphaned`, o qual permite deletar os documentos órfãs de um `Shard`, cujas `keys values` caem em um único ou uma única faixa contínua que não pertencem ao `Shard`.

        - flushRouterConfig
            - Usuário pode executar o comando `flushRouterConfig`, o qual permite limpar as informações do cluster atual em cache por uma instância `mongos` e recarrega todos as `metadata` compartilhadas desse cluster do `config database`.

        - listShards
            - Usuário pode executar o comando `listShards`, o qual retorna uma lista de `Shards` configurados.

        - removeShard
            - Usuário pode executar o comando `removeShard`, o qual permite remover um `Shard` do cluster compartilhado.

        - replSetConfigure
            - Usuário pode executar o comando `replSetConfigure`, o qual permite configurar uma `replica set`.

        - replSetGetStatus
            - Usuário pode executar o comando `replSetGetStatus`, o qual retorna o `status` da `replica set` do ponto de vista do servidor atual.

        - replSetStateChange
            - O usuário pode alterar o estado de uma `replica set` através dos comandos replSetFreeze, replSetMaintenance, replSetStepDown, e replSetSyncFrom.

        - resync
            - Usuário pode executar o comando `resync`, o qual força uma instância `mongod slave` a re-sincronizar-se.  Note que este comando é relevante para a `master-slave replication` somente. Ela não se aplica a `replica set`.

    * Fornece as seguintes ações em todo o banco de dados no cluster:
        - enableSharding
            - Usuário pode habilitar `sharding` em um banco de dados usando o comando `enableSharding` e pode "shardear" uma coleção usando o comando `shardCollection`. Aplicar essa ação para o banco de dados ou coleção de recursos.

        - moveChunk
            - Usuário pode executar o comando `moveChunk`. Alem disso, o usuário pode executar o comando `movePrimary` desde que o privilégio é aplicado a um recurso base de dados apropriada. Aplicar esta ação para banco de dados ou de cobrança de recursos.

        - splitChunk
            - O usuário pode executar o comando `splitChunk`, que permite dividir os chunks.

        - splitVector
            - O usuário pode executar o comando `splitVector`.

    * No banco de dados `config`, oferece as seguintes ações na coleção `settings`:
        - insert
            - Permite inserir dados

        - remove
            - Permite remover dados

        - update
            - Permite fazer alterações nos dados

    *
---     

## Explique todas as ações de privilégio listadas em Privilege Actions.
