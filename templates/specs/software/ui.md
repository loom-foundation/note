---
id: <namespace>:spec:<opaque>
name: <Name>
kind: specification
status: draft
authority: []
---

The target screen specifications for <system or scope>, covering component hierarchy, navigation flows, data bindings, layout constraints, and accessibility requirements.

## File Convention

<!-- One MDX file per screen, named in kebab-case, at <scope>/specs/ui/<screen>.mdx. Each screen is a discrete artifact with its own route, access rules, components, and navigation. -->

- Location: `<scope>/specs/ui/<screen-name>.mdx`
- One screen per file; filename matches the screen's primary route segment in kebab-case.

## Screen Frontmatter

<!-- Required YAML frontmatter fields for each screen file. All three fields must be present; missing fields are a specification error. -->

```yaml
route: <url path for this screen>
access: <authentication and permission requirement>
title: <human-readable screen title>
```

## Purpose

<!-- One to three sentences stating what this screen does for its user. Not layout or implementation detail; the user's goal this screen serves. -->

<Screen purpose: what the user accomplishes here.>

## Navigation

<!-- Mermaid flowchart showing inbound and outbound navigation links for this screen. May be omitted only for screens with no inbound or outbound links. -->

```mermaid
flowchart LR
  <ScreenName> --> <OtherScreen>
```

## Components

<!-- JSX expressing the component hierarchy. Each component tag must carry a name prop. Data-bound components carry a ref prop pointing to the relevant entity schema by opaque id. State-driven components carry a state prop pointing to the relevant state machine by opaque id. Do not use readable path-based cross-reference grammar; use angle-bracket placeholders at authoring time. -->

```jsx
<<ScreenName>>
  <<ComponentName> name="<ComponentName>" />
  <<DataBoundComponent> name="<ComponentName>" ref={<entity-schema-id>} />
  <<StateDrivenComponent> name="<ComponentName>" state={<state-machine-id>} />
</<ScreenName>>
```

## Responsive

<!-- One entry per named breakpoint. Breakpoints are named thresholds (e.g., mobile, tablet, desktop); pixel values are a design token concern and do not belong here. State layout changes, not pixel values. -->

| Breakpoint | Layout variation |
|------------|-----------------|
| `<breakpoint name>` | <layout change at this breakpoint> |

## Accessibility

<!-- Required semantic HTML elements, ARIA attributes, and keyboard navigation requirements for this screen. Check completeness against WCAG 2.2 (Level AA minimum) and ARIA Authoring Practices Guide. -->

| Requirement | Detail |
|-------------|--------|
| Semantic element | `<element>` for `<purpose>` |
| ARIA attribute | `<attribute>` on `<component>` |
| Keyboard navigation | `<key or sequence>` performs `<action>` |

## Rationale

<!-- Include only where the design makes a choice the requirement leaves open. One line per non-obvious decision. -->

- <design choice>: <one-line reason>

## Relations

- satisfies: [<Requirement>](../../requirements/system/<requirement>.md){id=<namespace>:req:<opaque>}
