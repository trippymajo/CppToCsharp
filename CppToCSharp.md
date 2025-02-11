# Basic Types related
> [!IMPORTANT]
> string, short, int, long ... - are just keywords. Which forces to use .NET types like `using System`  

* `var x` - sometheing like auto `auto x = 32`. Compile time check. No casting required.
* `object x` - like void* `void* obj = &example`. Compile time check. Casting needed.
* `dynamic x` - Try avoid it. It is like void*. Runtime check. Dynamic programming, APIs. Pretty slow.
* `System.Convert` - everything from basic type could be converted to other basic types.
## Strings
> [!IMPORTANT]
> Strings are immutable. And each time you do some concat, +, and etc. operations, at first it uses buffer polling (2-3 optimized operations), but when more - it starts to allocate new memory, mening drop in speed. So it is better to use `StringBuilder`.  

* `@"text"` - Verbatim strings, raw string just text without escape sequence.
* `$$"text with {{x}}` - Interpolated, $$ means how many {{ should be for variable.

> [!TIP]
> For searching: `Contains` or `IndexOf` - single search, `SearchValues<T>` - multiple search, `Regex` - complex search

## Floating points
They have got IsInfinity and etc. So its possible to use it with higher math's uncertainties.
* `decimal z` - introduced, 16 bytes represents as int. Not working with higher math calculations like dividing by zero and etc. Higher precision but slower than `float` and `double`.
* `System.Half` - 2-byte type. Alternative for float and double. Some architectures lack native 16-bit floating-point support (.NET 5). 
## Int
* `nint, nuint` - Native-sized integers for platform specific dev. Pointers to integer value in memory. Its all about 32/64 bit.
* `System.Numerics.BigInteger` - Integer for realy large numbers, which using dynamic memory meaning it almost has no ranges (limits).
* `System.Numerics.Complex` - 16 bytes integer for complex math can be represented as `a + bi`, where a and b - real numbers, i - imaginary unit.
* `System.Numerics.Quaternion` - 16 bytes for smooth 3D rotation. Can do only multiplications `*`.
## Array
* `string[,] grid` - Two (or more) dimensinal array like `new int[5][4]`.
* `string [][] jag` - Its like put in array another array. Like a `int[3] = new int[5]`.
* Pattern matchings - like [], [..] and etc (C# 11).
* `Tensor<T>` - Multidimensional arrays for AI workaround (.NET 9).

# Memory
## new
Could be used with type or without - `Person pers = new()` and `Person pers = new Person();` Both right. Any thing else works familiar to C++.

## IDisposable
Implementing the IDisposable interface helps prevent memory leaks by ensuring that unmanaged resources are properly released. To enable automatic cleanup, a class should implement the Dispose() method, where it releases resources such as file handles, database connections, or unmanaged memory allocations.  
In C++, we achieve similar behavior using destructors (delete in ~ClassName()) or smart pointers (std::unique_ptr, std::shared_ptr) for RAII (Resource Acquisition Is Initialization).  
After that you can use your class like:
```cs
using (var cls = new MyClass())
{
    // Some code with
}  // Dispose() is called automaticly
```

# Attributes
## [Flag]
Before enum will make it like an ordinal enum from C++. Use it for bitwise operations. Better to use enums with byte like: `public enum Vals : byte` and with each val go through the byte range 0 to 128 (256 not included). 

# Operators
* `nameof()` - returns name of a var.
* `var? x` - signaling that x - a nullable type and need to handle null exceptions on ur own. Check if the object is not null `Shout?.Invoke(this, EventArgs.Empty)`
* `x ?? 30` or `x ??= 30` - Null-coalescing. Means if input null accept as value following.
* `Person man!!` - Checks whether value is null and if so, thorws exception. Same as `ArgumentNullException.ThrowIfNull(man)`
* `name!.Length` - Null forgiving. Means no more warnings about nullable varibale.

# Keywords
## Pre-Code
* `using static System.Console` - like `using namespace std`.
## Functions && Params
* `x is int i` - Check if x is int then assign to variable i.
* `x = z switch { z == 4 => doSmth() }` - Switch without using break and case. Also `_` - default statemet. C++ switch could be used too (C# 8).
* `foreach(var z in variables)` - range loop, like `for(const auto& z : varibales)`. IEnumerable need to be omplemented for the used type.
* `in` and `out` - `in` in C++ is `(const int value)` and C# dont support const in params, `out` - reuired output param in C++ is `(int &val)` , but not required.
## Exceptions
* `checked {}` - Causing runtime exceptions related to overflow to be thrown. `unchecked {}` - opposive, disable compile time checks.
## Access modificators
* `public` - YEAH, its a bit different. Here it is like dllexported public function in C++.
* `internal` - Public within same assembly. It is just public function not accesible using LoadLibrary. Classic public.
* `private` - Only same class within same assembly.
* `protected` - Same class and the derived classes from other assemblies.
* `protected internal` - Ist like protected + internal, Class + Derived for other assemblies, but not other classes in other asseblies
* `file` - type could be used within its .cs file. Use it when there are multiple classes in .cs and you need them to wrok all with each other (.NET 7).
* `sealed` - sealed restrict other clases to derive from this class. Or can be used with methods, which prevents further overriding from your class.
## Class related
* `record Data` - immutable value based (not ref) structure. Used for Data modeling. Basicly its a struct with const params with only initializing. Supports equlity checks with `==`. Could be mutable with `get; set;`
* `struct Data` - mutable value based (not ref). Used for Data modeling.
* `abstract class Program` - a class with some pure virtual functions mixed with concrete implementations.
* `interface IProg` - is a abstract class with only pure virtual functions inside. All members are public. Serialization not working.
* `partial class Program` - just like header files, but function are inlined in it.
* `Employee emp = person as Employee` - as just another casting, but reutrn reference type and null, without throwing exception if the converting is not possible. Note that C-style casting `(Employee)person` throws an exception if no completed.
## Field related
* `required` - must have params of the class when initialising. In C++ its basicly constructors' work (C# 11).
* `get; set;` - Getters and setters. Also can be used with lambdas. Also could be `init` means only one setting works great with `record`(C# 9).
* `public Preson this[int index]` - Indexers, use in a pair with get and set. In C++ using with overloading `[]` operator.

# Collections (Data Structures)
Two types. `System.Collections` -> not type-safe annd less efficient; `System.Collections.Generic` -> type-safe and efficient

## List
`List<T>`
Data Structure: Array
C++: std::vector

## Dictionary
`Dictionary<TKey, TValue>`
Data Structure: Hashmap
C++: std::unordered_map

## Set 
`HashSet<T>`
Data Structure: Hashmap
C++: std::unordered_set

## Stack
`Stack<T>`
Data Structure: Stack (LIFO)
C++: std::stack

## Queue
`Queue<T>`
Data Structure: Queue (FIFO)
C++: std::stack

# Features
## Less {} for using and namspace (C# 10)
You allowed not to put all the code in brackets for `using` and `namespace`.

### Tuples
`public (string Name, int Number) doSmth(){}` - like a std::tuple but syntax is different.

## Pattern Mathcing (C# 8)
Allows to feed the pattern in order to get what you want to find in value or class. In classes used with keyword `when` and switch statements like:
```cs
foreach (Passenger passenger in passengers)
{
  int out = passenger switch
  {
    FirstClassPass p when p.AirMiles > 35000 => 140, // C# 8
    ...
    // Or C# 9:
    FirstClassPass p => p.AirMiles switch
    {
      > 35000 => 140
      ...
    }
    ...
  }
}
```

## Generics (C# 2)
Generics allow to pass any type to class, method and interface. Common use with `System.Collections.Generic` data structures.
Generics do compile time checks for types increasing the type safety, thats why they should be prefered over non-generic `System.Collections`.In C# It allows to work and use collections which are pretty similiar to STL. All these stuff is like stl, mfc types. Basicaly it is templates. 
```cs
public class GenericContainer<T>
{
    private T item;

    public void Add(T newItem)
    {
        item = newItem;
    }

    public T Get()
    {
        return item;
    }
}
```

## Delegates
Delegates is a type-safe method pointer. In C++ it is just `void (*funcPtr)(string)`. Event in C# build on top of the delegates. Got built-in support for async. **Note:**  Events built on top of delegates and are used to define a publisher-subscriber relationship. Events can only be invoked by the class that declares them. While <ins>delegates can directly invoke the methods they reference.</ins>
Predefined delegates: `public delegate void EventHandler(object? sender, EventArgs e)`
```cs
public delegate void MyDelegate(string message);

public static void PrintMessage(string message)
{
    Console.WriteLine($"Message: {message}");
}

MyDelegate del = PrintMessage;
del("Hello, Delegates!"); // Output: Message: Hello, Delegates!
```
Also, delegates are multicast, meaning you can assign as many functions to it as you want.
```cs
public static void PrintMessage1(string message) => Console.WriteLine($"Message 1: {message}");
public static void PrintMessage2(string message) => Console.WriteLine($"Message 2: {message}");

MyDelegate del = PrintMessage1;
del += PrintMessage2; // Add another method

del("Hello!"); // Calls both PrintMessage1 and PrintMessage2

del -= PrintMessage1; // Remove a method
del("Hi!"); // Calls only PrintMessage2
```

# C# code style
## Method chaining/Fluent style
Multiple method calls are chained together in a single statement.
```cs
public class Person
{
    public string Name { get; set; }
    public string Age { get; set; }
    
    public Person SetName (string name)
    {
        Name = name;
        return this;
    }

    public Person SetAge(int age)
    {
        Age = age;
        return this;
    }
}
```
Usage:
```cs
Person person = new()
    .SetName("Joe Peach")
    .SetAge(38);
```

## Extension methods
It is a compiler trick (huh?) works as free functions in C++, free from class functions. In C# this works with decaring static public class with public static methods with `this` in parameters. In C# it looks like:
```cs
public static class StringExtensions
{
    public static bool IsPalindrome(this string str)
    {
        if (string.IsNullOrWhiteSpace(str)) return false;

        var reversed = new string(str.Reverse().ToArray());
        return string.Equals(str, reversed, StringComparison.OrdinalIgnoreCase);
    }
} 
```
Using:
```cs
string word = "Racecar";
bool result = word.IsPalindrome(); // True
```

# Compilation
## Just-In-Time (JIT)
By default, C# code is compiled at runtime using JIT (Just-In-Time) compilation. This means that the .NET runtime compiles IL (Intermediate Language) into native machine code just before execution. While this allows for cross-platform compatibility and optimizations at runtime, it results in slower startup times compared to fully compiled applications.
## Ahead of Time (AOT)
AOT compilation precompiles the application into native machine code before execution, similar to how C++ compilers work. Faster startup time, better performance but larger output files. Also there are some limitations:
* No Reflection-based Features – Many reflection-based APIs (System.Reflection, dynamic) may not work.
* No Dynamic Assembly Loading
* Requires Trimming – To reduce file size, AOT requires trimming (PublishTrimmed=true), which removes unused code.