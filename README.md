# notes
Anotações de estudo para consulta

## Subir um servidor
Referência - Livro do [Otávio](https://otaviopace.github.io/livro-desenvolvimento-web-basico/book/usando_corpo_body_e_json.html)

No desafio da Api utilizei:
- Express
  - Facilita as rotas para o desenvolvimento das requisições. (define as rota e chama as funções que serão executadas, conhecidas como middleware)
```
npm install --save express
```

- BodyPaser
  - É um módulo capaz de converter o body da requisição para vários formatos. Um desses formatos é json, que o que eu utilizo.
```
npm install --save body-parser
```

- Nodemon
  - Com o nodemon podemos rodar o terminal sem precisar reiniciar ele a cada alteração.
```
npm install --global nodemon
```

Subindo o servidor:
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
  - Sequelize é um ORM (Object-Relational Mapper) para Node.js. Eles faz o mapeamento de dados relacionais (armazenados tabelas, linhas e colunas) para objetos em JS. Ele permite criar, buscar, alterar e remover dados do banco usando objetos e métodos em JS, além de fazer alterações na estrutura das tabelas.
```
npm install --save sequelize
```

- Sequelize Cli
```
npm install --save sequelize-cli
```

- SQlite3
  - Banco de dados
```
npm install --save sqlite3
```

- Postman
  - Permite enviar requisições para o banco de dados que criamos. Indicamos a porta, método, rota e requisição.

- Dbeaver
  - Permite visualizar as tabelas do banco de dados, basta conectar com nosso arquivo database.

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

- Usar HOOKS do Sequelize para mexer nos dados da requisição antes de salvá-las no banco
  - Eu incluí direto na models
```
  Transactions.addHook('beforeCreate', transaction => {
    console.log('card_number: ', transaction.card_number)
    transaction.card_number = transaction.card_number.substr(-4)
  })
```
