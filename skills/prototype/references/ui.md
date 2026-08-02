# UI Prototype

Create three structurally different variants by default and no more than five. Variants must disagree about layout, information hierarchy, or primary affordance rather than only color or copy.

## Placement

Prefer an existing route so variants experience real navigation, density, data, and surrounding chrome. Switch only its rendered subtree with a `?variant=` search parameter. Use a clearly named throwaway route only when no plausible host exists.

## Switcher

Add one high-contrast floating bar that:

- displays the current variant;
- cycles backward and forward with wrapping;
- updates `?variant=` through the project's router so URLs are shareable;
- supports left/right arrow keys except while an input, textarea, or editable element is focused;
- is excluded from production builds.

Use the project's existing components and styling system, but keep variant layouts independent enough to explore genuinely different directions. Stub mutations; this prototype answers a visual or interaction question, not whether the backend works.

After the human chooses, record the winning variant and rationale as Evidence. Remove the switcher and losing variants from production work; keep the complete comparison only on the throwaway branch.
