# Deepening Modules

Classify dependencies before placing seams.

## Dependency Shapes

1. **In-process**: pure computation or in-memory state. Merge behind the module interface and test it directly; no adapter is needed.
2. **Local-substitutable**: infrastructure with a faithful local stand-in, such as an in-memory filesystem or local database. Keep the seam internal and test the module with the stand-in.
3. **Remote but owned**: another owned service. Define a port at the network seam, with a production transport adapter and an in-memory test adapter.
4. **External**: an unowned third-party system. Inject an operation-specific port and supply a controlled mock adapter in tests.

## Replace, Do Not Layer

Test observable behavior through the deepened module's interface. Once those tests cover the behavior, remove shallow tests that duplicate internal structure. A test should survive an implementation rewrite behind the same interface.

One adapter makes a hypothetical seam. Two justified adapters make a real seam. Do not expose an internal seam merely because tests use it.
