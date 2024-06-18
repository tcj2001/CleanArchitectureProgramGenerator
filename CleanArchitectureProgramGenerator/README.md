# Clean Architecture Style Code Generator  
This is a .Net8.0 Clean Architecture style code generator which will generate Domain project containing entities; Application project containing repository interfaces, service interfaces, service implementations; Persistence project containg ApplicationDbcontext, repository implementations; it will also generate controllers for each entity in the WebAPI or WEBMVC project.  

**A working WEBAPI and WEBMVC project pointing a database with multiple tables can be generated and smoke tested under 4 minutes.**

Version 8.1.0 and above supports Generating **Angular 18 Frontend** that make use of the WebAPI backend, all genereted with this program generator.
- [Angular 18 Frontend](#clean-architecture-angular-generatortt)

 
---
## Table of Contents
- [Getting Started](#getting-started)
- [Github Link](#github-link)
- [Installing template from Nuget Package Manager](#installing-template-from-nuget-package-manager)
- [How to check if this really works](#how-to-check-if-this-really-works)
    * Adding new entities
      * [Code First approach](#code-first-approach)
      * [Database First approach](#database-first-approach)
- [Some useful commands](#some-useful-commands)

---
# Getting Started
This is a NuGet package that should be installed as a template in dotnet cli.  
You can browse this package using manage NuGet packages by searching for "Thomson Mathews" or "CleanArchitectureProgramGenerator"  
![Imgur](https://i.imgur.com/OZQPWBX.png)  
This will install four template files in your project.  
[Clean Architecture Angular Generator.tt](#clean-architecture-angular-generatortt)  
[Clean Architecture Database Access Generator.tt](#clean-architecture-database-access-generator.tt)  
[Clean Architecture WebAPI Generator.tt](#clean-architecture-webapi-generator.tt)  
[Clean Architecture WebMVC Generator.tt](#clean-architecture-webmvc-generator.tt)  
![Imgur](https://i.imgur.com/i1OPN4T.png)

Once these template files are installed.   

Run **Clean Architecture Database Access Generator.tt** template by right clicking on the template and select "Run Custom Tool".  
![Imgur](https://i.imgur.com/MpsMt8f.png) 

This will generate the following projects.  
![Imgur](https://i.imgur.com/F913Fx4.png)  
Now define entities in the Domain Project entities folder using code first approach or database first approach and ApplicationDbContext in Persistence project context folder.  
![Imgur](https://i.imgur.com/Ul0NKnH.png)  
**Run Clean Architecture Database Access Generator.tt again** to generate all repositories, services for the each entity that was added in the previous step.  

**Run Clean Architecture WebAPI Generator.tt** to generate API controllers in WebAPI project.   

**Run Clean Architecture WebMVC Generator.tt** to generate MVC controllers in WebMVC project.   

**Run Clean Architecture Angular Generator.tt** to generate Agular 18 frontend project.   

set WebAPI or WebMVC or AngularProject1 as a startup project.    

**Voila! a working WebAPI or WebMVC or AngularProject1 is ready for you**.  

if more entities are added, just run all these three transformation again, that's it.

---
## Clean Architecture Database Access Generator.tt
This template will generate 4 projects:  
Domain, Application, Persistence, Startup.  
![Imgur](https://i.imgur.com/F913Fx4.png)

**Domain Project:**  
Define all entities in Entities folder, either using code first approach or database approach, Exceptions folder defines some basic useful exceptions that can be used in global error handling. This project also refers to the latest Microsoft EntityFramework 
![Imgur](https://i.imgur.com/l9vUPg0.png)

**Application Project**  
Defines Interface for ServiceManager, Services in the ServiceInterfaces folder, implementation of ServiceManager and Services in Services folder, interfaces for RepositoryManager, GenericRepository, Repositories and UnitOfWork in RepositoryInterface folder.  
![Imgur](https://i.imgur.com/6YmGnbF.png)

**Persistence Project:**     
ApplicationDbContext should be defined or generated using Entity Framework in the context folder, Repositories folder contains GenericRepository, Repositories, RepositoryManager and UnitOfWork implementation.  
![Imgur](https://i.imgur.com/qbu36A0.png)

**Startup Project:**  
This is a console application that will create a Generic Host which will help in dependency injection, here ApplicationDbContext is added to the ServiceCollection, this project will help you to run Entity Framework commands to do entity migrations to a database or generate entities and ApplicationDbContext from existing database. It also has a appsettings.json file containing the connection string.  
![Imgur](https://i.imgur.com/trueaY6.png)  

Startup project is only used to run Entity Framework commands with out a WebAPI project and Startup project is not required if WebAPI project is generated.  

*Once you add more entities, you can **run this template again to generate** repository interfaces for the new Entities in the Domain Project, repository implementation for the new Entities in Persistence Project and Services and its Service interfaces for the new Entities in the Application Project*.  

---
## Clean Architecture WebAPI Generator.tt
This template will open a dialog box, select "**ASP.NET Core Web API**" project template to generate a initial skelton of Web API project which will be modified by the "Clean Architecture WebAPI Generator template" 

This template will generate open a dialog box, select ASP.NET Core WebAPI project and it will create a project named **WebAPI**
![Imgur](https://i.imgur.com/NIWie2l.png)  

**WebAPI Project:**  
This contains controllers and other required classes.  
![Imgur](https://i.imgur.com/FQvYm1E.png)  

**Controller Folder:**  
Contains generated controller for each entities defined in Domain project.  

**Extensions Folder:**  
Contains extension method to add BasicAuthMiddleware to the HTTP request pipeline.    

**MiddleWare Folder:**     
Contains implementation for BasicAuthMiddleware and ExceptionHandlingMiddleware.  

**Appsetting.json:**   
Contains configuration for Serilog logging, connection string and basic authentication details.  

**Appsetting Folder:**   
Contains classes structures to read from appsettings.json file.    

**Program.cs**
This connect all the wiring between the projects.
![Imgur](https://i.imgur.com/zxu0z6b.png)  
![Imgur](https://i.imgur.com/c78Vu0r.png)  

*Once you add more entities, you can **run this template again to generate** controllers for the new Entities in the WebAPI Project.*  

---
## Clean Architecture WebMVC Generator.tt
This template will open a dialog box, select "**ASP.NET Core Web app (Mode-View-Controller)**" project template to generate a initial skelton of MVC project which will be modified by the "Clean Architecture WebMVC Generator template" 
it will create a project named **WebAPI**
![Imgur](https://i.imgur.com/fh5AqG2.png)  

**WebAPI Project:**  
This contains controllers and other required classes.  
![Imgur](https://i.imgur.com/aRxJCbS.png)  

**Controller Folder:**  
Contains generated controller for each entities defined in Domain project.  

**Extensions Folder:**  
Contains extension method to add BasicAuthMiddleware to the HTTP request pipeline.    

**MiddleWare Folder:**     
Contains implementation for BasicAuthMiddleware and ExceptionHandlingMiddleware.  

**Appsetting.json:**   
Contains configuration for Serilog logging, connection string and basic authentication details.  

**Appsetting Folder:**   
Contains classes structures to read from appsettings.json file.    

**Program.cs**
This connect all the wiring between the projects.
![Imgur](https://i.imgur.com/JvQp9vz.png) 

*Once you add more entities, you can **run this template again to generate** controllers for the new Entities in the WebAPI Project.*  

---
## Clean Architecture Angular Generator.tt
To make use of this generator, you need to have Angular CLI installed in your system.
**npm install –g @angular/cli**

Next step is to create a Standalone TypeScript Angular Project in Visual Studio
![Imgur](https://i.imgur.com/QnNV7er.png)  

This will create a project named AngularProject1, (Important: Leave the project name as **AngularProject1**).
![Imgur](https://i.imgur.com/EYNzCe7.png)  

this will create the following structure in the solution explorer.
![Imgur](https://i.imgur.com/1hrvdCL.png)  

Go to your Developer PowerShell and change directory to the AngularProject1 folder.
![Imgur](https://i.imgur.com/CpXF3NI.png)  

Now install these packages
**npm install bootstrap**
**npm install ngx-pagination**

Right click on the **Clean Architecture Angular Generator.tt** and select "Run Custom Tool"
![Imgur](https://i.imgur.com/cHhmXQp.png)  

This will generate module and its component for each entity defined in the Domain project.
![Imgur](https://i.imgur.com/Mm7JBmM.png)  


---
## T4Helper.ttinclude
This file contains function used by the above T4Template files.

---
## Github Link
https://github.com/tcj2001/CleanArchitectureProgramGenerator  

---
## Installing template from Nuget Package Manager
From your package manager console.  
**dotnet new install CleanArchitectureProgramGenerator**  
This will add a new template in your dotnet cli environment.  
![Imgur](https://i.imgur.com/4xfUr1Z.png)  

**dotnet new list**  
you can use the above command to check if the template was installed. 
![Imgur](https://i.imgur.com/3v70m6Q.png)  

**CAPG** is shortname for the template

There are **two way** to use the template.

**First Method**.  
Go to a directory where you want to make use of the template and type command.   
**dotnet new CAPG -o yourProjectSolution** 
![Imgur](https://i.imgur.com/G0WnT58.png)  

This will create a ClassLibrary project named CleanArchitectureProgramGenerator within in your project solution  
![Imgur](https://i.imgur.com/60G7kGd.png)

**Second Method**.  
When you select new project in visual studio you will see a template named CleanArchitectureProgramGenerator, if you don't see filter the project type and select Clean Architecture, select this template and create your project.   
![Imgur](https://i.imgur.com/V32Ny3x.png)  

This will create a ClassLibrary project named Clean_Architecture_Program_Generator_for_CSharp_and_NET6 within YourProjectFolderName.    
![Imgur](https://i.imgur.com/60G7kGd.png)
  
---
## How to check if this really works
Once all the Data related projects are generated using the "**Clean Architecture Database Access Generator.tt**" template.    
Domain project by default will be provided one entity named **Sample** and it's Repository and Service.  

![Imgur](https://i.imgur.com/p9we3ju.png)
When you add new entities in the Domain project under Entities folder:  
The classes highlighted in green will get generated for **each entity** defined in the Domain project entities folder.    
The Classes highlighted in red gets re-generated every time with entity details.  

Startup project adds ApplicationDbContext to the service collection for dependency injection and points to a database, **change** the the connection string as needed, before you proceed to next step.   
![Imgur](https://i.imgur.com/zEEwBBJ.png)

## Code First approach 
Since we already have a sample entity defined for you by the template, let's just make use of it.   

In the Startup project modify appsettings.json to edit the connection string.  
![Imgur](https://i.imgur.com/x7yNBU4.png)  


**dotnet ef migrations add "Add Sample entity to Database" --project Persistence --startup-project Startup**    
**dotnet ef database update --project Persistence --startup-project Startup**  
![Imgur](https://i.imgur.com/qaY1YRK.png)    

These commands will add Sample table to the database.    

Note: Here **Startup** project is used to run Entity Framework commands.

Now use **Clean Architecture WebAPI Generator.tt** to generate **WebAPI** project.
This will also create a controller for the Sample entity in the project.  

Update the WebAPI projects appsetting.json to point to the correct database.  

**Set WebAPI as a startup project and run it.**  
![Imgur](https://i.imgur.com/OGxNSBs.png)  


## Database First approach
Here we will make use of a BookStoresDB database in a Sql Server setup. 
This database was grabbed from internet, credit goes to the person who made it available for community.
![Imgur](https://i.imgur.com/0qdEcWC.png)  

In the Startup project modify appsettings.json to edit the connection string.
![Imgur](https://i.imgur.com/x7yNBU4.png)  

Run this command to generate entities in the domain\Entities folder and ApplicationDbContect in Persitence\Context folder.  
**scaffold-DbContext -Connection "Name=SqlServerDB" -Provider Microsoft.EntityFrameworkCore.SqlServer -Project Persistence -StartupProject Startup -OutputDir ..\Domain\Entities -Context ApplicationDbContext -ContextDir ..\Persistence\Context -Namespace Domain.Entities -ContextNamespace Persistence.Context -DataAnnotations -force**  

*note: if scaffold-DbContext uses a Named connection string, you won't be able to add controllers using visual studio in-built scaffolded mechanism, you can avoid that by providing connection string directly in the scaffold-DbContext command.  

This will generate all entities in domain project  
![Imgur](https://i.imgur.com/RN1FCHt.png)  

Run template:  
**Clean Architecture Database Access Generator.tt**  
To generate repositories and Services for the **new entities**
![Imgur](https://i.imgur.com/VwOeTO5.png)
![Imgur](https://i.imgur.com/6hVZab8.png)  

Run template:  
**Clean Architecture WebAPI Generator.tt**  
To generate controllers for WebAPI project.  
![Imgur](https://i.imgur.com/vEowcAL.png)  

Update the WebAPI projects appsetting.json to point to the correct database.  

Set WebAPI as a startup project and run it.  
![Imgur](https://i.imgur.com/bBLUjZD.png)  
By default the WebAPI uses BasicAuthentication the userid and password is defined in the appsettings.json file  
![Imgur](https://i.imgur.com/SoB2Ame.png)  

Run template:  
**Clean Architecture WebMVC Generator.tt**  
To generate controllers for WebMVC project.  
![Imgur](https://i.imgur.com/xuZR1aG.png)  
![Imgur](https://i.imgur.com/IW00oMb.png)

Run template:  
**Clean Architecture Angular Generator.tt**  
This is going to make use of the WebAPI project to get data from the database, so make sure you have the WebAPI project running.
Now edit the proxy.conf.json file to point to the WebAPI url
![Imgur](https://i.imgur.com/bbznkjW.png)  
Set AngularProject1 as a startup project and run it and you will see the Angular project handling the **CRUD** operation of each entities.
![Imgur](https://i.imgur.com/7Va9oIu.png)  

---
## Some useful commands

**Code First Migrations**  
dotnet ef migrations add "initialmigration1" --project Persistence --startup-project Startup  
dotnet ef migrations add "initialmigration2" --project Persistence --startup-project WebAPI

dotnet ef database update --project Persistence  --startup-project Startup  
dotnet ef database update --project Persistence  --startup-project WebAPI  

**Database First Migrations**  
scaffold-DbContext -Connection "Server=DESKTOP-GBANT4V; Database=BookStoresDB; Trusted_Connection=True;" -Provider Microsoft.EntityFrameworkCore.SqlServer -Project Persistence -StartupProject Startup -OutputDir ..\Domain\Entities  -Context ApplicationDbContext -ContextDir ..\Persistence\Context -Namespace Domain.Entities -ContextNamespace Persistence.Context  -DataAnnotations -Force

If possible do not use connection string directly in the above command.  

if you have an appsettings.json define connection strings as shown  
  "ConnectionStrings": {
    "SqlServerDB": "Server=DESKTOP-GBANT4V; Database=BookStoresDB; Trusted_Connection=True;"
  }  
then use "Name=SqlServerDB" in the scaffold-DbContext -Connection parameter


**Remove migration**  
dotnet ef migrations remove

**List migrations**    
dotnet ef migrations list

**Install Entity Framework**    
dotnet tool install --global dotnet-ef  
dotnet tool update --global dotnet-ef  

**Create a solution with the current director name**    
dotnet new solution

**Create a startup project if webapi or mvc not used**    
dotnet new worker -n Startup

**Create class library**    
dotnet new classlib -o projectName

**Add solution file**    
dotnet sln add SomeFolder/SomeProject.csproj AnotherFolder/AnotherProject.csproj 

**Add project dependency**    
dotnet add SomeFolder/SomeProject.csproj reference AnotherFolder/AnotherProject.csproj

**Add package dependencies**    
dotnet add SomeFolder/SomeProject.csproj package microsoft.entityframeworkcore
