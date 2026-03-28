# Documentação Técnica Completa sobre os Princípios SOLID em C#

## Introdução
Os princípios SOLID são um conjunto de cinco princípios de design de software que visam tornar o software mais compreensível, flexível e mantenível. Esses princípios ajudam os desenvolvedores a criar sistemas que são mais fáceis de gerenciar e adaptar a mudanças futuras.

## Explicação dos Princípios SOLID

1. **S** - **Single Responsibility Principle (Princípio da Responsabilidade Única)**  
   Cada classe deve ter uma única responsabilidade, ou seja, deve haver apenas uma razão para que uma classe possa mudar.

2. **O** - **Open/Closed Principle (Princípio Aberto/Fechado)**  
   As classes devem ser abertas para extensão, mas fechadas para modificação. Isso significa que deve ser possível adicionar novas funcionalidades sem modificar o código existente.

3. **L** - **Liskov Substitution Principle (Princípio da Substituição de Liskov)**  
   As subclasses devem ser substituíveis por suas classes base sem alterar a correção do programa. Isso promove a reutilização e a flexibilidade do código.

4. **I** - **Interface Segregation Principle (Princípio da Segregação de Interface)**  
   Uma classe n��o deve ser forçada a implementar interfaces que não utiliza. É melhor ter várias interfaces específicas do que uma interface única e abrangente.

5. **D** - **Dependency Inversion Principle (Princípio da Inversão de Dependência)**  
   Os módulos de alto nível não devem depender de módulos de baixo nível, ambos devem depender de abstrações. Isso resulta em um código mais modular e flexível.

## Tecnologia Stack
- .NET Core
- C#
- Entity Framework
- xUnit
- Docker
- Git

## Estrutura do Projeto
    ├── src  
    │   ├── Project  
    │   │   ├── Controllers  
    │   │   ├── Models  
    │   │   ├── Services  
    │   │   └── Repositories  
    └── tests  
        ├── Project.Tests  
        └── Project.IntegrationTests

## Guia de Instalação
1. Certifique-se de que você tem o [.NET SDK](https://dotnet.microsoft.com/download) instalado.
2. Clone este repositório:  
   `git clone https://github.com/jrmoreiram/solid-csharp`
3. Navegue até o diretório do projeto:  
   `cd solid-csharp`
4. Restaure as dependências:  
   `dotnet restore`
5. Execute o projeto:  
   `dotnet run`

## Exemplos de Uso
```csharp
public class ExampleController : ControllerBase  
{  
    private readonly IExampleService _exampleService;
    
    public ExampleController(IExampleService exampleService)  
    {  
        _exampleService = exampleService;  
    }  
}
```

## Diretrizes de Contribuição
1. Faça um fork deste repositório.
2. Crie uma nova branch (`git checkout -b feature/YourFeature`).
3. Faça suas alterações e adicione os arquivos (`git add .`).
4. Faça commit das suas alterações (`git commit -m 'Adiciona nova feature'`).
5. Envie para o repositório remoto (`git push origin feature/YourFeature`).
6. Crie um novo Pull Request.

## Recursos Adicionais
- [Princípios SOLID no Design de Software](https://www.pluralsight.com/guides/solid-principles-in-software-development)
- [Artigo sobre SOLID](https://medium.com/@itsmeatalex/a-simple-guide-to-solid-principles-in-c-41b73da0e750)  
- [Cursos sobre Design Patterns e SOLID](https://www.udemy.com/course/design-patterns-in-csharp/)  


---