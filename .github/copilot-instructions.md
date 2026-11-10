# Copilot instructions

## Project overview

This repository is a dependency-free, single-page space quiz. The complete application lives in `index.html`; it contains the document structure, theme-aware CSS, quiz data, and browser-side interaction logic. It is intentionally runnable as a local file, without a server, package manager, build step, or framework.

The UI is organized into:

- A mission-control header with branding, live telemetry, and the light/dark theme toggle.
- A quiz view with the current question, progress bar, score, answer buttons, feedback, and next button.
- A results view that replaces the quiz after question 10 and provides a restart action.
- Decorative presentation layers including the hex-grid background, star field, orbital branding, animated feedback, and confetti.

Quiz state is held in the script's `current`, `score`, and `locked` variables. `renderQuestion()` rebuilds the answer buttons for the current item, `chooseAnswer()` locks and evaluates one answer, `showResults()` switches to the results view, and `restart()` resets the state.

## Build, test, and lint

There are no build, test, lint, or dependency-install commands in this repository. Do not add a toolchain for routine changes.

Run the app by opening `index.html` directly in a browser. For browser-level validation, use the integrated browser with:

```text
file:///C:/GitHub/space-quiz/index.html
```

Manually verify the initial render, theme toggle, keyboard focus order, correct and incorrect answer feedback, score/progress updates, results screen, and restart flow. There is no single-test command; a focused check means exercising the affected interaction in the browser.

## Code and design conventions

- Keep the app self-contained in `index.html`; do not introduce a server, bundler, framework, or external runtime dependency for ordinary feature work.
- Keep quiz content in the `questions` array. Each item uses `emoji`, `question`, `answers`, and zero-based `correct` fields.
- Use the existing `$()` helper and DOM update functions rather than adding a second state-management pattern.
- Preserve the current two-view flow: answer selection locks the choices, then the next button advances or opens results on the final question.
- Preserve native `<button>` controls for answers, theme switching, next, and restart so keyboard access continues to work.
- Keep decorative elements non-interactive and hidden from assistive technology where appropriate (`aria-hidden="true"` and `pointer-events: none` are used for visual-only layers).
- Keep theme colors in the `:root` and `:root.light` custom-property sets. Any new visual treatment should have suitable values for both themes.
- Use the existing `DM Sans` and `Space Grotesk` font pairing, compact space/mission-control visual language, rounded cards, gradients, and low-contrast decorative effects.
- Keep responsive behavior working within the existing narrow-column layout, especially the `max-width: 430px` rules.
- Avoid raising decorative animation intensity or contrast enough to compete with question text and answer controls. Preserve readable text and visible focus behavior.
