# Integrando o F\#

Abra o arquivo `Library.fs` no projeto `LoadRules`. Ele terá um código de exemplo a seguir:

```f#
namespace LoanRules

module Say =
    let hello name =
        printfn "Hello %s" name
```

`namespace` é autoexplicativo e indica como é a hierarquia da bibllioteca.

Dentro do `namespace` há um módulo chamado `Say` e uma função chamada `hello` com um argumento.

Essa função não é pura devido ao print embutido dentro dela.

## Primeiro Passo

Sem modificar a biblioteca ainda, vamos tentar realizar a chamada dessa função no C# e fazer com que ela imprima o resultado no terminal.

Ao abrir o arquivo `Program.cs`, você notará que possui apenas um print:

```c#
Console.WriteLine("Hello, World!");
```

Apague essa linha e faça a chamada de função da biblioteca:

```c#
using LoanRules; // reference F# DLL

// Call function hello in module Say in LoanRules
Say.hello("John Doe");
```

Apesar da função estar em F#, a sintaxe a ser utilizada deve ser a do C#, que é análoga ao do Java.

A integração dentro do ambiente .net é automática e transparente. Ao rodar a aplicação, a solução monta ambos os projetos e preparam o código em .net IL para executar na Virtual Machine. Para o C#, a biblioteca não é em F#, mas em uma representação intermediária que é acessível por todo o ecoessistema .net. 

Essa interoperabilidade é muito produtiva para aplicações complexas, com diversos times trabalhando na solução, isolando as atribuições de cada grupo e sem problemas ou camadas de integração.

## Isolando o side-effect

Vamos agora tornar a função pura e jogar o efeito colateral para o C#.

!!! exercise "Exercício 1:"
    Modifique a função hello para receber uma string e retornar uma string, concatenando o prefixo "Hello, " no argumento.
    
!!! exercise "Exercício 2:"
    Modifique o arquivo Program.cs para chamar a função na biblioteca e imprimir o resultado.