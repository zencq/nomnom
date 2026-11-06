---
applyTo: "**/*.cs"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Tests

## Conventions

- Tests use MSTest, in a test project per project under `/tests`.
- Test method names describe behavior, as `Method_Scenario_Expectation`, with `// Arrange / // Act / // Assert` sections; test file and class names mirror the class under test (`Foo.cs` becomes `FooTests.cs`). A class split into partial files still gets one test file (`OrderBook.Export.cs` becomes `OrderBookTests.cs`).
- Don't call real web services. Move request-independent logic into `internal` methods and test them directly.
- Tests run in parallel at method level (`[assembly: Parallelize(Scope = ExecutionScope.MethodLevel)]` in each test project), so they must not share mutable state.
- Each project under test exposes its internals to its test project via `InternalsVisibleTo`.

## Writing tests

- Any behavioral change includes tests. For a regression fix, add or update a test that fails before the fix and passes after it.
- For pending functionality, don't mark new tests with `[Ignore]` or any other skip attribute. Leave them failing to keep the TDD red-green flow in local work. Commits must keep CI green unless the user explicitly asks otherwise.
- In data-driven tests (`[DataRow]`, `[DynamicData]`), keep the rows readable and in a stable order so diffs stay understandable.
- CI runs the tests for every target framework on Windows, macOS, and Linux. Don't depend on path separators, line endings, time zone, or culture.
- Coverage runs on one framework only while the code behaves the same on every target framework. Once code behaves differently per framework, collect coverage per framework and merge the reports.

## Running tests

- Run focused tests for what you touched first (one framework with a filter), then the full suite on all target frameworks. Code with framework fallbacks can pass on one framework and fail on another.
