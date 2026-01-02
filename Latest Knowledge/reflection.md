[source](https://www.bytehide.com/blog/reflection-csharp)
## C# What is Reflection?
* Reflection is a powerful feature in .NET that enables you to analyze, inspect, and interact with the metadata of types, objects, and assemblies during runtime. 
* In simpler terms, it allows your program to “think” and gain insights about itself or other types, properties, methods, etc., _dynamically_.
## The Purpose and Benefits of Using C# Reflection

Reflection plays a vital role in scenarios where you want to:

- Inspect the structure and metadata of types and assemblies at runtime.
- Load an assembly without referencing or compile-time dependencies.
- Create instances of objects and invoke methods or instantiate types dynamically.
- Implement runtime code generation, serialization, or design patterns based on interfaces, attributes or naming conventions.
## C# Reflection Key Components

1. **Assemblies**: Executable modules (usually with `.dll` or `.exe` extensions) containing compiled code, resources, and metadata.
2. **Types**: Classes, interfaces, enums, structures, and delegates that hold metadata and can be used to generate objects or interact with members.
3. **Members**: Properties, fields, methods, events, and constructors associated with a Type.
## Writing code at runtime
—also known as dynamic code generation or metaprogramming—means ==creating, compiling, and executing code while the application is already running, rather than before it starts==.