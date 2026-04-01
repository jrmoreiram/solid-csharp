# 🏆 Sistema de Leilão Online - Alura

![.NET Core](https://img.shields.io/badge/.NET%20Core-3.1-512BD4?style=flat-square&logo=.net)
![C#](https://img.shields.io/badge/C%23-10.0-239120?style=flat-square&logo=c-sharp)
![Entity Framework](https://img.shields.io/badge/Entity%20Framework-3.1-512BD4?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg?style=flat-square)

## 📋 Índice

- [Sobre o Projeto](#-sobre-o-projeto)
- [Arquitetura e Princípios SOLID](#%EF%B8%8F-arquitetura-e-princípios-solid)
- [Tecnologias Utilizadas](#%EF%B8%8F-tecnologias-utilizadas)
- [Funcionalidades](#-funcionalidades)
- [Estrutura do Projeto](#-estrutura-do-projeto)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação e Configuração](#-instalação-e-configuração)
- [Executando o Projeto](#%EF%B8%8F-executando-o-projeto)
- [API REST](#api-rest)
- [Testes](#-testes)
- [Padrões de Projeto Implementados](#-padrões-de-projeto-implementados)
- [Contribuindo](#-contribuindo)
- [Licença](#-licença)
- [Autor](#%E2%80%8D-autor)

---

## 📖 Sobre o Projeto

O **Sistema de Leilão Online - Alura** é uma aplicação web ASP.NET Core MVC desenvolvida como projeto educacional para demonstrar a aplicação prática dos **princípios SOLID** na programação orientada a objetos com C#. 

O sistema permite o gerenciamento completo de leilões online, incluindo cadastro, edição, remoção, início e finalização de pregões, além de consultas por categorias. O projeto foi estruturado seguindo as melhores práticas de desenvolvimento, separação de responsabilidades e arquitetura em camadas.

### 🎯 Objetivos

- Demonstrar a aplicação dos 5 princípios SOLID em um projeto real
- Implementar uma arquitetura limpa e desacoplada
- Fornecer exemplos práticos de inversão de dependências
- Criar código testável e manutenível
- Aplicar padrões de projeto reconhecidos pela indústria

---

## 🏗️ Arquitetura e Princípios SOLID

Este projeto foi desenvolvido aplicando rigorosamente os cinco princípios SOLID:

### 1️⃣ **Single Responsibility Principle (SRP)** - Princípio da Responsabilidade Única

Cada classe possui uma única responsabilidade bem definida:

- **Controllers**: Gerenciam apenas as requisições HTTP e respostas
- **Services**: Contêm exclusivamente a lógica de negócio
- **DAOs**: Responsáveis apenas pelo acesso a dados
- **Models**: Representam apenas as entidades de domínio

```csharp
// ✅ Cada classe tem uma única responsabilidade
public class LeilaoController : Controller { } // Gerencia HTTP
public class DefaultAdminService : IAdminService { } // Lógica de negócio
public class LeilaoDaoComEfCore : ILeilaoDao { } // Acesso a dados
```

### 2️⃣ **Open/Closed Principle (OCP)** - Princípio Aberto/Fechado

O sistema está aberto para extensão, mas fechado para modificação:

```csharp
// É possível adicionar novos comportamentos sem modificar código existente
public class ArquivamentoAdminService : IAdminService 
{
    // Estende comportamento padrão adicionando arquivamento
    // sem modificar DefaultAdminService
}
```

### 3️⃣ **Liskov Substitution Principle (LSP)** - Princípio da Substituição de Liskov

Implementações podem ser substituídas sem quebrar o sistema:

```csharp
// Ambas implementações podem ser usadas intercambiavelmente
IAdminService service = new DefaultAdminService(dao, categoriaDao);
// ou
IAdminService service = new ArquivamentoAdminService(dao, categoriaDao);
```

### 4️⃣ **Interface Segregation Principle (ISP)** - Princípio da Segregação de Interface

Interfaces específicas e coesas evitam dependências desnecessárias:

```csharp
public interface ICommand<T> // Interface focada em comandos
{
    void Incluir(T obj);
    void Alterar(T obj);
    void Excluir(T obj);
}

public interface IQuery<T> // Interface focada em consultas
{
    IEnumerable<T> BuscarTodos();
    T BuscarPorId(int id);
}
```

### 5️⃣ **Dependency Inversion Principle (DIP)** - Princípio da Inversão de Dependência

Módulos de alto nível não dependem de módulos de baixo nível, ambos dependem de abstrações:

```csharp
public class LeilaoController : Controller
{
    IAdminService _service; // Depende da abstração, não da implementação
    
    public LeilaoController(IAdminService service)
    {
        _service = service; // Injeção de dependência
    }
}
```

---

## 🛠️ Tecnologias Utilizadas

### **Framework e Linguagem**
| Tecnologia | Versão | Descrição |
|------------|--------|-----------|
| **.NET Core** | 3.1 | Framework multiplataforma para desenvolvimento web |
| **C#** | 10.0 | Linguagem de programação orientada a objetos |
| **ASP.NET Core MVC** | 3.1 | Framework web baseado no padrão Model-View-Controller |

### **Banco de Dados e ORM**
| Tecnologia | Versão | Descrição |
|------------|--------|-----------|
| **Entity Framework Core** | 3.1.0 | ORM para acesso a dados |
| **SQL Server LocalDB** | - | Banco de dados local para desenvolvimento |
| **EF Core InMemory** | 3.1.0 | Provedor em memória para testes |

### **Bibliotecas e Pacotes**
| Pacote | Versão | Finalidade |
|--------|--------|-----------|
| **Microsoft.EntityFrameworkCore.SqlServer** | 3.1.0 | Provider SQL Server para EF Core |
| **Microsoft.EntityFrameworkCore.Tools** | 3.1.0 | Ferramentas de linha de comando para migrations |
| **Microsoft.AspNetCore.Mvc.NewtonsoftJson** | 3.1.1 | Serialização JSON com Newtonsoft |
| **xUnit** | 2.4.0 | Framework de testes unitários |
| **Microsoft.NET.Test.Sdk** | 16.5.0 | SDK para execução de testes |

### **Ferramentas de Desenvolvimento**
- **Visual Studio 2019** (versão 16.0 ou superior)
- **Visual Studio Code** (alternativa)
- **SQL Server Management Studio** (opcional, para gerenciar banco de dados)

---

## ⚡ Funcionalidades

### 🎯 Módulo de Administração (Web MVC)

- ✅ **Listagem de Leilões**: Visualização de todos os leilões cadastrados
- ✅ **Cadastro de Leilões**: Inclusão de novos leilões com categoria, título, descrição e datas
- ✅ **Edição de Leilões**: Atualização de informações de leilões existentes
- ✅ **Remoção de Leilões**: Exclusão lógica (arquivamento) ou física de leilões
- ✅ **Início de Pregão**: Transição do leilão de rascunho para pregão ativo
- ✅ **Finalização de Pregão**: Encerramento de leilões em andamento
- ✅ **Busca Avançada**: Pesquisa por título, descrição ou categoria
- ✅ **Gestão de Categorias**: Consulta de categorias com estatísticas de leilões

### 🌐 API REST (Web API)

- 🔹 **GET /api/leiloes** - Lista todos os leilões
- 🔹 **GET /api/leiloes/{id}** - Busca leilão por ID
- 🔹 **POST /api/leiloes** - Cadastra novo leilão
- 🔹 **PUT /api/leiloes** - Atualiza leilão existente
- 🔹 **DELETE /api/leiloes/{id}** - Remove leilão
- 🔹 **POST /api/leiloes/{id}/pregao** - Inicia pregão
- 🔹 **DELETE /api/leiloes/{id}/pregao** - Finaliza pregão

### 💻 Interface CLI (Command Line Interface)

- 📝 **listar** - Lista todos os leilões cadastrados
- 📝 **detalhe <ID>** - Exibe detalhes de um leilão específico

### 📊 Estados do Leilão

O sistema gerencia 4 estados distintos de leilão:

1. **Rascunho** - Leilão criado mas não iniciado
2. **Pregão** - Leilão ativo recebendo lances
3. **Finalizado** - Pregão encerrado
4. **Arquivado** - Leilão removido logicamente do sistema

---

## 📂 Estrutura do Projeto

```
solid-csharp-main/
│
├── 📄 projeto.sln                          # Solution do Visual Studio
├── 📄 README.md                            # Documentação original
├── 📄 .gitignore                           # Arquivos ignorados pelo Git
│
├── 📁 src/                                 # Código-fonte da aplicação
│   ├── 📁 Alura.LeilaoOnline.WebApp/      # Aplicação Web Principal
│   │   ├── 📁 Controllers/                 # Controladores MVC e API
│   │   │   ├── HomeController.cs          # Controller da página inicial
│   │   │   ├── LeilaoController.cs        # Controller MVC de leilões
│   │   │   └── LeilaoApiController.cs     # API REST de leilões
│   │   │
│   │   ├── 📁 Models/                      # Entidades de domínio
│   │   │   ├── Leilao.cs                  # Modelo de leilão
│   │   │   ├── Categoria.cs               # Modelo de categoria
│   │   │   └── SituacaoLeilao.cs          # Enum de situações
│   │   │
│   │   ├── 📁 Services/                    # Camada de serviços (lógica de negócio)
│   │   │   ├── IAdminService.cs           # Interface do serviço administrativo
│   │   │   ├── IProdutoService.cs         # Interface do serviço de produtos
│   │   │   └── 📁 Handlers/                # Implementações dos serviços
│   │   │       ├── DefaultAdminService.cs  # Serviço padrão de administração
│   │   │       ├── ArquivamentoAdminService.cs # Serviço com arquivamento
│   │   │       └── DefaultProdutoService.cs    # Serviço de produtos
│   │   │
│   │   ├── 📁 Dados/                       # Camada de acesso a dados (DAL)
│   │   │   ├── ICommand.cs                # Interface genérica de comandos
│   │   │   ├── IQuery.cs                  # Interface genérica de consultas
│   │   │   ├── ILeilaoDao.cs              # Interface DAO de leilões
│   │   │   ├── ICategoriaDao.cs           # Interface DAO de categorias
│   │   │   └── 📁 EfCore/                  # Implementações com Entity Framework
│   │   │       ├── AppDbContext.cs         # Contexto do banco de dados
│   │   │       ├── LeilaoDaoComEfCore.cs   # DAO de leilões com EF Core
│   │   │       └── CategoriaDaoComEfCore.cs # DAO de categorias com EF Core
│   │   │
│   │   ├── 📁 Views/                       # Views Razor MVC
│   │   │   ├── 📁 Home/                    # Views da home
│   │   │   ├── 📁 Leilao/                  # Views de leilão
│   │   │   └── 📁 Shared/                  # Views compartilhadas
│   │   │
│   │   ├── 📁 wwwroot/                     # Arquivos estáticos (CSS, JS, imagens)
│   │   ├── 📁 Seeding/                     # Scripts de inicialização do banco
│   │   ├── Program.cs                      # Ponto de entrada da aplicação
│   │   ├── Startup.cs                      # Configuração de serviços e middleware
│   │   └── Alura.LeilaoOnline.WebApp.csproj # Arquivo de projeto
│   │
│   └── 📁 Alura.LeilaoOnline.CLI/         # Aplicação Console
│       ├── Program.cs                      # Interface de linha de comando
│       └── Alura.LeilaoOnline.CLI.csproj  # Arquivo de projeto CLI
│
└── 📁 tests/                               # Projeto de testes
    └── 📁 Alura.LeilaoOnline.Testes/      # Testes unitários
        ├── LeilaoControllerRemove.cs       # Testes do controller
        └── Alura.LeilaoOnline.Testes.csproj # Arquivo de projeto de testes
```

---

## 🎯 Funcionalidades

### **Sistema Web (MVC)**

#### Gerenciamento de Leilões
- **Listar Leilões**: Exibe todos os leilões não arquivados com suas informações
- **Criar Leilão**: Formulário para cadastro de novos leilões
- **Editar Leilão**: Atualização de dados de leilões existentes
- **Remover Leilão**: Arquivamento lógico de leilões (não remove fisicamente)
- **Iniciar Pregão**: Transição de leilão de "Rascunho" para "Pregão"
- **Finalizar Pregão**: Encerramento de leilões ativos
- **Pesquisar**: Busca textual em título, descrição e categoria

#### Gestão de Categorias
- Consulta de categorias disponíveis
- Estatísticas por categoria (rascunhos, em pregão, finalizados)
- Associação de leilões a categorias

### **API REST**

API RESTful completa seguindo convenções HTTP para integração com outros sistemas:

| Método | Endpoint | Descrição | Status Code |
|--------|----------|-----------|-------------|
| GET | `/api/leiloes` | Lista todos os leilões | 200 OK |
| GET | `/api/leiloes/{id}` | Busca leilão por ID | 200 OK / 404 Not Found |
| POST | `/api/leiloes` | Cria novo leilão | 200 OK |
| PUT | `/api/leiloes` | Atualiza leilão | 200 OK / 404 Not Found |
| DELETE | `/api/leiloes/{id}` | Remove leilão | 204 No Content / 404 Not Found |
| POST | `/api/leiloes/{id}/pregao` | Inicia pregão | 200 OK / 404 Not Found |
| DELETE | `/api/leiloes/{id}/pregao` | Finaliza pregão | 200 OK / 404 Not Found |

### **Interface CLI**

Aplicação console para administração via linha de comando:

```bash
# Listar todos os leilões
dotnet run --project src/Alura.LeilaoOnline.CLI listar

# Ver detalhes de um leilão específico
dotnet run --project src/Alura.LeilaoOnline.CLI detalhe 1
```

---

## 🧩 Estrutura de Camadas

### **Camada de Apresentação**
- **Controllers**: Gerenciam requisições HTTP (MVC e API)
- **Views**: Templates Razor para renderização HTML
- **wwwroot**: Recursos estáticos (CSS, JavaScript, imagens)

### **Camada de Negócio**
- **Services**: Lógica de negócio e regras de domínio
  - `IAdminService`: Interface para serviços administrativos
  - `DefaultAdminService`: Implementação padrão com remoção física
  - `ArquivamentoAdminService`: Implementação com arquivamento lógico
  - `IProdutoService`: Interface para consultas públicas
  - `DefaultProdutoService`: Implementação de consultas de produtos

### **Camada de Dados**
- **DAOs (Data Access Objects)**: Abstração de acesso a dados
  - `ILeilaoDao` / `LeilaoDaoComEfCore`: Acesso a leilões
  - `ICategoriaDao` / `CategoriaDaoComEfCore`: Acesso a categorias
- **Interfaces Genéricas**:
  - `ICommand<T>`: Operações de escrita (Insert, Update, Delete)
  - `IQuery<T>`: Operações de leitura (Select)
- **Entity Framework Core**: ORM para mapeamento objeto-relacional

### **Camada de Domínio**
- **Models**: Entidades de negócio
  - `Leilao`: Representa um leilão com título, descrição, datas e categoria
  - `Categoria`: Agrupa leilões por tipo
  - `SituacaoLeilao`: Enum para controle de estado do leilão
  - `CategoriaComInfoLeilao`: DTO com estatísticas de categoria

---

## 📋 Pré-requisitos

Antes de executar o projeto, certifique-se de ter instalado:

- ✔️ **.NET Core SDK 3.1** ou superior ([Download](https://dotnet.microsoft.com/download/dotnet/3.1))
- ✔️ **SQL Server LocalDB** (incluído no Visual Studio) ou SQL Server Express
- ✔️ **Visual Studio 2019+** ou **Visual Studio Code** com extensão C#
- ✔️ **Git** (para clonar o repositório)

### Verificar Instalação

```bash
# Verificar versão do .NET
dotnet --version

# Verificar SDKs instalados
dotnet --list-sdks

# Verificar runtimes instalados
dotnet --list-runtimes
```

---

## 🚀 Instalação e Configuração

### **1. Clonar ou Extrair o Projeto**

```bash
# Se estiver em um repositório Git
git clone <url-do-repositorio>
cd solid-csharp-main

# Ou extrair o arquivo ZIP
unzip solid-csharp-main.zip
cd solid-csharp-main
```

### **2. Restaurar Dependências**

```bash
# Restaurar pacotes NuGet
dotnet restore
```

### **3. Configurar Banco de Dados**

O projeto utiliza SQL Server LocalDB por padrão. A string de conexão está configurada em `AppDbContext.cs`:

```csharp
Server=(localdb)\\MSSQLLocalDB;Database=AluraLeiloesDB;Trusted_Connection=true
```

Para usar outro banco de dados, modifique a string de conexão conforme necessário.

### **4. Criar Banco de Dados**

O banco de dados é criado automaticamente na primeira execução através do método `DatabaseGenerator.Seed()`.

---

## ▶️ Executando o Projeto

### **Aplicação Web (MVC + API)**

```bash
# Navegar até o diretório do projeto web
cd src/Alura.LeilaoOnline.WebApp

# Executar a aplicação
dotnet run

# A aplicação estará disponível em:
# https://localhost:5001
# http://localhost:5000
```

### **Aplicação CLI**

```bash
# Executar comandos CLI
cd src/Alura.LeilaoOnline.CLI

# Exibir comandos disponíveis
dotnet run

# Listar leilões
dotnet run listar

# Detalhar leilão específico
dotnet run detalhe 1
```

### **Build da Solution**

```bash
# Compilar todos os projetos
dotnet build

# Compilar em modo Release
dotnet build --configuration Release
```

---

## 🧪 Testes

O projeto inclui testes unitários usando **xUnit** para validar o comportamento dos controllers.

### **Executar Testes**

```bash
# Executar todos os testes
dotnet test

# Executar testes com output detalhado
dotnet test --verbosity detailed

# Executar testes com cobertura
dotnet test /p:CollectCoverage=true
```

### **Testes Implementados**

- ✅ `DadoLeilaoInexistenteEntaoRetorna404`: Valida retorno 404 para leilão inexistente
- ✅ `DadoLeilaoEmPregaoEntaoRetorna405`: Valida bloqueio de remoção de leilão ativo
- ✅ `DadoLeilaoEmRascunhoEntaoExcluiORegistro`: Valida remoção de leilão em rascunho

---

## 🎨 Padrões de Projeto Implementados

### **1. Repository Pattern**
Abstração do acesso a dados através de DAOs (Data Access Objects):
```csharp
public interface ILeilaoDao : ICommand<Leilao>, IQuery<Leilao> { }
```

### **2. Dependency Injection (IoC)**
Injeção de dependências configurada no `Startup.cs`:
```csharp
services.AddTransient<ICategoriaDao, CategoriaDaoComEfCore>();
services.AddTransient<ILeilaoDao, LeilaoDaoComEfCore>();
services.AddTransient<IAdminService, ArquivamentoAdminService>();
```

### **3. Service Layer Pattern**
Separação da lógica de negócio em serviços:
- `IAdminService` - Operações administrativas
- `IProdutoService` - Consultas públicas de produtos

### **4. Command-Query Separation (CQS)**
Segregação de operações de leitura e escrita:
```csharp
ICommand<T>  // Comandos que modificam estado
IQuery<T>    // Consultas que apenas leem dados
```

### **5. Decorator Pattern**
`ArquivamentoAdminService` decora `DefaultAdminService` adicionando comportamento de arquivamento:
```csharp
public class ArquivamentoAdminService : IAdminService
{
    IAdminService _defaultService; // Composição ao invés de herança
}
```

### **6. MVC (Model-View-Controller)**
Separação clara de responsabilidades na camada de apresentação.

### **7. DTO (Data Transfer Object)**
`CategoriaComInfoLeilao` - Transferência de dados com informações agregadas.

---

## 🔧 Configuração de Injeção de Dependências

O projeto demonstra o uso avançado de IoC Container do ASP.NET Core:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Registro de DAOs
    services.AddTransient<ICategoriaDao, CategoriaDaoComEfCore>();
    services.AddTransient<ILeilaoDao, LeilaoDaoComEfCore>();
    
    // Registro de serviços de negócio
    services.AddTransient<IAdminService, ArquivamentoAdminService>();
    services.AddTransient<IProdutoService, DefaultProdutoService>();
    
    // Configuração do DbContext
    services.AddDbContext<AppDbContext>();
    
    // Configuração de controllers e JSON
    services
        .AddControllersWithViews()
        .AddNewtonsoftJson(options => 
        {
            options.SerializerSettings.ReferenceLoopHandling = 
                Newtonsoft.Json.ReferenceLoopHandling.Ignore;
        });
}
```

---

## 💾 Modelo de Dados

### **Entidade Leilao**
```csharp
public class Leilao
{
    public int Id { get; set; }
    public string Titulo { get; set; }           // Obrigatório
    public string Descricao { get; set; }
    public DateTime? Inicio { get; set; }        // Data de início do pregão
    public DateTime? Termino { get; set; }       // Data de término do pregão
    public int IdCategoria { get; set; }         // Chave estrangeira
    public Categoria Categoria { get; set; }     // Navegação
    public SituacaoLeilao Situacao { get; set; } // Estado atual
    public string PosterUrl { get; }             // URL da imagem
}
```

### **Entidade Categoria**
```csharp
public class Categoria
{
    public int Id { get; set; }
    public string Descricao { get; set; }
    public string Imagem { get; set; }
    public IList<Leilao> Leiloes { get; set; }  // Relação 1:N
}
```

### **Relacionamentos**
- **Categoria → Leilão**: Relacionamento 1:N (uma categoria possui vários leilões)

---

## 📐 Fluxo de Operações

### **Ciclo de Vida de um Leilão**

```
┌─────────────┐
│  Rascunho   │ ← Leilão criado
└──────┬──────┘
       │ Iniciar Pregão
       ▼
┌─────────────┐
│   Pregão    │ ← Leilão ativo (não pode ser removido)
└──────┬──────┘
       │ Finalizar Pregão
       ▼
┌─────────────┐
│ Finalizado  │ ← Pregão encerrado
└──────┬──────┘
       │ Arquivar
       ▼
┌─────────────┐
│ Arquivado   │ ← Removido logicamente
└─────────────┘
```

---

## 🔍 Exemplos de Uso

### **Exemplo 1: Cadastro de Leilão via API**

```bash
curl -X POST https://localhost:5001/api/leiloes \
  -H "Content-Type: application/json" \
  -d '{
    "titulo": "Notebook Dell i7",
    "descricao": "Notebook usado em ótimo estado",
    "idCategoria": 1
  }'
```

### **Exemplo 2: Buscar Leilões**

```bash
curl -X GET https://localhost:5001/api/leiloes
```

### **Exemplo 3: Iniciar Pregão**

```bash
curl -X POST https://localhost:5001/api/leiloes/1/pregao
```

### **Exemplo 4: Uso do Service com DI**

```csharp
public class LeilaoController : Controller
{
    IAdminService _service;
    
    public LeilaoController(IAdminService service) // Injetado automaticamente
    {
        _service = service;
    }
    
    public IActionResult Index()
    {
        var leiloes = _service.ConsultaLeiloes(); // Usa abstração
        return View(leiloes);
    }
}
```

---

## 🧠 Conceitos Avançados Demonstrados

### **1. Segregação de Interfaces (ISP)**
```csharp
// Interfaces pequenas e específicas
public interface ICommand<T>  // Apenas comandos de escrita
public interface IQuery<T>    // Apenas consultas de leitura
```

### **2. Composição sobre Herança**
```csharp
// ArquivamentoAdminService usa composição, não herança
public class ArquivamentoAdminService : IAdminService
{
    IAdminService _defaultService; // Composição
}
```

### **3. Injeção de Dependência via Construtor**
```csharp
public DefaultAdminService(ILeilaoDao dao, ICategoriaDao categoriaDao)
{
    _dao = dao;
    _categDao = categoriaDao;
}
```

### **4. Generic Types**
Uso de generics para reutilização de código:
```csharp
public interface ICommand<T>
public interface IQuery<T>
```

---

## 🎓 Aprendizado e Benefícios dos Princípios SOLID

### **Vantagens Implementadas**

✅ **Manutenibilidade**: Código fácil de entender e modificar  
✅ **Testabilidade**: Dependências podem ser mockadas facilmente  
✅ **Extensibilidade**: Novos comportamentos sem alterar código existente  
✅ **Reusabilidade**: Componentes podem ser reutilizados em outros contextos  
✅ **Desacoplamento**: Baixo acoplamento entre módulos  
✅ **Escalabilidade**: Arquitetura preparada para crescimento  

### **Exemplos Práticos no Projeto**

| Princípio | Implementação no Projeto |
|-----------|--------------------------|
| **SRP** | Controllers só gerenciam HTTP, Services só têm lógica de negócio |
| **OCP** | Novos tipos de serviços podem ser criados sem modificar existentes |
| **LSP** | `ArquivamentoAdminService` pode substituir `DefaultAdminService` |
| **ISP** | `ICommand` e `IQuery` separam operações de escrita e leitura |
| **DIP** | Controllers dependem de `IAdminService`, não de implementações concretas |

---

## 🔐 Segurança e Validações

- ✔️ **Model Validation**: Data Annotations para validação de entrada
- ✔️ **HTTPS Redirection**: Redirecionamento automático para HTTPS
- ✔️ **Status Code Pages**: Páginas customizadas para erros HTTP
- ✔️ **Developer Exception Page**: Página detalhada de exceções em desenvolvimento
- ✔️ **Reference Loop Handling**: Configuração para evitar loops em serialização JSON

---

## 👥 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. 🍴 Faça um **fork** do projeto
2. 🌿 Crie uma **branch** para sua feature (`git checkout -b feature/MinhaFeature`)
3. ✍️ Faça **commit** das suas alterações (`git commit -m 'Adiciona MinhaFeature'`)
4. 📤 Faça **push** para a branch (`git push origin feature/MinhaFeature`)
5. 🎉 Abra um **Pull Request**

### **Diretrizes de Código**

- Siga os princípios SOLID
- Mantenha a cobertura de testes
- Use PascalCase para classes e métodos
- Use camelCase para variáveis e parâmetros privados
- Adicione comentários apenas quando necessário
- Documente mudanças significativas

---

## 📚 Recursos Adicionais

### **Documentação Oficial**
- [Documentação ASP.NET Core](https://docs.microsoft.com/aspnet/core)
- [Entity Framework Core](https://docs.microsoft.com/ef/core)
- [C# Programming Guide](https://docs.microsoft.com/dotnet/csharp)

### **Princípios SOLID**
- [SOLID Principles - Wikipedia](https://en.wikipedia.org/wiki/SOLID)
- [SOLID Principles in C#](https://www.c-sharpcorner.com/UploadFile/damubetha/solid-principles-in-C-Sharp/)
- [Curso SOLID - Alura](https://www.alura.com.br/course?id=solid)

### **Padrões de Projeto**
- [Design Patterns in C#](https://refactoring.guru/design-patterns/csharp)
- [Repository Pattern](https://docs.microsoft.com/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)

---

## 📝 Notas de Desenvolvimento

### **Decisões Arquiteturais**

1. **Arquivamento vs Exclusão**: Por padrão, o sistema usa `ArquivamentoAdminService` que arquiva leilões ao invés de removê-los fisicamente, preservando histórico.

2. **Command-Query Separation**: Interfaces `ICommand` e `IQuery` separam claramente operações de escrita e leitura.

3. **Injeção de Dependência**: Todo o sistema usa DI, facilitando testes e substituição de implementações.

4. **Entity Framework Core**: Uso de Include para carregamento eager de relacionamentos, evitando N+1 queries.

---

## 📄 Licença

Este projeto está licenciado sob a **Licença MIT** - veja o arquivo LICENSE para mais detalhes.

```
MIT License

Copyright (c) 2024 jrmoreiram

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 👨‍💻 Autor

**Junior Moreira Martins**  
📧 E-mail: jumoreiram@gmail.com  
🔗 GitHub: [@jrmoreiram](https://github.com/jrmoreiram)

---

## 🙏 Agradecimentos

- **Alura** - Plataforma de ensino e conteúdo educacional
- **Alura** - Curso SOLID com C#: princípios da programação orientada a objetos
- Comunidade .NET e C#

---

## 📌 Versão

**v1.0.0** - Versão inicial com implementação completa dos princípios SOLID

---

## 🔄 Changelog

### [1.0.0] - 2024
- ✨ Implementação inicial do sistema de leilões
- ✨ Aplicação dos 5 princípios SOLID
- ✨ API REST completa
- ✨ Interface web MVC
- ✨ CLI para administração
- ✨ Testes unitários com xUnit
- ✨ Integração com Entity Framework Core
- ✨ Sistema de arquivamento de leilões

---

<div align="center">

**Desenvolvido com ❤️ usando C# e .NET Core**

[![.NET](https://img.shields.io/badge/.NET-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)](https://docs.microsoft.com/dotnet/csharp/)
[![Visual Studio](https://img.shields.io/badge/Visual%20Studio-5C2D91?style=for-the-badge&logo=visual-studio&logoColor=white)](https://visualstudio.microsoft.com/)

</div>
