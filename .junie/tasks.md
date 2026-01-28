# Current Status

## Next Steps (Sprint)
- [ ] LunyScriptVariable: replace with a variant type

## Backlog
- ### Unit Testing
  - [ ] add more LunyEngine agnostic tests to define native-engine contracts
  - [ ] Add Scene Load/Unload tests (call order)
  - [ ] Test scene (re-)load and hook up to scene service callbacks, verify against engine behaviour
  - [ ] (maybe) create separate Unity package / Godot addon for ContractTests, then port agnostic tests to use engine mocks of native implementations (problems: Godot has no unit testing, Unity's requires `IEnumerator` `[UnityTest]` tests)  => figure out how to approach this
- ### LunyEngine (Registries, Services)
    - [ ] LunyObjectRegistry: GetByName should use Dictionary, not FirstOrDefault
    - [ ] Scene Service: implement depth-first enumeration with pre-order or post-order (as IEnumerable?)
  - #### Asset Service
      - [ ] Implement Asset/Resource loading by name/path
      - [ ] Return valid "error" objects from Asset service
      - [ ] Addressing: LunyUrl/LunyPath: handles resource path conversion & cleanup ie remove "res://")
- ### LunyScript Design & Lifecycle
    - [ ] ensure deterministic LunyScript execution order (follow scene hierarchy order?)
    - [ ] call "OnReady" for children first (depth-first, post-order - like Godot)
    - [ ] test LunyScript running on global object (autoload, DDOL) - should still run after scene (re)load
    - [ ] Sandboxed script execution (Limit access to objects, assets, API)
    - [ ] Handle LunyObject parenting with hierarchy gaps
    - [ ] Review OnIntervalUpdate implementation in script Scheduler and object event handler
    - [ ] [[LunyScript Hot Reload]] with manual triggers
    - [ ] How to pass references to blocks via event parameters (eg Scene, "Other" from colliders, etc) => Design
    - [ ] consider LunyScript.Every.* (updates) running unconditionally / globally (not tied to object - but then: context?)
    - [ ] LunyScript.Method.Run => could use overloads for When/Every BUT I don't want to make it "too easy" to inject lambdas
    - [ ] [[Lua Integration]]
    - [X] Setup LunyLua and LunyLua-Test with Lua.dll reference
    - [ ] Consider: Case insensitive and partial name matching for object-script activator (controlled by LunyScript flags), configurable: starts with/contains/etc
- ### LunyScript Variables
    - [ ] Variable validation (log read access of non-existing variables)
    - [ ] Metadata for global variable read/write tracking
- ### LunyScript Blocks & API
    - [ ] [[Conditional Blocks]] (if/else)
    - [ ] [[Composite Blocks]] (loops, timers, coroutines)
    - [ ] [[Event Handling Blocks]] foundation (Input, Collision, SendMessage)
    - [ ] [[Variable Blocks]]
    - [ ] Create ReloadScene block
    - [ ] Implement Random/Shuffle blocks and API
- ### Diagnostics & Infrastructure
    - ..
- ### Engine Specific
    - Unity: Add `[IgnoredByDeepProfiler]` attribute to debug methods

## Epics
- **Reflective/Generated API**: Lua API generator needed; maybe C# reflected/generated engine bindings? (if it speeds up adding features)
- **Repository Structure**: LunyEngine as separate package from LunyScript
- **Distribution**: versioning of LunyEngine for multiple frameworks? Lightweight package manager?
- **Hot Reload**: Support for both C# and Lua
- **Sandboxed Script Execution**: API filters (Lua blacklist/whitelist, C# custom sandbox service)
- **On-Screen Diagnostics**: Display design and required services
- **Cross-Engine Editor Tooling**: Custom importers, build scripts, editor windows/settings
- **Developer SDK Documentation**: Observer patterns, Service API extension, engine support guide, behavioral contracts
- **Portable Scene Format**: Design in Godot, import in Unity (portable asset types)
- **Ingame Console**: Run blocks/runnables at runtime via console

## DONE

### CW05-2026
- [X] Godot: SceneTree should inherit from MainLoop, with GetMainLoop() returning MainLoop just like Godot
- [X] Godot: Node class' Notification const must be 'long' just like Godot
- [X] Godot: Name property must be of type 'StringName'
- [X] Godot: ensure classes that are require to be 'partial' in Godot have the 'partial' keyword. Add an "empty" partial stub just so the 'partial' keyword sticks when running "code cleanup" (which removes keywords and usings it determines to be superfluous)
- [X] LunyScriptVariables: renamed to LunyTable
- [X] LunyScriptVariable implementation changes:
    - [X] Rename class to `LunyVariable`, add `ILunyVariable` interface
    - [X] Memory footprint optimization: `Name` returns "(N/A)" in non-debug builds
    - [X] Private constructor, `Create` static methods, updated signature (value first)
- [X] `LunyNumber` struct: wraps a `System.Double` type
    - [X] complete implicit conversion to any other type from byte to long and float and bool ("loss of precision" casts are acceptable)
    - [X] cast to bool: first cast to long, if result is 0 it's 'false', otherwise 'true'
    - [X] add arithmetic operators for bool and string that throw an exception (overrule implicit conversions)

### CW04-2026
- [X] Contract Tests now contain LunyScript tests which should not be there => separate contract from implementation tests
- [X] Move LunyEngine tests from Luny-ContractTest to Luny-Test
- [X] *BridgeTest: should they inherit from ContractTestBase? (YES)
- [X] Remove LunyTestableAttribute (unused, we now have tests in separate projects)
- [X] Check if we can make the native engine projects build by providing Mocks for native APIs (enables engine-wide refactoring!)
- [X] LunyServiceRegistry: refactor engine check, remove adapter and replace with global "engine name" property provided by adapter
- [X] refactor existing *-Test tests:
    - [X] make tests use contract test infrastructure
    - [X] make all tests run once with each engine adapter, without duplicating the test code
    - [X] where it makes sense, move tests to Luny-ContractTest
- [X] GetAllObjects(): change to only convert to LunyObject if scripted
- [X] LunyObject: return cached instance before creating new one
- [X] Implement FindByName (with proxy fallback) for Object.Create that should run a script (consider prebuilt scripts)
- [X] Implement Every.TimeInterval block
- [X] LunyScript.When.Self (updates) should not run while disabled
- [X] Create object via API and register (activate script)
- [X] Get and destroy registered object via API
