## BACKEND

HTTP

SERVIDOR

HEADER
- chave e valor
- contém por exemplo qual é o tipo do nosso body da requisição (tipo json)

MODELOS DE API
- Rest (pagar.me)
- Soap 
    - Body usa XML


## JAVASCRIPT

JS é uma linguagem de tipagem dinâmica. 

#### TIPOS
<p>Boolean: true ou false</p>
<p>Null: define o valor null</p>
<p>Undefined</p>
<p>Number: js não possui float, integer e tal. Apenas number para números</p>
<p>Object: estrutura que pode ser composta por demais tipos da linguagem</p>

#### ESCOPO
Contexto delimitado onde a declaração de variáveis, funções e objetos são encontradas de forma isolada. Em JS exista o global por default e dentro de cada função tem o seu próprio escopo.

#### VAR, LET E CONST
<p>Var: permite declarar variáveis baseada em escopo</p>
<p>Let: parecido com var, mas controlar melhor o escopo definido em blocos (só existe dentro da função/bloco que foi declarada)</p>
<p>Const: funciona exatamente como let, mas o valor atribuído é fixo</p>

#### HOISTING
Todo código JS é primeiro compilado/interpretado para depois sem executado. 
```
a = 2
var a 
cosole.log(a)
```
O console vai mostrar 2. Por exemplo, ele procura a variável a e depois ve o valor dela. Ao atribuir/declarar tudo direitinho, você evita o hoisting.

#### ASYNC E SYNC
<p>Sync: acontece de forma sequencial</p>
<p>Async: utilização de eventos para chamar as funções, por exemplo</p>
- Promise: usada para trabalhar fluxo async. 

```
return Promise.resolve()
    .then.("faça isso")
    .then("depois faça isso")
```
