# spraypixel/skills

SPRAYPIXEL.AI plugin marketplace for Claude Code. Five composition skills for producing single-file HTML artifacts — from production-grade dashboards under design-system discipline to throwaway editors you make once and discard.

## Install

```
/plugin marketplace add spraypixel/skills
```

Then install individual plugins:

```
/plugin install component-composer@spraypixel
/plugin install spraypixel@spraypixel              # the Tufte-quiet theme
/plugin install spraypixel-terminal@spraypixel     # the terminal theme
/plugin install html-sketch@spraypixel             # casual one-off HTML
```

`component-composer` depends on `generator-critic`, which installs as a dependency.

## Plugins

| Plugin | What | Use when |
|---|---|---|
| [`generator-critic`](skills/generator-critic) | Abstract refinement-loop primitive. Drafter LLM proposes, hybrid critic scores, loop until pass. Artifact-agnostic. | Building a new `<thing>-composer` skill that needs the loop machinery. |
| [`component-composer`](skills/component-composer) | Production-grade HTML data graphics via the loop. Consumes generator-critic, adds HTML-specific output style, theme spec, mechanical DOM checks. | Recurring dashboards, multi-theme reports, design-system-enforced artifacts. |
| [`spraypixel`](skills/spraypixel) | Tufte-quiet theme for the composer. Light + dark + system modes. DM Sans + JetBrains Mono + Georgia. | Editorial / analytical data graphics. |
| [`spraypixel-terminal`](skills/spraypixel-terminal) | Terminal-aesthetic theme. Dark-only, all JetBrains Mono caps, ASCII bars, sharp borders. | Dashboards that should read like a Bloomberg terminal. |
| [`html-sketch`](skills/html-sketch) | Casual one-off HTML — throwaway editors, side-by-side variants, interactive tuners, single-page reports. Includes copy-as-prompt footer. | One-shot artifacts; situations where the composer's validator loop is overkill. |

## Architecture

```
generator-critic        ← abstract loop (drafter, critic, HUD, audit summary)
       ▲
       │ consumes
       │
component-composer      ← HTML specialization (output-style, theme spec, DOM checks)
       ▲
       │ themed by
       ├── spraypixel               ← Tufte-quiet design tokens + criteria
       └── spraypixel-terminal      ← Terminal-aesthetic tokens + criteria

html-sketch             ← separate skill, no loop, casual patterns
```

`generator-critic` is artifact-agnostic — any future `<thing>-composer` (markdown, code, schemas, prose) can consume it the same way `component-composer` does.

## Heritage

Extracted from [`infolog-io/skills`](https://github.com/infolog-io/skills) in 2026-05. The five skills here previously lived in that marketplace; spinning off into SPRAYPIXEL.AI gives the composition family its own identity and independent release cycle. The `infolog-io/skills` marketplace continues to ship process and engineering skills (PIP, JTBD, sizing, semantic organization, GitHub kanban, goal execution).

## Acknowledgements

`html-sketch` encodes patterns documented by Thariq Shihipar in [The Unreasonable Effectiveness of HTML](https://www.anthropic.com/engineering/claude-code-html). The composer's style anchor is [`ThariqS/html-effectiveness`](https://github.com/ThariqS/html-effectiveness).
