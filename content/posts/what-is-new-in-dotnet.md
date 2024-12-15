---
date: '2024-10-22T18:45:04+01:00'
draft: true
description: "This is a post about a talk about .NET by Starfisk"
title: 'What Is New in Dotnet'

# weight: 1
# aliases: ["/first"]
tags: ["tech", "passive event"]
author: "Wolf Schevelenbos"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "/images/starfisk-entrance.jpg" # image path/url
    alt: "me and friends at Starfisk's entrance" # alt text
    linkFullImage: true # click image to open it at full size
    caption: "me and friends at Starfisk's entrance" # display caption under cover
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Starfisk is a small company of 9 people in Bruges. They're consultants. Colin Bundervoet, one of their developers, held an event called "What's new in .Net" to inform students, like me, of the new developments in dotnet.

![picture of Colin Bundervoet](/images/starfisk-speaker.jpg#center)

## .Net

> .NET is a free, open-source developer platform created by Microsoft for building a wide range of applications. It supports multiple programming languages and enables the development of web, desktop, mobile, cloud, gaming, Internet of Things (IoT), and artificial intelligence (AI) applications.

This was a general introduction to .NET. It was common knowledge for most, if not all, of us students that went to visit Starfisk's event. Colin Bundervoet then went on to tell us of the history on .NET.

### History

The .NET Framework. It is an older, Windows-only platform ideal for legacy applications and technologies like WPF and Windows Forms, but it's no longer actively evolving.

In contrast, .NET Core is a modern, cross-platform, high-performance framework designed for building cloud-native and scalable applications, now unified under .NET 5 and beyond. While the .NET Framework remains stable for existing projects, .NET Core (or .NET 5+) is the future of .NET development.

### Versions

Even-numbered .NET versions (e.g., .NET 6, .NET 8) are long-term support (LTS) releases, designed for stability and supported for three years, making them ideal for production environments.

Odd-numbered versions (e.g., .NET 5, .NET 7) are standard-term releases with shorter support of one year, focusing on delivering new features and improvements quickly.

![.NET release schedule](/images/dotnet-release-schedule.svg)

He then went on to go over some notable changes through the ages per version. I'll briefly list those he covered below, though be warned as it can get fairly technical. Feel free to skip to the _Predictions_ section of this text.

#### Early versions (up to C# 9 & .NET 5)

**Records** in C# are reference types designed for immutable data models, introduced in C# 9. They provide concise syntax for defining objects with value-based equality, making them ideal for scenarios like data transfer objects. Unlike regular classes, records use with expressions for shallow copies and automatically generate useful methods like `ToString`, `GetHashCode`, and equality checks.

`Span<T>` is a stack-allocated, high-performance type for managing contiguous memory, ideal for scenarios requiring slicing or processing memory without allocations. It is restricted to synchronous operations and cannot be stored in fields or used across asynchronous calls.

`Memory<T>`, in contrast, is a heap-allocated, more flexible type that supports asynchronous use cases and allows safe persistence in fields. While less performant than `Span<T>`, it provides compatibility with broader scenarios like async methods and background processing.

#### C# 10 & .NET 6

**Global usings** allow you to declare commonly used namespaces in a single file (e.g., global using System;), making them accessible throughout the entire project. This reduces boilerplate code by avoiding repeated using statements in every file.

```C#
global using System;
global using System.Collections.Generic;
```

**Top-Level Statements** simplify the entry point of an application by allowing you to write code directly without wrapping it in a Main method or class. Perfect for small programs and reduces boilerplate.

```C#
Console.WriteLine("Hello, World!"); // No need for "static void Main" or a class wrapper.
```

**Target-Typed new** simplifies object initialization by inferring the type from the context, reducing redundancy when declaring variables.

```C#
List<int> numbers = new(); // Compiler infers List<int> as the type.
```

**Constant interpolated strings** can now be marked as const if their contents consist only of other constant values.

```
const string name = "World";
const string greeting = $"Hello, {name}!";
```

**Tuple-based declarations and assignments**, useful for swapping values or initializing multiple variables concisely, were introduced.

```
int a = 1, b = 2;
(a, b) = (b, a); // Swaps the values of a and b.
Console.WriteLine($"a: {a}, b: {b}"); // Output: a: 2, b: 1
```

**Pattern matching** extended support was introduced for switch expressions, relational patterns (<, >=, etc.), and logical patterns (and, or, not) for more expressive and readable conditions.

```C#
int number = 42;
string result = number switch
{
    < 0 => "Negative",
    >= 0 and <= 10 => "Small",
    > 10 => "Large"
};
```

**DateOnly and TimeOnly** were introduced as lightweight types for working specifically with dates or times, simplifying scenarios where DateTime was overkill.

```C#
DateOnly date = DateOnly.FromDateTime(DateTime.Now); // Just the date.
TimeOnly time = TimeOnly.FromDateTime(DateTime.Now); // Just the time.
Console.WriteLine($"Date: {date}, Time: {time}");
```

#### C# 11 & .NET 7

**The required keyword** ensures certain properties are initialized during object creation, with checks enforced at compile time. This complements nullable reference types by preventing unintentionally uninitialized values.

```C#
public class Person
{
    public required string Name { get; init; } // Must be set when creating the object.
}


var person = new Person { Name = "Alice" }; // Valid.
var invalidPerson = new Person(); // Compile-time error: Name is required.
```

**Generated Regex** through the RegexGenerator attribute generates highly efficient, precompiled regular expressions at compile time. This avoids runtime overhead and ensures better performance.

```C#
using System.Text.RegularExpressions;

[GeneratedRegex("^[a-zA-Z0-9]*$")]
private static partial Regex AlphanumericRegex();

bool isValid = AlphanumericRegex().IsMatch("Sample123"); // Uses precompiled regex.
```

**String Improvements** introduced multiline triple quotes and multiline JSON, which allows strings to span multiple lines easily, preserving indentation and formatting.

```C#
string multiline = """
    This is a
    multi-line string
    with "quotes" and special characters!
    """;

string json = """
    {
        "name": "Alice",
        "age": 30
    }
    """;
```

**Enhanced generic support** makes it easier to create APIs or response types with consistent, type-safe handling of different data structures.

```C#
public class ApiResponse<T>
{
    public T Data { get; set; }
    public int StatusCode { get; set; }
}

var response = new ApiResponse<string> { Data = "Success", StatusCode = 200 };
```

**File-scoped files** allow you to declare types that are only accessible within the file they are defined in, improving encapsulation and reducing unintentional exposure.

```C#
file class InternalHelper
{
    public static void DoSomething() => Console.WriteLine("This is file-scoped.");
}
```

#### C# 12 & .NET 8

**Primary Constructors** made it so classes and structs could now declare constructor parameters directly within the type declaration, simplifying initialization and reducing boilerplate.

```C#
public class Person(string name, int age)
{
    public string Name { get; } = name;
    public int Age { get; } = age;
}
```

**Collection Expressions** provided a unified syntax for initializing collections, allowing concise creation of arrays, lists, and spans, with support for spread elements to include existing collections.

```C#
int[] numbers = [1, 2, 3];
var moreNumbers = [..numbers, 4, 5];
```

**Alias Any Type** as the using directive now supported it, including tuples and pointer types, enhancing code readability and disambiguation.

```
using Point = (int X, int Y);
Point p = (10, 20);
```

**Layered Dependency Injection** was improved. .NET 8 enhanced injection by allowing registration of multiple exception handlers that can be executed in a specified order, facilitating more granular error handling.

```C#
builder.Services.AddExceptionHandler<TimeoutExceptionHandler>();
builder.Services.AddExceptionHandler<GlobalExceptionHandler>();
```

**Enhanced Exception Handling** improved with the introduction of the IExceptionHandler interface, which enabled structured global exception handling without the need for custom middleware, allowing for more modular and maintainable error management.

```C#
public class GlobalExceptionHandler : IExceptionHandler
{
    public async ValueTask<bool> TryHandleAsync(HttpContext httpContext, Exception exception, CancellationToken cancellationToken)
    {
        // Handle exception
        return true;
    }
}
```

#### C# 13 & .NET 9

At the time of the event, this version wasn't released yet. However, we did know what was coming and could talk about it.

**The params keyword** has been enhanced to support various collection types beyond arrays, such as `Span<T>`, `ReadOnlySpan<T>`, and types implementing `IEnumerable<T>` with an `Add` method. This enhancement allows for more flexible and efficient method parameter definitions.

```C#
public void AddNumbers(params Span<int> numbers)
{
    foreach (var number in numbers)
    {
        Console.WriteLine(number);
    }
}

AddNumbers(1, 2, 3); // Now valid with Span<int>
```

**Ordered dictionaries** were added. .NET 9 introduces `OrderedDictionary<TKey, TValue>`, a generic collection that maintains the order of elements as they are added, combining the features of a list and a dictionary.

```C#
var orderedDict = new OrderedDictionary<string, int>
{
    ["apple"] = 1,
    ["banana"] = 2,
    ["cherry"] = 3
};

foreach (var item in orderedDict)
{
    Console.WriteLine($"{item.Key}: {item.Value}");
}
```

**The read-only set** is a new collection type `ReadOnlySet<T>` that provides a read-only wrapper around a set, allowing for the exposure of set data without permitting modifications.

```C#
var modifiableSet = new HashSet<int> { 1, 2, 3 };
var readOnlySet = new ReadOnlySet<int>(modifiableSet);

Console.WriteLine(readOnlySet.Contains(2)); // True
// readOnlySet.Add(4); // Compile-time error
```

**LINQ Enhancements** were made. C# 13 introduces improvements to Language Integrated Query (LINQ), including support for indexing and new aggregation methods, enhancing the expressiveness and performance of LINQ queries.

```C#
var numbers = new[] { 1, 2, 3, 4, 5 };
var thirdElement = numbers.ElementAt(^3); // Index from end, retrieves 3

var sum = numbers.AggregateBy((total, next) => total + next); // Hypothetical new method
```

**The partial keyword** has been extended to properties and indexers, allowing their declarations to be split across multiple partial class definitions.

```C#
// In one part of the partial class
public partial class SampleClass
{
public partial string Name { get; set; }
}

// In another part of the partial class
public partial class SampleClass
{
public partial string Name { get; set; } = "Default";
}
```

## Predictions

According to Colin Bundervoet, the future of .NET lies in leveraging **extensions and roles** to drive flexibility and maintainability in application development.

He predicts that extensions will continue to evolve as a way to add functionality to existing types without altering their original design, allowing for more modular and reusable code.

Bundervoet also sees roles as a game-changer, enabling type aliases with constraints and context-specific behaviors that enforce compile-time safety while improving code readability.

He believes these features will align .NET with modern design paradigms like domain-driven design, making it easier to build adaptable, scalable applications. In Bundervoet's view, this focus on extensions and roles cements .NET's position as a versatile and forward-thinking platform.

## Final remarks

In the end, we ended up networking a bit amongst ourselves and with the people at Starfisk. We discussed Bruges, our studies and the Colin Bundervoet's talk extensively. There were free drinks and snacks as well, which kept us there for about half an hour after.

![group picture](/images/starfisk-group.jpg)
