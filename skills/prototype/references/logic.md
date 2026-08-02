# Logic Prototype

Use one self-contained HTML file that a non-developer can open directly and use to drive the model.

## Process

1. Put the exact design question in a visible introduction.
2. Implement the logic as a pure reducer, explicit state machine, pure function set, or small state-owning module in one script block. It must not depend on the DOM.
3. Wrap it in a thin page with domain-language labels.
4. Render the full relevant state as labeled fields after every action.
5. Provide free-play actions and deterministic guided scenarios. Include the happy path, a difficult edge case, and an illegal action when applicable.
6. Reset each guided scenario to a known initial state.

Use plain HTML, CSS, and JavaScript with no framework, bundler, server, persistence, or tests. The page is disposable. The validated model may inform later production implementation, but prototype code is not production code.
