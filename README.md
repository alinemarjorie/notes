# notes
Anotações de estudo para consulta

## Subir um servidor
Referência - Livro do [Otávio](https://otaviopace.github.io/livro-desenvolvimento-web-basico/book/usando_corpo_body_e_json.html)

No desafio da Api utilizei:
- Express
  - Facilita as rotas para o desenvolvimento das requisições. (define as rota e chama as funções que serão executadas, conhecidas como middleware)
- BodyPaser

```
const express = require('express')
const bodyParser = require('body-parser')
const PORT = 8000

const app = express()

app.use(bodyParser.json())

app.post('/', function (req, res) {
  res.send(req.body)
})

app.listen(PORT)
```

## Sequelize e SQlite
No desafio da Api utilizei:
- Node
- Sequelize
- Sequelize Cli
- SQlite3
- Postman
- Dbeaver

### Passos:
- Criar conexão conforme está na documentação do [Sequelize](https://sequelize.org/master/manual/migrations.html) Migrations.
- Executar o migrate para criar a tabela (eu inclui um script no config para fazer isso e rodei ele no terminal com "npm run [nome do script]).
```
"script-migrate": "sequelize db:migrate"
```
- Enviar requisições pelo Postman para ver se está funcionando.
- Criar conexão e visualizar o banco pelo Dbearver. 
- O arquivo de config para chamar o sqlite ficou da seguinte forma:
```
{
  "development": {
    "dialect": "sqlite",
    "storage": "./database.sqlite3"
  },
  "test": {
    "dialect": "sqlite",
    "storage": ":memory"
  },
  "production": {
    "dialect": "sqlite",
    "storage": "./database.sqlite3"
  }
}
```

### Estrutura do projeto
O que são Models, Controllers, Migrations...

- O arquivo na pasta de origem "app.js" é onde eu executo o servidor e chamo o banco de dados com o Sequelize.
- A pasta controllers contem os arquivos com as funções que executam as requisições.
- As pastas migrations e models possuem arquivos criados automaticamente pelo Sequelize Migrate.

### Métodos e requisições
Baseado no desafio da API pagarminho.

- Enviar/processar transações
    - Método: POST
```
const models = require('./models');
const Transactions = models.Transactions;

app.post('/transactions', function (req, res) {
  return Transactions.create(req.body)
  .then(transaction => {
    return  res.status(201).send(transaction)
  })
  .catch(error => {
    console.log("Deu erro")
    console.log(error)
  })
})
```

- Retornar lista com todas as transações
  - Método: GET
```
const models = require('./models');
const Transactions = models.Transactions;

app.get('/transactions', function (res, res) {
  return Transactions.findAll()
  .then(transactions => res.send(transactions))
})
```
