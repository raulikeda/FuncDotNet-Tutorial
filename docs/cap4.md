# Para ir além

Você pode agora colocar outras funções na biblioteca e complementar o *payload* de retorno do *endpoint*:

1. Função que retorna as parcelas por tabela SAC
1. Função que retorna as parcelas por tabela Price
1. Função que calcula o valor de um colateral em caso de hipoteca
1. Função que calcula o valor de um leasing baseado em entrada e parcela final

Ou qualquer outra *feature* dos modelos de empréstimo.

## A Cereja do Bolo

Para quem gosta de tecnologias *vintage*:

Linux:

```shell
dotnet new install Avalonia.Templates
dotnet new avalonia.app -n LoanApp.Avalonia
dotnet run --project LoanApp.Avalonia
```

Esse é um projeto derivado das aplicações `Windows Forms`. O .net já havia um novo modelo mais moderno chamado XAML para a construção de telas client-size, e Avalonia é uma portabilidade para outras plataformas, como Linux.

Vamos alterar alguns arquivos no projeto para utilizar a biblioteca do F#. Primeiro adicionar a referência à biblioteca:

```shell
dotnet add LoanApp.Avalonia/LoanApp.Avalonia.csproj reference LoanRules/LoanRules.fsproj
```

Agora, alterar os arquivos:

* Arquivo: `MainWindow.axaml.cs`

```c#
using Avalonia.Controls;
using Avalonia.Interactivity;
using LoanRules; // reference F# DLL

namespace LoanApp.Avalonia;

public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
        this.WindowStartupLocation = WindowStartupLocation.CenterScreen;
    }
    private void SubmitButton_Click(object? sender, RoutedEventArgs e)
        {
            var age = this.FindControl<TextBox>("AgeTextBox").Text;
            var income = this.FindControl<TextBox>("IncomeTextBox").Text;
            var score = this.FindControl<TextBox>("ScoreTextBox").Text;

            var amount = this.FindControl<TextBox>("AmountTextBox").Text;
            var rate = this.FindControl<TextBox>("RateTextBox").Text;
            var term = this.FindControl<TextBox>("TermTextBox").Text;

            var customer = new Customer(
                int.Parse(age), 
                double.Parse(income), 
                int.Parse(score));
            
            // Create a Loan record
            var loan = new Loan(
                double.Parse(amount), 
                double.Parse(rate), 
                int.Parse(term));

            // Call the F# function to check eligibility
            // Note: The F# function is static and can be called directly
            bool eligible = Eligibility.isEligible(customer, loan);
            var result = eligible ? "Approved" : "Denied";

            this.FindControl<TextBox>("ResultTextBox").Text = result;
           
        }
}
```

* Arquivo: `MainWindow.axaml`

```xml
<Window xmlns="https://github.com/avaloniaui"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d" d:DesignWidth="800" d:DesignHeight="500"
        x:Class="LoanApp.Avalonia.MainWindow"
        MinWidth="300" MinHeight="490"
        Title="LoanApp.Avalonia">
    <StackPanel Margin="10">
        <TextBlock Text="Age:"/>
        <TextBox Name="AgeTextBox" Margin="0,5,0,10"/>
        <TextBlock Text="Income:"/>
        <TextBox Name="IncomeTextBox" Margin="0,5,0,10"/>
        <TextBlock Text="Credit Score:"/>
        <TextBox Name="ScoreTextBox" Margin="0,5,0,10"/>
        <TextBlock Text="Amount:"/>
        <TextBox Name="AmountTextBox" Margin="0,5,0,10"/>
        <TextBlock Text="Rate:"/>
        <TextBox Name="RateTextBox" Margin="0,5,0,10"/>
        <TextBlock Text="Term:"/>
        <TextBox Name="TermTextBox" Margin="0,5,0,10"/>
        <Button Content="Submit" Click="SubmitButton_Click"/>
        <TextBlock Text="Result:"/>
        <TextBox Name="ResultTextBox" Margin="0,5,0,10" IsEnabled="false"/>
    </StackPanel>
</Window>
```

Agora só falta rodar:

```shell
dotnet run --project LoanApp.Avalonia
```

Para quem quiser saber mais: [XAML](https://learn.microsoft.com/pt-br/shows/vs-code-livestreams/vs-code-for-xaml-and-csharp-devs)

Enjoy!
