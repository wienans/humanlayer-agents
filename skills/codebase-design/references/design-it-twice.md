# Design It Twice

Use isolated parallel workers to avoid anchoring on the first interface.

## Process

1. State the behavior, constraints, dependencies, domain vocabulary, and candidate seam without proposing an interface.
2. Dispatch at least three workers with the same facts and different constraints:
   - minimize the interface to maximize leverage;
   - maximize extension flexibility;
   - optimize the common caller;
   - when relevant, optimize around ports and adapters.
3. Require each worker to return:
   - the complete interface, including invariants and errors;
   - a caller example;
   - behavior hidden behind the seam;
   - dependency and adapter strategy;
   - testing surface;
   - trade-offs.
4. Present each design independently, then compare depth, locality, seam placement, and caller burden.
5. Recommend one design or an explicit hybrid and wait for the human's choice.

Workers design; they do not edit code, approve intent, or modify Domain Documentation.
