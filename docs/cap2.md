# Programando o F\#

Vamos começar escrevendo uma biblioteca em F# para um caso de Credit Allowance.

A ideia é criar funções puras em F# que vão suportar a aplicação, não importanto qual a plataforma de interação com o usuário. Além das funções, é possível também manter os `Records` na biblioteca.

A sintaxe de F# é muito parecido com OCaml, com algumas pequenas diferenças. Por exemplo, usa-se `PascalCase` em F#, enquanto que em OCaml, é usado `snake_case`.

O projeto `LoadRules` cria automaticamente o arquivo Library.fs. Vamos utilizar esse mesmo arquivo para escrever o código, mantendo uma estrutura básica

# Records

Vamos começar com o record que representa o cliente. Essa estrutura irá armazenar dados como idade, proventos e score de crédito:

Customer:
- Age: int
- Income: float
- CreditScore: int

Você pode criar o Record de forma análoga a feita em OCaml, mas lembrando que precisa ser em PascalCase:

```F#
type Customer = {
    Age: int
    Income: float
    CreditScore: int
}
```

**Ex 1:** Crie agora um novo `Record` chamado `Loan` com 3 campos: `Amount`, `InterestRate` e `TermMonths`. Os dois primeiros são `float` e o último é inteiro.

**Ex 2:** Crie um `Record` chamado `LoanRequest` com 2 campos: `Customer` e `Loan`.

A nova estrutura irá conter os dados referentes a um empréstimo em específico.

# Functions

Por último vamos substituir o módulo atual por um novo módulo chamado `Elegibility`. Dentro colocaremos uma única função por enquanto chamada `isEligible`. Essa função irá receber um record referente ao usuário e um record referente ao empréstimo e retorna um `boolean`.

A regra de negócio é para aprovação do empréstimo (retorno true):

- Se o usuário tem 18 anos ou mais
- Se a renda é maior ou igual ao dobro do valor do empréstimo
- Se o score de crédito é superior a 649

**Ex 3:** Codificar a função acima no módulo

# Integração

Na integração entre as plataformas, o `Record` se tornará algo parecido com uma classe com um construtor automático contendo todos os campos.

Logo, é possível construir objetos em C# usando o Record declarado em F#:

```c#
var customer = new Customer(30, 60000, 700);
```

O único detalhe principal é que a ordem declarada precisa ser mantida no construtor, ao contrário do OCaml que permitia qualquer ordem.

!!! exercise "Exercise 4: Hello Function"
    Reescreva o programa em C# para realizar a chamada da nova função.


