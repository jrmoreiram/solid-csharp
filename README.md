# SOLID com C#: princípios da programação orientada a objetos

![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg) ![License](https://img.shields.io/badge/license-MIT-blue.svg) ![Version](https://img.shields.io/badge/version-1.0.0-orange.svg)

## Introdução
Este projeto fornece uma documentação técnica abrangente sobre os princípios SOLID, baseado no curso SOLID com C#: princípios da programação orientada a objetos da DevMedia. Esses princípios são princípios de design de software que visam tornar o software mais compreensível, flexível e mantenível.

## Princípios SOLID

1. **Single Responsibility Principle (SRP)**  
   - **Antes:**  Uma classe que faz muitas coisas.  
   - **Depois:** Uma classe que tem apenas uma responsabilidade.

   ```csharp
   // Antes
   public class UserManager { 
       public void RegisterUser(User user) { }
       public void SendEmail(User user) { }
   }
   
   // Depois
   public class UserManager { 
       public void RegisterUser(User user) { }
   }

   public class EmailService { 
       public void SendEmail(User user) { }
   }
   ```

2. **Open/Closed Principle (OCP)**  
   - **Antes:** Classe que precisa ser modificada para novos comportamentos.  
   - **Depois:** Classe que pode ser estendida sem modificar o código existente.
   
   ```csharp
   // Antes
   public class Payment { 
       public void ProcessPayment(PaymentType type) { }
   }
   
   // Depois
   public interface IPaymentMethod { }
   public class Paypal : IPaymentMethod { }
   public class CreditCard : IPaymentMethod { }
   ```

3. **Liskov Substitution Principle (LSP)**  
   - **Antes:** Substituição de classes que não respeitam contratos.  
   - **Depois:** Classes filhas que podem ser substituídas sem quebrar funcionalidades.

4. **Interface Segregation Principle (ISP)**  
   - **Antes:** Interfaces grandes que forçam implementações desnecessárias.  
   - **Depois:** Múltiplas interfaces pequenas e específicas.
   
5. **Dependency Inversion Principle (DIP)**  
   - **Antes:** Módulos de alto nível dependem de módulos de baixo nível.  
   - **Depois:** Ambos dependem de abstrações.

   ```csharp
   // Antes
   public class NotificationService { 
       private EmailService _emailService;
       public NotificationService() { 
           _emailService = new EmailService();
       }
   }
   
   // Depois
   public class NotificationService { 
       private readonly IEmailService _emailService;
       public NotificationService(IEmailService emailService) { 
           _emailService = emailService;
       }
   }
   ```

## Technology Stack
| Tecnologia        | Versão      |
|-------------------|-------------|
| C#                | 10.0        |
| .NET Core         | 3.1         |
| Entity Framework  | 5.0         |

## Estrutura do Projeto
```
/myproject
  /src
  /tests
  /docs
```

## Pré-requisitos
* .NET Core 3.1 
* Visual Studio ou VS Code

## Guia de Instalação
1. Clone o repositório.
2. Execute `dotnet restore` no diretório do projeto.
3. Execute `dotnet build`.

## Exemplos de Uso
```csharp
var userManager = new UserManager();
userManager.RegisterUser(new User());
```

## Padrões e Convenções
- Nomeação em PascalCase para classes
- Método deve ser nomeado em camelCase

## Diretrizes de Contribuição
1. Faça um fork do repositório.
2. Crie uma branch para suas alterações.
3. Envie um Pull Request.

## Recursos Adicionais
* [DevMedia SOLID Course](https://www.devmedia.com.br/course?id=solid)
* [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)

## Licença
Este projeto está licenciado sob a Licença MIT.

## Informações do Autor
Criado por: **jrmoreiram** | E-mail: jumoreiram@gmail.com
