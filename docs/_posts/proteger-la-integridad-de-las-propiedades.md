---
layout: post
title: "Proteger la integridad de las propiedades"
date: 2024-03-04 00:00:00 -0800
categories: dotnet csharp oop
---
Alguna vez nos ha tocado tener que trabajar en un bug causado por que un programador decidió modificar el valor de una propiedad de un objeto en un método largo y complejo y simplemente le dio pereza averiguar el impacto que este podría tener en la aplicación.

La solución a este problema es educar a los jóvenes programadores sobre la importancia de mantener la integridad de estado de un objeto (las propiedades de un objeto no deben ser utilizadas solo como simples variables). Además, una buena practica es limitar que el programador pueda cambiar el valor de las propiedades de un objeto al remover el modificador de acceso SET y solo permitir la asignación de valores a través de un constructor, el modificador INIT o un método miembro de la clase.

```csharp
public class User
{
    public string FirstName { get; }

    public string LastName { get; }

    public User(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }

    public void UpdateFirstName(string firstName)
    {
        FirstName = firstName;
    }
}

var user = new User("John","Smith");

//user.FirstName = "Jimmy"; el programador no puede modificar el estado de la propiedad por medio del modificador de acceso SET
```

```csharp
public class User
{
    public string FirstName { get; init; }

    public string LastName { get; init; }
}

var user = new User
{
    FirstName = "John",
    LastName = "Smith"
}

//user.FirstName = "Jimmy"; el programador no puede modificar el estado de la propiedad por medio del modificador de acceso SET
```

En caso de ser necesario modificar el estado de alguna de las propiedades podemos definir un método en la clase

```csharp
public class User
{
    //...

    public void UpdateName(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
    }
}

//...

user.UpdateName("James", "Smith");

//user.FirstName = "Jimmy"; el programador no puede modificar el estado de la propiedad por medio del modificador de acceso SET
```