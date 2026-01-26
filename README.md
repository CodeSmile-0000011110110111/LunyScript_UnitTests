# LunyScript_UnitTests

Development project for LunyEngine and LunyScript. 
Defines engine contracts and uses TDD approach to verify engine behaviour.

Engine mocks/shims are used to emulate engine API and behaviour. 
These enable fast and reliable feature development, unit testing, 
and refactoring across multiple engines all at once!

The switch between engine mocks/shims and actual engine APIs is a zero-friction setup,
as types are implicitly switched (no conditional compilation).
