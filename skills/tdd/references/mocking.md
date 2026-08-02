# Test Doubles

Prefer real in-process collaborators and faithful local stand-ins. Use test doubles only at system seams:

- external APIs;
- remote services;
- time and randomness;
- hardware or operating-system interfaces;
- databases or filesystems when no practical local stand-in exists.

Inject an operation-specific interface rather than a generic transport. A payment dependency should expose `charge`, not arbitrary `fetch`; a clock should expose `now`, not an entire runtime. This keeps fixtures declarative and failures tied to behavior.

Do not mock owned classes or internal modules merely to isolate a function. If a test must script internal call order, move the test to the module's public interface or reconsider the seam.
