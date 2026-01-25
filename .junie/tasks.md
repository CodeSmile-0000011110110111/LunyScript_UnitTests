# Current Status

## Next Steps (Sprint)
- [ ] Check if we can make the native engine projects build by providing Mocks for native APIs (enables engine-wide refactoring!) 
- [X] GetAllObjects(): change to only convert to LunyObject if scripted
- [X] LunyObject: return cached instance before creating new one
- [ ] Implement GetSingleObject (by name) (with proxy fallback) for Object.Create that should run a script (consider prebuilt scripts)
- [ ] Test scene (re-)load and hook up to scene service callbacks
- [ ] Create ReloadScene block
- [ ] Gather info about scene unload event handling across engines (timing, reliability, additive vs whole)
- [ ] Implement Every.TimeInterval block
- [ ] "GetInstance()" awaitable to handle ctor/ready timing scenario
- [X] LunyScript.When.Self (updates) should not run while disabled
- [X] Create object via API and register (activate script)
- [X] Get and destroy registered object via API

## Backlog
- ### Unit Testing
  - [ ] analyze how agnostic tests could port to engine-native tests (replace mocks with native implementations) 
  - [ ] add more LunyEngine agnostic tests to define native-engine contracts
- ### Assets
  - [ ] Implement Asset/Resource loading by name/path
  - [ ] Return valid "error" objects from Asset service
- ### Design & Lifecycle
    - [ ] call OnReady for children first (depth-first, post-order)
    - [ ] ensure deterministic LunyScript execution order (follow scene hierarchy order?)
    - [ ] test LunyScript running on global object (autoload, DDOL) - should still run after scene (re)load
    - [ ] Sandboxed script execution (Limit access to objects, assets, API)
    - [ ] Register/create/enable API methods for engine-native code
    - [ ] Handle LunyObject parenting with hierarchy gaps
- ### Registries
    - [ ] LunyObjectRegistry: GetByName should use Dictionary, not FirstOrDefault
- ### Services
    - [ ] Scene: implement depth-first enumeration with pre-order or post-order (as IEnumerable?)
- ### LunyScript Blocks & API
    - [ ] [[Conditional Blocks]] (if/else)
    - [ ] [[Composite Blocks]] (loops, timers, coroutines)
    - [ ] [[LunyScript Hot Reload]] with manual triggers
    - [ ] [[Event Handling Blocks]] foundation (Input, Collision, SendMessage)
    - [ ] [[Variable Blocks]]
    - [ ] Variables aliases: `Vars.Global[]` / `Vars.G[]`
    - [ ] Pass scene name to blocks via event parameters
    - [ ] Implement Random/Shuffle blocks and API
    - [ ] LunyScript.Every.* (updates) should run unconditionally and globally (not tied to object - but then: context?)
    - [ ] LunyScript.Method.Run => use When/Every overloads in addition?
- ### Diagnostics & Infrastructure
    - [ ] [[Diagnostics]] Profiling Hooks for scripts and runnables
    - [ ] Internal verbose logging with categories/levels
    - [ ] [[Testing Infrastructure]]
    - [ ] [[Resource Addressing]] (LunyUrl)
    - [ ] [[Lua Integration]]
- ### Improvements & Engine Specific
    - [ ] Unity: Add `[IgnoredByDeepProfiler]` attribute to debug methods
    - [ ] Case insensitive and partial name matching for object-script activator (controlled by LunyScript flags?)
      - [ ] Configurable name matching (starts with/contains)
    - [ ] Variable validation (log read access of non-existing variables)
    - [ ] Metadata for global variable read/write tracking

## Epics
- **Reflective/Generated API**: Lua API generator or reflective shifts
- **Repository Structure**: LunyEngine as separate package, lightweight package manager
- **Hot Reload**: Support for both C# and Lua
- **Sandboxed Script Execution**: API filters (Lua blacklist/whitelist, C# custom sandbox service)
- **On-Screen Diagnostics**: Display design and required services
- **Cross-Engine Editor Tooling**: Custom importers, build scripts, editor windows/settings
- **Developer SDK Documentation**: Observer patterns, Service API extension, engine support guide, behavioral contracts
- **Portable Scene Format**: Design in Godot, import in Unity (portable asset types)
- **Ingame Console**: Run blocks/runnables at runtime via console
