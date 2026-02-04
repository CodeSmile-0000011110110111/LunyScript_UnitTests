# Current Status

## Next Steps (Sprint)
- [X] Rename example engine project repos to "LunyScript_*"
- [X] LunyScript: refactor Api classes to their own files (namespace: LunyScript.Api.DebugApi)
- [X] table.NotifyVariableChanged => move into table ?
- [X] Refactor Table OnValueChanged => move responsibility into VarHandle
- [X] rename: ArithmaticOperationBlockBase (AddVariableBlock); ComparisonBlockBase (IsGreaterVariableBlock)
- [X] VariableConditionBlock: refactor to individual classes
- [X] Variable API: refactor from Var.Add("name", ..) => Var("name").Add/Is(..)
- [ ] Variables: complex operations fail => `hp.Sub((hp + 10) / 2)` 
- [X] Variables: support `Var("..") > 50` etc
- [ ] Testcase: Write prefab spawner script with new flow constructs and inline variables
- [ ] Primitives: should have a "WithPhysics()" setting that properly sets up the thing to work physically (Unity: adds Rigidbody, Godot: do the 20 things to make it a working physics object)
- [ ] Test scene (un-)(re-)load and hook up to scene service callbacks, verify against engine call order (get this first)

- .. Improve execution speed of git pull/commit script (parallelize? rewrite to non-generic version for better control?)
- .. Consider: auto-pull per solution, so i only need to switch autopull in the solution i don't work in (even automate the switch?? cautions?)
- .. Consider: a proper C# tool instead of 'bush' script?
- .. Consider: a way for me to very quickly get an overview of what's changed, and view the diffs, and perhaps even comment on them (code review tool?)
		i could then try the document-driven planning protocol for AI that jetbrains blog recommends -> actual commit docs, be instructional


## Backlog
- ### Refactor
  - Consider: LunyEngine explicit Interface Implementations to "hide" Developer SDK methods from public API (beginner-level users) while allowing developers to utilize the SDK features without having to use InternalsVisibleTo. Alternatively: a DeveloperApi, similar to how LunyScript implements its fluent Api.
  - [ ] LunyEngine: consider the registries as service providers - don't pass their references around, instead pass the data, or maybe relay calls via LunyEngine
  - [ ] LunyObjectRegistry: GetByName should use Dictionary, not FirstOrDefault
  - [ ] Check if LunyScript.GlobalVars/LocalVars can be replaced by Var and GVar APIs
  - [ ] consider renaming LunyLogger to just Logger for brevity (good idea??)
- ### Engine Mocks
    - [ ] ..
- ### LunyEngine
    - [ ] Table: allow nested Tables with path-based indexing (dot and/or slash, or multiple indexers: t["1st"]["2nd"])
    - [ ] Scene Service: implement depth-first enumeration with pre-order or post-order (as IEnumerable?)
- ### LunyScript Design & Lifecycle
    - [ ] ensure deterministic LunyScript execution order (follow scene hierarchy order?)
    - [ ] Handle LunyObject parenting with hierarchy gaps
    - [ ] Review OnIntervalUpdate implementation in script Scheduler and object event handler
    - [ ] How to pass references to blocks via event parameters (eg Scene, "Other" from colliders, etc) => Design
- ### LunyScript Debug / Profile
    - [ ] Variable validation (log read access of non-existing variables)
    - [ ] Metadata for global variable read/write tracking
- ### LunyScript Blocks & API
    - For parameterless calls we may even use a property returning a corresponding block to omit unnecessary ():
      var block = If(Self.IsEnabled).Then(..);
    - [ ] [[Timer Blocks]]
    - [ ] [[Event Handling Blocks]] foundation (Input, Collision, SendMessage)
    - [ ] Create Scene load blocks
    - [ ] Implement Random/Shuffle blocks and API
    - [ ] Roslyn Generator to inject extension interface properties (base interface: ILunyScriptApi, property: )
      - Should be a incremental generator, using [LunyScriptExtension] and [LunyScriptApi] attributes
      - separate project, compiled to DLL, DLL for both engines
      - Godot generator is installed by modifying .csproj (sticky, ie via plugin.gd)
      - Analyzer message if class isn't partial, but only if it implements a ILunyScriptApi interface
      - `public interface IExtension { ExtensionApi Extension => new(); } // user defined` 
      - `public ExtensionApi Extension => ((IExtensionApi)this).Extension; // injected property`
- ### Engine Specific
  - ..
- ### LATER (minor)
  - [ ] consider LunyScript.Every.* (updates) running unconditionally / globally (not tied to object - but then: context?)
  - [ ] LunyScript.Method.Run => could use overloads for When/Every BUT I don't want to make it "too easy" to inject lambdas
  - [ ] Consider: Case insensitive and partial name matching for object-script activator (controlled by LunyScript flags), configurable: starts with/contains/etc
  - [ ] Unity: Add `[IgnoredByDeepProfiler]` attribute to debug methods
- ### EPICS (needs design)
  - LunyScript running on global object (autoload, DDOL) - should still run after scene (re)load
  - [[Lua Integration]] of scripting API
  - **Repository Structure**: LunyEngine as separate package/addon from LunyScript?
  - **Distribution**: versioning of LunyEngine for multiple frameworks? Lightweight package manager?
  - **Hot Reload**: Support for both C# and Lua, manual triggers for testing
  - **Sandboxed Script Execution**: API filter (Lua: blacklist/whitelist, C#: custom sandbox service), object/asset filters
  - **On-Screen Diagnostics**: Display design and required services
  - **Developer SDK Documentation**: Observer patterns, Service API extension, engine support guide, behavioral contracts
  - **Ingame Console**: Run blocks/runnables at runtime via console
  - (maybe) create separate Unity package / Godot addon for in-engine ContractTest verification => figure out how to approach this
- ### Ideas "Outside Project Scope" ...
  - **Cross-Engine Editor Tooling**: Custom importers, build scripts, editor windows/settings
  - **Portable Scene Format**: Design in Godot, import in Unity, and vice versa (portable asset types)
  - Luny could have a 1-click solution to setting up a git repository for source control. and instructions how to put it in the cloud (github, aws, .. whatever is easy/popular)

## DONE

### CW06-2026
- [X] GDSharp: GDScript wrapper following C# guidelines => https://github.com/CodeSmile-0000011110110111/GDSharp
- [X] add LunyScript-Analyzers (Roslyn), always builds release, copies DLL to LunyScript/Analyzers, plugin.gd updates Godot .csproj, and tested working callbacks in Godot + Unity (stub only, no function)

### CW05-2026
- [X] Godot: SceneTree should inherit from MainLoop, with GetMainLoop() returning MainLoop just like Godot
- [X] Godot: Node class' Notification const must be 'long' just like Godot
- [X] Godot: Name property must be of type 'StringName'
- [X] Godot: ensure classes that are require to be 'partial' in Godot have the 'partial' keyword. Add an "empty" partial stub just so the 'partial' keyword sticks when running "code cleanup" (which removes keywords and usings it determines to be superfluous)
- [X] Setup LunyLua and LunyLua-Test with Lua.dll reference
- [X] LunyScriptVariables: renamed to LunyTable
- [X] LunyScriptVariable implementation changes:
    - [X] Rename class to `LunyVariable`, add `ILunyVariable` interface
    - [X] Memory footprint optimization: `Name` returns "(N/A)" in non-debug builds
    - [X] Private constructor, `Create` static methods, updated signature (value first)
- [X] `LunyNumber` struct: wraps a `System.Double` type
    - [X] complete implicit conversion to any other type from byte to long and float and bool ("loss of precision" casts are acceptable)
    - [X] cast to bool: first cast to long, if result is 0 it's 'false', otherwise 'true'
    - [X] add arithmetic operators for bool and string that throw an exception (overrule implicit conversions)
- [X] Variable: refactor to variant type
- [X] Add remaining tests for Table class
- [X] LunyScript: refactor the s_Instance away by changing static subclasses to static struct and assign the instance in Initialize
- [X] [[Conditional Blocks]] (if/else, while, AND/OR/NOT)
- [X] [[Variable Blocks]]
- #### Asset Service ✓
    - [X] Implement Asset/Resource loading by name/path ✓
    - [X] Addressing: LunyUrl/LunyPath: handles resource path conversion & cleanup ie remove "res://") ✓
    - [X] we also need an `AssetID` for LunyEngine internal addressing (indexing) of assets/resources, and mapping to engine-native addressing (ID, GUID, Path) ✓
    - [X] Return valid "error" objects from Asset service ✓
    - [X] Implement loading of "prefabs" (Godot: packedscene, or just any scene?) ✓

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
