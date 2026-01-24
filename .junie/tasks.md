# Current Status

## Next Steps (Sprint)
- [ ] Gather info about scene unload event handling across engines (timing, reliability, additive vs whole)
- [ ] GetAllObjects() optimization: only convert to LunyObject if scripted
- [ ] Implement GetSingleObject with proxy fallback
- [ ] Test scene (re-)load and hook up to scene service callbacks
- [ ] Create ReloadScene block
- [ ] Implement Every.TimeInterval block
- [ ] "GetInstance()" awaitable to handle ctor/ready timing scenario

## Backlog
- ### Design & Lifecycle
    - [ ] Sandboxed script execution (Limit access to objects, assets, API)
    - [ ] Register/create/enable API methods for regular code
    - [ ] Create object via API and register (activate script)
    - [ ] Get and destroy registered object via API
    - [ ] Update methods should not run when object is disabled in hierarchy
    - [ ] Handle LunyObject parenting with hierarchy gaps
- ### Blocks & Features
    - [ ] [[Conditional Blocks]] (if/else)
    - [ ] [[Composite Blocks]] (loops, timers, coroutines)
    - [ ] [[LunyScript Hot Reload]] with manual triggers
    - [ ] [[Event Handling Blocks]] foundation (Input, Collision, SendMessage)
    - [ ] [[Variable Blocks]]
    - [ ] Variables refactor to `Vars.Global[]` / `Vars.G[]`
    - [ ] Pass scene name to blocks via event parameters
- ### Diagnostics & Infrastructure
    - [ ] [[Diagnostics]] Profiling Hooks for scripts and runnables
    - [ ] Internal verbose logging with categories/levels
    - [ ] [[Testing Infrastructure]]
    - [ ] [[Resource Addressing]] (LunyUrl)
    - [ ] [[Lua Integration]]
- ### Improvements & Engine Specific
    - [ ] Return valid "error" objects from Asset service
    - [ ] Unity: Add `[IgnoredByDeepProfiler]` attribute
    - [ ] Case insensitive activator object-script name matching
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
