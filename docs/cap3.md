# Criando uma API REST

Próximo passo agora é criar uma API REST em C# para expor um endpoint que consome o método da biblioteca.

Devido ao ambiente .net, é possível fazer tudo em F#, contudo é muito mais prático fazê-lo em C#. Esse isolamento soma o melhor de cada linguagem.

## Criar um projeto LoanAPI

O primeiro passo é criar um novo projeto chamado LoanAPI. Em C# não podemos simplesmente substituir o códido em LoanApp para rodar a aplicação no terminal, como em Python. É preciso preparar o projeto para expor os endpoints via webserver.

```shell
dotnet new webapi -n LoanApi
dotnet add LoanApi/LoanApi.csproj reference LoanRules/LoanRules.fsproj
```

Para testar, você pode rodar:

```shell
dotnet run --project LoanApi
```

Isso irá rodar o webserver e expor os endpoints em: [localhost](http://localhost:5156/weatherforecast)

## Montando a API REST

Alterar o arquivo `LoanApi.http` para o endpoint correto: /loan/

Alterar o arquivo `Program.cs` do Projeto LoanApi:

```c#
using LoanRules; // reference F# DLL

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.MapPost("/loan", (LoanRequest request) =>
{

    //Implement:

    // Create a Customer record from request
    // Create a Loan record from request
    // Call the F# function to check eligibility
    // Note: The F# function is static and can be called directly

    bool eligible = true; // Call the F# function here

    return Results.Ok(new
    {
        LoanEligibility = eligible ? "Approved" : "Denied"
    });
})
.WithName("PostLoan")
.WithOpenApi();

app.Run();

```

Testar usando usando uma chamada com o verbo post:

```shell
curl -X POST http://localhost:5189/loan   -H "Content-Type: application/json"   -d '{
    "customer": {
      "age": 30,
      "income": 60000.0,
      "creditScore": 700
    },
    "loan": {
      "amount": 20000.0,
      "interestRate": 5.5,
      "termMonths": 60
    }
  }' -k
```
