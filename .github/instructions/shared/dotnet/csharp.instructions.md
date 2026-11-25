---
applyTo: "**/*.cs"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# C# code

## Build constraints

- `TreatWarningsAsErrors`, `Nullable`, `EnforceCodeStyleInBuild`, and the .NET analyzers are all enabled in `Directory.Build.props`, so any analyzer or style warning fails the build. Handle nullability explicitly.

## General

- `.editorconfig` is authoritative for formatting, indentation, brace style, and naming. Where no rule is explicit, follow the style of nearby files.
- These rules win over existing code. Existing code may not follow them; convert it only in lines you change anyway, and reorder a file's members only when you rework most of it.
- Use file-scoped namespaces.
- Prefer immutable design where practical: `readonly` fields, init-only properties, or constructor initialization.
- Use expressive type and member names, and avoid abbreviations unless they are established terms. Private and protected instance fields use `_camelCase`; constants and static readonly fields use `UPPER_SNAKE_CASE`.
- Use the same term for the same concept in names, XML docs, and messages. Method names start with a verb that says what they return: `Get…` returns a value, `Try…` returns a `bool` with an `out` parameter, and `Create…` builds a new object. Other `bool` methods and properties read as a statement that is true or false, with the prefix that fits its meaning, such as `Is…` for a state, `Can…` for an ability, `Has…` for possession, `Should…` for a recommendation, or `Show…` for visibility (for example `IsExpired`, `CanRetry`, or `HasDiscount`). Async methods end in `Async`.
- Keep methods small and focused. Put reusable code in extension classes (`XxxExtensions`) or in classes named after what they are or do, not vague `XxxHelper` or `XxxUtils` names: `OrderTotal`, `RetryPolicy`. Classes that call a web API end in `Client` (`WeatherClient`). Don't repeat the class name in its methods (`Invoice.SaveAsync`, not `SaveInvoiceAsync`).
- Extract a method when its name says more than its code, when it keeps the caller at one level of detail (see Member order), or when it holds logic worth testing without I/O; being used only once is no reason to inline it. Inline it when the expression is as clear as any name, or when the method would only forward or rename.
- Put a method on the type whose data it uses: logic about one item goes on that type (`Order.GetLineTotal` sums its own lines), and logic over a collection that only one class needs stays in that class (`OrderBook.GetLatestOrder`). Use the narrowest access that works, `internal` only so tests can reach it, and widen it only when a second user needs it.
- Replace magic numbers and strings with named constants that say what they mean (for example `MAX_RETRY_COUNT`).

## Structure

- Inside a project, folders map to namespaces.
- Keep enums close to where they are used. An enum used by one class goes at the top of that class's file, as a top-level type (not nested, so its name stays stable). An enum used by several classes gets its own file in their namespace; if they span namespaces, in the namespace it mostly belongs to.
- Split a large class that covers several distinct areas into `partial` files named `<ClassName>.<DistinctArea>.cs` next to `<ClassName>.cs` (for example `OrderBook.Export.cs`). The main file keeps the type's XML documentation, fields, properties, and constructors, plus the private members that all parts share; each part holds the members of one area and follows the member order within itself.

## Types and `var`

- When creating an object, declare the type on the left and use target-typed `new()` on the right, or a collection expression for collections: `Dictionary<string, Order> map = new();`, `List<User> users = [];`.
- Use an explicit type when the right side doesn't make it obvious, for example a method whose return type isn't clear from its name: `decimal totalDiscount = CalculateModifier();`. Reviews on GitHub have no IntelliSense.
- Use `var` for anonymous types and for complex LINQ results such as `IEnumerable<IGrouping<string, Order>>`, and wherever the type is otherwise obvious from the right side (a cast, `as`, or a generic type argument).

## Language features

- The language version is `latest`. Prefer modern language features supported by the target frameworks when they improve readability, such as target-typed `new()` and collection expressions.
- Extension methods use `extension(T source) { ... }` blocks inside a `static class XxxExtensions`:

  ```csharp
  public static class StringExtensions
  {
      extension(string source)
      {
          public bool IsBlank => string.IsNullOrWhiteSpace(source);
      }
  }
  ```

- Prefer collection expressions (`[value]`, `[a, b]`, `[.. items]`) over `new[] { ... }` and collection initializers.
- Use patterns for null checks (`is null`, `is not null`) instead of `== null` and `!= null`, and for comparisons with constants (`x is 0 or 1`, `x is >= 0 and < 10`).
- Keep a single-statement `if` body on the same line: `if (condition) return;`, and likewise for `return value;`, `continue;`, `break;`, and `throw ...;`.
- Don't use digit separators in numeric literals: write `1000000`, not `1_000_000`.

## Member order

- Group members by kind, each group with its section comment, in this order: `// Constants` (constants and static readonly fields), `// Fields`, `// Properties`, `// Events`, `// Constructors`, `// Methods`.
- Within each group, public and protected members come before internal and private ones.
- Methods that belong to a lifecycle come first, in lifecycle order (for example `OnNavigatedTo` first and `Dispose` last). The internal and private methods follow the stepdown rule: each comes after the first method that calls it, in the order they are called. Keep each method at one level of detail: a higher-level method reads as the workflow, and the details live in the methods it calls.
- Don't use non-private mutable fields.

## Comments

- Comment why, not what: constraints, API quirks, and workarounds (for example, why a limit or a header is needed). Don't restate obvious code flow, and remove comments that no longer match the code.
