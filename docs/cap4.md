# Para ir além

Você pode agora colocar outras funções na biblioteca e complementar o *payload* de retorno do *endpoint*:

1. Função que retorna as parcelas por tabela SAC
1. Função que retorna as parcelas por tabela Price
1. Função que calcula o valor de um colateral em caso de hipoteca
1. Função que calcula o valor de um leasing baseado em entrada e parcela final

Ou qualquer outra *feature* dos modelos de empréstimo.

# Cereja do Bolo

Para quem gosta de coisas *vintage*:

Linux:

```shell
dotnet new install Avalonia.Templates
dotnet new avalonia.app -n LoanApp.Avalonia
dotnet run --project LoanApp.Avalonia
```

Windows:

```shell
dotnet new wpf -n LoanApp.Wpf
dotnet run --project LoanApp.Wpf
```

Para quem quiser saber mais: [XAML](https://learn.microsoft.com/pt-br/shows/vs-code-livestreams/vs-code-for-xaml-and-csharp-devs)

Enjoy!
