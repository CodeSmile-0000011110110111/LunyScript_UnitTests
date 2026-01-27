# Guidelines

## Project Overview
- Unit-testing and implementation project for LunyEngine (cross-engine C# for Unity, Godot, etc.).
- Folder structure:
    - `Luny/`: Engine-agnostic types.
    - `Luny-ContractTest/`: Engine contract verification tests of `*.*-Mock` types that simulate engine behaviour
    - `Luny-Test/`: Tests for `Luny` and `LunyEngine` SDK features.
    - `LunyLua/`: Lua-CSharp framework.
    - `LunyLua-Test/`: Tests for `LunyLua`.
    - `LunyScript/`: Scripting types.
    - `LunyScript-Test/`: Tests for `LunyScript`.
    - `*.Unity` / `*.Godot`: Engine-specific bindings using `*.*-Mock` types (this solution) or engine types (engine projects)
    - `*.Unity-Mock` / `*.Godot-Mock`: Engine mocks/shims simulating native engine API and behaviour (this solution)
- `.junie/plan.md`: specific, step-by-step strategy for the current active task
- `.junie/tasks.md`: high-level roadmap / todo list
- `*.csproj` locations
  - repository root (preferred): required for projects referenced in engine projects (eg Luny, Luny.Godot, Luny.Unity, ..)
  - subfolders: for `*-Test/` projects

## Implementation Preferences
- **Step-by-Step Mode**: Always operate in a strict planning-first mode.
- **Explicit Confirmation**: Do not modify any files or start implementation until the user has explicitly confirmed the plan.
- **No "Running Ahead"**: Wait for confirmation after each major phase (Planning -> Implementation -> Verification).
- **Logging**: Use `LunyLogger` methods: `LogInfo`, `LogWarning`, `LogError`, `LogException`. Do not modify existing `LunyLogger` log strings without permission, prefer to add a new log statement instead.
- **Compatibility**: Code restricted to C# 9 and .NET Standard 2.1 for Unity 6 compatibility.
- `ILunyScriptBlock` implementations are internal and require a static Create() method, ctors are private to enforce use of Create()
- When renaming/adding/removing .csproj files also update the .slnx file
- do not remove or modify LICENSE and README.md files, unless instructed (ask)
- Unit Tests:
  - avoid reflection for calls made during test runs, unless instructed (ask) 
  - do not add methods to reset (static) state, unless instructed (ask)
 
## Code Style
- **Control Flow**:
    - No single-line `if` or `else` statements.
    - No braces around single-line statements (if, else, for, etc.) except for `do/while` and `using`.
- **Expression Syntax**: Properties and methods should be single-line "expression" syntax (`=>`) whenever possible. Use ternary if needed, but avoid nested ternaries.
- **Types and Interfaces**:
    - Prefer using interfaces over concrete types for public APIs.
      - Exception: implementations of `ILunyScriptBlock` 
    - Interfaces for only one type should be in the same file as the implementation, placed above the type.
    - Use `nameof(Type)` or `instance.GetType().Name` instead of hardcoded type strings.
- **Empty Methods**: Should `throw new NotImplementedException("name of type and method")`.
- **NUnit**: Use `Assert.That` instead of classic assertions

## Useful Commands
- **Build Solution**: `dotnet build` (Note: Platform-specific projects like `.Unity` and `.Godot` may not compile and can be ignored or excluded if necessary).
- **Run All Tests**: `dotnet test`
- **Test Core**: `dotnet test Luny-Test\Luny-Test.csproj`
- **Test Scripting**: `dotnet test LunyScript-Test\LunyScript-Test.csproj`
- **Test Lua Integration**: `dotnet test LunyLua-Test\LunyLua-Test.csproj`
