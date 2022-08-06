# DDD Project Template (Domain Driven Design)

Implemented a template for use in Visual Studio 2019, using "_DDD_" and some other Designer Patterns.

# Designer Patterns and Concepts
1. Inversion of Control (IoC) - [The Inversion of Control pattern](https://imasters.com.br/dotnet/o-padrao-de-inversao-de-controle-ioc)

2. Dependency Injection (DI) - [Design Patterns - Dependency Injection with C#](https://www.devmedia.com.br/design-patterns-injecao-de-dependencia-com-csharp/23671)

3. Repository Pattern - [Understanding the Repository Pattern](https://medium.com/@renicius.pagotto/entendendo-o-repository-pattern-fcdd0c36b63b)

4. Notification Pattern - [Don't Throw Exceptions on Your Domain... Use Notifications!](https://medium.com/tableless/n%C3%A3o-lance-exceptions-em-seu-dom%C3%ADnio-use-notifications-70b31f7148d3)

5. Value Objects - [alue Objects: A Technique For Self-Documented Code And Fewer Errors](https://carlosschults.net/pt/value-objects-ferramenta/)


# How do I use this template?

Copy the Template.zip file that is inside the Template folder to the folder "C:/Users/[USER]/Documents\Visual Studio 2019\Templates\ProjectTemplates\Visual C#"... Simple as that...

After pasting the .zip in the folder, just open Visual Studio 2019 and ask to create a new project. Follow the image below

![Visual_Studio_2019](TemplateVS2019.png)

# Understanding...

# Research and study carried out in several locations, follow a link to guide - [More detailed explanation about DDD and its pillars](https://medium.com/beelabacademy/domain-driven-design-vs-arquitetura-em-camadas-d01455698ec5)

# “All architecture is design, but not all design is architecture” — Grady Booch

### **1.Application**

Like every project, we need a gateway for our requests and for this template, I'm using the ASP.NET API, but I could also be using ASP.NET MVC (change that implies changing the way we develop Dependency injection) .

### **2.Domain**

For this template, the Domain project is responsible for managing all the application's business rules. The domain layer is the basis for the entire DDD (Domain Driven Design) concept.

The _Repositories_ interfaces were also defined in the Domain project, so any rule to access the database will be implemented in this project.

### **3.InfraEstructure**

The Infrastructure project for this template is responsible for managing access to the database and also Dependency Injection. For that it was segregated into two other projects _CrossCutting_ and _Data_.

- **CrossCutting**

    In this part of the template, the Dependency Injection of the repositories, Services and also the Context that was used in the template was implemented (lines for using the SQL Server Database as a context are commented).

    There are some examples that the CrossCutting layer is responsible for including all application security rules, Cache and others. The Shared project was included for this template, thus leaving the Application project with less possible responsibilities.

- **Date**

    It is responsible for implementing the Context used, for example, if you use Entity Framework, it is in this layer where the _Unit of Work_ would be implemented, where the DbSet and all EF configuration would be implemented.

    The interfaces of the repositories that were declared in the Domain project are implemented in this project.

### **3.Services**

The Services layer's responsibility is to 'translate' the API requests to the Repositories, for example, to map a _DTO (Data Transfer Object)_ to an entity and thus perform an insert through the Repository. This template is separated into two projects, _Interfaces_ and _Services_ for better organization.

- **Interface**

    In the template, this project is used for the implementation of the DTO classes, responsible for receiving the information sent by the _Application_ layer, and also for defining the interfaces that will be used in the Service project. Used the AutoMapper component for mapping between a DTO and an Entity.

- **Services**

    In this project, it contains the implementations of the Services interfaces and is responsible for carrying out the necessary validations so that the request that arrived via API, for example, is trafficked to the appropriate repositories.

### **4.Shared**

The _Shared_ project implements every rule that needs to be shared with the other layers of the project, for example, the _Value Objects_ abstract class.

### **5.Tests**
This project is responsible for creating and running all types of tests.
