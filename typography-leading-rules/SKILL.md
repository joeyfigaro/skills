---
name: typography-leading-rules
description: Apply consistent line-height rules for body text, subheadings, and titles. Use whenever a user asks to fix typography styling, improve text legibility or readability, make reading more comfortable, or set, correct, or standardize leading or line-height in HTML, CSS, or UI components. Apply font-size multipliers of 1.5 for paragraphs, 1.25 for subheadings, and 0.9 for titles. Do not use for font, color, or layout-only work that does not affect text leading.
---

# Typography leading rules

## When to apply this skill

Treat a request to improve typography, readability, legibility, or reading comfort as a leading task when line spacing can reasonably contribute to the stated problem. This includes requests such as “the text feels cramped,” “make this article easier to read,” “fix the heading spacing,” or “clean up the typography.” Apply the ratios below to the relevant default elements, while leaving font selection, color, width, and other typography decisions within the user's requested scope.

Apply `line-height = font-size × multiplier` using these default semantic mappings:

| Text role | Default elements | Multiplier | Example |
| --- | --- | --- | --- |
| Body text | `p` | `1.5` | 16px → 24px |
| Subheadings | `h2`, `h3`, `h4`, `h5`, `h6` | `1.25` | 24px → 30px |
| Titles | `h1` | `0.9` | 64px → 57.6px |

## Apply the rules

1. Inspect the target markup, components, and existing typography styles. Identify the rendered HTML elements, including those emitted by reusable components. Use the semantic mappings above unless the user explicitly supplies different role mappings.
2. Update the existing shared typography rules or components in the requested scope. Preserve font sizes, fonts, weights, margins, and semantic markup. Do not reclassify text based only on its visual size or change unrelated elements such as buttons, labels, or list items.
3. Prefer unitless CSS line-height values. The browser multiplies them by each element's own font size automatically, including responsive, inherited, `rem`, and fluid `clamp()` sizes. No JavaScript measurement or resize listener is needed.

   ```css
   p {
     line-height: 1.5;
   }

   h2, h3, h4, h5, h6 {
     line-height: 1.25;
   }

   h1 {
     line-height: 0.9;
   }
   ```

4. Adapt the declarations to the project's existing styling system and scope. In utility-based components, replace conflicting leading utilities with exact equivalents such as `leading-[1.5]`, `leading-[1.25]`, and `leading-[0.9]`. Check component variants, breakpoints, inline styles, and later `font` shorthands for overrides. Resolve conflicts at their source instead of adding blanket `!important` declarations. Set the ratio on the mapped elements rather than a common ancestor so titles do not inherit the body ratio.
5. If the output platform requires an absolute leading value, multiply the actual font size by the role's multiplier in the same unit. Retain fractional results rather than rounding to whole pixels. For relative or fluid sizes, keep the ratio dynamic rather than freezing a value measured at one viewport.
6. Verify the three ratios in the resulting styles, including responsive overrides. If a preview is available, check multiline titles and accented characters for clipping or overlap: `0.9` is intentionally tight. Preserve the requested ratio and fix clipping constraints within scope; report any remaining visual limitation. Respect user stylesheet overrides and text-spacing accessibility settings.

## Report the result

Briefly state which styles or components changed and the applied ratios. When asked only for a calculation, return the computed leading with its unit and role. Distinguish checks actually performed from those unavailable.
